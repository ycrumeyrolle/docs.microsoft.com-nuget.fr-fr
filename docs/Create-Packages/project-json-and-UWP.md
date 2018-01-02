---
title: Fichier project.json NuGet avec les projets UWP | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 37caf4d7-dabd-4a78-aad2-7d445f818457
description: "Description de la façon dont le fichier project.json est utilisé pour suivre les dépendances NuGet dans les projets de plateforme Windows universelle (UWP)."
keywords: "Dépendances NuGet, NuGet et UWP, UWP et project.json, fichier project.json NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 40507e541997cea368052c373a4124d9c4a00a51
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="19261-104">project.json et UWP</span><span class="sxs-lookup"><span data-stu-id="19261-104">project.json and UWP</span></span>

<span data-ttu-id="19261-105">Ce document décrit la structure du package qui utilise les fonctionnalités de NuGet 3+ (Visual Studio 2015 et versions ultérieures).</span><span class="sxs-lookup"><span data-stu-id="19261-105">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="19261-106">La propriété `minClientVersion` de votre `.nuspec` peut être utilisée pour indiquer que vous avez besoin des fonctionnalités décrites ici en lui affectant la valeur 3.1.</span><span class="sxs-lookup"><span data-stu-id="19261-106">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="19261-107">Ajout de la prise en charge de la plateforme Windows universelle à un package existant</span><span class="sxs-lookup"><span data-stu-id="19261-107">Adding UWP support to an existing package</span></span>

<span data-ttu-id="19261-108">Si vous disposez d’un package existant et que vous souhaitez ajouter la prise en charge des applications de la plateforme Windows universelle (UWP), alors vous n’avez pas besoin d’adopter le format d’empaquetage décrit ici.</span><span class="sxs-lookup"><span data-stu-id="19261-108">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="19261-109">Vous devez uniquement adopter ce format si vous avez besoin des fonctionnalités qu’il décrit et que vous voulez travailler uniquement avec les clients qui ont effectué une mise à jour vers la version 3+ du client NuGet.</span><span class="sxs-lookup"><span data-stu-id="19261-109">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="19261-110">Je cible déjà netcore45</span><span class="sxs-lookup"><span data-stu-id="19261-110">I already target netcore45</span></span>

<span data-ttu-id="19261-111">Si vous ciblez déjà `netcore45` et que vous n’avez pas besoin des fonctionnalités décrites ici, aucune action n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="19261-111">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="19261-112">Les packages `netcore45` peuvent être consommés par les applications UWP.</span><span class="sxs-lookup"><span data-stu-id="19261-112">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="19261-113">Je veux exploiter les API spécifiques de Windows 10</span><span class="sxs-lookup"><span data-stu-id="19261-113">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="19261-114">Dans ce cas, vous devez ajouter le moniker de la version cible de .Net Framework `uap10.0` (TFM ou TxM) à votre package.</span><span class="sxs-lookup"><span data-stu-id="19261-114">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="19261-115">Créez un dossier dans votre package et ajoutez l’assembly qui a été compilé pour utiliser Windows 10 dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="19261-115">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="19261-116">Je n’ai pas besoin des API spécifiques de Windows 10, mais je veux utiliser les nouvelles fonctionnalités .NET ou je n’ai pas encore netcore45</span><span class="sxs-lookup"><span data-stu-id="19261-116">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="19261-117">Dans ce cas, ajoutez le TxM `dotnet` à votre package.</span><span class="sxs-lookup"><span data-stu-id="19261-117">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="19261-118">Contrairement aux autres TxM, `dotnet` n’implique pas de surface d’exposition ni de plateforme.</span><span class="sxs-lookup"><span data-stu-id="19261-118">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="19261-119">Il indique que votre package fonctionne sur n’importe quelle plateforme sur laquelle vos dépendances fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="19261-119">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="19261-120">Quand vous générez un package avec le TxM `dotnet`, vous êtes susceptible d’avoir de nombreuses dépendances propres au TxM dans votre `.nuspec`, puisque vous devez définir les packages BCL dont vous dépendez, comme `System.Text`, `System.Xml`, etc. Les emplacements sur lesquels ces dépendances fonctionnent définissent ceux auxquels votre package fonctionne.</span><span class="sxs-lookup"><span data-stu-id="19261-120">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="19261-121">Comment trouver mes dépendances</span><span class="sxs-lookup"><span data-stu-id="19261-121">How do I find out my dependencies</span></span>

<span data-ttu-id="19261-122">Il existe deux façons de déterminer les dépendances à répertorier :</span><span class="sxs-lookup"><span data-stu-id="19261-122">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="19261-123">Utilisez l’outil [Générateur de dépendances NuSpec](https://github.com/onovotny/ReferenceGenerator) **tiers**.</span><span class="sxs-lookup"><span data-stu-id="19261-123">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="19261-124">Cet outil automatise le processus et met à jour votre fichier `.nuspec` avec les packages dépendants pendant la génération.</span><span class="sxs-lookup"><span data-stu-id="19261-124">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="19261-125">Il est disponible par le biais d’un package NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="19261-125">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>
2. <span data-ttu-id="19261-126">(Méthode plus difficile) Utilisez `ILDasm` pour examiner votre `.dll` pour voir quels assemblys sont en fait nécessaires au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="19261-126">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="19261-127">Déterminez ensuite de quel package NuGet ils proviennent.</span><span class="sxs-lookup"><span data-stu-id="19261-127">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="19261-128">Consultez la rubrique [`project.json`](../Schema/project-json.md) pour plus d’informations sur les fonctionnalités qui facilitent la création d’un package prenant en charge le TxM `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="19261-128">See the [`project.json`](../Schema/project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="19261-129">Si votre package est prévu pour fonctionner avec des projets de la bibliothèque de classes portables, nous vous recommandons fortement de créer un dossier `dotnet`, pour éviter les avertissements et les éventuels problèmes de compatibilité.</span><span class="sxs-lookup"><span data-stu-id="19261-129">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>


## <a name="directory-structure"></a><span data-ttu-id="19261-130">Structure de répertoires</span><span class="sxs-lookup"><span data-stu-id="19261-130">Directory structure</span></span>

<span data-ttu-id="19261-131">Les packages NuGet qui utilisent ce format ont le dossier et les comportements connus suivants :</span><span class="sxs-lookup"><span data-stu-id="19261-131">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="19261-132">Dossier</span><span class="sxs-lookup"><span data-stu-id="19261-132">Folder</span></span> | <span data-ttu-id="19261-133">comportements</span><span class="sxs-lookup"><span data-stu-id="19261-133">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="19261-134">Générer</span><span class="sxs-lookup"><span data-stu-id="19261-134">Build</span></span> | <span data-ttu-id="19261-135">Contient des fichiers de cibles et de propriétés MSBuild dans ce dossier qui sont intégrées différemment au projet, mais à part cela, il n’y a aucun changement.</span><span class="sxs-lookup"><span data-stu-id="19261-135">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="19261-136">Outils</span><span class="sxs-lookup"><span data-stu-id="19261-136">Tools</span></span> | <span data-ttu-id="19261-137">`install.ps1` et `uninstall.ps1` ne sont pas exécutés.</span><span class="sxs-lookup"><span data-stu-id="19261-137">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="19261-138">`init.ps1` fonctionne comme il l’a toujours fait.</span><span class="sxs-lookup"><span data-stu-id="19261-138">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="19261-139">Contenu</span><span class="sxs-lookup"><span data-stu-id="19261-139">Content</span></span> | <span data-ttu-id="19261-140">Le contenu n’est pas copié automatiquement dans le projet de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19261-140">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="19261-141">Une prise en charge de l’inclusion de contenu dans le projet est prévue dans une prochaine version.</span><span class="sxs-lookup"><span data-stu-id="19261-141">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="19261-142">Lib</span><span class="sxs-lookup"><span data-stu-id="19261-142">Lib</span></span> | <span data-ttu-id="19261-143">Pour de nombreux packages, le dossier `lib` fonctionne de la même manière que dans NuGet 2.x, mais avec des options étendues pour les noms utilisables et une meilleure logique pour récupérer le sous-dossier approprié lors de la consommation de packages.</span><span class="sxs-lookup"><span data-stu-id="19261-143">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="19261-144">Toutefois, lorsqu’il est utilisé conjointement avec `ref`, le dossier `lib` contient les assemblys qui implémentent la surface d’exposition définie par les assemblys inclus dans le dossier `ref`.</span><span class="sxs-lookup"><span data-stu-id="19261-144">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="19261-145">Ref</span><span class="sxs-lookup"><span data-stu-id="19261-145">Ref</span></span> | <span data-ttu-id="19261-146">`ref` est un dossier facultatif qui contient des assemblys .NET définissant la surface publique (types et méthodes publics) sur laquelle se compile une application.</span><span class="sxs-lookup"><span data-stu-id="19261-146">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="19261-147">Les assemblys inclus dans ce dossier n’ont peut-être aucune implémentation, ils sont purement utilisés pour définir la surface d’exposition du compilateur.</span><span class="sxs-lookup"><span data-stu-id="19261-147">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="19261-148">Si le package n’a pas de dossier `ref`, alors le dossier `lib` est à la fois l’assembly de référence et l’assembly d’implémentation.</span><span class="sxs-lookup"><span data-stu-id="19261-148">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="19261-149">Runtimes</span><span class="sxs-lookup"><span data-stu-id="19261-149">Runtimes</span></span> | <span data-ttu-id="19261-150">Le dossier `runtimes` est un dossier facultatif qui contient du code spécifique du système d’exploitation, comme l’architecture du processeur et d’autres fichiers binaires dépendant de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="19261-150">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |


## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="19261-151">Fichiers de cibles et de propriétés MSBuild dans des packages</span><span class="sxs-lookup"><span data-stu-id="19261-151">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="19261-152">Les packages NuGet peuvent contenir des fichiers `.targets` et `.props` importés dans un projet MSBuild dans lequel le package est installé.</span><span class="sxs-lookup"><span data-stu-id="19261-152">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="19261-153">Dans NuGet 2.x, il fallait injecter des instructions `<Import>` dans le fichier `.csproj` pour cela. Dans NuGet 3.0, il n’y a pas d’action d’« installation dans le projet » spécifique.</span><span class="sxs-lookup"><span data-stu-id="19261-153">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="19261-154">Le processus de restauration du package écrit plutôt deux fichiers `[projectname].nuget.props` et `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="19261-154">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="19261-155">MSBuild sait rechercher ces deux fichiers et les importe automatiquement au début et à la fin du processus de génération du projet.</span><span class="sxs-lookup"><span data-stu-id="19261-155">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="19261-156">Ce comportement est très similaire à celui de NuGet 2.x, avec une différence majeure : *l’ordre des fichiers de cibles/propriétés n’est pas garanti dans ce cas*.</span><span class="sxs-lookup"><span data-stu-id="19261-156">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="19261-157">Toutefois, MSBuild offre des moyens de définir l’ordre des cibles par le biais des attributs `BeforeTargets` et `AfterTargets` de la définition `<Target>` (consultez [Target, élément (MSBuild)](https://docs.microsoft.com/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="19261-157">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](https://docs.microsoft.com/visualstudio/msbuild/target-element-msbuild).</span></span>


## <a name="lib-and-ref"></a><span data-ttu-id="19261-158">Lib et Ref</span><span class="sxs-lookup"><span data-stu-id="19261-158">Lib and Ref</span></span>

<span data-ttu-id="19261-159">Le comportement du dossier `lib` n’a pas changé de manière significative dans NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="19261-159">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="19261-160">En revanche, tous les assemblys doivent se trouver dans des sous-dossiers nommés comme un TxM. Ils ne peuvent plus être placés directement sous le dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="19261-160">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="19261-161">Un TxM est le nom d’une plateforme pour laquelle une ressource donnée dans un package est supposée travailler.</span><span class="sxs-lookup"><span data-stu-id="19261-161">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="19261-162">Logiquement, il s’agit d’une extension de TFM (moniker de la version cible de .Net Framework). Notamment, `net45`, `net46`, `netcore50` et `dnxcore50` sont tous des exemples de TxM (consultez [Versions cibles de .Net Framework](../Schema/Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="19261-162">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../Schema/Target-Frameworks.md).</span></span> <span data-ttu-id="19261-163">TxM peut faire référence à un framework (TFM) ainsi qu’à d’autres surfaces d’exposition propre à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="19261-163">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="19261-164">Par exemple, le TxM UWP (`uap10.0`) représente la surface d’exposition .NET, ainsi que la surface d’exposition Windows des applications UWP.</span><span class="sxs-lookup"><span data-stu-id="19261-164">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="19261-165">Un exemple de structure lib :</span><span class="sxs-lookup"><span data-stu-id="19261-165">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="19261-166">Le dossier `lib` contient les assemblys utilisés au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="19261-166">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="19261-167">Pour la plupart des packages, un dossier sous `lib` pour chacun de TxM cibles est le seul élément requis.</span><span class="sxs-lookup"><span data-stu-id="19261-167">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="19261-168">Ref</span><span class="sxs-lookup"><span data-stu-id="19261-168">Ref</span></span>

<span data-ttu-id="19261-169">Il existe parfois des cas où un autre assembly doit être utilisé lors de la compilation (c’est le cas des assemblys de référence .NET aujourd’hui).</span><span class="sxs-lookup"><span data-stu-id="19261-169">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="19261-170">Dans ces cas, utilisez un dossier de niveau supérieur appelé `ref` (comprenez « assemblys de référence »).</span><span class="sxs-lookup"><span data-stu-id="19261-170">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="19261-171">La plupart des auteurs de package n’ont pas besoin du dossier `ref`.</span><span class="sxs-lookup"><span data-stu-id="19261-171">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="19261-172">Il s’avère utile pour les packages qui doivent fournir une surface d’exposition cohérente pour la compilation et IntelliSense, mais qui ont une implémentation différente pour différents TxM.</span><span class="sxs-lookup"><span data-stu-id="19261-172">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="19261-173">Les principaux cas d’usage impliquent les packages `System.*` produits dans le cadre de la fourniture de .NET Core sur NuGet.</span><span class="sxs-lookup"><span data-stu-id="19261-173">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="19261-174">Ces packages ont des implémentations différentes unifiées par un ensemble cohérent d’assemblys de référence.</span><span class="sxs-lookup"><span data-stu-id="19261-174">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="19261-175">Mécaniquement, les assemblys inclus dans le dossier `ref` sont les assemblys de référence passés au compilateur.</span><span class="sxs-lookup"><span data-stu-id="19261-175">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="19261-176">Pour ceux qui ont utilisé csc.exe, il s’agit des assemblys que nous passons au commutateur de [l’option C# /reference](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="19261-176">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="19261-177">La structure du dossier `ref` est la même que `lib`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="19261-177">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll


<span data-ttu-id="19261-178">Dans cet exemple, les assemblys inclus dans les répertoires `ref` sont tous identiques.</span><span class="sxs-lookup"><span data-stu-id="19261-178">In this example the assemblies in the `ref` directories would all be identical.</span></span>


## <a name="runtimes"></a><span data-ttu-id="19261-179">Runtimes</span><span class="sxs-lookup"><span data-stu-id="19261-179">Runtimes</span></span>

<span data-ttu-id="19261-180">Le dossier des runtimes contient des assemblys et des bibliothèques natives devant s’exécuter sur des « runtimes » spécifiques, qui sont généralement définis par le système d’exploitation et l’architecture du processeur.</span><span class="sxs-lookup"><span data-stu-id="19261-180">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="19261-181">Ces runtimes sont identifiés à l’aide d’[identificateurs de runtime (RID)](https://docs.microsoft.com/dotnet/core/rid-catalog) comme `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span><span class="sxs-lookup"><span data-stu-id="19261-181">These runtimes are identified using [Runtime Identifiers (RIDs)](https://docs.microsoft.com/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-light-up"></a><span data-ttu-id="19261-182">Éclairage natif</span><span class="sxs-lookup"><span data-stu-id="19261-182">Native light-up</span></span>

<span data-ttu-id="19261-183">L’exemple suivant montre un package qui a une implémentation purement managée pour plusieurs plateformes, mais qui utilise des assistances natives sur Windows 8, où il peut appeler des API natives propres à Windows 8.</span><span class="sxs-lookup"><span data-stu-id="19261-183">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="19261-184">Avec le package ci-dessus, les événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="19261-184">Given the above package the following things happen:</span></span>

- <span data-ttu-id="19261-185">En dehors de Windows 8, l’assembly `lib/net40/MyLibrary.dll` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="19261-185">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="19261-186">Sur Windows 8, `runtimes/win8-<architecture>/lib/MyLibrary.dll` est utilisé et `native/MyNativeHelper.dll` est copié dans la sortie de votre génération.</span><span class="sxs-lookup"><span data-stu-id="19261-186">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="19261-187">Dans l’exemple ci-dessus, l’assembly `lib/net40` est purement du code managé, tandis que les assemblys du dossier des runtimes utilisent p/invoke dans l’assembly d’assistance native pour appeler les API propres à Windows 8.</span><span class="sxs-lookup"><span data-stu-id="19261-187">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="19261-188">Un seul dossier `lib` est sélectionné, donc s’il existe un dossier propre au runtime, il est préféré à un `lib` non propre au runtime.</span><span class="sxs-lookup"><span data-stu-id="19261-188">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it is chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="19261-189">Le dossier natif est additif ; s’il existe, il est copié dans la sortie de la génération.</span><span class="sxs-lookup"><span data-stu-id="19261-189">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="19261-190">Wrapper managé</span><span class="sxs-lookup"><span data-stu-id="19261-190">Managed wrapper</span></span>

<span data-ttu-id="19261-191">Une autre façon d’utiliser les runtimes consiste à fournir un package qui est purement un wrapper managé sur un assembly natif.</span><span class="sxs-lookup"><span data-stu-id="19261-191">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="19261-192">Dans ce scénario, vous créez un package comme le suivant :</span><span class="sxs-lookup"><span data-stu-id="19261-192">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="19261-193">Dans ce cas, il n’y a pas de dossier `lib` de niveau supérieur puisque qu’il n’y a pas d’implémentation de ce package qui ne repose pas sur l’assembly natif correspondant.</span><span class="sxs-lookup"><span data-stu-id="19261-193">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="19261-194">Si l’assembly managé, `MyLibrary.dll`, était exactement le même dans les deux cas, alors nous pouvons le placer dans un dossier `lib` de niveau supérieur, mais étant donné que l’absence d’un assembly natif n’entraîne pas l’échec de l’installation du package s’il a été installé sur une plateforme autre que win-x86 ou win-x64, alors le dossier lib de niveau supérieur est utilisé sans qu’aucun assembly natif ne soit copié.</span><span class="sxs-lookup"><span data-stu-id="19261-194">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>


## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="19261-195">Création de packages pour NuGet 2 et NuGet 3</span><span class="sxs-lookup"><span data-stu-id="19261-195">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="19261-196">Si vous souhaitez créer un package consommable par des projets à l’aide de `packages.config` ainsi que des packages à l’aide de `project.json`, alors les conditions suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="19261-196">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="19261-197">Les dossiers ref et runtimes fonctionnent uniquement sur NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="19261-197">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="19261-198">Ils sont tous les deux ignorés par NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="19261-198">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="19261-199">Vous ne pouvez pas compter sur le fonctionnement de `install.ps1` ou `uninstall.ps1`.</span><span class="sxs-lookup"><span data-stu-id="19261-199">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="19261-200">Ces fichiers s’exécutent lorsque vous utilisez `packages.config`, mais ils sont ignorés avec `project.json`.</span><span class="sxs-lookup"><span data-stu-id="19261-200">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="19261-201">Par conséquent, votre package doit être utilisable sans qu’ils s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="19261-201">So your package needs to be usable without them running.</span></span> <span data-ttu-id="19261-202">`init.ps1` s’exécute toujours sur NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="19261-202">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="19261-203">L’installation des cibles et des propriétés est différente, alors vérifiez que votre package fonctionne comme prévu sur les deux clients.</span><span class="sxs-lookup"><span data-stu-id="19261-203">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="19261-204">Les sous-répertoires de lib doivent être un TxM dans NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="19261-204">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="19261-205">Vous ne pouvez pas placer des bibliothèques à la racine du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="19261-205">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="19261-206">Le contenu n’est pas copié automatiquement avec NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="19261-206">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="19261-207">Les consommateurs de votre package peuvent copier les fichiers eux-mêmes ou utiliser un outil comme un exécuteur de tâches pour automatiser la copie des fichiers.</span><span class="sxs-lookup"><span data-stu-id="19261-207">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="19261-208">Les transformations de fichiers sources et de configuration ne sont pas exécutées par NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="19261-208">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="19261-209">Si vous prenez en charge NuGet 2 et 3, alors votre `minClientVersion` doit être la version la plus basse du client NuGet 2 sur laquelle fonctionne votre package.</span><span class="sxs-lookup"><span data-stu-id="19261-209">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="19261-210">Dans le cas d’un package existant, aucune modification n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="19261-210">In the case of an existing package it shouldn't need to change.</span></span>