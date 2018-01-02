---
title: "Vue d’ensemble et flux de travail de la création de packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: feb7918c-4709-48a4-a106-8d65c41014dc
description: "Vue d’ensemble du processus de création et de publication d’un package NuGet, avec des liens vers d’autres parties particulières du processus."
keywords: "Création de packages NuGet, vue d’ensemble de la création NuGet, flux de travail de la création NuGet, flux de travail de la création de packages, vue d’ensemble de la création de packages."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 25822d22c53c07e4c1a2f4ab310c4a5da09b7661
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="package-creation-workflow"></a><span data-ttu-id="90449-104">Flux de travail de la création de packages</span><span class="sxs-lookup"><span data-stu-id="90449-104">Package creation workflow</span></span>

<span data-ttu-id="90449-105">La création d’un package commence par le code compilé (en général, des assemblys .NET) à empaqueter et à partager en utilisant la galerie nuget.org publique ou une galerie privée au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="90449-105">Creating a package starts with the compiled code (typically .NET assemblies) that you want to package and share with others, either through the public nuget.org gallery or a private gallery within your organization.</span></span> <span data-ttu-id="90449-106">Le package peut également inclure des fichiers supplémentaires comme un fichier Lisez-moi qui s’affiche pendant son installation, ainsi que des transformations apportées à certains fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="90449-106">The package can also include additional files such as a readme that is displayed when the package is installed, and can include transformations to certain project files.</span></span>

<span data-ttu-id="90449-107">Un package peut également servir à uniquement extraire d’autres dépendances, sans contenir de code propre.</span><span class="sxs-lookup"><span data-stu-id="90449-107">A package can also serve to only pull in any number of other dependencies, without containing any code of its own.</span></span> <span data-ttu-id="90449-108">Ce type de package est un moyen pratique de fournir un kit SDK composé de plusieurs packages indépendants.</span><span class="sxs-lookup"><span data-stu-id="90449-108">Such a package is a convenient way to deliver an SDK that's composed of multiple independent packages.</span></span> <span data-ttu-id="90449-109">Dans d’autres cas, un package peut contenir uniquement des fichiers (`.pdb`) de symboles pour faciliter le débogage.</span><span class="sxs-lookup"><span data-stu-id="90449-109">In other cases, a package may contain only symbol (`.pdb`) files to aid debugging.</span></span>

> [!Note]
> <span data-ttu-id="90449-110">Lorsque vous créez un package pour qu’il soit utilisé par d’autres développeurs, il est important de comprendre que ceux-ci deviennent dépendants de votre travail.</span><span class="sxs-lookup"><span data-stu-id="90449-110">When you create a package for use by other developers, it's important to understand that they are taking a dependency on your work.</span></span> <span data-ttu-id="90449-111">C’est pourquoi la création et la publication d’un package impliquent aussi de s’engager à corriger les bogues et à apporter d’autres mises à jour, ou tout du moins, à rendre le package disponible en open source afin que d’autres puissent participer à sa maintenance.</span><span class="sxs-lookup"><span data-stu-id="90449-111">As such, creating and publishing a package also implies a commitment to fixing bugs and making other updates, or at the very least making the package available as open source so others can help to maintain it.</span></span>

<span data-ttu-id="90449-112">Dans tous les cas, la création d’un package commence par déterminer quels assemblys et autres fichiers doivent être empaquetés.</span><span class="sxs-lookup"><span data-stu-id="90449-112">Whatever the case, creating a package begins with deciding which assemblies and other files to package.</span></span> <span data-ttu-id="90449-113">Ensuite, vous créez un fichier manifeste, appelé fichier `.nuspec`, pour décrire le contenu du package, ainsi que son identificateur, son numéro de version, ses informations de copyright, ses cibles et propriétés MSBuild, etc.</span><span class="sxs-lookup"><span data-stu-id="90449-113">You then create a manifest file, referred to as a `.nuspec` file, to describe the package's contents along with its identifer, version number, copyright information, MSBuild props and targets, and much more.</span></span>

<span data-ttu-id="90449-114">Lorsque vous avez préparé tous les fichiers nécessaires dans les dossiers appropriés et que vous avez créé le fichier `.nuspec` approprié, utilisez la commande `nuget pack` (ou la [cible MSBuild pack](../Schema/msbuild-targets.md)) pour tout placer dans un fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="90449-114">When you've prepared all the necessary files in the appropriate folders and have created the appropriate `.nuspec` file, you then use the `nuget pack` command (or the [MSBuild pack target](../Schema/msbuild-targets.md)) to put everything together into a `.nupkg` file.</span></span> <span data-ttu-id="90449-115">Ensuite, vous êtes prêt à déployer le package sur l’hôte qui le met à la disposition d’autres développeurs.</span><span class="sxs-lookup"><span data-stu-id="90449-115">You're then ready to deploy the package to whatever host makes it available to other developers.</span></span>

> [!Tip]
> <span data-ttu-id="90449-116">Un package NuGet portant l’extension `.nupkg` n’est qu’un fichier ZIP.</span><span class="sxs-lookup"><span data-stu-id="90449-116">A NuGet package with the `.nupkg` extension is simply a ZIP file.</span></span> <span data-ttu-id="90449-117">Pour examiner facilement le contenu d’un package, remplacez l’extension par `.zip` et développez son contenu comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="90449-117">To easily examine any package's contents, change the extension to `.zip` and expand its contents as usual.</span></span> <span data-ttu-id="90449-118">Veillez simplement à remodifier l’extension en `.nupkg` avant d’essayer de charger le package sur un hôte.</span><span class="sxs-lookup"><span data-stu-id="90449-118">Just be sure to change the extension back to `.nupkg` before attempting to upload it to a host.</span></span>

<span data-ttu-id="90449-119">Pour apprendre et comprendre le processus de création, commencez par [Création d’un package](../create-packages/creating-a-package.md), qui vous guide tout au long des processus de base communs à tous les packages.</span><span class="sxs-lookup"><span data-stu-id="90449-119">To learn and understand the creation process, start with [Creating a package](../create-packages/creating-a-package.md) which guides you through the core processes common to all packages.</span></span> 

<span data-ttu-id="90449-120">À partir de là, vous pouvez envisager plusieurs autres options pour votre package :</span><span class="sxs-lookup"><span data-stu-id="90449-120">From there, you can consider a number of other options for your package:</span></span>

-  <span data-ttu-id="90449-121">[Prise en charge de plusieurs frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md) décrit comment créer un package avec plusieurs variantes pour différents .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="90449-121">[Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md) describes how to create a package with multiple variants for different .NET Frameworks.</span></span>
-  <span data-ttu-id="90449-122">[Création de packages localisés](../create-packages/creating-localized-packages.md) décrit comment structurer un package avec plusieurs ressources linguistiques et comment utiliser des packages satellites localisés distincts.</span><span class="sxs-lookup"><span data-stu-id="90449-122">[Creating Localized Packages](../create-packages/creating-localized-packages.md) describes how to structure a package with multiple language resources and how to use separate localized satellite packages.</span></span>
-  <span data-ttu-id="90449-123">[Packages en préversion](../create-packages/prerelease-packages.md) montre comment publier des packages alpha, bêta et rc pour les clients intéressés.</span><span class="sxs-lookup"><span data-stu-id="90449-123">[Pre-release Packages](../create-packages/prerelease-packages.md) demonstrates how to release alpha, beta, and rc packages to those customers who are interested.</span></span>
-  <span data-ttu-id="90449-124">[Transformations de fichiers sources et de configuration](../create-packages/source-and-config-file-transformations.md) décrit comment effectuer des remplacements unilatéraux de jetons dans les fichiers ajoutés à un projet et modifier `web.config` et `app.config` avec des paramètres qui s’annulent à la désinstallation du package.</span><span class="sxs-lookup"><span data-stu-id="90449-124">[Source and Config File Transformations](../create-packages/source-and-config-file-transformations.md) describes how you can do both one-way token replacements in files that are added to a project, and modify `web.config` and `app.config` with settings that are also backed out when the package is uninstalled.</span></span>
-  <span data-ttu-id="90449-125">[Packages de symboles](../create-packages/symbol-packages.md) propose des conseils pour fournir des symboles relatifs à votre bibliothèque visant à permettre aux consommateurs de parcourir votre code pendant le débogage.</span><span class="sxs-lookup"><span data-stu-id="90449-125">[Symbol Packages](../create-packages/symbol-packages.md) offers guidance for supplying symbols for your library that allow consumers to step into your code while debugging.</span></span>
-  <span data-ttu-id="90449-126">[Gestion des versions de package](../reference/package-versioning.md) explique comment identifier les versions exactes que vous autorisez pour vos dépendances (autres packages que vous consommez à partir de votre package).</span><span class="sxs-lookup"><span data-stu-id="90449-126">[Package versioning](../reference/package-versioning.md) discusses how to identify the exact versions that you allow for your dependencies (other packages that you consume from your package).</span></span>
-  <span data-ttu-id="90449-127">[Packages natifs](../create-packages/native-packages.md) décrit le processus de création d’un package pour les consommateurs C++.</span><span class="sxs-lookup"><span data-stu-id="90449-127">[Native Packages](../create-packages/native-packages.md) describes the process for creating a package for C++ consumers.</span></span>

<span data-ttu-id="90449-128">Lorsque vous êtes prêt à publier un package sur nuget.org, suivez le processus simple décrit dans [Publier un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="90449-128">When you're then ready to publish a package to nuget.org, follow the simple process in [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="90449-129">Si vous voulez utiliser un flux privé au lieu de nuget.org, consultez [Vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="90449-129">If you want to use a private feed instead of nuget.org, see the [Hosting Packages Overview](../hosting-packages/overview.md)</span></span>