---
title: "Didacticiel : intégration d’Azure Active Directory à Humanity | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Humanity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.translationtype: Human Translation
ms.sourcegitcommit: ef1e603ea7759af76db595d95171cdbe1c995598
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.contentlocale: fr-fr
ms.lasthandoff: 06/16/2017

---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a>Didacticiel : intégration d’Azure Active Directory à Humanity

L’objectif de ce didacticiel est de vous apprendre à intégrer Humanity à Azure Active Directory (Azure AD).

Intégrer Humanity à Azure AD offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler l’accès à Humanity
- Vous pouvez autoriser vos utilisateurs à être automatiquement connectés à Humanity (via l’authentification unique) avec leur compte Azure AD
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

Pour configurer l’intégration d’Azure AD avec Humanity, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Humanity pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajouter Humanity à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-humanity-from-the-gallery"></a>Ajouter Humanity à partir de la galerie
Pour configurer l’intégration de Humanity à Azure AD, vous devez ajouter Humanity, disponible à partir de la galerie, à votre liste d’applications SaaS gérées.

**Pour ajouter Humanity à partir de la galerie, réalisez les étapes suivantes :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, tapez **Humanity**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. Dans le panneau de résultats, sélectionnez **Humanity**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Humanity, grâce à un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Humanity correspondant dans Azure AD. En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Humanity associé.

Dans Humanity, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec Humanity, vous devez compléter les instructions des blocs de construction suivants :

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur de test Humanity](#creating-a-humanity-test-user)** pour avoir un équivalent de Britta Simon dans Humanity qui est lié à la représentation d’un utilisateur Azure AD.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Humanity.

**Pour configurer l’authentification unique Azure AD avec Humanity, réalisez les étapes suivantes :**

1. Dans le portail Azure, sur la page d’intégration de l’application **Humanity**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. Sur la section **Domaine et URL Humanity**, réalisez les étapes suivantes :

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://company.humanity.com/includes/saml/`

    b. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://company.humanity.com/app/`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels. Pour obtenir ces valeurs, contactez l’[équipe de support aux clients Humanity](https://www.humanity.com/support/). 
 
4. Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. Pour ouvrir la fenêtre **Configurer l’authentification**, sur la section **Configuration Humanity**, cliquez sur **Configurer Humanity**. Copiez l’**URL du service d’authentification unique SAML et l’URL de déconnexion** à partir de la section **Référence rapide**.

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. Dans une autre fenêtre de navigateur web, ouvrez une session sur votre site d’entreprise **Humanity** en tant qu’administrateur.

8. Dans le menu situé en haut, cliquez sur **Admin**.
   
    ![Administrateur](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administrateur")

9. Sous **Integration**, cliquez sur **Single Sign-On**.
   
    ![Authentification unique](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Authentification unique")

10. Dans la section **Single Sign-On** , procédez comme suit :
   
    ![Authentification unique](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Authentification unique")
   
    a. Sélectionnez **SAML Enabled**.

    b. Sélectionnez **Allow Password Login**.

    c. Collez la valeur de l’**URL du service d’authentification unique SAML** dans la zone de texte **URL de l’émetteur SAML**.

    d. Collez la valeur de l’**URL de déconnexion** dans la zone de texte **URL de déconnexion distante**.
   
    e. Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **X.509 Certificate** .

11. Cliquez sur **Save Settings**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-humanity-test-user"></a>Créer un utilisateur de test Humanity

Pour permettre aux utilisateurs Azure AD de se connecter à Humanity, vous devez les approvisionner dans Humanity. Dans le cas de Humanity, l’approvisionnement est une tâche manuelle.

**Pour approvisionner un compte d’utilisateur, procédez comme suit :**

1. Ouvrez une session en tant qu’administrateur sur votre site d’entreprise **Humanity**.

2. Cliquez sur **Admin**.
   
    ![Administrateur](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administrateur")

3. Cliquez sur **Staff**.
   
    ![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")

4. Sous **Actions**, cliquez sur **Ajouter des employés**.
   
    ![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")

5. Dans la section **Add employees** , procédez comme suit :
   
    ![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")
   
    a. Indiquez dans les zones de texte correspondantes le **prénom**, le **nom** et **l’e-mail** du compte AAD valide que vous souhaitez approvisionner.

    b. Cliquez sur **Save Employees**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur Humanity fourni par ce site pour approvisionner des comptes d’utilisateurs AAD.

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Humanity.

![Affecter des utilisateurs][200] 

**Pour assigner Britta Simon à Humanity, réalisez les étapes suivantes :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **Humanity**.

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

En cliquant sur la vignette Humanity dans le Panneau d’accès, vous allez en principe être connecté automatiquement à votre application Humanity.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png


