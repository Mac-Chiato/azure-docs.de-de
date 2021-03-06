---
title: Verwenden von OpenFaaS mit Azure Kubernetes Service (AKS)
description: Bereitstellen und Verwenden von OpenFaaS mit Azure Kubernetes Service (AKS)
services: container-service
author: justindavies
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 03/05/2018
ms.author: juda
ms.custom: mvc
ms.openlocfilehash: e26f1c298b05153736edd2b2efd0f1b27162bc3d
ms.sourcegitcommit: d98d99567d0383bb8d7cbe2d767ec15ebf2daeb2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2018
---
# <a name="using-openfaas-on-aks"></a>Verwenden von OpenFaaS mit AKS

[OpenFaaS][open-faas] ist ein Framework zum Erstellen von serverlosen Funktionen für Container. Das Open-Source-Projekt wurde bereits sehr umfassend in der Community eingesetzt. In diesem Dokument werden die Installation und Verwendung von OpenFaaS in einem Azure Kubernetes Service-Cluster (AKS) beschrieben.

## <a name="prerequisites"></a>Voraussetzungen

Sie benötigen Folgendes, um die Schritte in diesem Artikel ausführen zu können.

* Grundlegende Kenntnisse von Kubernetes
* Einen AKS-Cluster (Azure Kubernetes Service) und konfigurierte AKS-Anmeldeinformationen in Ihrem Entwicklungssystem
* Eine Installation der Azure CLI auf Ihrem Entwicklungssystem.
* Auf Ihrem System installierte Git-Befehlszeilentools

## <a name="get-openfaas"></a>Abrufen von OpenFaaS

Klonen Sie das OpenFaaS-Projektrepository auf Ihrem Entwicklungssystem.

```azurecli-interactive
git clone https://github.com/openfaas/faas-netes
```

Wechseln Sie in das Verzeichnis des geklonten Repositorys.

```azurecli-interactive
cd faas-netes
```

## <a name="deploy-openfaas"></a>Bereitstellen von OpenFaaS

Es empfiehlt sich, OpenFaaS und OpenFaaS Funktionen in einem eigenen Kubernetes-Namespace zu speichern.

Erstellen Sie einen Namespace für das OpenFaaS-System.

```azurecli-interactive
kubectl create namespace openfaas
```

Erstellen Sie einen zweiten Namespace für die OpenFaaS-Funktionen.

```azurecli-interactive
kubectl create namespace openfaas-fn
```

Ein Helm-Diagramm für OpenFaaS ist im geklonten Repository enthalten. Verwenden Sie dieses Diagramm, um OpenFaaS in Ihrem AKS-Cluster bereitzustellen.

```azurecli-interactive
helm install --namespace openfaas -n openfaas \
  --set functionNamespace=openfaas-fn, \
  --set serviceType=LoadBalancer, \
  --set rbac=false chart/openfaas/
```

Ausgabe:

```
NAME:   openfaas
LAST DEPLOYED: Wed Feb 28 08:26:11 2018
NAMESPACE: openfaas
STATUS: DEPLOYED

RESOURCES:
==> v1/ConfigMap
NAME                 DATA  AGE
prometheus-config    2     20s
alertmanager-config  1     20s

{snip}

NOTES:
To verify that openfaas has started, run:

  kubectl --namespace=openfaas get deployments -l "release=openfaas, app=openfaas"
```

Es wird eine öffentliche IP-Adresse für den Zugriff auf das OpenFaaS-Gateway erstellt. Sie rufen diese IP-Adresse mit dem Befehl [kubectl get service][kubectl-get] ab. Es dauert möglicherweise einige Zeit, bis die IP-Adresse dem Dienst zugewiesen wird.

```console
kubectl get service -l component=gateway --namespace openfaas
```

Ausgabe

```console
NAME               TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)          AGE
gateway            ClusterIP      10.0.156.194   <none>         8080/TCP         7m
gateway-external   LoadBalancer   10.0.28.18     52.186.64.52   8080:30800/TCP   7m
```

Browsen Sie zum Testen des OpenFaaS-Systems zur externen IP-Adresse an Port 8080 – in diesem Beispiel `http://52.186.64.52:8080`.

![OpenFaaS-Benutzeroberfläche](media/container-service-serverless/openfaas.png)

Installieren Sie abschließend die OpenFaaS-Befehlszeilenschnittstelle. In diesem Beispiel wird brew verwendet. Weitere Optionen finden Sie in der [Dokumentation zur OpenFaaS-Befehlszeilenschnittstelle][open-faas-cli].

```console
brew install faas-cli
```

## <a name="create-first-function"></a>Erstellen der ersten Funktion

Nachdem OpenFaaS einsatzbereit ist, erstellen Sie eine Funktion über das OpenFaaS-Portal.

Klicken Sie auf **Neue Funktion bereitstellen**, und suchen Sie nach **Figlet**. Wählen Sie die Figlet-Funktion aus, und klicken Sie auf **Bereitstellen**.

![Figlet](media/container-service-serverless/figlet.png)

Verwenden Sie zum Aufrufen der Funktion cURL. Ersetzen Sie die IP-Adresse im folgenden Beispiel durch die Ihres OpenFaaS-Gateways.

```azurecli-interactive
curl -X POST http://52.186.64.52:8080/function/figlet -d "Hello Azure"
```

Ausgabe:

```console
 _   _      _ _            _
| | | | ___| | | ___      / \    _____   _ _ __ ___
| |_| |/ _ \ | |/ _ \    / _ \  |_  / | | | '__/ _ \
|  _  |  __/ | | (_) |  / ___ \  / /| |_| | | |  __/
|_| |_|\___|_|_|\___/  /_/   \_\/___|\__,_|_|  \___|

```

## <a name="create-second-function"></a>Erstellen der zweiten Funktion

Erstellen Sie nun eine zweite Funktion. Dieses Beispiel wird mithilfe der OpenFaaS-Befehlszeilenschnittstelle bereitgestellt. Es enthält ein benutzerdefiniertes Containerimage und umfasst auch das Abrufen von Daten aus einer Cosmos DB-Instanz. Es müssen mehrere Elemente konfiguriert werden, bevor Sie die Funktion erstellen.

Erstellen Sie zunächst eine neue Ressourcengruppe für Cosmos DB.

```azurecli-interactive
az group create --name serverless-backing --location eastus
```

Stellen Sie eine Cosmos DB-Instanz vom Typ `MongoDB` bereit. Die Instanz benötigt einen eindeutigen Namen. Ersetzen Sie daher `openfaas-cosmos` durch einen in Ihrer Umgebung eindeutigen Wert.

```azurecli-interactive
az cosmosdb create --resource-group serverless-backing --name openfaas-cosmos --kind MongoDB
```

Rufen Sie die Verbindungszeichenfolge für die Cosmos-Datenbank ab, und speichern Sie sie in einer Variable.

Ändern Sie den Wert des `--resource-group`-Arguments in den Namen der Ressourcengruppe und den des `--name`-Arguments in den Namen Ihrer Cosmos DB-Instanz.

```azurecli-interactive
COSMOS=$(az cosmosdb list-connection-strings \
  --resource-group serverless-backing \
  --name openfaas-cosmos \
  --query connectionStrings[0].connectionString \
  --output tsv)
```

Füllen Sie nun die Cosmos DB-Instanz mit Testdaten auf. Erstellen Sie eine Datei namens `plans.json`, und fügen Sie den folgenden JSON-Code ein.

```json
{
    "name" : "two_person",
    "friendlyName" : "Two Person Plan",
    "portionSize" : "1-2 Person",
    "mealsPerWeek" : "3 Unique meals per week",
    "price" : 72,
    "description" : "Our basic plan, delivering 3 meals per week, which will feed 1-2 people.",
    "__v" : 0
}
```

Verwenden Sie das Tool *mongoimport*, um Daten in die Cosmos DB-Instanz zu laden.

Installieren Sie ggf. die MongoDB-Tools. Im folgenden Beispiel werden diese Tools mit brew installiert. Weitere Optionen finden Sie in der [MongoDB-Dokumentation][install-mongo].

```azurecli-interactive
brew install mongodb
```

Laden Sie die Daten in die Datenbank.

```azurecli-interactive
mongoimport --uri=$COSMOS -c plans < plans.json
```

Ausgabe:

```console
2018-02-19T14:42:14.313+0000    connected to: localhost
2018-02-19T14:42:14.918+0000    imported 1 document
```

Führen Sie den folgenden Befehl aus, um die Funktion zu erstellen. Ersetzen Sie den Wert des `-g`-Arguments durch die Adresse Ihres OpenFaaS-Gateways.

```azurecli-interctive
faas-cli deploy -g http://52.186.64.52:8080 --image=shanepeckham/openfaascosmos --name=cosmos-query --env=NODE_ENV=$COSMOS
```

Nach der Bereitstellung sollte der neu erstellte OpenFaaS-Endpunkt für die Funktion angezeigt werden.

```console
Deployed. 202 Accepted.
URL: http://52.186.64.52:8080/function/cosmos-query
```

Testen Sie die Funktion mit cURL. Ersetzen Sie die IP-Adresse durch die Adresse Ihres OpenFaaS-Gateways.

```console
curl -s http://52.186.64.52:8080/function/cosmos-query
```

Ausgabe:

```json
[{"ID":"","Name":"two_person","FriendlyName":"","PortionSize":"","MealsPerWeek":"","Price":72,"Description":"Our basic plan, delivering 3 meals per week, which will feed 1-2 people."}]
```

Sie können die Funktion auch auf der OpenFaaS-Benutzeroberfläche testen.

![alt text](media/container-service-serverless/OpenFaaSUI.png)

## <a name="next-steps"></a>Nächste Schritte

Die Standardbereitstellung von OpenFaaS muss für das OpenFaaS-Gateway und OpenFaaS-Funktionen abgesichert werden. Der [Blogbeitrag von Alex Ellis](https://blog.alexellis.io/lock-down-openfaas/) enthält weitere Details zu sicheren Konfigurationsoptionen.

<!-- LINKS - external -->
[install-mongo]: https://docs.mongodb.com/manual/installation/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[open-faas]: https://www.openfaas.com/
[open-faas-cli]: https://github.com/openfaas/faas-cli