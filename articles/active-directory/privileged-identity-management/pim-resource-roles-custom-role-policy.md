---
title: Verwenden benutzerdefinierter Rollen für Privileged Identity Management-Einstellungen für Azure-Ressourcen | Microsoft Docs
description: Beschreibt, wie benutzerdefinierte Rollen für Azure-Ressourcen mit PIM verwendet werden.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/30/2018
ms.author: billmath
ms.openlocfilehash: e3df34e761f17aa3c1949af390e57360d84a304f
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="use-custom-roles-to-target-privileged-identity-management-settings"></a>Verwenden benutzerdefinierter Rollen für Privileged Identity Management-Einstellungen

Es kann erforderlich sein, strikte PIM-Einstellungen (Privileged Identity Management) auf einige Mitglieder einer Rolle anzuwenden, während anderen mehr Freiheiten gewährt werden. Stellen Sie sich ein Szenario vor, in dem eine Organisation mehrere Vertragspartner nutzt, um Unterstützung bei der Entwicklung einer Anwendung zu leisten, die in einem Azure-Abonnement ausgeführt wird.

Als Ressourcenadministrator wünschen Sie sich, dass Mitarbeiter ohne Genehmigung für den Zugriff berechtigt sind. Allerdings muss für alle Vertragspartner eine Genehmigung vorhanden sein, wenn sie Zugriff auf die Ressourcen eines Unternehmens anfordern.

Führen Sie die im nächsten Abschnitt angegebenen Schritte aus, um PIM-Zieleinstellungen für Azure-Ressourcenrollen einzurichten.

## <a name="create-the-custom-role"></a>Erstellen der benutzerdefinierten Rolle

Um eine benutzerdefinierte Rolle für eine Ressource zu erstellen, führen Sie die Schritte unter [Erstellen benutzerdefinierter Rollen für rollenbasierte Zugriffssteuerung in Azure](../role-based-access-control-custom-roles.md) aus.

Wenn Sie benutzerdefinierte Rollen erstellen, fügen Sie einen beschreibenden Namen hinzu, damit Sie sich leicht merken können, welche integrierte Rolle dupliziert werden soll.

> [!NOTE]
> Stellen Sie sicher, dass die benutzerdefinierte Rolle ein Duplikat der integrierten Rolle ist, die Sie duplizieren möchten, und dass ihr Bereich mit der integrierten Rolle übereinstimmt.

## <a name="apply-pim-settings"></a>Anwenden von PIM-Einstellungen

Nachdem die Rolle in Ihrem Mandanten im Azure-Portal erstellt wurde, navigieren Sie zum Bereich **Privileged Identity Management: Azure-Ressourcen**. Wählen Sie die Ressource aus, für die die Rolle gelten soll.

![Der Bereich „Privileged Identity Management: Azure-Ressourcen“](media/azure-pim-resource-rbac/aadpim_manage_azure_resource_some_there.png)

[Konfigurieren Sie PIM-Rolleneinstellungen](pim-resource-roles-configure-role-settings.md), die für diese Mitglieder der Rolle gelten sollen.

Führen Sie abschließend das [Zuweisen von Rollen](pim-resource-roles-assign-roles.md) für einzelne Gruppen mit Mitgliedern aus, für die diese Einstellungen gelten sollen.

## <a name="next-steps"></a>Nächste Schritte

[Überprüfen der Abonnementbesitzer und des Zugriffs](pim-resource-roles-perform-access-review.md)
