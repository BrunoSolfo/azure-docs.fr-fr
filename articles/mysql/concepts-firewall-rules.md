---
title: "Règles de pare-feu d’un serveur de base de données Azure pour MySQL | Microsoft Docs"
description: "Décrit les règles de pare-feu d’un serveur de base de données Azure pour MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.translationtype: Human Translation
ms.sourcegitcommit: 71fea4a41b2e3a60f2f610609a14372e678b7ec4
ms.openlocfilehash: 511cc50c28b9b114b763f3c46cb1e26f15575349
ms.contentlocale: fr-fr
ms.lasthandoff: 05/10/2017

---

# <a name="azure-database-for-mysql-server-firewall-rules"></a>Règles de pare-feu d’un serveur de base de données Azure pour MySQL
Le pare-feu empêche tout accès à votre serveur de base de données jusqu’à ce que vous spécifiiez les ordinateurs qui disposent d’autorisations. Le pare-feu octroie l’accès au serveur en fonction de l’adresse IP d’origine de chaque demande.

Pour configurer votre pare-feu, vous créez des règles de pare-feu qui spécifient les plages d’adresses IP acceptables. Vous pouvez créer des règles de pare-feu au niveau du serveur.

**Règles de pare-feu :** ces règles permettent aux clients d’accéder à l’ensemble de votre serveur de base de données Azure pour MySQL, c’est-à-dire à toutes les bases de données qui se trouvent sur le même serveur logique. Les règles de pare-feu au niveau du serveur peuvent être configurées en utilisant le Portail Azure ou des commandes d’Azure CLI. Pour créer des règles de pare-feu au niveau du serveur, vous devez être le propriétaire de l’abonnement ou collaborateur.

## <a name="firewall-overview"></a>Présentation du pare-feu
Par défaut, tous les accès au serveur de base de données Azure pour MySQL sont bloqués par le pare-feu. Pour pouvoir utiliser votre serveur à partir d’un autre ordinateur, vous devez spécifier une ou plusieurs règles de pare-feu au niveau du serveur afin de permettre l’accès à votre serveur. Utilisez les règles de pare-feu pour spécifier les plages d’adresses IP d’Internet à autoriser. L’accès au site web du Portail Azure proprement dit n’est pas affecté par les règles de pare-feu.

Les tentatives de connexion à partir d’Internet et d’Azure doivent franchir le pare-feu pour pouvoir atteindre votre base de données Azure pour MySQL, comme l’illustre le diagramme suivant :

![Exemple de flux de fonctionnement du pare-feu](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a>Connexion à partir d’Internet
Les règles de pare-feu au niveau du serveur s’appliquent à toutes les bases de données qui se trouvent sur le serveur de base de données Azure pour MySQL.

Si l’adresse IP de la demande appartient à une des plages spécifiées dans les règles de pare-feu au niveau du serveur, la connexion est accordée.

Si l’adresse IP de la demande n’appartient pas aux plages spécifiées dans des règles de pare-feu au niveau du serveur ou de la base de données, la demande de connexion échoue.

## <a name="programmatically-managing-firewall-rules"></a>Gestion par programmation des règles de pare-feu
En dehors du Portail Azure, les règles de pare-feu peuvent être gérées par programmation à l’aide d’Azure CLI. Consultez également la page [Créer et gérer des règles de pare-feu de la base de données Azure pour MySQL à l’aide d’Azure CLI](./howto-manage-firewall-using-cli.md).

## <a name="troubleshooting-the-database-firewall"></a>Dépannage du pare-feu de base de données
Considérez les points suivants quand l’accès au service de serveur de base de données Microsoft Azure pour MySQL présente un comportement anormal :

* **Les modifications apportées à la liste d’approbation n’ont pas encore pris effet :** jusqu’à cinq minutes peuvent s’écouler avant que les modifications apportées à la configuration du pare-feu du serveur de base de données Azure pour MySQL ne soient effectives.

* **La connexion n’est pas autorisée ou un mot de passe incorrect a été utilisé :** si une connexion n’a pas d’autorisations sur le serveur de base de données Azure pour MySQL ou que le mot de passe est incorrect, la connexion au serveur de base de données Azure pour MySQL est refusée. Créer un paramètre de pare-feu permet uniquement aux clients de tenter de se connecter à votre serveur ; chaque client doit fournir les informations d’identification de sécurité nécessaires.

* **Adresse IP dynamique :** si vous avez une connexion Internet avec adressage IP dynamique et que le pare-feu demeure infranchissable, vous pouvez essayer une des solutions suivantes :

* Demandez à votre fournisseur de services Internet (ISP) la plage d’adresses IP affectée à vos ordinateurs clients qui accèdent au serveur de base de données Azure pour MySQL, puis ajoutez cette plage dans une règle de pare-feu.

* Obtenez un adressage IP statique à la place pour vos ordinateurs clients, puis ajoutez les adresses IP en tant que règles de pare-feu.

## <a name="next-steps"></a>Étapes suivantes

[Créer et gérer les règles de pare-feu de la base de données Azure pour MySQL à l’aide du Portail Azure](./howto-manage-firewall-using-portal.md)
[Créer et gérer les règles de pare-feu de la base de données Azure pour MySQL à l’aide d’Azure CLI](./howto-manage-firewall-using-cli.md)

