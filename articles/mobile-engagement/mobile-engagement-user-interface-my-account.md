---
title: Interface utilisateur d'Azure Mobile Engagement - Mon compte
description: "Apprenez à gérer le profil de votre compte et à tester les périphériques à l'aide d'Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 22832678-3959-4b8c-9fb2-f2ff5974e5d1
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.translationtype: Human Translation
ms.sourcegitcommit: 06e16033435ed0a37d5688055743875827d3aec2
ms.openlocfilehash: 4e463e973dcfa1faa7b08e4738192161980b3aa2
ms.contentlocale: fr-fr
ms.lasthandoff: 03/01/2017

---
# <a name="how-to-manage-your-account-profile-and-test-devices"></a>Gestion du profil de votre compte et test des périphériques
Cet article décrit la page **d’accueil** du portail **Mobile Engagement**. Le portail **Mobile Engagement** sert à surveiller et à gérer vos applications mobiles. 

Pour accéder à la page **Mon compte** , cliquez sur votre compte en haut de la page.

La section Mon compte de l'interface utilisateur vous permet d'afficher et de modifier les paramètres associés à votre compte, y compris les paramètres de votre profil et les ID de vos appareils de test. Ces paramètres contiennent des éléments auxquels vous pouvez également accéder via l'API de l'appareil.

![Mon compte 1][7]  

## <a name="profile"></a>Profil :
Vous pouvez afficher ou modifier tous les paramètres de votre compte affichés ci-dessous. Vous pouvez également autoriser un autre utilisateur à utiliser votre application grâce à son adresse de messagerie depuis la section [Accueil](mobile-engagement-user-interface-home.md).

![Mon compte 2][8]  

## <a name="devices"></a>Appareils :
Vous pouvez afficher, ajouter ou supprimer l’ID des appareils de test que vous pouvez utiliser pour tester vos campagnes **Reach** et **Push**. Les instructions contextuelles sur la procédure de recherche d'ID de l'appareil des appareils pour chaque plateforme (iOS, Android, Windows Phone, etc.) s'affichent lorsque vous cliquez sur « Nouvel appareil ». 

![Mon compte 3][9]  

Pour utiliser l'API Push ou l'API de l'appareil, vous devez connaître l'identificateur unique de l'appareil de vos utilisateurs (le paramètre deviceid). Vous pouvez le récupérer de plusieurs façons :

1. À partir de votre serveur principal, utilisez la fonctionnalité « Get » de l'API de l'appareil pour obtenir la liste complète des identificateurs d'appareil.
2. À partir de votre application, utilisez le Kit de développement logiciel (SDK) pour l'obtenir. (Sur Android, appelez la fonction getDeviceID() de la classe Agent, et sur iOS lisez la propriété deviceid de la classe Agent).
3. À partir d’une annonce Reach, si l’URL de l’action associée à l’annonce contient le modèle {deviceid}, il sera automatiquement remplacé par l’identificateur de l’appareil à l’origine de l’action.
   http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata will be replaced by: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata 
4. À partir d'une annonce Web Reach, si le code HTML de l'annonce contient le modèle {deviceid}, celui-ci sera automatiquement remplacé par l'identificateur de l'appareil qui affiche l'annonce Web.
   Voici mon identificateur de périphérique : {deviceid} sera remplacé par : Voici mon identificateur de périphérique : XXXXXXXXXXXXXXXX
5. Ouvrez votre application sur votre appareil et créez un Événement dans votre application identifiée.
   À partir de « IU - votre application - Surveillance - Événements - Détails », cherchez l'événement que vous avez créé dans la liste.
   Cliquez sur cet événement dans le Moniteur.
   Vous devriez trouver l'ID de votre appareil dans la liste des appareils qui ont créé cet événement.
   Vous pouvez ensuite copier cet ID de l'appareil et l'enregistrer dans « IU - Mon compte - Appareils - Nouvel appareil - Sélectionnez la plateforme de votre appareil ».
   >(Notez que lorsque l'IDFA est désactivé pour iOS, l'ID de l'appareil peut changer après un certain temps si vous désinstallez et réinstallez votre application).

## <a name="troubleshooting-guide"></a>Guide de résolution des problèmes
* [Guide de résolution des problèmes - Service][Link 24]

## <a name="see-also"></a>Voir aussi
* [Documentation de l'interface utilisateur (IU) - Accueil][Link 13]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md





