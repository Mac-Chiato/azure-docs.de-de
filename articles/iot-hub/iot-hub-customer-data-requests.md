---
title: Funktionen für Kundendatenanforderungen
author: dominicbetts
ms.author: dobett
ms.date: 05/16/2018
ms.topic: conceptual
ms.service: iot-hub
ms.openlocfilehash: 3af76fe22e93b6c5d502733196994bda61b9a93e
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/20/2018
ms.locfileid: "34361514"
---
# <a name="summary-of-customer-data-request-features"></a>Übersicht über Funktionen für Kundendatenanforderungen

Azure IoT Hub ist ein REST-API-basierter Clouddienst, der auf Unternehmenskunden ausgerichtet ist und eine sichere und bidirektionale Kommunikation zwischen Millionen von Geräten und einem partitionierten Azure-Dienst ermöglicht.

[!INCLUDE [gdpr-intro-sentence](../../includes/gdpr-intro-sentence.md)]

Ein Mandantenadministrator weist einzelnen Geräten einen Gerätebezeichner (eine Geräte-ID) zu. Die Gerätedaten basieren auf der zugewiesenen Geräte-ID. Microsoft behält keine Informationen und hat keinen Zugriff auf Daten, die eine Korrelation zwischen Geräte-ID und Benutzer zulassen würden.

Viele der in Azure IoT Hub verwalteten Geräte sind keine persönlichen Geräte, z. B. ein Bürothermostat oder ein Werkroboter. Kunden können jedoch einige Geräte als persönlich identifizierbar betrachten und nach eigenem Ermessen ihre eigenen Asset- oder Bestandsnachverfolgungsmethoden anwenden, die Geräte an Personen binden. Azure IoT Hub verwaltet und speichert alle Daten, die mit Geräten verknüpft sind, so, als wären es persönliche Daten.

Mandantenadministratoren können das Azure-Portal oder die REST-APIs des Diensts verwenden, um Informationsanforderungen durch das Exportieren oder Löschen der einer Geräte-ID zugeordneten Daten zu erfüllen.

Wenn Sie die Routingfunktion des Azure IoT Hub-Diensts zum Weiterleiten von Gerätenachrichten an andere Dienste verwenden, müssen Datenanforderungen vom Mandantenadministrator für jeden Routingendpunkt ausgeführt werden, um eine vollständige Anforderung für ein bestimmtes Gerät abzuschließen. Weitere Details finden Sie in der Referenzdokumentation zu den einzelnen Endpunkten. Weitere Informationen zu unterstützten Endpunkten finden Sie unter [Referenz: IoT Hub-Endpunkte](iot-hub-devguide-endpoints.md).

Wenn Sie die Azure Event Grid-Integrationsfunktion des Azure IoT Hub-Diensts verwenden, müssen Datenanforderungen vom Mandantenadministrator für jeden Abonnenten dieser Ereignisse ausgeführt werden. Weitere Informationen finden Sie unter [Reagieren auf Ereignisse in IoT Hub mithilfe von Event Grid](iot-hub-event-grid.md).

Wenn Sie die Azure Monitor-Integrationsfunktion des Azure IoT Hub-Diensts zum Erstellen von Diagnoseprotokollen verwenden, müssen Datenanforderungen vom Mandantenadministrator für die gespeicherten Protokolle ausgeführt werden. Weitere Informationen finden Sie unter [Überwachen der Integrität von Azure IoT Hub](iot-hub-monitor-resource-health.md).

## <a name="deleting-customer-data"></a>Löschen von Kundendaten

Mandantenadministratoren können im Azure-Portal das Blatt „IoT-Geräte“ der Azure IoT Hub-Erweiterung verwenden, um ein Gerät zu löschen. Dabei werden die dem Gerät zugeordneten Daten gelöscht.

Löschvorgänge für Geräte können auch mithilfe von REST-APIs ausgeführt werden. Weitere Informationen finden Sie unter [Geräte-API – Gerät löschen](https://docs.microsoft.com/rest/api/iothub/deviceapi/deletedevice).

## <a name="exporting-customer-data"></a>Exportieren von Kundendaten

Mandantenadministratoren können im Azure-Portal auf dem Blatt „IoT-Geräte“ der Azure IoT Hub-Erweiterung die Funktionen zum Kopieren und Einfügen verwenden, um die einem Gerät zugeordneten Daten zu exportieren.

Exportvorgänge für Geräte können auch mithilfe von REST-APIs ausgeführt werden. Weitere Informationen finden Sie unter [Geräte-API – Gerät abrufen](https://docs.microsoft.com/rest/api/iothub/deviceapi/getdevice).

> [!NOTE]
> Wenn Sie Microsoft Enterprise Services verwenden, generiert Microsoft einige Informationen, die als vom System generierte Protokolle bezeichnet werden. Auf einige vom System generierte Azure IoT Hub-Protokolle können Mandantenadministratoren nicht zugreifen bzw. können einige dieser Protokolle nicht von Mandantenadministratoren exportiert werden. Diese Protokolle stellen faktische Aktionen dar, die innerhalb der Dienst- und Diagnosedaten einzelner Geräte ausgeführt werden.

## <a name="links-to-additional-documentation"></a>Links zu zusätzlicher Dokumentation

Die vollständige Dokumentation zu Azure IoT Hub-Geräte-APIs finden Sie unter [https://docs.microsoft.com/rest/api/iothub/deviceapi](https://docs.microsoft.com/rest/api/iothub/deviceapi).