---
title: "Examen de l’architecture de la réplication VMware sur Azure | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble des composants et de l’architecture utilisés lors de la réplication de machines virtuelles VMware locales sur Azure avec le service Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d03d2dd3-2455-4ca8-a942-a342030ee6ce
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2017
ms.author: raynew
ms.translationtype: HT
ms.sourcegitcommit: 0e862492c9e17d0acb3c57a0d0abd1f77de08b6a
ms.openlocfilehash: ac1151d15a88650f5845cb879cd210e9f7cba0fd
ms.contentlocale: fr-fr
ms.lasthandoff: 09/27/2017

---

# <a name="vmware-to-azure-replication-architecture"></a>Architecture de la réplication VMware vers Azure

Cet article décrit l’architecture et les processus utilisés quand vous répliquez, basculez et récupérez des machines virtuelles VMware entre un site VMware local et Azure, à l’aide du service [Azure Site Recovery](site-recovery-overview.md).


## <a name="architectural-components"></a>Composants architecturaux

Le tableau et le graphique suivants fournissent une vue d’ensemble des composants utilisés pour la réplication VMware vers Azure.  

**Composant** | **Prérequis** | **Détails**
--- | --- | ---
**Microsoft Azure** | Un abonnement Azure, un compte de stockage Azure et un réseau Azure. | Les données répliquées à partir de machines virtuelles locales sont stockées dans le compte de stockage. Les machines virtuelles Azure sont créées avec les données répliquées quand vous exécutez un basculement depuis le site local vers Azure. Les machines virtuelles Azure se connectent au réseau virtuel Azure lors de leur création.
**Serveur de configuration** | Une seule machine virtuelle VMware locale est déployée pour exécuter tous les composants Site Recovery locaux. La machine virtuelle exécute le serveur de configuration, le serveur de traitement et le serveur cible maître. | Le serveur de configuration coordonne la communication entre les ordinateurs locaux et Azure.et gère la réplication des données.
 **Serveur de traitement**:  | Installé par défaut avec le serveur de configuration. | Fait office de passerelle de réplication. Reçoit les données de réplication, les optimise grâce à la mise en cache, la compression et le chiffrement et les envoie vers le stockage Azure.<br/><br/> En outre, le serveur de traitement installe le service Mobilité sur les machines virtuelles que vous voulez répliquer et effectue la découverte automatique des machines virtuelles sur les serveurs VMware locaux.<br/><br/> À mesure que s’étend votre déploiement, vous pouvez ajouter des serveurs de traitement distincts afin de gérer de plus grands volumes de trafic de réplication.
 **Serveur cible maître** | Installé par défaut avec le serveur de configuration. | Gère les données de réplication pendant la restauration automatique à partir d’Azure.<br/><br/> Pour les déploiements à grande échelle, vous pouvez ajouter un serveur cible maître distinct à des fins de restauration automatique.
**Serveurs VMware** | Les machines virtuelles VMware sont hébergées sur des serveurs vSphere ESXi locaux. Nous recommandons d’utiliser un serveur vCenter pour gérer les hôtes. | Pendant le déploiement de Site Recovery, vous ajoutez des serveurs VMware au coffre Recovery Services.
**Machines répliquées** | Le service Mobilité est installé sur chaque machine virtuelle VMware que vous répliquez. | Nous vous recommandons d’autoriser l’installation automatique à partir du serveur de traitement. Vous pouvez également installer le service manuellement, ou utiliser une méthode de déploiement automatisé telle que System Center Configuration Manager. 

**Architecture VMware vers Azure**

![Composants](./media/concepts-vmware-to-azure-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Processus de réplication

1. Vous configurez le déploiement, notamment celui des composants locaux et des composants Azure. Dans le coffre Recovery Services, vous spécifiez la source et la cible de réplication, configurez le serveur de configuration, créez une stratégie de réplication et activez la réplication.
2. Les machines sont répliquées conformément à la stratégie définie, et une copie initiale des données des machines virtuelles est répliquée dans le stockage Azure.
3. La réplication des modifications delta dans Azure commence à l’issue de la réplication initiale. Le suivi des modifications d’une machine est conservé dans un fichier .hrl.
    - Les machines communiquent avec le serveur de configuration sur le port HTTPS 443 entrant, pour la gestion de la réplication.
    - Les machines envoient des données de réplication au serveur de traitement sur le port HTTPS 9443 entrant (modification possible).
    - Le serveur de configuration orchestre la gestion de la réplication avec Azure sur le port HTTPS 443 sortant.
    - Le serveur de traitement reçoit les données à partir des machines source, puis les chiffre et les envoie au stockage Azure via le port 443 sortant.
    - Si vous activez la cohérence multimachine virtuelle, les machines du groupe de réplication communiquent entre elles sur le port 20004. Le mode multimachine virtuelle est utilisé si vous regroupez plusieurs machines dans des groupes de réplication qui partagent des points de récupération cohérents en cas d’incident et avec les applications lorsqu’ils basculent. Cela est utile si les machines exécutent la même charge de travail et doivent être cohérentes.
4. Le trafic est répliqué sur des points de terminaison publics de stockage Azure via Internet. L’autre solution consiste à utiliser l’[homologation publique](../expressroute/expressroute-circuit-peerings.md#azure-public-peering) Azure ExpressRoute. La réplication du trafic à partir d’un site local vers Azure via un réseau VPN de site à site n’est pas prise en charge.


**Processus de réplication VMware vers Azure**

![Processus de réplication](./media/concepts-vmware-to-azure-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Processus de basculement et de restauration automatique

Après avoir configuré la réplication et exécuté une simulation de récupération d’urgence (test de basculement) pour vérifier que tout fonctionne comme prévu, vous pouvez exécuter un basculement et une restauration automatique en fonction de vos besoins.

1. Vous pouvez basculer une seule machine ou créer des plans de récupération pour basculer plusieurs machines virtuelles.
2. Quand vous exécutez un basculement, les machines virtuelles Azure sont créées à partir des données répliquées dans le stockage Azure.
3. Après avoir déclenché le basculement initial, validez-le pour accéder à la charge de travail à partir de la machine virtuelle Azure.

Lorsque votre site local principal est à nouveau disponible, vous pouvez lancer la restauration automatique.
1. Vous devez configurer une infrastructure de restauration automatique, notamment les aspects suivants :
    - **Serveur de traitement temporaire dans Azure** : pour effectuer une restauration automatique à partir d’Azure, vous configurez une machine virtuelle Azure en tant que serveur de traitement pour gérer la réplication à partir d’Azure. Vous pourrez supprimer cette machine virtuelle une fois la restauration terminée.
    - **Connexion VPN** : pour la restauration automatique, vous avez besoin d’une connexion VPN (ou Azure ExpressRoute) du réseau Azure vers le site local.
    - **Serveur cible maître distinct** : par défaut, le serveur cible maître local qui a été installé avec le serveur de configuration, sur la machine virtuelle VMware locale, gère la restauration automatique. Toutefois, si vous devez restaurer automatiquement de grands volumes de trafic, vous devez configurer un serveur cible maître local distinct à cet effet.
    - **Stratégie de restauration automatique** : pour répliquer vers votre site local, vous avez besoin d’une stratégie de restauration automatique. Celle-ci a été automatiquement créée au moment de la création de votre stratégie de réplication depuis le site local vers Azure.
2. Une fois les composants en place, la restauration automatique s’effectue en trois étapes :
    - Étape 1 : Reprotégez les machines virtuelles Azure afin qu’elles répliquent depuis Azure vers les machines virtuelles VMware locales.
    - Étape 2 : Exécutez un basculement vers le site local.
    - Étape 3 : Une fois les charges de travail automatiquement restaurées, vous réactivez la réplication pour les machines virtuelles locales.

**Restauration automatique VMware à partir d’Azure**

![Restauration automatique](./media/concepts-vmware-to-azure-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Étapes suivantes

Passer en revue la matrice de prise en charge Suivre le didacticiel montrant comment activer la réplication VMware vers Azure
Exécuter un basculement et une restauration automatique.
