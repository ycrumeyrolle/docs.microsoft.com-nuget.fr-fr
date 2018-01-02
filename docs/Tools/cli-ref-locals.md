---
title: Commande de variables locales NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Référence de la commande de variables locales de nuget.exe"
keywords: "référence de variables locales de NuGet, commande de variables locales"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a><span data-ttu-id="d77f1-104">commande de variables locales (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d77f1-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="d77f1-105">**S’applique à :** package consommation &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="d77f1-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d77f1-106">Efface ou des listes de ressources NuGet locales telles que le cache de requête http, le cache de packages et le dossier packages global d’échelle de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d77f1-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="d77f1-107">Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="d77f1-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="d77f1-108">Pour plus d’informations, consultez [gestion du NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="d77f1-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d77f1-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="d77f1-109">Usage</span></span>

```
nuget locals <cache> [options]
```

<span data-ttu-id="d77f1-110">où `<cache>` est un des `all`, `http-cache`, `packages-cache`, `global-packages`, et `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="d77f1-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="d77f1-111">Options</span><span class="sxs-lookup"><span data-stu-id="d77f1-111">Options</span></span>

| <span data-ttu-id="d77f1-112">Option</span><span class="sxs-lookup"><span data-stu-id="d77f1-112">Option</span></span> | <span data-ttu-id="d77f1-113">Description</span><span class="sxs-lookup"><span data-stu-id="d77f1-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d77f1-114">Effacer</span><span class="sxs-lookup"><span data-stu-id="d77f1-114">Clear</span></span> | <span data-ttu-id="d77f1-115">Efface le cache spécifié.</span><span class="sxs-lookup"><span data-stu-id="d77f1-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="d77f1-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d77f1-116">ConfigFile</span></span> | <span data-ttu-id="d77f1-117">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="d77f1-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d77f1-118">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d77f1-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d77f1-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d77f1-119">ForceEnglishOutput</span></span> | <span data-ttu-id="d77f1-120">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="d77f1-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d77f1-121">Help</span><span class="sxs-lookup"><span data-stu-id="d77f1-121">Help</span></span> | <span data-ttu-id="d77f1-122">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="d77f1-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="d77f1-123">Liste</span><span class="sxs-lookup"><span data-stu-id="d77f1-123">List</span></span> | <span data-ttu-id="d77f1-124">Répertorie l’emplacement du cache spécifié, ou les emplacements de tous les caches lorsqu’il est utilisé avec *tous les*.</span><span class="sxs-lookup"><span data-stu-id="d77f1-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="d77f1-125">Non interactif</span><span class="sxs-lookup"><span data-stu-id="d77f1-125">NonInteractive</span></span> | <span data-ttu-id="d77f1-126">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="d77f1-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d77f1-127">Commentaires</span><span class="sxs-lookup"><span data-stu-id="d77f1-127">Verbosity</span></span> | <span data-ttu-id="d77f1-128">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="d77f1-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d77f1-129">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d77f1-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d77f1-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="d77f1-130">Examples</span></span>

```
nuget locals all -list
nuget locals http-cache -clear
```