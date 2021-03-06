---
title: Commande de recherche de l’interface CLI NuGet
description: Référence pour la commande de recherche de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779161"
---
# <a name="search-command-nuget-cli"></a>commande Search (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : 5.8 +

Recherche une source donnée à l’aide de la chaîne de requête fournie. Si aucune source n’est spécifiée, toutes les sources définies dans% AppData% \NuGet\NuGet.config sont utilisées.

## <a name="usage"></a>Utilisation

```cli
nuget search [search terms] [options]
```

où les termes de recherche sont appliqués aux noms des packages, aux balises et aux descriptions des packages, comme c’est le cas lorsque vous les utilisez sur nuget.org.

## <a name="options"></a>Options

| Name | Description | Usage |
| ---  |     ---     |  :-:  |
| Version préliminaire | Les packages de préversion ne sont pas inclus par défaut, mais peuvent être inclus à l’aide de cet argument | -Version préliminaire |
| Source | Source (s) de package spécifique à rechercher au lieu d’interroger les sources par défaut dans __nuget.config__ | -Source `<Source URL>`|
| Take | Nombre de résultats à retourner. La valeur par défaut est 20. | -Take `<positive integer>` |
| Commentaires | Niveau de détail à afficher dans la sortie. La valeur par défaut est _normal_. (Voir la remarque ci-dessous)  | -Verbosité `<quiet|normal|detailed>` |
| Aide | Affiche des informations d’aide pour la commande | -Aide |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

> [!NOTE] 
> Niveaux de détail :
> * _Quiet_ : ID de package, version
> * _normal_ : ID de package, version, téléchargements, aperçu de la description
> * _detailed_ : ID de package, version, téléchargements, description complète, autres informations comme l’URL de la requête

## <a name="examples"></a>Exemples

Rechercher les packages liés à la *journalisation* à partir des sources par défaut :
```
nuget search logging
```
Recherchez des packages liés à la *journalisation* avec un niveau de détail détaillé :
```
nuget search logging -Verbosity detailed
```
Recherchez les packages liés à la *journalisation* et Affichez uniquement les 5 premiers résultats :
```
nuget search logging -Take 5
```
Recherchez des packages *JSON*, y compris des versions préliminaires, à partir de la source/du flux spécifiés :
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Rechercher des packages *JSON* à partir de plusieurs sources/flux :
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
