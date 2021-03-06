---
title: Erstellen von Hadoop-Clustern mit einem Webbrowser – Azure HDInsight | Microsoft-Dokumentation
description: Erfahren Sie, wie Hadoop-, HBase-, Storm- oder Spark-Cluster unter Linux für HDInsight mithilfe eines Webbrowsers und des Azure-Vorschauportals erstellt werden.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: conceptual
ms.date: 02/21/2018
ms.author: nitinme
ms.openlocfilehash: 13f746697a7e694da79a6e376b45f95529049a44
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-linux-based-clusters-in-hdinsight-using-the-azure-portal"></a>Erstellen von Linux-basierten Clustern in HDInsight mithilfe des Azure-Portals
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Das Azure-Portal ist ein webbasiertes Verwaltungstool für Dienste und Ressourcen, die in der Microsoft Azure-Cloud gehostet werden. In diesem Artikel erfahren Sie, wie Sie mit dem Portal Linux-basierte HDInsight-Cluster erstellen.

## <a name="prerequisites"></a>Voraussetzungen
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Ein Azure-Abonnement**. Siehe [Kostenlose Azure-Testversion](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Ein zeitgemäßer Webbrowser**. Das Azure-Portal verwendet HTML5 und JavaScript und funktioniert in älteren Webbrowsern unter Umständen nicht richtig.

## <a name="create-clusters"></a>Erstellen von Clustern
Das Azure-Portal macht die meisten Clustereigenschaften verfügbar. Mithilfe der Azure Resource Manager-Vorlage können Sie viele Details ausblenden. Weitere Informationen finden Sie unter [Erstellen Linux-basierter Hadoop-Cluster in HDInsight mithilfe von Azure Resource Manager-Vorlagen](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an.
2. Klicken Sie auf **+**, auf **Intelligence + Analyse** und anschließend auf **HDInsight**.
   
    ![Erstellen eines neuen Clusters im Azure-Portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "Erstellen eines neuen Clusters im Azure-Portal")

3. Klicken Sie auf dem Blatt **HDInsight** auf **Benutzerdefiniert (Größe, Einstellungen, Apps)**, klicken Sie auf **Grundlagen**, und geben Sie dann die folgenden Informationen ein.

    ![Erstellen eines neuen Clusters im Azure-Portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "Erstellen eines neuen Clusters im Azure-Portal")

    * Geben Sie den **Clusternamen**ein: Dieser Name muss global eindeutig sein.

    * Wählen Sie in der Dropdownliste **Abonnement** das Azure-Abonnement aus, das für den Cluster verwendet wird.

    * Klicken Sie auf **Clustertyp**, und wählen Sie dann den Typ (Hadoop, Spark usw.) des Clusters aus, den Sie erstellen möchten. Klicken Sie unter **Betriebssystem** auf **Linux**, und wählen Sie dann eine Version aus. Verwenden Sie die Standardversion, wenn Sie nicht wissen, was Sie auswählen sollen. Weitere Informationen finden Sie unter [HDInsight-Clusterversionen](hdinsight-component-versioning.md).

        Für Cluster der Typen Hadoop, Spark und Interactive Query können Sie sich außerdem entscheiden, das **Sicherheitspaket für Unternehmen** zu installieren. Das Sicherheitspaket für Unternehmen aktiviert Sicherheitsfunktionen wie Azure Active Directory-Integration und Apache Ranger für die Cluster. Weitere Informationen finden Sie unter [Sicherheitspaket für Unternehmen in Azure HDInsight](./domain-joined/apache-domain-joined-introduction.md).

        ![Sicherheitspaket für Unternehmen aktivieren](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-enable-enterprise-security-package.png "Sicherheitspaket für Unternehmen aktivieren")
     
        > [!IMPORTANT]
        > HDInsight-Cluster gibt es in vielen verschiedenen Typen, die der Workload oder Technologie entsprechen, für die der Cluster optimiert ist. Es ist keine unterstützte Methode zum Erstellen eines Clusters vorhanden, bei der mehrere Typen kombiniert werden, z.B. Storm und HBase in einem Cluster. 
        > 
        > 
        
    * Geben Sie für **Clusterbenutzername** und **Clusteranmeldekennwort** den Benutzernamen und das Kennwort für den Administratorbenutzer ein.

    * Geben Sie einen **SSH-Benutzernamen** ein, und wenn Sie möchten, dass das SSH-Kennwort mit dem Administratorkennwort identisch ist, das Sie zuvor angegeben haben, aktivieren Sie das Kontrollkästchen **Dasselbe Kennwort wie für die Clusteranmeldung verwenden**. Falls nicht, geben Sie entweder ein **KENNWORT** oder einen **ÖFFENTLICHEN SCHLÜSSEL** zum Authentifizieren des SSH-Benutzers ein. Es wird empfohlen, einen öffentlichen Schlüssel zu verwenden. Klicken Sie unten auf **Auswählen** , um die Konfiguration der Anmeldeinformationen zu speichern.
   
    Informationen hierzu finden Sie unter [Verwenden von SSH mit Linux-basiertem Hadoop in HDInsight unter Linux, Unix oder OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

    * Geben Sie für **Ressourcengruppe** an, ob Sie eine neue Ressourcengruppe erstellen oder eine vorhandene verwenden möchten.

    * Geben Sie einen **Speicherort** im Rechenzentrum an, an dem der Cluster erstellt wird.

    * Klicken Sie auf **Weiter**.

4. Geben Sie unter **Speicher** an, ob Azure Storage (WASB) oder Data Lake Store als Standardspeicher verwendet werden soll. Weitere Informationen finden Sie weiter unten in der Tabelle.

    ![Erstellen eines neuen Clusters im Azure-Portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "Erstellen eines neuen Clusters im Azure-Portal")

    | Speicher                                      | BESCHREIBUNG |
    |----------------------------------------------|-------------|
    | **Azure Storage-Blobs als Standardspeicher**   | <ul><li>Wählen Sie für **Primärer Speichertyp** **Azure Storage**. Anschließend können Sie für **Auswahlmethode** die Option **Meine Abonnements** auswählen, wenn Sie ein Speicherkonto angeben möchten, das Bestandteil Ihres Azure-Abonnements ist. Wählen Sie dann das Speicherkonto aus. Klicken Sie andernfalls auf **Zugriffsschlüssel**, und geben Sie die Informationen für das nicht in Ihrem Azure-Abonnement enthaltene Speicherkonto an, das Sie auswählen möchten.</li><li>Als **Standardcontainer** können Sie den vom Portal vorgeschlagenen Standardcontainernamen verwenden oder einen eigenen angeben.</li><li>Wenn Sie WASB als Standardspeicher verwenden, können Sie (optional) auf **Zusätzliche Speicherkonten** klicken, um dem Cluster weitere Speicherkonten zuzuordnen. Klicken Sie unter **Azure-Speicherschlüssel** auf **Speicherschlüssel hinzufügen**. Anschließend können Sie ein Speicherkonto aus Ihren Azure-Abonnements oder anderen Abonnements bereitstellen (durch Bereitstellen der Speicherkonto-Zugriffsschlüssel).</li><li>Wenn Sie WASB als Standardspeicher verwenden, können Sie (optional) auf **Data Lake Store-Zugriff** klicken, um Azure Data Lake Store als zusätzlichen Speicher anzugeben. Weitere Informationen hierzu finden Sie unter [Erstellen eines HDInsight-Clusters mit Data Lake Store mithilfe des Azure-Portals](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store als Standardspeicher** | Wählen Sie für **Primärer Speichertyp** **Data Lake Store** aus, und befolgen Sie dann die Anweisungen im Artikel [Erstellen eines HDInsight-Clusters mit Data Lake-Speicher mithilfe des Azure-Portals](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). |
    | **Externe Metastores**                      | Optional können Sie eine SQL-Datenbank angeben, die zum Speichern von Hive- und Oozie-Metadaten für den Cluster verwendet werden soll. Wählen Sie für **SQL-Datenbank für Hive auswählen** eine SQL-Datenbank aus, und geben Sie dann den Benutzernamen und das Kennwort für die Datenbank ein. Wiederholen Sie diese Schritte für Oozie-Metadaten.<br><br>Noch ein paar Überlegungen zur Verwendung der Azure SQL-Datenbank für Metastores. <ul><li>Die als Metastore verwendete Azure SQL-Datenbank muss für die Konnektivität mit anderen Azure-Diensten konfiguriert sein, inklusive Azure HDInsight. Klicken Sie im Dashboard der Azure SQL-Datenbank mit der rechten Maustaste auf den Servernamen. Dies ist der Server, auf dem die SQL-Datenbankinstanz läuft. Öffnen Sie die Serveransicht, klicken Sie auf **Konfigurieren**, wählen Sie unter **Azure Services** den Wert **Ja** aus, und klicken Sie auf **Speichern**.</li><li>Verwenden Sie beim Erstellen eines Metastores keinen Datenbanknamen, der Gedankenstriche oder Bindestriche enthält, da dadurch der Clustererstellungsprozess misslingen kann.</li></ul> |

    Klicken Sie auf **Weiter**. 

    > [!WARNING]
    > Die Verwendung eines zusätzlichen Speicherkontos an einem anderen Ort als dem HDInsight-Cluster wird nicht unterstützt.

5. Klicken Sie optional auf **Anwendungen**, um Anwendungen zu installieren, die mit HDInsight-Clustern verwendet werden können. Diese Anwendungen können von Microsoft oder von unabhängigen Softwareanbietern (Independent Software Vendors, ISVs) bezogen oder aber selbst entwickelt werden. Weitere Informationen finden Sie unter [Installieren von HDInsight-Anwendungen](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Klicken Sie auf **Clustergröße**, um Informationen zu den Knoten anzuzeigen, die für diesen Cluster verwendet werden. Legen Sie die Anzahl von Workerknoten fest, die Sie für den Cluster benötigen. Die geschätzten Kosten der Clusterausführung werden ebenfalls angezeigt.
   
    ![Knotenpreistarife](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Anzahl der Clusterknoten angeben")
   
   > [!IMPORTANT]
   > Wenn Sie mehr als 32 Workerknoten planen, entweder direkt bei der Erstellung des Clusters oder durch eine Skalierung des Clusters nach der Erstellung, müssen Sie eine Hauptknotengröße von mindestens 8 Kernen und 14 GB Arbeitsspeicher (RAM) auswählen.
   > 
   > Weitere Informationen zu Knotengrößen und den damit verbundenen Kosten finden Sie unter [HDInsight – Preise](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Klicken Sie auf **Weiter**, um die Konfiguration der Knotenpreise zu speichern.

7. Klicken Sie auf **Erweiterte Einstellungen**, um andere optionale Einstellungen wie die Verwendung von **Skriptaktionen** zum Anpassen eines Clusters zum Installieren von benutzerdefinierten Komponenten oder den Beitritt zu einem **Virtuellen Netzwerk** zu konfigurieren. Weitere Informationen finden Sie weiter unten in der Tabelle.

    ![Knotenpreistarife](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Anzahl der Clusterknoten angeben")

    | Option | BESCHREIBUNG |
    |--------|-------------|
    | **Skriptaktionen** | Verwenden Sie diese Option, wenn Sie einen Cluster bei seiner Erstellung mit einem benutzerdefinierten Skript anpassen möchten. Weitere Informationen zu Skriptaktionen finden Sie unter [Anpassen von HDInsight-Clustern mithilfe von Skriptaktionen](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Virtual Network** | Wählen Sie ein virtuelles Azure-Netzwerk und das Subnetz aus, wenn Sie den Cluster in einem virtuellen Netzwerk platzieren möchten. Informationen zur Verwendung von HDInsight mit Virtual Network, einschließlich spezifischer Konfigurationsanforderungen für Virtual Network, finden Sie unter [Erweitern der HDInsight-Funktionen mit Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md). |

    Klicken Sie auf **Weiter**.

8. Überprüfen Sie unter **Zusammenfassung** die Informationen, die Sie zuvor eingegeben haben, und klicken Sie dann auf **Erstellen**.

    ![Knotenpreistarife](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Anzahl der Clusterknoten angeben")
    
    > [!NOTE]
    > Die Erstellung des Clusters dauert in der Regel ca. 15 Minuten. Sie können den Status des Bereitstellungsprozesses auf der Kachel im Startmenü oder im linken Bereich der Seite unter **Benachrichtigungen** überprüfen.
    > 
    > 
12. Klicken Sie nach Abschluss des Erstellungsprozesses im Startmenü auf die Kachel für den Cluster. Im Clusterfenster werden die folgenden Informationen angezeigt.
    
    ![Clusterschnittstelle](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Clustereigenschaften")
    
    Die folgenden Informationen dienen zur Erläuterung der Symbole oben.
    
    * Auf der Registerkarte **Übersicht** werden alle grundlegenden Informationen zum Cluster angezeigt, z.B. der Name, die zugehörige Ressourcengruppe, der Standort, das Betriebssystem, die URL für das Cluster-Dashboard usw.
    * **Dashboard** führt Sie zu dem mit dem Cluster verbundenen Ambari-Portal.
    * **Secure Shell**: Für den Zugriff auf den Cluster über SSH erforderliche Informationen.
    * **Cluster skalieren** ermöglicht Ihnen, die Anzahl der mit dem Cluster verbundenen Workerknoten zu erhöhen.
    * **Löscht**: Löscht den HDInsight-Cluster.
    

## <a name="customize-clusters"></a>Anpassen von Clustern
* Weitere Informationen finden Sie unter [Anpassen von HDInsight-Clustern mithilfe von Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Weitere Informationen finden Sie unter [Anpassen von HDInsight-Clustern mithilfe von Skriptaktionen](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-the-cluster"></a>Löschen des Clusters
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Problembehandlung

Falls beim Erstellen von HDInsight-Clustern Probleme auftreten, sehen Sie sich die [Voraussetzungen für die Zugriffssteuerung](hdinsight-administer-use-portal-linux.md#create-clusters) an.

## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie einen HDInsight-Cluster erfolgreich erstellt haben, nutzen Sie die folgenden Informationen, um zu erfahren, wie Sie mit Ihrem Cluster arbeiten:

### <a name="hadoop-clusters"></a>Hadoop-Cluster
* [Verwenden von Hive mit HDInsight](hadoop/hdinsight-use-hive.md)
* [Verwenden von Pig mit HDInsight](hadoop/hdinsight-use-pig.md)
* [Verwenden von MapReduce mit HDInsight](hadoop/hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase-Cluster
* [Erste Schritte mit HBase in HDInsight](hbase/apache-hbase-tutorial-get-started-linux.md)
* [Entwickeln von Java-Anwendungen für HBase in HDInsight](hbase/apache-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm-Cluster
* [Entwickeln von Java-Topologien für Storm in HDInsight](storm/apache-storm-develop-java-topology.md)
* [Verwenden von Python-Komponenten in Storm in HDInsight](storm/apache-storm-develop-python-topology.md)
* [Bereitstellen und Überwachen von Topologien mit Storm in HDInsight](storm/apache-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Spark-Cluster
* [Erstellen einer eigenständigen Anwendung mit Scala](spark/apache-spark-create-standalone-application.md)
* [Remoteausführung von Aufträgen in einem Spark-Cluster mithilfe von Livy](spark/apache-spark-livy-rest-interface.md)
* [Spark mit BI: Durchführen interaktiver Datenanalysen mithilfe von Spark in HDInsight mit BI-Tools](spark/apache-spark-use-bi-tools.md)
* [Spark mit Machine Learning: Vorhersage von Lebensmittelkontrollergebnissen mithilfe von Spark in HDInsight](spark/apache-spark-machine-learning-mllib-ipython.md)

