---
title: "Services et schémas pris en charge par les journaux de diagnostic Azure | Microsoft Docs"
description: "Découvrez les services pris en charge et le schéma d’événement pour les journaux de diagnostic Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: johnkem
ms.translationtype: HT
ms.sourcegitcommit: c3a2462b4ce4e1410a670624bcbcec26fd51b811
ms.openlocfilehash: 23da12e518d88109fd7271fd363b6c1f099c5ab6
ms.contentlocale: fr-fr
ms.lasthandoff: 09/25/2017

---
# <a name="supported-services-schemas-and-categories-for-azure-diagnostic-logs"></a>Services, schémas et catégories pris en charge pour les journaux de diagnostic Azure

Les [journaux de diagnostic des ressources Azure](monitoring-overview-of-diagnostic-logs.md) sont des journaux générés par vos ressources Azure qui décrivent le fonctionnement de cette ressource. Ces journaux sont spécifiques au type de ressource. Dans cet article, nous présentons l’ensemble des services pris en charge et le schéma d’événement des événements générés par chaque service. Cet article inclut également une liste complète des catégories de journal disponibles par type de ressource.

## <a name="supported-services-and-schemas-for-resource-diagnostic-logs"></a>Services et schémas pris en charge pour les journaux de diagnostic des ressources
Le schéma des journaux de diagnostic des ressources varie en fonction de la ressource et de la catégorie de journal.   

| Service | Schéma et documentation |
| --- | --- |
| API Management | Schéma non disponible. |
| Passerelles d’application |[Journalisation des diagnostics pour Application Gateway](../application-gateway/application-gateway-diagnostics.md) |
| Azure Automation |[Log Analytics pour Azure Automation](../automation/automation-manage-send-joblogs-log-analytics.md) |
| Azure Batch |[Journalisation des diagnostics Azure Batch](../batch/batch-diagnostics.md) |
| Insights client | Schéma non disponible. |
| Réseau de distribution de contenu | Schéma non disponible. |
| CosmosDB | Schéma non disponible. |
| Data Lake Analytics |[Accès aux journaux de diagnostic d’Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) |
| Data Lake Store |[Accès aux journaux de diagnostic d’Azure Data Lake Store](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| Event Hubs |[Journaux de diagnostic d’Azure Event Hubs](../event-hubs/event-hubs-diagnostic-logs.md) |
| Service IoT Hub Provisioning | Schéma non disponible. |
| Key Vault |[Journalisation d’Azure Key Vault](../key-vault/key-vault-logging.md) |
| Load Balancer |[Analytique des journaux de l'équilibreur de charge Azure](../load-balancer/load-balancer-monitor-log.md) |
| Logic Apps |[Schéma de suivi personnalisé Logic Apps B2B](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| Network Security Group |[Analytique des journaux pour les groupes de sécurité réseau (NSG)](../virtual-network/virtual-network-nsg-manage-log.md) |
| Protection DDOS d’adresse IP publique | Schéma non disponible. |
| Recovery Services | Schéma non disponible.|
| Recherche |[Activation et utilisation de la fonctionnalité Rechercher l’analyse du trafic](../search/search-traffic-analytics.md) |
| Gestion de serveur | Schéma non disponible. |
| Service Bus |[Journaux de diagnostic Azure Service Bus](../service-bus-messaging/service-bus-diagnostic-logs.md) |
| Base de données SQL | [Journalisation de diagnostic de base de données SQL Azure](../sql-database/sql-database-metrics-diag-logging.md) |
| Stream Analytics |[Journaux de diagnostic des travaux](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |
| Virtual Network | Schéma non disponible. |

## <a name="supported-log-categories-per-resource-type"></a>Catégories de journaux prises en charge par type de ressource
|Type de ressource|Catégorie|Nom d’affichage de la catégorie|
|---|---|---|
|Microsoft.ApiManagement/service|GatewayLogs|Journaux relatifs à la passerelle ApiManagement|
|Microsoft.Automation/automationAccounts|JobLogs|Journaux de travail|
|Microsoft.Automation/automationAccounts|JobStreams|Flux de travail|
|Microsoft.Automation/automationAccounts|DscNodeStatus|État du nœud DSC|
|Microsoft.Batch/batchAccounts|ServiceLog|Journaux de service|
|Microsoft.Cdn/profiles/endpoints|CoreAnalytics|Obtient les métriques du point de terminaison, par exemple, la bande passante, la sortie, etc.|
|Microsoft.CustomerInsights/hubs|AuditEvents|AuditEvents|
|Microsoft.DataLakeAnalytics/accounts|Audit|Journaux d’audit|
|Microsoft.DataLakeAnalytics/accounts|Requêtes|Journaux de requête|
|Microsoft.DataLakeStore/accounts|Audit|Journaux d’audit|
|Microsoft.DataLakeStore/accounts|Requêtes|Journaux de requête|
|Microsoft.Devices/provisioningServices|DeviceOperations|Opérations sur les appareils|
|Microsoft.Devices/provisioningServices|ServiceOperations|Opérations de service|
|Microsoft.DocumentDB/databaseAccounts|DataPlaneRequests|DataPlaneRequests|
|Microsoft.EventHub/namespaces|ArchiveLogs|Journaux d’archivage|
|Microsoft.EventHub/namespaces|OperationalLogs|Journaux des opérations|
|Microsoft.EventHub/namespaces|AutoScaleLogs|Journaux de mise à l’échelle automatique|
|Microsoft.KeyVault/vaults|AuditEvent|Journaux d’audit|
|Microsoft.Logic/workflows|WorkflowRuntime|Événements de diagnostic de runtime de workflow|
|Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|Suivi des événements de compte d’intégration|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|Événement de groupe de sécurité réseau|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|Compteur de règle de groupe de sécurité réseau|
|Microsoft.Network/loadBalancers|LoadBalancerAlertEvent|Événements d’alerte d’équilibreur de charge|
|Microsoft.Network/loadBalancers|LoadBalancerProbeHealthStatus|État d’intégrité de la sonde d’équilibreur de charge|
|Microsoft.Network/publicIPAddresses|DDoSProtectionNotifications|Notifications de protection DDoS|
|Microsoft.Network/virtualNetworks|VMProtectionAlerts|Alertes de protection de machine virtuelle|
|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|Journal d’accès à la passerelle d’application|
|Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|Journal de performance de la passerelle d’application|
|Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|Journal de pare-feu de la passerelle d’application|
|Microsoft.RecoveryServices/Vaults|AzureBackupReport|Données de rapport de sauvegarde Azure|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryJobs|Travaux Azure Site Recovery|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryEvents|Événements Azure Site Recovery|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicatedItems|Éléments répliqués d’Azure Site Recovery|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicationStats|Statistiques de réplication Azure Site Recovery|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryRecoveryPoints|Points de récupération Azure Site Recovery|
|Microsoft.Search/searchServices|OperationLogs|Journaux des opérations|
|Microsoft.ServiceBus/namespaces|OperationalLogs|Journaux des opérations|
|Microsoft.Sql/servers/databases|QueryStore|Magasin de requêtes|
|Microsoft.Sql/servers/databases|QueryStoreRuntimeStatistics|Statistiques d’exécution du magasin de données des requêtes|
|Microsoft.Sql/servers/databases|QueryStoreWaitStatistics|Statistiques d’attente du magasin de requêtes|
|Microsoft.Sql/servers/databases|Errors|Errors|
|Microsoft.Sql/servers/databases|DatabaseWaitStatistics|Statistiques d’attente de base de données|
|Microsoft.Sql/servers/databases|Timeouts|Délais d’expiration|
|Microsoft.Sql/servers/databases|Blocks|Blocs|
|Microsoft.Sql/servers/databases|SQLInsights|SQL Insights|
|Microsoft.StreamAnalytics/streamingjobs|Exécution|Exécution|
|Microsoft.StreamAnalytics/streamingjobs|Création|Création|

## <a name="next-steps"></a>Étapes suivantes

* [En savoir plus sur les journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md)
* [Diffuser en continu les journaux de diagnostic des ressources vers **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Modifier les paramètres de diagnostic des ressources via l’API REST Azure Monitor](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analyser les journaux du stockage Azure avec Log Analytics](../log-analytics/log-analytics-azure-storage.md)

