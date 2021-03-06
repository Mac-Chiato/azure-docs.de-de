---
title: 'Tutorial: Azure Active Directory-Integration mit NetDocuments | Microsoft Docs'
description: Erfahren Sie, wie Sie das einmalige Anmelden zwischen Azure Active Directory und NetDocuments konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a2753d1091adfd03427d159f48474f7a98288d05
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/20/2018
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a>Tutorial: Azure Active Directory-Integration mit NetDocuments

In diesem Tutorial erfahren Sie, wie Sie NetDocuments in Azure Active Directory (Azure AD) integrieren.

Die Integration von NetDocuments in Azure AD bietet die folgenden Vorteile:

- Sie können in Azure AD steuern, wer Zugriff auf NetDocuments hat.
- Benutzer können sich mit ihren Azure AD-Konten automatisch bei NetDocuments anmelden (einmaliges Anmelden).
- Sie können Ihre Konten an einem zentralen Ort verwalten – im Azure-Portal.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Voraussetzungen

Um die Azure AD-Integration in NetDocuments konfigurieren zu können, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein NetDocuments-Abonnement, für das einmaliges Anmelden aktiviert ist

> [!NOTE]
> Um die Schritte in diesem Tutorial zu testen, wird empfohlen, keine Produktionsumgebung zu verwenden.

Um die Schritte in diesem Tutorial zu testen, sollten Sie folgende Empfehlungen beachten:

- Verwenden Sie die Produktionsumgebung nur, wenn dies unbedingt erforderlich ist.
- Wenn Sie keine Azure AD-Testumgebung haben, können Sie [hier](https://azure.microsoft.com/pricing/free-trial/)eine einmonatige Testversion anfordern.

## <a name="scenario-description"></a>Beschreibung des Szenarios
In diesem Tutorial testen Sie das einmalige Anmelden für Azure AD in einer Testumgebung. Das in diesem Tutorial beschriebene Szenario besteht aus zwei Hauptbestandteilen:

1. Hinzufügen von NetDocuments aus dem Katalog
2. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## <a name="adding-netdocuments-from-the-gallery"></a>Hinzufügen von NetDocuments aus dem Katalog
Zum Konfigurieren der Integration von NetDocuments in Azure AD müssen Sie NetDocuments aus dem Katalog der Liste mit den verwalteten SaaS-Apps hinzufügen.

**Um NetDocuments aus dem Katalog hinzuzufügen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** auf das Symbol für **Azure Active Directory**. 

    ![Active Directory][1]

2. Navigieren Sie zu **Unternehmensanwendungen**. Wechseln Sie dann zu **Alle Anwendungen**.

    ![ANWENDUNGEN][2]
    
3. Klicken Sie oben im Dialogfeld auf die Schaltfläche **Neue Anwendung**, um eine neue Anwendung hinzuzufügen.

    ![ANWENDUNGEN][3]

4. Geben Sie im Suchfeld den Suchbegriff **NetDocuments** ein.

    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. Wählen Sie im Ergebnisbereich die Option **NetDocuments** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um die Anwendung hinzuzufügen.

    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen der einmaligen Anmeldung von Azure AD
In diesem Abschnitt konfigurieren und testen Sie das einmalige Anmelden von Azure AD mit NetDocuments basierend auf einer Testbenutzerin mit dem Namen Britta Simon.

Damit einmaliges Anmelden funktioniert, muss Azure AD wissen, welcher Benutzer in NetDocuments als Entsprechung für einen Benutzer in Azure AD fungiert. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in NetDocuments muss eine Linkbeziehung eingerichtet werden.

Weisen Sie in NetDocuments den Wert des **Benutzernamens** in Azure AD als Wert für **Benutzername** zu, um eine Linkbeziehung herzustellen.

Um das einmalige Anmelden von Azure AD mit NetDocuments konfigurieren und testen zu können, ist Folgendes erforderlich:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**, um Ihren Benutzern das Verwenden dieser Funktion zu ermöglichen.
2. **[Erstellen eines Azure AD-Testbenutzers](#creating-an-azure-ad-test-user)** , um das einmalige Anmelden von Azure AD mit der Testbenutzerin Britta Simon zu testen.
3. **[Erstellen eines NetDocuments-Testbenutzers](#creating-a-netdocuments-test-user)**, um eine Entsprechung von Britta Simon in NetDocuments zu erhalten, die mit ihrer Darstellung in Azure AD verknüpft ist.
4. **[Zuweisen des Azure AD-Testbenutzers](#assigning-the-azure-ad-test-user)**, um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
5. **[Testing Single Sign-On](#testing-single-sign-on)** , um zu überprüfen, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens von Azure AD

In diesem Abschnitt ermöglichen Sie das einmalige Anmelden von Azure AD im Azure-Portal und konfigurieren das einmalige Anmelden in Ihrer NetDocuments-Anwendung.

**Führen Sie zum Konfigurieren des einmaligen Anmeldens von Azure AD in NetDocuments die folgenden Schritte aus:**

1. Klicken Sie im Azure-Portal auf der Anwendungsintegrationsseite für **NetDocuments** auf **Einmaliges Anmelden**.

    ![Configure Single Sign-On][4]

2. Wählen Sie im Dialogfeld **Einmaliges Anmelden** als **Modus** die Option **SAML-basierte Anmeldung** aus, um einmaliges Anmelden zu aktivieren.
 
    ![Configure Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. Führen Sie auf der Seite **Domäne und URLs für NetDocuments** die folgenden Schritte aus:

    ![Configure Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    a. Geben Sie im Textfeld **Anmelde-URL** eine URL im folgenden Format ein: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`.

    b. Geben Sie im Textfeld **Antwort-URL** eine URL nach folgendem Muster ein: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`

    > [!NOTE] 
    > Hierbei handelt es sich um Beispielwerte. Ersetzen Sie diese Werte durch die tatsächliche Anmelde-URL und Antwort-URL. Wenden Sie sich an das [NetDocuments-Supportteam](https://support.netdocuments.com/hc/), um diese Werte zu erhalten.
 
4. Klicken Sie im Abschnitt **SAML-Signaturzertifikat** auf **Metadaten-XML**, und speichern Sie die Metadatendatei dann auf Ihrem Computer.

    ![Configure Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. Klicken Sie auf die Schaltfläche **Save** .

    ![Configure Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. Melden Sie sich in einem anderen Webbrowserfenster bei der NetDocuments-Unternehmenswebsite als Administrator an.

7. Wechseln Sie zu **Administrator**.

8. Klicken Sie auf **Benutzer und Gruppen hinzufügen und entfernen**.
   
    ![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")

9. Klicken Sie auf **Erweiterte Authentifizierungsoptionen konfigurieren**.
    
    ![Erweiterte Authentifizierungsoptionen konfigurieren](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Erweiterte Authentifizierungsoptionen konfigurieren")

10. Führen Sie im Dialogfeld **Identitätsverbund** die folgenden Schritte aus:
   
    ![Identitätsverbund](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identitätsverbund")
   
    a. Wählen Sie als **Servertyp für Identitätsverbund** die Option **Active Directory-Verbunddienste** aus.
   
    b. Klicken Sie auf **Datei auswählen**, um die Metadatendatei hochzuladen, die Sie über das Azure-Portal heruntergeladen haben.
   
    c. Klicken Sie auf **OK**.

> [!TIP]
> Während der Einrichtung der App können Sie im [Azure-Portal](https://portal.azure.com) nun eine Kurzfassung dieser Anweisungen lesen.  Nachdem Sie diese App aus dem Abschnitt **Active Directory > Unternehmensanwendungen** heruntergeladen haben, klicken Sie einfach auf die Registerkarte **Einmaliges Anmelden**, und rufen Sie die eingebettete Dokumentation über den Abschnitt **Konfiguration** um unteren Rand der Registerkarte auf. Weitere Informationen zur eingebetteten Dokumentation finden Sie hier: [Eingebettete Azure AD-Dokumentation]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="creating-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers
Das Ziel dieses Abschnitts ist das Erstellen eines Testbenutzers namens Britta Simon im Azure-Portal.

![Azure AD-Benutzer erstellen][100]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **Azure-Portals** auf das Symbol für **Azure Active Directory**.

    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. Wechseln Sie zu **Benutzer und Gruppen**, und klicken Sie auf **Alle Benutzer**, um die Liste der Benutzer anzuzeigen.
    
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. Klicken Sie oben im Dialogfeld auf **Hinzufügen**, um das Dialogfeld **Benutzer** zu öffnen.
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. Führen Sie auf der Dialogfeldseite **Benutzer** die folgenden Schritte aus:
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    a. Geben Sie in das Textfeld **Name** den Namen **BrittaSimon** ein.

    b. Geben Sie in das Textfeld **Benutzername** die **E-Mail-Adresse** von Britta Simon ein.

    c. Wählen Sie **Kennwort anzeigen** aus, und notieren Sie sich den Wert des **Kennworts**.

    d. Klicken Sie auf **Create**.
 
### <a name="creating-a-netdocuments-test-user"></a>Erstellen eines NetDocuments-Testbenutzers

Damit sich Azure AD-Benutzer bei NetDocuments anmelden können, müssen sie in NetDocuments bereitgestellt werden.  
Im Fall von NetDocuments ist die Bereitstellung eine manuelle Aufgabe.

**Führen Sie zum Bereitstellen eines Benutzerkontos die folgenden Schritte aus:**

1. Melden Sie sich bei Ihrer **NetDocuments** -Unternehmenswebsite als Administrator an.

2. Klicken Sie oben im Menü auf **Administrator**.
   
    ![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")

3. Klicken Sie auf **Benutzer und Gruppen hinzufügen und entfernen**.
   
    ![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")

4. Geben Sie im Textfeld **E-Mail-Adresse** die E-Mail-Adresse eines gültigen Azure Active Directory-Kontos ein, das Sie bereitstellen möchten, und klicken Sie auf **Benutzer hinzufügen**.
   
    ![E-Mail-Adresse](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "E-Mail-Adresse")
   
   >[!NOTE]
   >Der Besitzer des Azure Active Directory-Kontos erhält eine E-Mail mit einem Link zur Bestätigung des Kontos, bevor es aktiv wird. Sie können Azure Active Directory-Benutzerkonten auch mithilfe von anderen Tools zum Erstellen von NetDocuments-Benutzerkonten oder mithilfe der von NetDocuments bereitgestellten APIs erstellen.

### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt ermöglichen Sie Britta Simon das einmalige Anmelden bei Azure, indem Sie ihr Zugriff auf NetDocuments gewähren.

![Benutzer zuweisen][200] 

**Um Britta Simon NetDocuments zuzuweisen, führen Sie die folgenden Schritte aus:**

1. Öffnen Sie im Azure-Portal die Anwendungsansicht, navigieren Sie zur Verzeichnisansicht, wechseln Sie dann zu **Unternehmensanwendungen**, und klicken Sie auf **Alle Anwendungen**.

    ![Benutzer zuweisen][201] 

2. Wählen Sie in der Anwendungsliste **NetDocuments** aus.

    ![Configure Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. Klicken Sie im Menü auf der linken Seite auf **Benutzer und Gruppen**.

    ![Benutzer zuweisen][202] 

4. Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie dann im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Benutzer zuweisen][203]

5. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Benutzerliste **Britta Simon** aus.

6. Klicken Sie im Dialogfeld **Benutzer und Gruppen** auf die Schaltfläche **Auswählen**.

7. Klicken Sie im Dialogfeld **Zuweisung hinzufügen** auf **Zuweisen**.
    
### <a name="testing-single-sign-on"></a>Testen der einmaligen Anmeldung

In diesem Abschnitt testen Sie die Azure AD-Konfiguration für einmaliges Anmelden über den Zugriffsbereich.

Wenn Sie im Zugriffsbereich auf die Kachel „NetDocuments“ klicken, sollten Sie automatisch bei Ihrer NetDocuments-Anwendung angemeldet werden.
Weitere Informationen zum Zugriffsbereich finden Sie unter [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

