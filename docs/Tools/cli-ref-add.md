---
title: NuGet CLI ajouter commande | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Informations de référence pour le nuget.exe ajouter (commande)"
keywords: "Ajouter une référence de NuGet, ajouter la commande de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="99d7a-104">ajouter des commandes (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="99d7a-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="99d7a-105">**S’applique aux**: publication du package &bullet; **versions prises en charge**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="99d7a-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="99d7a-106">Ajoute un package spécifié à une source de package de non-HTTP (un dossier ou un chemin d’accès UNC) de façon hiérarchique, dans lequel les dossiers sont créés pour le numéro d’ID et la version de package.</span><span class="sxs-lookup"><span data-stu-id="99d7a-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="99d7a-107">Exemple :</span><span class="sxs-lookup"><span data-stu-id="99d7a-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="99d7a-108">Lorsque vous restaurez ou mise à jour par rapport à la source du package, disposition hiérarchique fournit améliorer considérablement les performances.</span><span class="sxs-lookup"><span data-stu-id="99d7a-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="99d7a-109">Pour développer tous les fichiers dans le package à la source de package de destination, utilisez la `-Expand` basculer.</span><span class="sxs-lookup"><span data-stu-id="99d7a-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="99d7a-110">Cela se produit généralement dans les sous-dossiers supplémentaires qui apparaissent dans la destination, tel que `tools` et `lib`.</span><span class="sxs-lookup"><span data-stu-id="99d7a-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="99d7a-111">Utilisation</span><span class="sxs-lookup"><span data-stu-id="99d7a-111">Usage</span></span>

```
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="99d7a-112">où `<packagePath>` est le chemin d’accès au package à ajouter, et `<sourcePath>` spécifie la source du package de basé sur le dossier dans lequel le package sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="99d7a-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="99d7a-113">Les sources HTTP ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="99d7a-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="99d7a-114">Options</span><span class="sxs-lookup"><span data-stu-id="99d7a-114">Options</span></span>

| <span data-ttu-id="99d7a-115">Option</span><span class="sxs-lookup"><span data-stu-id="99d7a-115">Option</span></span> | <span data-ttu-id="99d7a-116">Description</span><span class="sxs-lookup"><span data-stu-id="99d7a-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="99d7a-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="99d7a-117">ConfigFile</span></span> | <span data-ttu-id="99d7a-118">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="99d7a-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="99d7a-119">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="99d7a-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="99d7a-120">Expand</span><span class="sxs-lookup"><span data-stu-id="99d7a-120">Expand</span></span> | <span data-ttu-id="99d7a-121">Ajoute tous les fichiers dans le package à la source du package.</span><span class="sxs-lookup"><span data-stu-id="99d7a-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="99d7a-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="99d7a-122">ForceEnglishOutput</span></span> | <span data-ttu-id="99d7a-123">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="99d7a-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="99d7a-124">Help</span><span class="sxs-lookup"><span data-stu-id="99d7a-124">Help</span></span> | <span data-ttu-id="99d7a-125">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="99d7a-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="99d7a-126">Non interactif</span><span class="sxs-lookup"><span data-stu-id="99d7a-126">NonInteractive</span></span> | <span data-ttu-id="99d7a-127">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="99d7a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="99d7a-128">Commentaires</span><span class="sxs-lookup"><span data-stu-id="99d7a-128">Verbosity</span></span> | <span data-ttu-id="99d7a-129">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="99d7a-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="99d7a-130">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="99d7a-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="99d7a-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="99d7a-131">Examples</span></span>

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```