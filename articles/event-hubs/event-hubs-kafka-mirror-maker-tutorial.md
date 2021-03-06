---
title: Verwenden von Kafka MirrorMaker mit Azure Event Hubs für das Kafka-Ökosystem | Microsoft-Dokumentation
description: Verwenden Sie Kafka MirrorMaker, um einen Kafka-Cluster in Event Hubs zu spiegeln.
services: event-hubs
documentationcenter: .net
author: basilhariri
manager: timlt
ms.service: event-hubs
ms.topic: mirror-maker
ms.custom: mvc
ms.date: 05/07/2018
ms.author: bahariri
ms.openlocfilehash: 819071321d5609728e7c62abb5b25bf354107850
ms.sourcegitcommit: d98d99567d0383bb8d7cbe2d767ec15ebf2daeb2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2018
ms.locfileid: "33941238"
---
# <a name="using-kafka-mirrormaker-with-event-hubs-for-kafka-ecosystems"></a>Verwenden von Kafka MirrorMaker mit Event Hubs für Kafka-Ökosysteme

> [!NOTE]
> Dieses Beispiel ist auf [GitHub](https://github.com/Azure/azure-event-hubs) verfügbar.

Ein wichtiger Aspekt von modernen Cloud-Apps für die Skalierung ist die Möglichkeit, die Infrastruktur zu aktualisieren, zu verbessern und zu ändern, ohne den Dienst zu unterbrechen. In diesem Tutorial wird gezeigt, wie mit einem Kafka-fähigen Event Hub und mit Kafka MirrorMaker eine vorhandene Kafka-Pipeline in Azure integriert werden kann, indem der Kafka-Eingabedatenstrom im Event Hub-Dienst „gespiegelt“ wird. 

Mit einem Azure Event Hubs-Kafka-Endpunkt können Sie eine Verbindung mit Azure Event Hubs herstellen, indem Sie das Kafka-Protokoll (Kafka-Clients) verwenden. Durch minimale Änderungen an einer Kafka-Anwendung können Sie eine Verbindung mit Azure Event Hubs herstellen und die Vorteile des Azure-Ökosystems nutzen. Kafka-fähige Event Hubs unterstützen derzeit die Kafka-Version 1.0 und höher.

In diesem Beispiel wird gezeigt, wie Sie einen Kafka-Broker in einem Kafka-fähigen Event Hub mit Kafka MirrorMaker spiegeln.

   ![Kafka MirrorMaker mit Event Hubs](./media/event-hubs-kafka-mirror-maker-tutorial/evnent-hubs-mirror-maker1.png)

## <a name="prerequisites"></a>Voraussetzungen

Damit Sie dieses Tutorial ausführen können, benötigen Sie folgende Komponenten:

* Ein Azure-Abonnement. Wenn Sie keins besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) erstellen, bevor Sie beginnen.
* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
    * Führen Sie unter Ubuntu `apt-get install default-jdk` aus, um das JDK zu installieren.
    * Achten Sie darauf, dass die Umgebungsvariable „JAVA_HOME“ auf den Ordner verweist, in dem das JDK installiert ist.
* Führen Sie den [Download](http://maven.apache.org/download.cgi) und die [Installation](http://maven.apache.org/install.html) eines binären Maven-Archivs durch.
    * Unter Ubuntu können Sie `apt-get install maven` ausführen, um Maven zu installieren.
* [Git-Client](https://www.git-scm.com/downloads)
    * Unter Ubuntu können Sie `sudo apt-get install git` ausführen, um Git zu installieren.

## <a name="create-an-event-hubs-namespace"></a>Erstellen eines Event Hubs-Namespace

Ein Event Hubs-Namespace ist erforderlich, um Nachrichten an einen Event Hubs-Dienst zu senden und von diesem zu empfangen. Eine Anleitung zum Abrufen eines Event Hubs-Kafka-Endpunkts finden Sie unter [Creating a Kafka enabled Event Hub](event-hubs-create.md) (Erstellen eines Kafka-fähigen Event Hub). Kopieren Sie die Event Hubs-Verbindungszeichenfolge zur späteren Verwendung.

## <a name="clone-the-example-project"></a>Klonen des Beispielprojekts

Nachdem Sie nun über eine Kafka-fähige Event Hubs-Verbindungszeichenfolge verfügen, können Sie das Azure Event Hubs-Repository klonen und zum Unterordner `mirror-maker` navigieren:

```shell
git clone https://github.com/Azure/azure-event-hubs.git
cd azure-event-hubs/samples/kafka/mirror-maker
```

## <a name="set-up-a-kafka-cluster"></a>Einrichten eines Kafka-Clusters

Verwenden Sie die [Kafka-Schnellstartanleitung](https://kafka.apache.org/quickstart), um einen Cluster mit den gewünschten Einstellungen einzurichten (oder verwenden Sie einen vorhandenen Kafka-Cluster).

## <a name="kafka-mirrormaker"></a>Kafka MirrorMaker

Mit Kafka MirrorMaker wird die „Spiegelung“ eines Datenstroms ermöglicht. Für Kafka-Quell- und -Zielcluster wird mit MirrorMaker sichergestellt, dass alle Nachrichten, die an den Quellcluster gesendet werden, sowohl vom Quell- als auch vom Zielcluster empfangen werden. In diesem Beispiel wird gezeigt, wie Sie einen Kafka-Quellcluster mit einem Kafka-fähigen Event Hub als Ziel spiegeln. Dieses Szenario kann verwendet werden, um Daten aus einer vorhandenen Kafka-Pipeline an Event Hubs zu senden, ohne den Datenfluss zu unterbrechen. 

Ausführlichere Informationen zu Kafka MirrorMaker finden Sie im [Leitfaden zur Kafka-Spiegelung und zu MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330).

### <a name="configuration"></a>Konfiguration

Richten Sie zum Konfigurieren von Kafka MirrorMaker einen Kafka-Cluster als Consumer/Quelle und einen Kafka-fähigen Event Hub als Producer/Ziel ein.

#### <a name="consumer-configuration"></a>Consumerkonfiguration

Aktualisieren Sie die Konfigurationsdatei `source-kafka.config` für den Consumer, über die MirrorMaker die Eigenschaften des Kafka-Quellclusters mitgeteilt werden.

##### <a name="source-kafkaconfig"></a>source-kafka.config

```xml
bootstrap.servers={SOURCE.KAFKA.IP.ADDRESS1}:{SOURCE.KAFKA.PORT1},{SOURCE.KAFKA.IP.ADDRESS2}:{SOURCE.KAFKA.PORT2},etc
group.id=example-mirrormaker-group
exclude.internal.topics=true
client.id=mirror_maker_consumer
```

#### <a name="producer-configuration"></a>Producerkonfiguration

Aktualisieren Sie nun die Konfigurationsdatei `mirror-eventhub.config` für den Producer, mit der MirrorMaker angewiesen wird, die duplizierten (bzw. „gespiegelten“) Daten an den Event Hubs-Dienst zu senden. Ändern Sie `bootstrap.servers` und `sasl.jaas.config` so, dass darin auf Ihren Event Hubs-Kafka-Endpunkt verwiesen wird. Für den Event Hubs-Dienst ist eine sichere Kommunikation (SASL) erforderlich. Dies wird erreicht, indem die letzten drei Eigenschaften in der folgenden Konfiguration festgelegt werden: 

##### <a name="mirror-eventhubconfig"></a>mirror-eventhub.config

```xml
bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093
client.id=mirror_maker_producer

#Required for Event Hubs
sasl.mechanism=PLAIN
security.protocol=SASL_SSL
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";
```

### <a name="run-mirrormaker"></a>Ausführen von MirrorMaker

Führen Sie das Kafka MirrorMaker-Skript im Kafka-Stammverzeichnis aus, indem Sie die aktualisierten Konfigurationsdateien verwenden. Achten Sie darauf, dass Sie entweder die Konfigurationsdateien in das Kafka-Stammverzeichnis kopieren oder die Pfade im folgenden Befehl aktualisieren.

```shell
bin/kafka-mirror-maker.sh --consumer.config source-kafka.config --num.streams 1 --producer.config mirror-eventhub.config --whitelist=".*"
```

Sie können überprüfen, ob die Ereignisse den Kafka-fähigen Event Hub erreichen, indem Sie im [Azure-Portal](https://azure.microsoft.com/features/azure-portal/) die Eingangsstatistiken anzeigen oder einen Consumer für den Event Hub ausführen.

Bei Ausführung von MirrorMaker werden alle Ereignisse, die an den Kafka-Quellcluster gesendet werden, sowohl vom Kafka-Cluster als auch vom gespiegelten Kafka-fähigen Event Hub-Dienst empfangen. Indem MirrorMaker und ein Event Hubs-Kafka-Endpunkt verwendet werden, können Sie eine vorhandene Kafka-Pipeline zum verwalteten Azure Event Hubs-Dienst migrieren, ohne den vorhandenen Cluster zu ändern oder einen ausgehenden Datenfluss zu unterbrechen.

## <a name="next-steps"></a>Nächste Schritte

* [Informationen zu Event Hubs](event-hubs-what-is-event-hubs.md)
* [Informationen zu Event Hubs für das Kafka-Ökosystem](event-hubs-for-kafka-ecosystem-overview.md)
* Informieren Sie sich über [MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) und das Streamen von Ereignissen von der lokalen Kafka-Instanz zu Kafka-fähigen Event Hubs in der Cloud.
