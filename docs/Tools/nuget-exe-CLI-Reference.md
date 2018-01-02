---
title: "Référence de l’Interface de ligne de commande (CLI) NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d777c424-0cf3-4bc0-8abd-7ca16c22192b
description: "Index de référence de ligne de commande pour l’interface CLI de nuget.exe"
keywords: "index de référence de NuGet.exe, interface de ligne de commande de nuget.exe, nuget.exe CLI, commande nuget"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3d1c3585d8bbf4c9bd9b50c8167e860594a42055
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-cli-reference"></a><span data-ttu-id="c6dc1-104">Référence de NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="c6dc1-104">NuGet CLI reference</span></span>

<span data-ttu-id="c6dc1-105">Le NuGet Interface de ligne de commande (CLI) `nuget.exe`, fournit l’éventail complet des fonctionnalités de NuGet pour installer, créer, publier et gérer les packages sans apporter de modifications aux fichiers de projet.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-105">The NuGet Command Line Interface (CLI), `nuget.exe`, provides the full extent of NuGet functionality to install, create, publish, and manage packages without making any changes to project files.</span></span>

<span data-ttu-id="c6dc1-106">Pour utiliser une commande, ouvrez une fenêtre de commande ou bash shell, puis exécutez `nuget` suivie de la commande et les options appropriées, telles que `nuget help pack` (pour afficher l’aide sur la commande pack).</span><span class="sxs-lookup"><span data-stu-id="c6dc1-106">To use any command, open a command window or bash shell, then run `nuget` followed by the command and appropriate options, such as `nuget help pack` (to view help on the pack command).</span></span>

## <a name="installing-nugetexe"></a><span data-ttu-id="c6dc1-107">L’installation de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c6dc1-107">Installing nuget.exe</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

## <a name="availability"></a><span data-ttu-id="c6dc1-108">Disponibilité</span><span class="sxs-lookup"><span data-stu-id="c6dc1-108">Availability</span></span>

- <span data-ttu-id="c6dc1-109">Toutes les commandes sont disponibles sur Windows.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-109">All commands are available on Windows.</span></span>
- <span data-ttu-id="c6dc1-110">Toutes les commandes de travail avec [nuget.exe en cours d’exécution sur Mono](../guides/install-nuget.md#mac-osx-and-linux) à l’endroit indiqué pour `pack`, `restore`, et `update`.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-110">All commands work with [nuget.exe running on Mono](../guides/install-nuget.md#mac-osx-and-linux) except where indicated for `pack`, `restore`, and `update`.</span></span>
- <span data-ttu-id="c6dc1-111">Le `pack`, `restore`, `delete`, `locals`, et `push` commandes sont également disponibles sur le Mac et Linux via le [dotnet CLI](dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="c6dc1-111">The `pack`, `restore`, `delete`, `locals`, and `push` commands are also available on Mac and Linux through the [dotnet CLI](dotnet-Commands.md).</span></span> 

## <a name="commands-and-applicability"></a><span data-ttu-id="c6dc1-112">Commandes et mise en application</span><span class="sxs-lookup"><span data-stu-id="c6dc1-112">Commands and applicability</span></span>

<span data-ttu-id="c6dc1-113">Commandes disponibles et la mise en application à la création du package, la consommation de package ou publication d’un package vers un ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="c6dc1-113">Available commands and applicability to package creation, package consumption, and/or publishing a package to a host:</span></span>

| <span data-ttu-id="c6dc1-114">Commandes courantes</span><span class="sxs-lookup"><span data-stu-id="c6dc1-114">Common Commands</span></span> | <span data-ttu-id="c6dc1-115">Rôles applicables.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-115">Applicable Roles</span></span> | <span data-ttu-id="c6dc1-116">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="c6dc1-116">NuGet Version</span></span> | <span data-ttu-id="c6dc1-117">Description</span><span class="sxs-lookup"><span data-stu-id="c6dc1-117">Description</span></span> | 
| --- | --- | --- | --- |
| [<span data-ttu-id="c6dc1-118">pack</span><span class="sxs-lookup"><span data-stu-id="c6dc1-118">pack</span></span>](cli-ref-pack.md) | <span data-ttu-id="c6dc1-119">Création</span><span class="sxs-lookup"><span data-stu-id="c6dc1-119">Creation</span></span> | <span data-ttu-id="c6dc1-120">2.7+</span><span class="sxs-lookup"><span data-stu-id="c6dc1-120">2.7+</span></span> | <span data-ttu-id="c6dc1-121">Crée un package NuGet à partir un `.nuspec` ou fichier projet.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-121">Creates a NuGet package from a `.nuspec` or project file.</span></span> <span data-ttu-id="c6dc1-122">Lors de l’exécution sur Mono, la création d’un package à partir d’un fichier de projet n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-122">When running on Mono, creating a package from a project file is not supported.</span></span> |
| [<span data-ttu-id="c6dc1-123">push</span><span class="sxs-lookup"><span data-stu-id="c6dc1-123">push</span></span>](cli-ref-push.md) | <span data-ttu-id="c6dc1-124">Publication</span><span class="sxs-lookup"><span data-stu-id="c6dc1-124">Publishing</span></span> | <span data-ttu-id="c6dc1-125">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-125">All</span></span> | <span data-ttu-id="c6dc1-126">Publie un package à une source de package.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-126">Publishes a package to a package source.</span></span> |
| [<span data-ttu-id="c6dc1-127">configuration</span><span class="sxs-lookup"><span data-stu-id="c6dc1-127">config</span></span>](cli-ref-config.md) | <span data-ttu-id="c6dc1-128">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-128">All</span></span> | <span data-ttu-id="c6dc1-129">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-129">All</span></span> | <span data-ttu-id="c6dc1-130">Obtient ou définit les valeurs de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-130">Gets or sets NuGet configuration values.</span></span> |
| [<span data-ttu-id="c6dc1-131">aide ou ?</span><span class="sxs-lookup"><span data-stu-id="c6dc1-131">help or ?</span></span>](cli-ref-help.md) | <span data-ttu-id="c6dc1-132">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-132">All</span></span> | <span data-ttu-id="c6dc1-133">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-133">All</span></span> | <span data-ttu-id="c6dc1-134">Affiche l’aide des informations ou à l’aide d’une commande.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-134">Displays help information or help for a command.</span></span> |
| [<span data-ttu-id="c6dc1-135">variables locales</span><span class="sxs-lookup"><span data-stu-id="c6dc1-135">locals</span></span>](cli-ref-locals.md) | <span data-ttu-id="c6dc1-136">Consommation</span><span class="sxs-lookup"><span data-stu-id="c6dc1-136">Consumption</span></span> | <span data-ttu-id="c6dc1-137">3.3+</span><span class="sxs-lookup"><span data-stu-id="c6dc1-137">3.3+</span></span> | <span data-ttu-id="c6dc1-138">Efface ou répertorie les packages dans des caches différents ou dans le dossier packages global identifie ces dossiers.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-138">Clears or lists packages in various caches or the global packages folder, or identifies those folders.</span></span> |
| [<span data-ttu-id="c6dc1-139">restore</span><span class="sxs-lookup"><span data-stu-id="c6dc1-139">restore</span></span>](cli-ref-restore.md) | <span data-ttu-id="c6dc1-140">Consommation</span><span class="sxs-lookup"><span data-stu-id="c6dc1-140">Consumption</span></span> | <span data-ttu-id="c6dc1-141">2.7+</span><span class="sxs-lookup"><span data-stu-id="c6dc1-141">2.7+</span></span> | <span data-ttu-id="c6dc1-142">Restaure tous les packages référencés par le format de référence de package en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-142">Restores all packages referenced by the package reference format in use.</span></span> <span data-ttu-id="c6dc1-143">Lors de l’exécution sur Mono, la restauration des packages en utilisant le format PackageReference n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-143">When running on Mono, restoring packages using the PackageReference format is not supported.</span></span> | 
| [<span data-ttu-id="c6dc1-144">setapikey</span><span class="sxs-lookup"><span data-stu-id="c6dc1-144">setapikey</span></span>](cli-ref-setapikey.md) | <span data-ttu-id="c6dc1-145">Publication, la consommation</span><span class="sxs-lookup"><span data-stu-id="c6dc1-145">Publishing, Consumption</span></span> | <span data-ttu-id="c6dc1-146">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-146">All</span></span> | <span data-ttu-id="c6dc1-147">Enregistre une clé d’API pour une source de package donné lors de la source du package nécessite une clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-147">Saves an API key for a given package source when that package source requires a key for access.</span></span> |
| [<span data-ttu-id="c6dc1-148">spécifications</span><span class="sxs-lookup"><span data-stu-id="c6dc1-148">spec</span></span>](cli-ref-spec.md) | <span data-ttu-id="c6dc1-149">Création</span><span class="sxs-lookup"><span data-stu-id="c6dc1-149">Creation</span></span> | <span data-ttu-id="c6dc1-150">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-150">All</span></span> | <span data-ttu-id="c6dc1-151">Génère un `.nuspec` de fichiers, l’utilisation de jetons si la génération du fichier à partir d’un projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-151">Generates a `.nuspec` file, using tokens if generating the file from a Visual Studio project.</span></span> |


| <span data-ttu-id="c6dc1-152">Commandes secondaires</span><span class="sxs-lookup"><span data-stu-id="c6dc1-152">Secondary Commands</span></span> | <span data-ttu-id="c6dc1-153">Rôles applicables.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-153">Applicable Roles</span></span> | <span data-ttu-id="c6dc1-154">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="c6dc1-154">NuGet Version</span></span> | <span data-ttu-id="c6dc1-155">Description</span><span class="sxs-lookup"><span data-stu-id="c6dc1-155">Description</span></span> | 
| --- | --- | --- | --- |
| [<span data-ttu-id="c6dc1-156">add</span><span class="sxs-lookup"><span data-stu-id="c6dc1-156">add</span></span>](cli-ref-add.md) | <span data-ttu-id="c6dc1-157">Publication</span><span class="sxs-lookup"><span data-stu-id="c6dc1-157">Publishing</span></span> | <span data-ttu-id="c6dc1-158">3.3+</span><span class="sxs-lookup"><span data-stu-id="c6dc1-158">3.3+</span></span> | <span data-ttu-id="c6dc1-159">Ajoute un package à une source de package de non-HTTP à l’aide de façon hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-159">Adds a package to a non-HTTP package source using hierarchical layout.</span></span> <span data-ttu-id="c6dc1-160">Pour les sources HTTP, utilisez *push*.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-160">For HTTP sources, use *push*.</span></span> |
| [<span data-ttu-id="c6dc1-161">delete</span><span class="sxs-lookup"><span data-stu-id="c6dc1-161">delete</span></span>](cli-ref-delete.md) | <span data-ttu-id="c6dc1-162">Publication</span><span class="sxs-lookup"><span data-stu-id="c6dc1-162">Publishing</span></span> | <span data-ttu-id="c6dc1-163">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-163">All</span></span> | <span data-ttu-id="c6dc1-164">Supprime ou unlists un package à partir d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-164">Removes or unlists a package from a package source.</span></span> |
| [<span data-ttu-id="c6dc1-165">init</span><span class="sxs-lookup"><span data-stu-id="c6dc1-165">init</span></span>](cli-ref-init.md) | <span data-ttu-id="c6dc1-166">Création</span><span class="sxs-lookup"><span data-stu-id="c6dc1-166">Creation</span></span> | <span data-ttu-id="c6dc1-167">3.3+</span><span class="sxs-lookup"><span data-stu-id="c6dc1-167">3.3+</span></span> | <span data-ttu-id="c6dc1-168">Ajoute des packages à partir d’un dossier à une source de package à l’aide de façon hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-168">Adds packages from a folder to a package source using hierarchical layout.</span></span> |
| [<span data-ttu-id="c6dc1-169">installer</span><span class="sxs-lookup"><span data-stu-id="c6dc1-169">install</span></span>](cli-ref-install.md) | <span data-ttu-id="c6dc1-170">Consommation</span><span class="sxs-lookup"><span data-stu-id="c6dc1-170">Consumption</span></span> | <span data-ttu-id="c6dc1-171">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-171">All</span></span> | <span data-ttu-id="c6dc1-172">Installe un package en cours de projet, mais ne pas modifier des projets ou référencer des fichiers.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-172">Installs a package into the current project but does not modify projects or reference files.</span></span> |
| [<span data-ttu-id="c6dc1-173">list</span><span class="sxs-lookup"><span data-stu-id="c6dc1-173">list</span></span>](cli-ref-list.md) | <span data-ttu-id="c6dc1-174">Consommation, voire de publication</span><span class="sxs-lookup"><span data-stu-id="c6dc1-174">Consumption, perhaps Publishing</span></span> | <span data-ttu-id="c6dc1-175">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-175">All</span></span> | <span data-ttu-id="c6dc1-176">Affiche les packages à partir d’une source donnée.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-176">Displays packages from a given source.</span></span> |
| [<span data-ttu-id="c6dc1-177">mise en miroir</span><span class="sxs-lookup"><span data-stu-id="c6dc1-177">mirror</span></span>](cli-ref-mirror.md) | <span data-ttu-id="c6dc1-178">Publication</span><span class="sxs-lookup"><span data-stu-id="c6dc1-178">Publishing</span></span> | <span data-ttu-id="c6dc1-179">Déconseillé dans 3.2 +</span><span class="sxs-lookup"><span data-stu-id="c6dc1-179">Deprecated in 3.2+</span></span> | <span data-ttu-id="c6dc1-180">Reflète un package et ses dépendances à partir d’une source vers un référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-180">Mirrors a package and its dependencies from a source to a target repository.</span></span> |
| [<span data-ttu-id="c6dc1-181">sources</span><span class="sxs-lookup"><span data-stu-id="c6dc1-181">sources</span></span>](cli-ref-sources.md) | <span data-ttu-id="c6dc1-182">La consommation, publication</span><span class="sxs-lookup"><span data-stu-id="c6dc1-182">Consumption, Publishing</span></span> | <span data-ttu-id="c6dc1-183">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-183">All</span></span> | <span data-ttu-id="c6dc1-184">Gère les sources de package dans les fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-184">Manages package sources in configuration files.</span></span> |
| [<span data-ttu-id="c6dc1-185">mise à jour</span><span class="sxs-lookup"><span data-stu-id="c6dc1-185">update</span></span>](cli-ref-update.md) | <span data-ttu-id="c6dc1-186">Consommation</span><span class="sxs-lookup"><span data-stu-id="c6dc1-186">Consumption</span></span> | <span data-ttu-id="c6dc1-187">Tout</span><span class="sxs-lookup"><span data-stu-id="c6dc1-187">All</span></span> | <span data-ttu-id="c6dc1-188">Met à jour les packages d’un projet pour les dernières versions disponibles.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-188">Updates a project's packages to the latest available versions.</span></span> <span data-ttu-id="c6dc1-189">Non pris en charge sur Mono.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-189">Not supported when running on Mono.</span></span> |

<span data-ttu-id="c6dc1-190">Assurez-vous de différentes commandes utiliser différents [variables d’environnement](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c6dc1-190">Different commands make use of various [Environment variables](cli-ref-environment-variables.md).</span></span>

<span data-ttu-id="c6dc1-191">Commandes de NuGet CLI en rôles applicables :</span><span class="sxs-lookup"><span data-stu-id="c6dc1-191">NuGet CLI commands by applicable roles:</span></span>

| <span data-ttu-id="c6dc1-192">Rôle</span><span class="sxs-lookup"><span data-stu-id="c6dc1-192">Role</span></span> | <span data-ttu-id="c6dc1-193">Commandes</span><span class="sxs-lookup"><span data-stu-id="c6dc1-193">Commands</span></span> |
| --- | --- |
| <span data-ttu-id="c6dc1-194">Consommation</span><span class="sxs-lookup"><span data-stu-id="c6dc1-194">Consumption</span></span> | <span data-ttu-id="c6dc1-195">`config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update`</span><span class="sxs-lookup"><span data-stu-id="c6dc1-195">`config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update`</span></span> | 
| <span data-ttu-id="c6dc1-196">Création</span><span class="sxs-lookup"><span data-stu-id="c6dc1-196">Creation</span></span> | <span data-ttu-id="c6dc1-197">`config`, `help`, `init`, `pack`, `spec`</span><span class="sxs-lookup"><span data-stu-id="c6dc1-197">`config`, `help`, `init`, `pack`, `spec`</span></span> |
| <span data-ttu-id="c6dc1-198">Publication</span><span class="sxs-lookup"><span data-stu-id="c6dc1-198">Publishing</span></span> | <span data-ttu-id="c6dc1-199">`add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources`</span><span class="sxs-lookup"><span data-stu-id="c6dc1-199">`add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources`</span></span> |

<span data-ttu-id="c6dc1-200">Les développeurs soucieux uniquement à la consommation des packages, par exemple, seulement besoin de comprendre que ce sous-ensemble de commandes NuGet.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-200">Developers concerned only with consuming packages, for example, need only understand that subset of NuGet commands.</span></span>

> [!Note]
> <span data-ttu-id="c6dc1-201">Noms d’options de commande respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="c6dc1-201">Command option names are case-insensitive.</span></span> <span data-ttu-id="c6dc1-202">Les options qui sont déconseillées ne sont pas incluses dans cette référence, tel que `NoPrompt` (remplacé par `NonInteractive`) et `Verbose` (remplacé par `Verbosity`).</span><span class="sxs-lookup"><span data-stu-id="c6dc1-202">Options that are deprecated are not included in this reference, such as `NoPrompt` (replaced by `NonInteractive`) and `Verbose` (replaced by `Verbosity`).</span></span>