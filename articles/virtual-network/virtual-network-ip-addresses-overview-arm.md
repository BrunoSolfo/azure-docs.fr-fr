---
title: "Types d’adresses IP dans Azure | Microsoft Docs"
description: "Apprenez-en plus sur les adresses IP publiques et privées dans Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/18/2017
ms.author: jdial
ms.translationtype: HT
ms.sourcegitcommit: 44e9d992de3126bf989e69e39c343de50d592792
ms.openlocfilehash: 8ddd582ed159e10add896252c40feb19780c42fb
ms.contentlocale: fr-fr
ms.lasthandoff: 09/25/2017

---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Types d’adresses IP et méthodes d’allocation dans Azure

Vous pouvez affecter des adresses IP à des ressources Azure pour communiquer avec d’autres ressources Azure, votre réseau local et Internet. Les adresses IP que vous pouvez utiliser dans Azure sont de deux types :

* **Adresses IP publiques** : Elles sont utilisées pour la communication avec Internet, notamment les services Azure accessibles au public.
* **Adresses IP privées**: elles sont utilisées pour la communication au sein d’un réseau virtuel Azure (VNet) et de votre réseau local lorsque vous utilisez une passerelle VPN ou un circuit ExpressRoute pour étendre votre réseau à Azure.

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).  Cet article traite de l’utilisation du modèle de déploiement Resource Manager que Microsoft recommande pour la plupart des nouveaux déploiements à la place du [modèle de déploiement classique](virtual-network-ip-addresses-overview-classic.md).
> 

Si vous êtes familiarisé avec le modèle de déploiement classique, vérifiez les [différences d’adressage IP entre les déploiements classiques et Resource Manager](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Adresses IP publiques

Les adresses IP publiques permettent aux ressources Azure de communiquer avec Internet et des services Azure accessibles au public, tels que le [Cache Redis Azure](https://azure.microsoft.com/services/cache), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs), les [bases de données SQL](../sql-database/sql-database-technical-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) et [Azure Storage](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

Dans Azure Resource Manager, une [adresse IP publique](virtual-network-public-ip-address.md) est une ressource ayant ses propres propriétés. Voici quelques unes des ressources auxquelles vous pouvez associer une ressource d’adresse IP publique :

* Interfaces réseau de machine virtuelle
* Équilibreurs de charge accessibles sur Internet
* Passerelles VPN
* Passerelles d’application

### <a name="ip-address-version"></a>Version de l’adresse IP

Les adresses IP publiques sont créées avec une adresse IPv4 et IPv6. Les adresses IPv6 publiques ne peuvent être assignées qu’à des équilibreurs de charge accessibles sur Internet.

### <a name="sku"></a>SKU

Les adresses IP publiques sont créées avec l’une des références SKU suivantes :

#### <a name="basic"></a>De base

Toutes les adresses IP publiques créées avant l’introduction de références SKU sont des adresses IP publiques de référence SKU de base. Depuis l’introduction des références SKU, vous avez la possibilité de spécifier quelle référence SKU attribuer à l’adresse IP publique. Les adresses de référence SKU de base sont :

- Sont assignées à l’aide de la méthode d’allocation statique ou dynamique.
- Sont assignées aux ressources Azure acceptant une adresse IP publique, comme les interfaces réseau, les passerelles VPN, les passerelles Application Gateway et les équilibreurs de charge accessibles sur Internet.
- Peuvent être assignées à une zone spécifique.
- Ne sont pas redondantes dans une zone. Pour en savoir plus sur les zones de disponibilité, consultez [Vue d’ensemble de zones de disponibilité](../availability-zones/az-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="standard"></a>Standard

Les adresses IP publiques de référence SKU standard :

- Sont assignées à l’aide de la méthode d’allocation statique uniquement.
- Peuvent être assignées à des interfaces réseau ou à des équilibreurs de charge standard accessibles sur Internet. Pour plus d’informations sur les références SKU de l’équilibreur de charge Azure, consultez [Référence SKU standard de l’équilibreur de charge Azure](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Sont redondantes dans une zone par défaut. Peuvent être créées pour une zone et garanties dans une zone de disponibilité spécifique.  Pour en savoir plus sur les zones de disponibilité, consultez [Vue d’ensemble de zones de disponibilité](../availability-zones/az-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
 
> [!NOTE]
> Quand vous assignez une adresse IP publique de référence SKU standard à l’interface réseau d’une machine virtuelle, vous devez explicitement autoriser le trafic prévu avec un [groupe de sécurité réseau](security-overview.md#network-security-groups).  La communication avec la ressource est possible uniquement si vous créez et associez un groupe de sécurité réseau et que vous autorisez explicitement le trafic prévu.

La référence SKU standard est disponible en version préliminaire. Si vous souhaitez créer une adresse IP publique de référence SKU standard, vous devez d’abord vous inscrire pour la version préliminaire et créer l’adresse dans un emplacement pris en charge. Pour vous inscrire pour la version préliminaire, consultez [S’inscrire pour la version préliminaire de la référence SKU standard](virtual-network-public-ip-address.md#register-for-the-standard-sku-preview). Pour obtenir la liste des emplacements (régions) pris en charge, consultez [Disponibilité des régions](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region-availability), ainsi que la page [Mises à jour du Réseau virtuel Microsoft Azure](https://azure.microsoft.com/updates/?product=virtual-network) pour voir si d’autres régions sont prises en charge.


### <a name="allocation-method"></a>Méthode d’allocation

L’allocation d’une adresse IP à la ressource d’une adresse IP publique est possible à l’aide de deux méthodes : *dynamique* ou *statique*. La méthode d’allocation par défaut est *dynamique*. Dans ce cas, une adresse IP n’est **pas** allouée au moment de sa création. Au lieu de cela, l’adresse IP publique est allouée lorsque vous démarrez (ou créez) la ressource associée (telle qu’une machine virtuelle ou un équilibreur de charge). L’adresse IP est libérée lorsque vous arrêtez (ou supprimez) la ressource. Après avoir été libérée de la ressource A, par exemple, l’adresse IP peut être assignée à une ressource différente. Si l’adresse IP est assignée à une ressource différente lorsque la ressource A est arrêtée, une adresse IP différente est assignée lors du redémarrage de la ressource A.

Pour vous assurer que l’adresse IP de la ressource associée ne change pas, vous pouvez définir explicitement à la méthode d’allocation sur *statique*. Une adresse IP statique est affectée immédiatement. L’adresse est libérée uniquement lorsque vous supprimez la ressource ou modifiez sa méthode d’allocation en *dynamique*.

> [!NOTE]
> Même lorsque vous définissez la méthode d’allocation sur *statique*, vous ne pouvez pas spécifier l’adresse IP réelle affectée à la ressource IP publique. Azure assigne l’adresse IP à partir d’un pool d’adresses IP disponibles dans l’emplacement Azure dans lequel la ressource est créée.
>

Des adresses IP publiques statiques sont fréquemment utilisées dans les cas suivants :

* Lorsque vous devez mettre à jour les règles de pare-feu pour communiquer avec vos ressources Azure.
* La résolution de noms DNS est telle qu’une modification de l’adresse IP nécessiterait une mise à jour des enregistrements A.
* Vos ressources Azure communiquent avec d’autres applications ou services qui utilisent un modèle de sécurité basé sur une adresse IP.
* Vous utilisez des certificats SSL liés à une adresse IP.

> [!NOTE]
> Azure alloue des adresses IP publiques d’une plage unique à chaque région Azure. Pour plus de détails, consultez[Plages IP du Centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Résolution de nom d’hôte DNS
Vous pouvez spécifier une étiquette de nom de domaine DNS pour une ressource IP publique, qui crée un mappage pour l’élément *domainnamelabel*.*location*.cloudapp.azure.com vers l’adresse IP publique dans les serveurs DNS gérés par Azure. Par exemple, si vous créez une ressource IP publique avec **contoso** en tant que *domainnamelabel* dans **l’emplacement** Azure *États-Unis de l’Ouest*, le nom de domaine complet (FQDN) **contoso.westus.cloudapp.azure.com** résout l’adresse IP publique de la ressource. Vous pouvez utiliser le nom de domaine complet pour créer un enregistrement CNAME de domaine personnalisé qui pointe vers l’adresse IP publique dans Azure.

> [!IMPORTANT]
> Chaque étiquette de nom de domaine créée doit être unique dans son emplacement Azure.  
>

### <a name="virtual-machines"></a>Machines virtuelles

Vous pouvez associer une adresse IP publique à une machine virtuelle [Windows](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) en l’affectant à son **interface réseau**. Vous pouvez affecter une adresse IP publique dynamique ou statique à une machine virtuelle. Apprenez-en davantage sur l’[assignation d’adresses IP à des interfaces réseau](virtual-network-network-interface-addresses.md).

### <a name="internet-facing-load-balancers"></a>Équilibreurs de charge accessibles sur Internet

Vous pouvez associer une adresse IP publique créée avec l’une des deux [références SKU](#SKU) à un [équilibreur de charge Azure](../load-balancer/load-balancer-overview.md) en l’assignant à la configuration **frontale** de l’équilibreur de charge. L’adresse IP publique sert d’adresse IP virtuelle (VIP) à charge équilibrée. Vous pouvez affecter une adresse IP publique dynamique ou statique à un équilibreur de charge frontal. Vous pouvez également affecter plusieurs adresses IP publiques à un équilibreur de charge frontal, ce qui permet des scénarios avec [plusieurs adresses IP virtuelles](../load-balancer/load-balancer-multivip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tels qu’un environnement mutualisé avec des sites web SSL. Pour plus d’informations sur les références SKU de l’équilibreur de charge Azure, consultez [Référence SKU standard de l’équilibreur de charge Azure](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="vpn-gateways"></a>Passerelles VPN

Une [passerelle VPN Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json) connecte un réseau virtuel Azure (VNet) à d’autres réseaux virtuels Azure ou à un réseau local. Une adresse IP publique est assignée à une passerelle VPN pour lui permettre de communiquer avec le réseau distant. Vous pouvez affecter une adresse IP publique *dynamique* uniquement à une passerelle VPN.

### <a name="application-gateways"></a>Passerelles d’application

Vous pouvez associer une adresse IP publique à une [Application Gateway](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json)Azure en l’affectant à la configuration **frontale** de la passerelle. Cette adresse IP publique sert d’adresse IP virtuelle à équilibrage de charge. Vous pouvez uniquement affecter une adresse IP publique *dynamique* à une configuration frontale de passerelle d’application.

### <a name="at-a-glance"></a>Aperçu
Le tableau ci-dessous présente la propriété spécifique par le biais de laquelle une adresse IP publique peut être associée à une ressource de niveau supérieur, ainsi que les méthodes d’allocation possibles (dynamique ou statique) utilisables.

| Ressources de niveau supérieur | Association d’adresse IP | dynamique | statique |
| --- | --- | --- | --- |
| Machine virtuelle |interface réseau |Oui |Oui |
| Équilibreur de charge accessible sur Internet |Configuration frontale |Oui |Oui |
| Passerelle VPN |Configuration IP de la passerelle |Oui |Non |
| Application Gateway |Configuration frontale |Oui |Non |

## <a name="private-ip-addresses"></a>Adresses IP privées
Les adresses IP privées permettent aux ressources Azure de communiquer avec d’autres ressources dans un [réseau virtuel](virtual-networks-overview.md) ou dans un réseau local par le biais d’une passerelle VPN ou d’un circuit ExpressRoute, sans utiliser d’adresse IP accessible via Internet.

Dans le modèle de déploiement Azure Resource Manager, une adresse IP privée est associée aux types ressources Azure suivants.

* Interfaces réseau de machine virtuelle
* Équilibreurs de charge interne (ILB)
* Passerelles d’application

### <a name="ip-address-version"></a>Version de l’adresse IP

Les adresses IP privées sont créées avec une adresse IPv4 et IPv6. Les adresses IPv6 privées ne peuvent être assignées qu’à l’aide d’une méthode d’allocation dynamique. La communication entre adresses IPv6 privées sur un réseau virtuel est impossible. La communication au sein d’une adresse IPv6 privée est possible depuis Internet, via un équilibreur de charge accessible sur Internet. Pour en savoir plus, consultez [Créer un équilibreur de charge Internet avec IPv6](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="allocation-method"></a>Méthode d’allocation

Une adresse IP privée est allouée à partir de la plage d’adresses du sous-réseau auquel la ressource est attachée. La plage d’adresses du sous-réseau lui-même fait partie de la plage d’adresses du réseau virtuel.

Il existe deux méthodes d’allocation d’adresses IP : *dynamique* ou *statique*. La méthode d’allocation par défaut est *dynamique*, où l’adresse IP est allouée automatiquement à partir du sous-réseau de la ressource (à l’aide de DHCP). Cette adresse IP peut changer lorsque vous arrêtez et démarrez la ressource.

Vous pouvez définir la méthode d’allocation *statique* pour vous assurer que l’adresse IP ne change pas. Lorsque vous spécifiez *statique*, vous devez aussi renseigner une adresse IP valide qui fait partie du sous-réseau de la ressource.

Les adresses IP privées statiques sont couramment utilisées pour :

* les machines virtuelles qui agissent en tant que contrôleurs de domaine ou serveurs DNS ;
* les ressources qui nécessitent des règles de pare-feu utilisant des adresses IP ;
* des ressources auxquelles d’autres applications/ressources accèdent via une adresse IP.

### <a name="virtual-machines"></a>Machines virtuelles

Une adresse IP privée est assignée à l’**interface réseau** d’une machine virtuelle [Windows](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Si la machine virtuelle possède plusieurs interfaces réseau, une adresse IP privée est assignée à chacune d’elles. Vous pouvez spécifier la méthode d’allocation dynamique ou statique pour une interface réseau.

#### <a name="internal-dns-hostname-resolution-for-virtual-machines"></a>Résolution de nom d’hôte DNS interne (pour les machines virtuelles)

Toutes les machines virtuelles Azure sont configurées avec des [serveurs DNS gérés par Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) par défaut, sauf si vous configurez explicitement des serveurs DNS personnalisés. Ces serveurs DNS assurent la résolution de noms interne pour les machines virtuelles qui résident dans le même réseau virtuel.

Lorsque vous créez une machine virtuelle, un mappage du nom d’hôte à son adresse IP privée est ajouté aux serveurs DNS gérés par Azure. Dans le cas d’une machine virtuelle dotée de plusieurs interfaces réseau, le nom d’hôte est mappé sur l’adresse IP privée de l’interface réseau principale.

Les machines virtuelles configurées avec des serveurs DNS gérés par Azure peuvent résoudre les noms d’hôtes de toutes les machines virtuelles figurant au sein du même réseau virtuel pour les adresses IP privées.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Équilibreurs de charge internes (ILB) et passerelles d’application

Vous pouvez affecter une adresse IP privée à la configuration **frontale** d’un [équilibreur de charge interne Azure](../load-balancer/load-balancer-internal-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (ILB) ou d’une [passerelle d’application Azure](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Cette adresse IP privée sert de point de terminaison interne, accessible uniquement aux ressources de son réseau virtuel, et de réseaux distants connectés au réseau virtuel. Vous pouvez affecter une adresse IP privée statique ou dynamique à la configuration frontale.

### <a name="at-a-glance"></a>Aperçu
Le tableau ci-dessous présente la propriété spécifique par le biais de laquelle une adresse IP publique peut être associée à une ressource de niveau supérieur, ainsi que les méthodes d’allocation possibles (dynamique ou statique) utilisables.

| Ressources de niveau supérieur | Association d’adresse IP | dynamique | statique |
| --- | --- | --- | --- |
| Machine virtuelle |interface réseau |Oui |Oui |
| Équilibrage de charge |Configuration frontale |Oui |Oui |
| Application Gateway |Configuration frontale |Oui |Oui |

## <a name="limits"></a>Limites
Les limites imposées pour l’adressage IP sont indiquées dans l’ensemble des [limites pour la mise en réseau](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) dans Azure. Ces limites sont exprimées par région et par abonnement. Vous pouvez [contacter le support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour augmenter les limites par défaut jusqu’aux limites maximum en fonction des besoins de votre entreprise.

## <a name="pricing"></a>Tarification
Les adresses IP publiques peuvent avoir un coût nominal. Pour en savoir plus sur la tarification des adresses IP dans Azure, lisez la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses).

## <a name="next-steps"></a>Étapes suivantes
* [Déployer une machine virtuelle avec une adresse IP publique statique à l’aide du portail Azure](virtual-network-deploy-static-pip-arm-portal.md)
* [Déployer une machine virtuelle avec une adresse IP publique statique à l’aide d’un modèle](virtual-network-deploy-static-pip-arm-template.md)
* [Déployer une machine virtuelle avec une adresse IP privée statique à l’aide du portail Azure](virtual-networks-static-private-ip-arm-pportal.md)

