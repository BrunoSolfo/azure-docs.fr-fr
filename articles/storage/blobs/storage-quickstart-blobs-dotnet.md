---
title: "Guide de démarrage rapide Azure - Transférer des objets vers/à partir de Stockage Blob Azure avec .NET | Microsoft Docs"
description: "Apprenez rapidement à transférer des objets vers/à partir de Stockage Blob Azure avec .NET"
services: storage
documentationcenter: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/01/2017
ms.author: robinsh
ms.translationtype: HT
ms.sourcegitcommit: c3a2462b4ce4e1410a670624bcbcec26fd51b811
ms.openlocfilehash: 97bacc2c1285fe4a467a54f224bb9fabbd851fee
ms.contentlocale: fr-fr
ms.lasthandoff: 09/25/2017

---

# <a name="transfer-objects-tofrom-azure-blob-storage-using-net"></a>Transférer des objets vers/à partir de Stockage Blob Azure avec .NET

Dans ce guide de démarrage rapide, vous apprenez à utiliser C#.NET pour charger, télécharger et lister des objets blob de blocs dans un conteneur Stockage Blob Azure sur Windows.

## <a name="prerequisites"></a>Prérequis

Pour effectuer ce démarrage rapide :

* Installez [Visual Studio 2017](https://www.visualstudio.com/en-us/visual-studio-homepage-vs.aspx) avec la charge de travail suivante :
    - **Développement Azure**

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="create-a-storage-account-using-the-azure-portal"></a>Créer un compte de stockage dans le portail Azure

Commencez par créer un compte de stockage à usage général pour les besoins de ce guide de démarrage rapide. 

1. Accédez au [portail Azure](https://portal.azure.com) et connectez-vous avec votre compte Azure. 
2. Dans le menu Hub, sélectionnez **Nouveau** > **Stockage** > **Compte de stockage - blob, fichier, table, file d’attente**. 
3. Entrez un nom pour votre compte de stockage. Le nom doit contenir entre 3 et 24 caractères, et uniquement des lettres minuscules et des chiffres. Il doit également être unique.
4. Définissez `Deployment model` sur **Resource Manager**.
5. Définissez `Account kind` sur **Usage général**.
6. Définissez `Performance` sur **Standard**. 
7. Définissez `Replication` sur **Stockage localement redondant (LRS)**.
8. Définissez `Storage service encryption` sur **Désactivé**.
9. Définissez `Secure transfer required` sur **Désactivé**.
10. Sélectionnez votre abonnement. 
11. Pour `resource group`, créez-en un et donnez-lui un nom unique. 
12. Sélectionnez le paramètre `Location` à utiliser pour votre compte de stockage.
13. Cochez **Épingler au tableau de bord** et cliquez sur **Créer** pour créer votre compte de stockage. 

Une fois votre compte de stockage créé, il est épinglé au tableau de bord. Cliquez sur le compte pour l’ouvrir. Sous PARAMÈTRES, cliquez sur **Clés d’accès**. Sélectionnez une clé et copiez la CHAÎNE DE CONNEXION dans le Presse-papiers, puis collez-la dans le Bloc-notes pour l’utiliser plus tard.

## <a name="download-the-sample-application"></a>Téléchargement de l'exemple d'application

L’exemple d’application utilisé dans ce guide de démarrage rapide est une application console de base. 

Utilisez [git](https://git-scm.com/) pour télécharger une copie de l’application dans votre environnement de développement. 

```bash
git clone https://github.com/Azure-Samples/storage-blobs-dotnet-quickstart.git
```

Cette commande clone le dépôt dans votre dossier git local. Pour ouvrir la solution Visual Studio, recherchez le dossier storage-blobs-dotnet-quickstart, ouvrez-le et double-cliquez sur storage-blobs-dotnet-quickstart.sln. 

## <a name="configure-your-storage-connection-string"></a>Configurer votre chaîne de connexion de stockage

Dans l’application, vous devez fournir la chaîne de connexion de votre compte de stockage. Ouvrez le fichier `app.config` à partir de l’Explorateur de solutions dans Visual Studio. Recherchez l’entrée StorageConnectionString. Dans le champ **valeur**, remplacez la valeur entière de la chaîne de connexion par celle que vous avez enregistrée à partir du portail Azure dans le Bloc-notes. Vous devez obtenir un résultat de ce type.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;
    AccountName=youraccountname;
    AccountKey=7NGE5jasdfdRzASDFNOMEx1u20W/thisisjustC/anexampleZK/Rt5pz2xNRrDckyv8EjB9P1WGF==" />
  </appSettings>
</configuration>
```

## <a name="run-the-sample"></a>Exécution de l'exemple

Cet exemple crée un fichier de test dans Mes Documents, le charge dans Stockage Blob, liste les objets blob dans le conteneur, puis télécharge le fichier avec un nouveau nom pour vous permettre de comparer les fichiers anciens et nouveaux. 

Exécutez l’exemple en appuyant sur F5. La sortie s’affiche dans une fenêtre de console et ressemble à ce qui suit : 

```
Temp file = C:\Users\azureuser\Documents\QuickStart_cbd5f95c-6ab8-4cbf-b8d2-a58e85d7a8e8.txt
Uploading to Blob storage as blob 'QuickStart_cbd5f95c-6ab8-4cbf-b8d2-a58e85d7a8e8.txt'
List blobs in container.
https://mystorage.blob.core.windows.net/quickstartblobs/QuickStart_cbd5f95c-6ab8-4cbf-b8d2-a58e85d7a8e8.txt
Downloading blob to C:\Users\azureuser\Documents\QuickStart_cbd5f95c-6ab8-4cbf-b8d2-a58e85d7a8e8_DOWNLOADED.txt
```

Quand vous appuyez sur n’importe quelle touche pour continuer, le conteneur de stockage et les fichiers sont supprimés. Avant de continuer, recherchez les deux fichiers dans Mes documents : vous pouvez les ouvrir et vérifier qu’ils sont identiques. Copiez l’URL de l’objet blob en dehors de la fenêtre de console et collez-la dans un navigateur pour afficher le contenu du fichier dans Stockage Blob.

Vous pouvez également utiliser un outil comme l’[Explorateur Stockage Azure](http://storageexplorer.com/?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) pour afficher les fichiers dans Stockage Blob. L’Explorateur Stockage Azure est un outil multiplateforme gratuit qui vous permet d’accéder aux informations de votre compte de stockage. 

Une fois que vous avez vérifié les fichiers, appuyez sur n’importe quelle touche pour terminer la démonstration et supprimer les fichiers de test. Maintenant que vous avec compris l’exemple, ouvrez le fichier Program.cs pour examiner le code. 

## <a name="get-references-to-the-storage-objects"></a>Obtenir des références aux objets de stockage

La première chose à faire est de créer les références aux objets utilisés pour accéder et gérer Stockage Blob. Ces objets reposent l’un sur l’autre : chacun est utilisé par le suivant dans la liste.

* Instanciez l’objet **CloudStorageAccount** pointant vers le compte de stockage. 

* Instanciez l’objet **CloudBlobClient** pointant vers le service Blob de votre compte de stockage. 

* Instanciez l’objet **CloudBlobContainer** qui représente le conteneur auquel vous accédez. Les conteneurs sont utilisés pour organiser vos objets blob de la même façon que vous utilisez des dossiers pour organiser vos fichiers sur votre ordinateur.

Une fois que vous avez le **CloudBlobContainer**, vous pouvez instancier l’objet **CloudBlockBlob** qui pointe vers l’objet blob spécifique qui vous intéresse, et effectuer une opération de chargement, téléchargement, copie, etc.

Dans cette section, vous instanciez les objets, créez un conteneur, puis définissez des autorisations sur le conteneur pour les objets blob soient publics et accessibles par une simple URL. Le conteneur est appelé **quickstartblobs**. 

Cet exemple utilise CreateIfNotExists, car nous voulons créer un conteneur chaque fois que l’exemple est exécuté. Dans un environnement de production où vous utilisez le même conteneur pour toute l’application, il est préférable d’appeler une seule fois CreateIfNotExists, ou de créer le conteneur à l’avance pour ne pas avoir à le créer dans le code.

```csharp
// Create a CloudStorageAccount instance pointing to your storage account.
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the CloudBlobClient that is used to call the Blob Service for that storage account.
CloudBlobClient cloudBlobClient = storageAccount.CreateCloudBlobClient();

// Create a container called 'quickstartblobs'. 
CloudBlobContainer cloudBlobContainer = 
    cloudBlobClient.GetContainerReference("quickstartblobs");
await cloudBlobContainer.CreateIfNotExistsAsync();

// Set the permissions so the blobs are public. 
BlobContainerPermissions permissions = new BlobContainerPermissions();
permissions.PublicAccess = BlobContainerPublicAccessType.Blob;
await cloudBlobContainer.SetPermissionsAsync(permissions);
```

## <a name="upload-blobs-to-the-container"></a>Charger des objets blob dans le conteneur

Stockage Blob prend en charge les objets blob de blocs, d’ajout et de pages. Les objets blob de blocs sont les plus couramment utilisés et nous les utilisons donc dans ce guide de démarrage rapide. 

Pour charger un fichier dans un objet blob, obtenez une référence à l’objet blob dans le conteneur cible. Une fois que vous avez la référence d’objet blob, vous pouvez y charger des données à l’aide de [CloudBlockBlob.UploadFromFileAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromfileasync). Cette opération crée l’objet blob s’il n’existe pas déjà, et le remplace s’il existe.

L’exemple de code crée un fichier local à utiliser pour le chargement et le téléchargement, en stockant le fichier à charger comme **fileAndPath** et le nom de l’objet blob dans **localFileName**. L'exemple suivant charge le fichier dans votre conteneur nommé **quickstartblobs**.

```csharp
// Create a file in MyDocuments to test the upload and download.
string localPath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
string localFileName = "QuickStart_" + Guid.NewGuid().ToString() + ".txt";
string fileAndPath = Path.Combine(localPath, localFileName);
File.WriteAllText(fileAndPath, "Hello, World!");

//Upload the file.
CloudBlockBlob blockBlob = container.GetBlockBlobReference(localFileName);
await blockBlob.UploadFromFileAsync(fileAndPath);
```

Il existe plusieurs méthodes de chargement que vous pouvez utiliser avec Stockage Blob. Par exemple, si vous avez un flux de mémoire, vous pouvez utiliser la méthode UploadFromStreamAsync au lieu de UploadFromFileAsync. 

Les objets blob de blocs peuvent atteindre une taille maximale de 4.7 To et peuvent représenter toutes sortes d’éléments allant des feuilles de calcul Excel aux fichiers vidéo volumineux. Les objets blob de pages sont principalement utilisés pour les fichiers VHD utilisés pour stocker des machines virtuelles IaaS. Les objets blob d’ajout sont utilisés pour la journalisation, par exemple, quand vous voulez écrire dans un fichier et continuer à ajouter d’autres informations. La plupart des objets stockés dans Stockage Blob sont des objets blob de blocs.

## <a name="list-the-blobs-in-a-container"></a>Créer la liste des objets blob d’un conteneur

Obtenez la liste des fichiers du conteneur à l’aide de [CloudBlobContainer.ListBlobsSegmentedAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobssegmentedasync). Le code suivant récupère la liste des objets blob, puis effectue une itération sur ces derniers pour montrer les URI des objets blob rencontrés. Vous pouvez copier l’URI à partir de la fenêtre Commande et la coller dans un navigateur pour afficher le fichier.

Si vous avez moins de 5 000 objets blob dans le conteneur, tous les noms d’objets blob sont récupérés en un appel à ListBlobsSegmentedAsync. Si vous avez plus de 5 000 objets blob dans le conteneur, le service récupère la liste par groupes de 5 000 jusqu'à ce que tous les noms d’objets blob soient récupérés. La première fois que cette API est appelée, elle retourne les 5 000 premiers noms d’objet blob et un jeton de liaison. La deuxième fois, vous fournissez le jeton et le service récupère le groupe suivant de noms d’objet blob et ainsi de suite, jusqu'à la nullité du jeton de continuation, qui indique que tous les noms d’objet blob ont été récupérés. 

```csharp
// List the blobs in the container.
Console.WriteLine("List blobs in container.");
BlobContinuationToken blobContinuationToken = null;
do
{
    var results = await cloudBlobContainer.ListBlobsSegmentedAsync(null, blobContinuationToken);
    foreach(IListBlobItem item in results.Results)
    {
        Console.WriteLine(item.Uri);
    }
} while (blobContinuationToken != null);
```

## <a name="download-blobs"></a>Télécharger des objets blob

Téléchargez des objets blob sur votre disque local à l’aide de [CloudBlob.DownloadToFileAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadtofileasync).

Le code suivant télécharge l’objet blob chargé dans la section précédente et ajoute le suffixe « _DOWNLOADED » au nom de l’objet blob pour pouvoir voir les deux fichiers sur le disque local. 

```csharp
// Download blob. In most cases, you would have to retrieve the reference
//   to cloudBlockBlob here. However, we created that reference earlier, and 
//   haven't changed the blob we're interested in, so we can reuse it. 
// First, add a _DOWNLOADED before the .txt so you can see both files in MyDocuments.
string fileAndPath2 = fileAndPath.Replace(".txt", "_DOWNLOADED.txt");
Console.WriteLine("Downloading blob to {0}", fileAndPath2);
await cloudBlockBlob.DownloadToFileAsync(fileAndPath2, FileMode.Create);
```

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’avez plus besoin des objets blob chargés dans ce guide de démarrage rapide, vous pouvez supprimer le conteneur à l’aide de [CloudBlobContainer.DeleteAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteasync). Supprimez aussi les fichiers créés s’ils ne sont plus nécessaires.

```csharp
await cloudBlobContainer.DeleteAsync();
File.Delete(fileAndPath);
File.Delete(fileAndPath2);    
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez appris à transférer des fichiers entre un disque local et Stockage Blob Azure avec .NET. Pour en savoir plus sur l’utilisation de Stockage Blob, consultez le Guide pratique de Stockage Blob.

> [!div class="nextstepaction"]
> [Guide pratique des opérations Stockage Blob](storage-dotnet-how-to-use-blobs.md)

Pour plus d’informations sur l’Explorateur Stockage et les objets blob, consultez [Gérer les ressources de stockage Blob Azure avec l’Explorateur Stockage](../../vs-azure-tools-storage-explorer-blobs.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

