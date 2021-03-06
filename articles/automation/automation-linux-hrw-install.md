---
title: Runbook Worker hybride Linux Azure Automation | Microsoft Docs
description: "Cet article fournit des informations sur l’installation d’un Runbook Worker hybride Azure Automation qui vous permet dexécuter des Runbooks sur les machines Linux de votre centre de données local ou de votre environnement cloud."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/07/2017
ms.author: magoedte
ms.translationtype: HT
ms.sourcegitcommit: 2c6cf0eff812b12ad852e1434e7adf42c5eb7422
ms.openlocfilehash: d01d9b8723e321ca0f2f9073d5b99b984e30d971
ms.contentlocale: fr-fr
ms.lasthandoff: 09/13/2017

---

# <a name="how-to-deploy-a-linux-hybrid-runbook-worker"></a>Déploiement d’un Runbook Worker hybride Linux
Dans Azure Automation, les Runbooks ne peuvent pas accéder aux ressources d’autres clouds ou dans votre environnement local car ils s'exécutent dans le cloud Azure.  La fonctionnalité de Runbook Worker hybride d’Azure Automation vous permet d’exécuter des Runbooks directement sur l’ordinateur qui héberge le rôle et par rapport aux ressources de l’environnement afin de gérer ces ressources locales. Les Runbooks sont stockés et gérés dans Azure Automation, puis remis à un ou plusieurs ordinateurs désignés.  

Cette fonctionnalité est illustrée dans l’image suivante :<br>  

![Vue d'ensemble des Runbooks Workers hybrides](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Pour obtenir un aperçu technique du rôle d’un Runbook Worker hybride, consultez [Présentation de l’architecture Automation](automation-offering-get-started.md#automation-architecture-overview). Consultez les informations suivantes concernant les [exigences matérielles et logicielles requise](automation-offering-get-started.md#hybrid-runbook-worker) et les [informations pour préparer votre réseau](automation-offering-get-started.md#network-planning) avant de commencer le déploiement d’un Runbook Worker hybride.  Une fois que vous avez déployé un runbook worker avec succès, consultez [exécuter des runbooks sur un Runbook Worker hybride](automation-hrw-run-runbooks.md) pour apprendre comment configurer vos runbooks afin d’automatiser les processus dans votre centre de données local ou un autre environnement cloud.     

## <a name="hybrid-runbook-worker-groups"></a>Groupes de Runbooks Workers hybrides
Chaque Runbook Worker hybride est membre d'un groupe de Runbooks Workers hybrides que vous spécifiez lorsque vous installez l'agent.  Un groupe peut inclure un seul agent, mais vous pouvez installer plusieurs agents dans un groupe pour une haute disponibilité.

Lorsque vous démarrez un Runbook sur un Runbook Worker hybride, vous spécifiez le groupe sur lequel il s’exécute.  Les membres du groupe déterminent quel Worker traite la demande.  Vous ne pouvez pas spécifier un Worker particulier.

## <a name="installing-linux-hybrid-runbook-worker"></a>Installation de la fonctionnalité Runbook Worker hybride Linux
L’installation et la configuration d’un Runbook Worker hybride sur un ordinateur Linux est un processus très simple qui permet d’installer et de configurer le rôle manuellement.   Cela nécessite l’activation de la solution **Automation Hybrid Worker** dans votre espace de travail OMS, puis l’exécution d’un ensemble de commandes pour inscrire l’ordinateur en tant que Worker et l’ajouter à un groupe nouveau ou existant. 

Avant de continuer, vous devez noter l’espace de travail Log Analytics auquel votre compte Automation est lié, ainsi que la clé primaire de votre compte Automation.  Vous trouverez ces deux informations sur le portail en sélectionnant votre compte Automation et l’**espace de travail** correspondant à l’ID d’espace de travail et **Clés** pour la clé primaire.  

1.  Activez la solution Automation Hybrid Worker dans OMS. Pour ce faire, vous pouvez :

   1. À partir de la Galerie de solutions du [portail OMS](https://mms.microsoft.com), activer la solution **Automation Hybrid Worker**
   2. Exécutez l’applet de commande suivante :

        ```powershell
         $null = Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName  <ResourceGroupName> -WorkspaceName <WorkspaceName> -IntelligencePackName  "AzureAutomation" -Enabled $true
        ```

2.  Exécutez la commande suivante en remplaçant les valeurs de paramètres *-w* et *-k* sur votre ordinateur Linux.
    
    ```
    sudo python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/scripts/onboarding.py --register -w <OMSworkspaceId> -k <AutomationSharedKey> --groupname <hybridgroupname> -e <automationendpoint>
    ```
3. Une fois la commande terminée, le panneau Groupes de Workers hybrides du portail Azure affiche le nouveau groupe et le nombre de membres, ou, si le groupe existe déjà, incrémente le nombre de membres.  Vous pouvez sélectionner le groupe dans la liste du panneau **Groupes de Workers hybrides** et sélectionner la vignette **Workers hybrides**.  Le panneau **Workers hybrides** affiche chaque membre du groupe listé.  

## <a name="next-steps"></a>Étapes suivantes

* Consultez [exécuter des runbooks sur un Runbook Worker hybride](automation-hrw-run-runbooks.md) pour apprendre comment configurer vos runbooks afin d’automatiser les processus dans votre centre de données local ou un autre environnement cloud.
* Pour obtenir des instructions sur la suppression des Runbooks Worker hybrides, consultez [Remove Azure Automation Hybrid Runbook Workers](automation-remove-hrw.md) (Supprimer des Runbooks Worker hybrides Azure Automation).
