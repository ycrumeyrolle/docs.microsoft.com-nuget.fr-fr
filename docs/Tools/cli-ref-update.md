---
title: NuGet CLI de commande update | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Référence de la commande de mise à jour de nuget.exe"
keywords: "référence de mise à jour de NuGet, commande d’un package de mise à jour"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="5a006-104">commande de mise à jour (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5a006-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="5a006-105">**S’applique à :** package consommation &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="5a006-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5a006-106">Met à jour tous les packages dans un projet (à l’aide de `packages.config`) pour leurs dernières versions disponibles.</span><span class="sxs-lookup"><span data-stu-id="5a006-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="5a006-107">Il est recommandé d’exécuter ['restore'](#restore) avant d’exécuter le `update`.</span><span class="sxs-lookup"><span data-stu-id="5a006-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="5a006-108">(Pour mettre à jour un package individuel, utilisez [ `nuget install` ](cli-ref-install.md) sans spécifier un numéro de version, dans lequel cas NuGet installe la dernière version.)</span><span class="sxs-lookup"><span data-stu-id="5a006-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="5a006-109">Remarque : `update` ne fonctionne pas avec l’interface CLI en cours d’exécution sous Mono (Mac OSX ou Linux).</span><span class="sxs-lookup"><span data-stu-id="5a006-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="5a006-110">La commande également ne fonctionne pas avec les projets à l’aide de `project.json` ou PackageReference gestion formats.</span><span class="sxs-lookup"><span data-stu-id="5a006-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="5a006-111">Le `update` commande met également à jour les références d’assembly dans le fichier projet, condition celles référence déjà exister.</span><span class="sxs-lookup"><span data-stu-id="5a006-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="5a006-112">Si un package de mise à jour a un assembly ajouté, une nouvelle référence est *pas* ajouté.</span><span class="sxs-lookup"><span data-stu-id="5a006-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="5a006-113">Nouvelles dépendances de package est également inutile leurs références d’assembly ajoutées.</span><span class="sxs-lookup"><span data-stu-id="5a006-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="5a006-114">Pour inclure ces opérations dans le cadre d’une mise à jour, mettre à jour le package dans Visual Studio à l’aide du Gestionnaire de Package UI ou la Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="5a006-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="5a006-115">Cette commande peut également servir à mettre à jour de nuget.exe lui-même à l’aide de la *-self* indicateur.</span><span class="sxs-lookup"><span data-stu-id="5a006-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="5a006-116">Utilisation</span><span class="sxs-lookup"><span data-stu-id="5a006-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="5a006-117">où `<configPath>` soit identifie un `packages.config` ou le fichier de solution qui répertorie les dépendances du projet.</span><span class="sxs-lookup"><span data-stu-id="5a006-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="5a006-118">Options</span><span class="sxs-lookup"><span data-stu-id="5a006-118">Options</span></span>

| <span data-ttu-id="5a006-119">Option</span><span class="sxs-lookup"><span data-stu-id="5a006-119">Option</span></span> | <span data-ttu-id="5a006-120">Description</span><span class="sxs-lookup"><span data-stu-id="5a006-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a006-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5a006-121">ConfigFile</span></span> | <span data-ttu-id="5a006-122">*(2.5 +)*  NuGet le fichier de configuration à appliquer.</span><span class="sxs-lookup"><span data-stu-id="5a006-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="5a006-123">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="5a006-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="5a006-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5a006-124">FileConflictAction</span></span> | <span data-ttu-id="5a006-125">*(2.5 +)*  Spécifie l’action à entreprendre lorsque vous êtes invité à remplacer ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="5a006-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5a006-126">Les valeurs sont *remplacer, ignorer, aucun*.</span><span class="sxs-lookup"><span data-stu-id="5a006-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="5a006-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5a006-127">ForceEnglishOutput</span></span> | <span data-ttu-id="5a006-128">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="5a006-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5a006-129">Help</span><span class="sxs-lookup"><span data-stu-id="5a006-129">Help</span></span> | <span data-ttu-id="5a006-130">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="5a006-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="5a006-131">Id</span><span class="sxs-lookup"><span data-stu-id="5a006-131">Id</span></span> | <span data-ttu-id="5a006-132">Spécifie une liste d’ID pour mettre à jour de package.</span><span class="sxs-lookup"><span data-stu-id="5a006-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="5a006-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="5a006-133">MSBuildPath</span></span> | <span data-ttu-id="5a006-134">*(4.0 +)*  Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="5a006-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="5a006-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="5a006-135">MSBuildVersion</span></span> | <span data-ttu-id="5a006-136">*(3.2 +)*  Spécifie la version de MSBuild à utiliser avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="5a006-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="5a006-137">Valeurs prises en charge sont 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="5a006-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="5a006-138">Par défaut que le MSBuild dans votre chemin d’accès est sélectionné, sinon la valeur par défaut pour la version installée la plus élevée de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5a006-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="5a006-139">Non interactif</span><span class="sxs-lookup"><span data-stu-id="5a006-139">NonInteractive</span></span> | <span data-ttu-id="5a006-140">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="5a006-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5a006-141">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="5a006-141">PreRelease</span></span> | <span data-ttu-id="5a006-142">Permet la mise à jour vers les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="5a006-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="5a006-143">Cet indicateur n’est pas nécessaire lors de la mise à jour des versions préliminaires des packages qui sont déjà installés.</span><span class="sxs-lookup"><span data-stu-id="5a006-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="5a006-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="5a006-144">RepositoryPath</span></span> | <span data-ttu-id="5a006-145">Spécifie le dossier local dans lequel les packages sont installés.</span><span class="sxs-lookup"><span data-stu-id="5a006-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="5a006-146">Safe</span><span class="sxs-lookup"><span data-stu-id="5a006-146">Safe</span></span> | <span data-ttu-id="5a006-147">Spécifie qui met à jour uniquement avec la version la plus récente disponible dans la même version majeure et mineure que le package installé sera installé.</span><span class="sxs-lookup"><span data-stu-id="5a006-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="5a006-148">Self</span><span class="sxs-lookup"><span data-stu-id="5a006-148">Self</span></span> | <span data-ttu-id="5a006-149">*(1.4 +)*  Nuget.exe des mises à jour vers la dernière version ; tous les autres arguments sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="5a006-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="5a006-150">Source</span><span class="sxs-lookup"><span data-stu-id="5a006-150">Source</span></span> | <span data-ttu-id="5a006-151">Spécifie la liste des sources de package (en tant qu’URL) pour utiliser les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="5a006-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="5a006-152">Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [NuGet de configuration de comportement](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5a006-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="5a006-153">Commentaires</span><span class="sxs-lookup"><span data-stu-id="5a006-153">Verbosity</span></span> | <span data-ttu-id="5a006-154">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="5a006-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="5a006-155">Version</span><span class="sxs-lookup"><span data-stu-id="5a006-155">Version</span></span> | <span data-ttu-id="5a006-156">Lorsqu’il est utilisé avec un ID de package, spécifie la version du package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="5a006-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="5a006-157">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5a006-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5a006-158">Exemples</span><span class="sxs-lookup"><span data-stu-id="5a006-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```