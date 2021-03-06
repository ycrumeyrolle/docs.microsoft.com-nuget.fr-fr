---
title: Définir un type de package NuGet
description: Décrit les types de packages pour indiquer l’utilisation prévue d’un package.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774369"
---
# <a name="set-a-nuget-package-type"></a>Définir un type de package NuGet

Avec NuGet 3.5+, les packages peuvent être marqués avec un *type de package* spécifique pour indiquer leur usage prévu. Les packages non marqués avec un type, notamment tous les packages créés avec des versions antérieures de NuGet, sont du type `Dependency` par défaut.

- Les packages de type `Dependency` ajoutent des ressources de build ou d’exécution aux bibliothèques et applications et peuvent être installés dans n’importe quel type de projet (en supposant qu’ils soient compatibles).

- Les packages de type `DotnetTool` sont des extensions de la [CLI dotnet](/dotnet/articles/core/tools/index) et ils sont appelés à partir de la ligne de commande. De tels packages peuvent être installés uniquement dans des projets .NET Core et n’ont aucun effet sur les opérations de restauration. Plus d’informations sur ces extensions par projet sont disponibles dans la documentation [Extensibilité de .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- `Template` les packages de type fournissent des [modèles personnalisés](/dotnet/core/tools/custom-templates) qui peuvent être utilisés pour créer des fichiers ou des projets comme une application, un service, un outil ou une bibliothèque de classes.

- Les packages de type personnalisé utilisent un identificateur de type arbitraire qui respecte les mêmes règles de format que les ID de package. Tous les types autres que `Dependency` et `DotnetTool`, en revanche, ne sont pas reconnus par le gestionnaire de package NuGet dans Visual Studio.

Les types de package sont définis dans le fichier `.nuspec`. Il est préférable pour la compatibilité descendante de ne *pas* définir explicitement le type `Dependency` et de plutôt compter sur le fait que NuGet supposera qu’il s’agit de ce type quand aucun type n’est spécifié.

- `.nuspec` : indique le type de package dans un nœud `packageTypes\packageType` sous l’élément `<metadata>` :

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
