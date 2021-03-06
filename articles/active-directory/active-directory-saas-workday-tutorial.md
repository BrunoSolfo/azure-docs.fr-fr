---
title: "Didacticiel : Intégration d’Azure Active Directory à Workday | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Workday."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.translationtype: HT
ms.sourcegitcommit: f76de4efe3d4328a37f86f986287092c808ea537
ms.openlocfilehash: 164d5c644f120fa86e2b690649241892764b64b7
ms.contentlocale: fr-fr
ms.lasthandoff: 07/11/2017

---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Didacticiel : Intégration d’Azure Active Directory à Workday

Dans ce didacticiel, vous allez apprendre à intégrer Workday avec Azure Active Directory (Azure AD).

L’intégration de Workday dans Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à Workday
- Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Workday (par le biais de l’authentification unique) avec leur compte Azure AD
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

Pour configurer l’intégration d’Azure AD à Workday, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Workday pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de Workday à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-workday-from-the-gallery"></a>Ajout de Workday à partir de la galerie
Pour configurer l’intégration de Workday à Azure AD, vous devez ajouter Workday à partir de la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter Workday à partir de la galerie, effectuez les étapes suivantes :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, tapez **Workday**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. Dans le volet de résultats, sélectionnez **Workday**, puis cliquez sur **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workday avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Workday équivalent dans Azure AD. En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Workday associé doit être établie.

Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** dans Workday.

Pour configurer et tester l’authentification unique Azure AD avec Workday, vous devez suivre les indications des sections suivantes :

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur de test Workday](#creating-a-workday-test-user)** pour avoir un équivalent de Britta Simon dans Workday lié à la représentation Azure AD de l’utilisateur.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Workday.

**Pour configurer l’authentification unique Azure AD avec Workday, effectuez les étapes suivantes :**

1. Dans le portail Azure, dans la page d’intégration de l’application **Workday**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. Dans la section **Domaine et URL Workday**, effectuez les étapes suivantes :

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez la valeur suivante : `https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Il ne s’agit pas des valeurs réelles. Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles. Votre URL de réponse doit avoir un sous-domaine (par exemple, www, wd2, wd3, wd3-impl, wd5, wd5-impl). Quelque chose comme « *http://www.myworkday.com* » fonctionnera, mais pas « *http://myworkday.com* ». Pour obtenir ces valeurs, contactez l’[équipe de support technique de Workday](https://www.workday.com/en-us/partners-services/services/support.html). 
 

4. Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. Dans la section **Configuration de Workday**, cliquez sur **Configurer Workday** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Workday en tant qu’administrateur.

8. Accédez à **Menu \> Workbench**.
   
    ![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")

9. Accédez à **Administration des comptes**.
   
    ![Administration des comptes](./media/active-directory-saas-workday-tutorial/IC782924.png "Administration des comptes")

10. Accédez à **Edit Tenant Setup – Security**.
   
    ![Modifier la sécurité du locataire](./media/active-directory-saas-workday-tutorial/IC782925.png "Modifier la sécurité du locataire")

11. Dans la section **Redirection URLs** , procédez comme suit :
   
    ![URL de redirection](./media/active-directory-saas-workday-tutorial/IC7829581.png "URL de redirection")
   
    a. Cliquez sur le **signe plus**pour ajouter une ligne.
   
    b. Dans les zones de texte **URL de redirection de connexion** et **URL de redirection mobile**, tapez l’**URL de connexion** que vous avez entrée dans la page **Domaine et URL Workday** du portail Azure.
   
    c. Dans le portail Azure, dans la fenêtre **Configurer l’authentification**, copiez l’**URL de déconnexion**, puis collez-la dans la zone de texte **Logout Redirect URL**.
   
    d.  Dans la zone de texte **Environment** , tapez le nom de l’environnement.  

    >[!NOTE]
    > La valeur de l’attribut Environment est liée à celle de l’URL du client :  
    >- Si le nom de domaine de l’URL du locataire Workday commence par impl (par exemple : *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), l’attribut **Environment** doit être défini sur Implementation.  
    >- Si le nom de domaine commence par autre chose, vous devez contacter l’[équipe de support technique de Workday](https://www.workday.com/en-us/partners-services/services/support.html) pour obtenir la valeur correspondante de l’attribut **Environment**.

12. Dans la section **SAML Setup** , procédez comme suit :
   
    ![Configuration de SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configuration de SAML")
   
    a.  Sélectionnez **Enable SAML Authentication**.
   
    b.  Cliquez sur le **signe plus**pour ajouter une ligne.

13. Dans la section SAML Identity Providers, procédez comme suit :
   
    ![Fournisseurs d’identité SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Fournisseurs d’identité SAML")
   
    a. Dans la zone de texte Identity Provider Name, entrez le nom d’un fournisseur (par exemple *SPInitiatedSSO*).
   
    b. Dans le portail Azure, dans la fenêtre **Configurer l’authentification**, copiez la valeur **ID d’entité SAML**, puis collez-la dans la zone de texte **Issuer**.
   
    c. Sélectionnez **Enable Workday Initiated Logout**.
   
    d. Dans le portail Azure, dans la fenêtre **Configurer l’authentification**, copiez la valeur d’**URL de déconnexion**, puis collez-la dans la zone de texte **Logout Request URL**.

    e. Cliquez sur **Certificat de clé publique du fournisseur d’identité**, puis sur **Créer**. 

    ![Créer](./media/active-directory-saas-workday-tutorial/IC782928.png "créer")

    f. Cliquez sur **Créer la clé publique x509**. 

    ![Créer](./media/active-directory-saas-workday-tutorial/IC782929.png "créer")


14. Dans la section **Afficher la clé publique x509** , procédez comme suit : 
   
    ![Afficher la clé publique x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Afficher la clé publique x509") 
   
    a. Dans la zone de texte **Name**, tapez le nom du certificat (par exemple *PPE\_SP*).
   
    b. Dans la zone de texte **Valid From** , tapez la valeur correspondante du certificat.
   
    c.  Dans la zone de texte **Valid To** , tapez la valeur correspondante du certificat.
   
    > [!NOTE]
    > Vous pouvez obtenir les dates de début et de fin de validité du certificat téléchargé en double-cliquant dessus.  Les dates sont répertoriées sous l’onglet **Details** .
    > 
    >
   
    d.  Ouvrez le certificat codé en base 64 dans le Bloc-notes, puis copiez son contenu.
   
    e.  Dans la zone de texte **Certificat** , collez le contenu du Presse-papiers.
   
    f.  Cliquez sur **OK**.

15. Procédez comme suit : 
   
    ![Configuration SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuration SSO")
   
    a.  Activez **x509 Private Key Pair**.
   
    b.  Dans la zone de texte **Service Provider ID**, tapez **http://www.workday.com**.
   
    c.  Sélectionnez **Enable SP Initiated SAML Authentication**.
   
    d.  Dans le portail Azure Classic, dans la page **Configurer l’authentification unique**, copiez la valeur de l’**URL du service d’authentification unique SAML**, puis collez-la dans la zone de texte **IdP SSO Service URL**.
   
    e. Sélectionnez **Ne pas compresser la demande d’authentification initiée par le fournisseur de services**.
   
    f. Comme **Méthode de signature de la demande d’authentification**, sélectionnez **SHA256**. 
   
    ![Méthode de signature de demande la d’authentification](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Méthode de signature de la demande d’authentification") 
   
    g. Cliquez sur **OK**. 
   
    ![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE>

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-workday-test-user"></a>Création d’un utilisateur de test Workday

Pour approvisionner un utilisateur test dans Workday, vous devez contacter l’[équipe du support technique de Workday](https://www.workday.com/en-us/partners-services/services/support.html).
L’[équipe de support technique de Workday](https://www.workday.com/en-us/partners-services/services/support.html) crée l’utilisateur pour vous.

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Workday.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à Workday, effectuez les étapes suivantes :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **Workday**.

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png


