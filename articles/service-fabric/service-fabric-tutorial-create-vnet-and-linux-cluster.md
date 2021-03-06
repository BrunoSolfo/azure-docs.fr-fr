---
title: "Créer un cluster Service Fabric dans Azure | Microsoft Docs"
description: "Découvrez comment créer un cluster Linux dans Azure à l’aide d’un modèle."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/16/2017
ms.author: ryanwi
ms.translationtype: HT
ms.sourcegitcommit: c3a2462b4ce4e1410a670624bcbcec26fd51b811
ms.openlocfilehash: aabf3a0767b2f6f96e357dc63f3e8ee737577a1f
ms.contentlocale: fr-fr
ms.lasthandoff: 09/25/2017

---

# <a name="deploy-a-secure-service-fabric-linux-cluster-into-an-azure-virtual-network"></a>Déployer un cluster Linux Service Fabric sécurisé dans un réseau virtuel Azure
Ce didacticiel est le premier de la série. Vous allez apprendre à créer un cluster Service Fabric (Linux) s’exécutant dans Azure, et à le déployer dans un réseau virtuel (VNET) et un sous-réseau existants. Lorsque vous avez terminé, vous disposez d’un cluster en cours d’exécution dans le cloud sur lequel vous pouvez déployer des applications. Pour créer un cluster Windows, consultez [Créer un cluster Windows sécurisé sur Azure à l’aide d’un modèle](service-fabric-tutorial-create-vnet-and-windows-cluster.md).

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un réseau virtuel dans Azure à l’aide d’un modèle
> * Créer un cluster Service Fabric sécurisé dans Azure à l’aide d’un modèle
> * Sécuriser le cluster avec un certificat X.509
> * Se connecter au cluster à l’aide de l’interface de ligne de commande (CLI) de Service Fabric
> * Supprimer un cluster

Cette série de didacticiels vous montre comment effectuer les opérations suivantes :
> [!div class="checklist"]
> * Créer un cluster sécurisé sur Azure à l’aide d’un modèle
> * [Déployer la Gestion des API avec Service Fabric](service-fabric-tutorial-deploy-api-management.md)

## <a name="prerequisites"></a>Prérequis
Avant de commencer ce didacticiel :
- Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- Installez l’[interface de ligne de commande (CLI) de Service Fabric](service-fabric-cli.md).
- Installez [Azure CLI 2.0](/cli/azure/install-azure-cli).

Les procédures suivantes créent un cluster Service Fabric à cinq nœuds. Le cluster est sécurisé par un certificat auto-signé et placé dans un coffre de clés. 

Pour calculer le coût lié à l’exécution d’un cluster Service Fabric dans Azure, utilisez la [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/).
Pour plus d’informations sur la création de clusters Service Fabric, consultez l’article [Créer un cluster Service Fabric à l’aide d’Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="sign-in-to-azure-and-select-your-subscription"></a>Se connecter à Azure et sélectionner un abonnement
Ce guide utilise l’interface de ligne de commande Azure. Lorsque vous démarrez une nouvelle session, connectez-vous à votre compte Azure et sélectionnez votre abonnement avant d’exécuter des commandes Azure.
 
Exécutez le script suivant pour vous connecter à votre compte Azure et sélectionner votre abonnement :

```azurecli
az login
az account set --subscription <guid>
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
Créez un groupe de ressources pour votre déploiement, puis donnez-lui un nom et un emplacement.

```azurecli
ResourceGroupName="sflinuxclustergroup"
Location="southcentralus"
az group create --name $ResourceGroupName --location $Location
```

## <a name="deploy-the-network-topology"></a>Déploiement de la topologie du réseau
Maintenant, configurez la topologie du réseau sur laquelle il est prévu de déployer la Gestion des API et le cluster Service Fabric. Le modèle Resource Manager [network.json][network-arm] est configuré pour créer un réseau virtuel (VNET) ainsi qu’un groupe de sécurité réseau (NSG) associé au sous-réseau pour Service Fabric, et un NSG associé à un sous-réseau pour la Gestion des API. En savoir plus sur les réseaux virtuels, les sous-réseaux et les groupes de sécurité réseau, [ici](../virtual-network/virtual-networks-overview.md).

Le fichier de paramètres [network.parameters.json][network-parameters-arm] contient les noms des sous-réseaux et des groupes de sécurité réseau sur lesquels Service Fabric et la Gestion des API sont déployés.  La Gestion des API est déployée dans le [didacticiel suivant](service-fabric-tutorial-deploy-api-management.md). Pour ce guide, il est inutile de changer les valeurs des paramètres. Les modèles Resource Manager pour Service Fabric utilisent ces valeurs.  Si vous les modifiez ici, vous devez en faire de même dans les autres modèles Resource Manager utilisés dans ce didacticiel et le [didacticiel Déployer la Gestion des API](service-fabric-tutorial-deploy-api-management.md). 

Téléchargez le modèle Resource Manager et le fichier de paramètres suivants :
- [network.json][network-arm]
- [network.parameters.json][network-parameters-arm]

Utilisez le script suivant pour déployer le modèle Resource Manager et les fichiers de paramètres nécessaires à la configuration du réseau :

```azurecli
az group deployment create \
    --name VnetDeployment \
    --resource-group $ResourceGroupName \
    --template-file network.json \
    --parameters @network.parameters.json
```
<a id="createvaultandcert" name="createvaultandcert_anchor"></a>
## <a name="deploy-the-service-fabric-cluster"></a>Déploiement du cluster Service Fabric
Une fois le déploiement des ressources réseau terminé, la prochaine étape consiste à déployer un cluster Service Fabric sur le réseau virtuel dans le sous-réseau et le groupe de sécurité réseau désignés pour le cluster Service Fabric. Dans cette série de didacticiels, le modèle Resource Manager pour Service Fabric est préconfiguré de façon à utiliser les noms du réseau virtuel, sous-réseau et groupe de sécurité réseau que vous avez configurés au cours d’une étape précédente.

Le déploiement d’un cluster sur un réseau virtuel existant et le sous-réseau associé (déployés précédemment dans cet article) nécessite un modèle Resource Manager.  Téléchargez le modèle Resource Manager et le fichier de paramètres suivants :
- [linuxcluster.JSON][cluster-arm]
- [linuxcluster.parameters.json][cluster-parameters-arm]

Renseignez les paramètres **clusterName**, **adminUserName** et **adminPassword** vides dans le fichier `linuxcluster.parameters.json` pour votre déploiement.  Ne renseignez pas les paramètres **certificateThumbprint**, **certificateUrlValue** et **sourceVaultValue** si vous souhaitez créer un certificat auto-signé.  Si vous disposez d’un certificat existant, chargé dans un coffre de clés, renseignez ces valeurs de paramètre.

Utilisez le script suivant pour déployer le cluster à l’aide du modèle Resource Manager et des fichiers de paramètres.  Un certificat auto-signé est créé dans le coffre de clés spécifié et est utilisé pour sécuriser le cluster.  Le certificat est également téléchargé localement.

```azurecli
Password="q6D7nN%6ck@6"
Subject="aztestcluster.southcentralus.cloudapp.azure.com"
VaultName="linuxclusterkeyvault"
az group create --name $ResourceGroupName --location $Location

az sf cluster create --resource-group $ResourceGroupName --location $Location \
   --certificate-output-folder . --certificate-password $Password --certificate-subject-name $Subject \
   --vault-name $VaultName --vault-resource-group $ResourceGroupName  \
   --template-file portalcluster.json --parameter-file portalcluster.parameters.json

```

## <a name="connect-to-the-secure-cluster"></a>Se connecter à un cluster sécurisé
Connectez-vous au cluster à l’aide de votre clé par le biais de la commande `sfctl cluster select` de l’interface de ligne de commande de Service Fabric.  Notez que vous ne pouvez utiliser que l’option **--no-verify** pour un certificat auto-signé.

```azurecli
sfctl cluster select --endpoint https://mysfcluster.southcentralus.cloudapp.azure.com:19080 \
--pem ./aztestcluster201709151446.pem --no-verify
```

Vérifiez que vous êtes connecté et que le cluster est sain à l’aide de la commande `sfctl cluster health`.

```azurecli
sfctl cluster health
```

## <a name="clean-up-resources"></a>Supprimer des ressources

Un cluster est composé d’autres ressources Azure en plus de la ressource de cluster elle-même. Le plus simple pour supprimer le cluster et toutes les ressources qu’il consomme consiste à supprimer le groupe de ressources.

Connectez-vous à Azure et sélectionnez l’ID d’abonnement pour lequel vous souhaitez supprimer le cluster.  Vous pouvez trouver votre ID d’abonnement en vous connectant au [portail Azure](http://portal.azure.com). Pour supprimer un groupe de ressources et toutes les ressources de cluster, utilisez la commande [az group delete](/cli/azure/group?view=azure-cli-latest#az_group_delete).

```azurecli
az group delete --name $ResourceGroupName
```

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créer un réseau virtuel dans Azure à l’aide d’un modèle
> * Créer un cluster Service Fabric sécurisé dans Azure à l’aide d’un modèle
> * Sécuriser le cluster avec un certificat X.509
> * Se connecter au cluster à l’aide de l’interface de ligne de commande (CLI) de Service Fabric
> * Supprimer un cluster

Ensuite, passez au didacticiel suivant pour apprendre à déployer une application existante.
> [!div class="nextstepaction"]
> [Déployer la Gestion des API](service-fabric-tutorial-deploy-api-management.md)


[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/linuxcluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/linuxcluster.parameters.json

