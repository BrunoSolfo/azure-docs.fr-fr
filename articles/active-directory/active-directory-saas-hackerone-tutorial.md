---
title: "Didacticiel : Intégration d’Azure Active Directory avec HackerOne | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et HackerOne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.translationtype: Human Translation
ms.sourcegitcommit: 857267f46f6a2d545fc402ebf3a12f21c62ecd21
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.contentlocale: fr-fr
ms.lasthandoff: 06/28/2017

---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a>Didacticiel : Intégration d’Azure Active Directory à HackerOne

Dans ce didacticiel, vous allez apprendre à intégrer HackerOne à Azure Active Directory (Azure AD).

L’intégration de HackerOne à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à HackerOne.
- Vous pouvez autoriser les utilisateurs à se connecter automatiquement à HackerOne (par le biais de l’authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l’intégration d’Azure AD à HackerOne, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Hackerone pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de HackerOne à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-hackerone-from-the-gallery"></a>Ajout de HackerOne à partir de la galerie
Pour configurer l’intégration de HackerOne à Azure AD, vous devez ajouter HackerOne à partir de la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter HackerOne à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, tapez **HackerOne**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. Dans le volet de résultats, sélectionnez **HackerOne**, puis cliquez sur **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HackerOne avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur HackerOne équivalent dans Azure AD. En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur HackerOne associé doit être établie.

Dans HackerOne, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec HackerOne, vous devez suivre les indications des sections suivantes :

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur de test HackerOne](#creating-a-hackerone-test-user)** pour avoir un équivalent de Britta Simon dans HackerOne lié à la représentation Azure AD associée.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application HackerOne.

**Pour configurer l’authentification unique Azure AD avec HackerOne, procédez comme suit :**

1. Dans le portail Azure, dans la page d’intégration de l’application **HackerOne**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. Dans la section **URL et identificateur d’authentification unique HackerOne**, effectuez les étapes suivantes :

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://hackerone.com/<company name>/authentication`

    b. Dans la zone de texte **Identificateur**, entrez une URL telle que celle-ci : `https://hackerone.com/users/saml/metadata`
    
    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettez à jour cette valeur avec l’URL de connexion réelle. Contactez [l’équipe de support technique de HackerOne](mailto:support@hackerone.com) pour obtenir cette valeur. 
 
4. Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. Dans la section **Configuration de HackerOne**, cliquez sur **Configurer HackerOne** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. Connectez-vous à votre locataire HackerOne en tant qu’administrateur.

8. Dans le menu situé en haut, cliquez sur « **Settings** ».
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. Accédez à « **Authentication** » et cliquez sur « **Add SAML settings** ».
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. Dans la boîte de dialogue **SAML Settings** (Paramètres SAML), procédez comme suit :
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    a. Dans la zone de texte **Email Domain** , entrez un domaine enregistré.

    b. Dans la zone de texte **Single Sign On URL**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.

    c. Ouvrez dans le Bloc-notes votre **Fichier de certificat** téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat X509**.
    
    d. Cliquez sur **Enregistrer**.

11. Dans la boîte de dialogue Authentication Settings, procédez comme suit :
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    a. Cliquez sur **Run test**.

    b. Si la valeur du champ **Status** est égale à **Last test status: created**, contactez l’[équipe de support technique HackerOne](mailto:support@hackerone.com) pour demander une révision de votre configuration.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-hackerone-test-user"></a>Création d'un utilisateur de test HackerOne

Vous allez maintenant créer un utilisateur nommé Britta Simon dans HackerOne. HackerOne prend en charge l’approvisionnement juste-à-temps, option activée par défaut.

Vous n’avez aucune opération à effectuer dans cette section. Lorsque vous accédez à HackerOne, un nouvel utilisateur est créé s'il n'existe pas déjà.

>[!NOTE]
>Si vous devez créer un utilisateur manuellement, contactez l’équipe du support technique Certify. 
> 

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à HackerOne.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à HackerOne, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **HackerOne**.

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Pour terminer, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.  

Quand vous cliquez sur la vignette HackerOne dans le volet d’accès, vous devez être connecté automatiquement à votre application HackerOne.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png


