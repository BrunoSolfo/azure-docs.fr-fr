---
title: "Préparer la cible (VMware vers Azure) | Microsoft Docs"
description: "Cet article décrit comment préparer votre environnement Azure de manière à lancer la réplication de machines virtuelles VMware vers Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.translationtype: Human Translation
ms.sourcegitcommit: db18dd24a1d10a836d07c3ab1925a8e59371051f
ms.openlocfilehash: c84a775564769ddc796aa9d75add019ef1003175
ms.contentlocale: fr-fr
ms.lasthandoff: 06/15/2017

---

# <a name="prepare-target-vmware-to-azure"></a>Préparer la cible (VMware vers Azure)
> [!div class="op_single_selector"]
> * [VMware vers Azure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [Physique vers Azure](./site-recovery-prepare-target-physical-to-azure.md)

Cet article décrit comment préparer votre environnement Azure de manière à lancer la réplication de machines virtuelles VMware vers Azure.

## <a name="prerequisites"></a>Prérequis

Cet article part des principes suivants :
- Vous avez créé un coffre Recovery Services pour protéger vos machines virtuelles VMware. Vous pouvez créer un coffre Recovery Services dans le [portail Azure](http://portal.azure.com "portail Azure").
- Vous avez [configuré votre environnement local](./site-recovery-set-up-vmware-to-azure.md) pour répliquer les machines virtuelles VMware vers Azure.

## <a name="prepare-target"></a>Préparer la cible

Après avoir réalisé **l’Étape 1 : Sélection de l’objectif de la protection** et **l’Étape 2 : Préparation de la source**, vous passez à **l’Étape 3 : Cible**.

![Préparer la cible](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. **Abonnement :** dans le menu déroulant, sélectionnez l’abonnement vers lequel vous souhaitez répliquer vos machines virtuelles.
2. **Modèle de déploiement :** sélectionnez le modèle de déploiement (Classique ou Gestionnaire de ressources).

Selon le modèle de déploiement choisi, une validation est exécutée pour vérifier que vous disposez au moins d’un compte de stockage et d’un réseau virtuel compatibles dans l’abonnement cible pour la réplication et le basculement de votre machine virtuelle.

Une fois les validations terminées avec succès, cliquez sur OK pour passer à l’étape suivante.

Si vous n’avez pas de compte de stockage Resource Manager ou réseau virtuel compatible, ou si vous souhaitez en ajouter d’autres, vous pouvez le faire en cliquant sur les boutons **+ Compte de stockage** ou **+ Réseau** en haut du panneau.

## <a name="next-steps"></a>Étapes suivantes
[Configurer les paramètres de réplication](./site-recovery-setup-replication-settings-vmware.md)

