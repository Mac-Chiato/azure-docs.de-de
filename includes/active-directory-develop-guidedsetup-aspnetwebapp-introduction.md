---
title: Includedatei
description: Includedatei
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/19/2018
ms.author: andret
ms.custom: include file
ms.openlocfilehash: cf6604a0e22ca72c8aabd0603e42469cc71c9680
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a>Hinzufügen von „Mit Microsoft anmelden“ zu einer ASP.NET-Web-App

Diese Anleitung veranschaulicht das Implementieren von „Mit Microsoft anmelden“ mithilfe einer ASP.NET MVC-Projektmappe mit einer herkömmlichen browserbasierten Anwendung mittels OpenID Connect. 

Am Ende dieser Anleitung kann Ihre Anwendung Anmeldungen von sowohl persönlichen Konten (z.B. outlook.com, live.com u.a.) als auch Geschäfts,- Schul- und Unikonten von Unternehmen oder Organisationen akzeptieren, die in Azure Active Directory integriert wurden. 

> Für diese Anleitung ist Visual Studio 2015 Update 3 oder Visual Studio 2017 erforderlich.  Sie haben beides nicht?  [Laden Sie Visual Studio 2017 kostenlos herunter](https://www.visualstudio.com/downloads/)

## <a name="how-the-sample-app-generated-by-this-guide-works"></a>Funktionsweise der über diesen Leitfaden generierten Beispiel-App

![Funktionsweise dieser Anleitung](media/active-directory-develop-guidedsetup-aspnetwebapp-intro/aspnetbrowsergeneral.png)

Die mithilfe dieser Anleitung erstellte Beispielanwendung basiert auf dem Szenario, in dem ein Benutzer den Browser für den Zugriff auf eine ASP.NET-Website verwendet und aufgefordert wird, sich über die Schaltfläche „Anmelden“ anzumelden. In diesem Szenario wird ein Großteil der Arbeit zum Rendern der Webseite auf dem Server erledigt.

## <a name="libraries"></a>Bibliotheken

In dieser Anleitung werden die folgenden Bibliotheken verwendet:

|Bibliothek|BESCHREIBUNG|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Middleware, die einer Anwendung das Verwenden von OpenIDConnect für die Authentifizierung ermöglicht|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Middleware, die einer Anwendung das Beibehalten der Benutzersitzung mithilfe von Cookies ermöglicht|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Ermöglicht OWIN-basierten Anwendungen die Ausführung in IIS mithilfe der ASP.NET-Anforderungspipeline|

