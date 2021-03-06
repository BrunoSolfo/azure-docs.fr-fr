---
title: "Résoudre les problèmes liés à Azure Files dans Linux | Microsoft Docs"
description: "Résolution des problèmes liés à Azure Files dans Linux"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2017
ms.author: genli
ms.translationtype: HT
ms.sourcegitcommit: c3a2462b4ce4e1410a670624bcbcec26fd51b811
ms.openlocfilehash: c4f46c0ee94cbeb39bc7b28874cd41f1faf5deb5
ms.contentlocale: fr-fr
ms.lasthandoff: 09/25/2017

---
# <a name="troubleshoot-azure-files-problems-in-linux"></a>Résoudre les problèmes liés à Azure Files dans Linux

Cet article répertorie les problèmes courants liés à Microsoft Azure Files quand vous vous connectez à partir de clients Linux. Il fournit également les causes possibles et les solutions de ces problèmes.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a>« [autorisation refusée] Quota de disque dépassé » lorsque vous essayez d’ouvrir un fichier

Dans Linux, vous recevez un message d’erreur semblable au suivant :

**<filename> [autorisation refusée] Quota de disque dépassé**

### <a name="cause"></a>Cause :

Vous avez atteint la limite supérieure de handles ouverts simultanément autorisés pour un fichier.

### <a name="solution"></a>Solution

Réduisez le nombre de handles ouverts simultanément en en fermant certains, puis réessayez l’opération. Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-files-in-linux"></a>Ralentissement des copies de fichiers vers et à partir d’Azure Files dans Linux

-   Si vous n’avez pas d’exigence de taille d’E/S minimum spécifique, nous vous recommandons d’utiliser une taille d’E/S de 1 Mo pour des performances optimales.
-   Si vous connaissez la taille finale d’un fichier que vous étendez à l’aide d’écritures, et si votre logiciel ne présente aucun problème de compatibilité lorsqu’une fin non écrite du fichier contient des zéros, définissez la taille du fichier à l’avance pour éviter que chaque écriture ne soit une écriture d’extension.
-   Utilisez la méthode de copie appropriée :
    -   Utilisez [AZCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) pour les transferts entre deux partages de fichiers.
    -   Utilisez [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre les partages de fichiers sur un ordinateur local.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>« Erreur de montage (112) : l’hôte est hors service » en raison d’un délai d’expiration de reconnexion

L’erreur de montage 112 se produit sur le client Linux s’il est resté inactif pendant une période prolongée. Après une durée d’inactivité prolongée, le client se déconnecte, et la connexion arrive à expiration.  

### <a name="cause"></a>Cause :

La connexion peut être inactive pour les raisons suivantes :

-   Des échecs de communication réseau qui empêchent le rétablissement d’une connexion TCP avec le serveur quand l’option de montage « conditionnel » par défaut est utilisée.
-   Les correctifs de reconnexion récents qui ne sont pas présents dans les anciens noyaux.

### <a name="solution"></a>Solution

Ce problème de reconnexion dans le noyau Linux est maintenant résolu dans le cadre des modifications suivantes :

- [Résoudre le problème de reconnexion pour ne pas différer la reconnexion de la session SMB3 longtemps après la reconnexion du socket](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Appeler le service d’écho immédiatement après la reconnexion du socket](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS : Corriger une éventuelle corruption de la mémoire lors de la reconnexion](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later) (CIFS : corriger un éventuel double verrouillage du mutex lors de la reconnexion [pour les noyaux v4.9 et ultérieurs])](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

Toutefois, il se peut que ces modifications n’aient pas encore été appliquées à l’ensemble des distributions Linux. Ce correctif et les autres correctifs de reconnexion sont apportés dans les noyaux Linux courants suivants : 4.4.40, 4.8.16 et 4.9.1. Vous pouvez obtenir ce correctif en procédant à la mise à niveau vers l’une de ces versions du noyau recommandées.

### <a name="workaround"></a>Solution de contournement

Vous pouvez contourner ce problème en spécifiant un montage inconditionnel. Cela contraint le client à attendre qu’une connexion soit établie ou qu’elle soit interrompue de façon explicite. Ce montage permet également d’empêcher les erreurs causées par les délais d’attente réseau. Toutefois, cette solution de contournement peut provoquer des attentes indéfinies. Préparez-vous à arrêter les connexions si nécessaire.

Si vous ne pouvez pas effectuer de mise à niveau vers les dernières versions du noyau, vous pouvez contourner ce problème en conservant un fichier dans le partage de fichiers Azure dans lequel vous écrivez toutes les 30 secondes au plus. Il doit s’agir d’une opération d’écriture, telle que la réécriture de la date de création ou de modification du fichier. Sinon, vous pouvez obtenir les résultats mis en cache, et votre opération peut ne pas déclencher la reconnexion.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-files-by-using-smb-30"></a>« Erreur de montage (115) : L’opération est en cours » quand vous montez Azure Files à l’aide de SMB 3.0

### <a name="cause"></a>Cause :

Certaines distributions Linux ne prennent pas encore en charge les fonctionnalités de chiffrement dans SMB 3.0, et les utilisateurs peuvent recevoir un message d’erreur « 115 » s’ils essaient de monter Azure Files à l’aide de SMB 3.0, en raison d’une fonctionnalité manquante.

### <a name="solution"></a>Solution

La fonctionnalité de chiffrement pour SMB 3.0 pour Linux a été introduite dans le noyau 4.11. Cette fonctionnalité permet le montage du partage de fichiers Azure en local ou à partir d’une autre région Azure. Quand nous avons publié cet article, cette fonctionnalité a été rétroportée dans Ubuntu 17.04 et Ubuntu 16.10. Si votre client SMB Linux ne prend pas en charge le chiffrement, montez Azure Files à l’aide de SMB 2.1 à partir d’une machine virtuelle Azure Linux se trouvant dans le même centre de données que le compte de stockage de fichiers.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Ralentissement des performances dans un partage de fichiers Azure monté sur une machine virtuelle

### <a name="cause"></a>Cause :

L’une des causes possibles du ralentissement des performances est la désactivation de la mise en cache.

### <a name="solution"></a>Solution

Pour vérifier si la mise en cache est désactivée, recherchez l’entrée **cache=**. 

**cache=none** indique que la mise en cache est désactivée.  Remontez le partage avec la commande de montage par défaut ou en ajoutant explicitement l’option **cache=strict** à la commande de montage pour vérifier l’activation de la mise en cache par défaut ou du mode de mise en cache « strict ».

Dans certains scénarios, l’option de montage **serverino** peut entraîner la commande **ls** à exécuter stat dans chaque entrée de répertoire. Ce comportement provoque une dégradation des performances lorsque vous répertoriez le contenu d’un répertoire volumineux. Vous pouvez vérifier les options de montage dans l’entrée **/etc/fstab** :

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Vous pouvez également vérifier si les options correctes sont utilisées en exécutant la commande **sudo mount | grep cifs** et en vérifiant sa sortie, comme l’exemple de sortie suivant :

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Si l’option **cache=strict** ou **serverino** n’est pas présente, démontez et remontez Azure Files en exécutant la commande de montage à partir de la [documentation](../storage-how-to-use-files-linux.md). Revérifiez ensuite que les options sont correctes pour l’entrée **/etc/fstab**.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a>Les horodatages ont été perdus lors de la copie des fichiers de Windows vers Linux

Sur les plateformes Linux/Unix, la commande **cp -p** échoue si les fichiers 1 et 2 sont détenus par différents utilisateurs.

### <a name="cause"></a>Cause :

L’indicateur Force **f** de COPYFILE provoque l’exécution de la commande **cp -p -f** sur Unix. Cette commande échoue également dans la conservation de l’horodatage du fichier que vous ne possédez pas.

### <a name="workaround"></a>Solution de contournement

Utilisez le nom de l’utilisateur du compte de stockage pour copier les fichiers :

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.

Si vous avez encore besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour résoudre rapidement votre problème.

