---
title: Commandes pack et restore NuGet comme cibles MSBuild
description: Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777711"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Commandes pack et restore NuGet comme cibles MSBuild

*NuGet 4.0+*

Avec le format [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + peut stocker toutes les métadonnées de manifeste directement dans un fichier projet plutôt que d’utiliser un `.nuspec` fichier séparé.

Avec MSBuild 15.1+, NuGet est également un citoyen MSBuild de première classe avec les cibles `pack` et `restore` comme décrit ci-dessous. Ces cibles vous permettent d’utiliser NuGet comme vous utiliseriez toute autre tâche ou cible MSBuild. Pour obtenir des instructions sur la création d’un package NuGet à l’aide de MSBuild, consultez [créer un package NuGet à l’aide de MSBuild](../create-packages/creating-a-package-msbuild.md). (Pour NuGet 3.x et versions antérieures, vous utilisez les commandes [pack](../reference/cli-reference/cli-ref-pack.md) et [restore](../reference/cli-reference/cli-ref-restore.md) via l’interface de ligne de commande NuGet à la place.)

## <a name="target-build-order"></a>Ordre de génération des cibles

Étant donné que `pack` et `restore` sont des cibles MSBuild, vous pouvez y accéder pour améliorer votre flux de travail. Par exemple, supposons que vous souhaitez copier votre package sur un partage réseau après compression. Pour ce faire, ajoutez le code suivant dans votre fichier projet :

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

De même, vous pouvez écrire une tâche MSBuild, écrire votre propre cible et consommer des propriétés NuGet dans la tâche MSBuild.

> [!NOTE]
> `$(OutputPath)` est relatif et s’attend à ce que vous exécutiez la commande à partir de la racine du projet.

## <a name="pack-target"></a>Cible pack

Pour les projets .NET qui utilisent le `PackageReference` format, l’utilisation de `msbuild -t:pack` dessine des entrées à partir du fichier projet à utiliser lors de la création d’un package NuGet.

Le tableau suivant décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier projet au sein du premier `<PropertyGroup>` nœud. Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel. Pour plus de commodité, la table est organisée par la propriété équivalente dans un [ `.nuspec` fichier](../reference/nuspec.md).

Notez que les propriétés `Owners` et `Summary` de `.nuspec` ne sont pas prises en charge avec MSBuild.

| Valeur d’attribut/NuSpec | Propriété MSBuild | Default | Notes |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) de MSBuild |
| Version | PackageVersion | Version | Compatible avec SemVer, par exemple « 1.0.0 », « version bêta 1.0.0 » ou « version bêta-1.0.0-00345 » |
| VersionPrefix | PackageVersionPrefix | empty | La définition de PackageVersion remplace PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) de MSBuild. La définition de PackageVersion remplace PackageVersionSuffix |
| Auteurs | Auteurs | Nom de l’utilisateur actuel | Liste délimitée par des points-virgules des auteurs de packages, qui correspondent aux noms de profil sur nuget.org. Ceux-ci sont affichés dans la galerie NuGet sur nuget.org et sont utilisés pour faire référence croisée aux packages par les mêmes auteurs. |
| Propriétaires | N/A | Ne figure pas dans NuSpec | |
| Titre | Titre | PackageId| Titre convivial du package, généralement utilisé dans les affichages de l’interface utilisateur comme sur nuget.org et dans le gestionnaire de package de Visual Studio. |
| Description | Description | « Description du package » | Description longue de l'assembly. Si `PackageDescription` n’est pas spécifié, cette propriété est également utilisée comme description du package. |
| Copyright | Copyright | empty | Détails de copyright pour le package. |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | Valeur booléenne qui spécifie si le client doit inviter l’utilisateur à accepter la licence du package avant d’installer le package. |
| license | PackageLicenseExpression | empty | Correspond à `<license type="expression">`. Consultez [compression d’une expression de licence ou d’un fichier de licence](#packing-a-license-expression-or-a-license-file). |
| license | PackageLicenseFile | empty | Chemin d’accès à un fichier de licence dans le package si vous utilisez une licence personnalisée ou une licence à laquelle aucun identificateur SPDX n’a été affecté. Vous devez explicitement compresser le fichier de licence référencé. Correspond à `<license type="file">`. Consultez [compression d’une expression de licence ou d’un fichier de licence](#packing-a-license-expression-or-a-license-file). |
| LicenseUrl | PackageLicenseUrl | empty | `PackageLicenseUrl` est déconseillé. Utilisez `PackageLicenseExpression` ou `PackageLicenseFile` à la place. |
| ProjectUrl | PackageProjectUrl | empty | |
| Icône | PackageIcon | empty | Chemin d’accès à une image dans le package à utiliser comme icône de package. Vous devez explicitement compresser le fichier image icône référencé. Pour plus d’informations, consultez [compression d’un fichier image d’icône](#packing-an-icon-image-file) et de [ `icon` métadonnées](/nuget/reference/nuspec#icon). |
| IconUrl | PackageIconUrl | empty | `PackageIconUrl` est déconseillé en faveur de `PackageIcon` . Toutefois, pour une expérience de niveau inférieur, vous devez spécifier `PackageIconUrl` en plus de `PackageIcon` . |
| Étiquettes | PackageTags | empty | Liste de balises séparées par un point-virgule qui désigne le package. |
| ReleaseNotes | PackageReleaseNotes | empty | Notes de publication du package. |
| Référentiel/URL | RepositoryUrl | empty | URL du référentiel utilisée pour cloner ou récupérer le code source. Exemple : *https://github.com/NuGet/NuGet.Client.git* . |
| Dépôt/type | RepositoryType | empty | Type de référentiel. Exemples : `git` (valeur par défaut), `tfs` . |
| Référentiel/branche | RepositoryBranch | empty | Informations de branche de référentiel facultatives. `RepositoryUrl` doit également être spécifié pour que cette propriété soit incluse. Exemple : *Master* (NuGet 4.7.0 +). |
| Dépôt/validation | RepositoryCommit | empty | Validation ou ensemble de modifications de référentiel facultatif pour indiquer la source à partir de laquelle le package a été généré. `RepositoryUrl` doit également être spécifié pour que cette propriété soit incluse. Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +). |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Résumé | Non pris en charge | | |

### <a name="pack-target-inputs"></a>entrées de cible pack

| Propriété | Description |
| - | - |
| IsPackable | Valeur booléenne qui spécifie si le projet peut être compressé. La valeur par défaut est `true`. |
| SuppressDependenciesWhenPacking | Affectez `true` la valeur pour supprimer les dépendances de package du package NuGet généré. |
| PackageVersion | Spécifie la version du package obtenu. Accepte toutes les formes de la chaîne de version NuGet. La valeur par défaut est la valeur de `$(Version)`, autrement dit, de la propriété `Version` dans le projet. |
| PackageId | Spécifie le nom du package obtenu. Si non spécifié, l’opération `pack` utilise par défaut le `AssemblyName` ou le nom du répertoire comme nom du package. |
| PackageDescription | Description longue du package pour l’affichage de l’interface utilisateur. |
| Auteurs | Liste délimitée par des points-virgules des auteurs de packages, qui correspondent aux noms de profil sur nuget.org. Ceux-ci sont affichés dans la galerie NuGet sur nuget.org et sont utilisés pour faire référence croisée aux packages par les mêmes auteurs. |
| Description | Description longue de l'assembly. Si `PackageDescription` n’est pas spécifié, cette propriété est également utilisée comme description du package. |
| Copyright | Détails de copyright pour le package. |
| PackageRequireLicenseAcceptance | Valeur booléenne qui spécifie si le client doit inviter l’utilisateur à accepter la licence du package avant d’installer le package. Par défaut, il s’agit de `false`. |
| DevelopmentDependency | Valeur booléenne qui spécifie si le package est marqué en tant que dépendance de développement uniquement, ce qui empêche l’inclusion du package en tant que dépendance dans d’autres packages. Avec `PackageReference` (NuGet 4.8 +), cet indicateur signifie également que les éléments multimédias de compilation sont exclus de la compilation. Pour plus d'informations, voir [Prise en charge de DevelopmentDependency pour PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference). |
| PackageLicenseExpression | Une expression ou un [identificateur de licence SPDX](https://spdx.org/licenses/) , par exemple, `Apache-2.0` . Pour plus d’informations, consultez [compression d’une expression de licence ou d’un fichier de licence](#packing-a-license-expression-or-a-license-file). |
| PackageLicenseFile | Chemin d’accès à un fichier de licence dans le package si vous utilisez une licence personnalisée ou une licence à laquelle aucun identificateur SPDX n’a été affecté. |
| PackageLicenseUrl | `PackageLicenseUrl` est déconseillé. Utilisez `PackageLicenseExpression` ou `PackageLicenseFile` à la place. |
| PackageProjectUrl | |
| PackageIcon | Spécifie le chemin d’accès de l’icône de package, relatif à la racine du package. Pour plus d’informations, consultez [compression d’une icône de fichier image](#packing-an-icon-image-file). |
| PackageReleaseNotes| Notes de publication du package. |
| PackageTags | Liste de balises séparées par un point-virgule qui désigne le package. |
| PackageOutputPath | Détermine le chemin de sortie dans lequel le package compressé est déposé. La valeur par défaut est `$(OutputPath)`. |
| IncludeSymbols | Cette valeur booléenne indique si le package doit créer un package de symboles supplémentaire quand le projet est compressé. Le format du package de symboles est contrôlé par la propriété `SymbolPackageFormat`. Pour plus d’informations, consultez [IncludeSymbols](#includesymbols). |
| IncludeSource | Cette valeur booléenne indique si le processus de compression doit créer un package source. Le package source contient le code source de la bibliothèque ainsi que les fichiers PDB. Les fichiers sources sont placés dans le répertoire `src/ProjectName` dans le fichier de package obtenu. Pour plus d’informations, consultez [IncludeSource](#includesource). |
| PackageTypes
| IsTool | Spécifie si tous les fichiers de sortie sont copiés dans le dossier *tools* au lieu du dossier *lib*. Pour plus d’informations, consultez [IsTool](#istool). |
| RepositoryUrl | URL du référentiel utilisée pour cloner ou récupérer le code source. Exemple : *https://github.com/NuGet/NuGet.Client.git* . |
| RepositoryType | Type de référentiel. Exemples : `git` (valeur par défaut), `tfs` . |
| RepositoryBranch | Informations de branche de référentiel facultatives. `RepositoryUrl` doit également être spécifié pour que cette propriété soit incluse. Exemple : *Master* (NuGet 4.7.0 +). |
| RepositoryCommit | Validation ou ensemble de modifications de référentiel facultatif pour indiquer la source à partir de laquelle le package a été généré. `RepositoryUrl` doit également être spécifié pour que cette propriété soit incluse. Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +). |
| SymbolPackageFormat | Spécifie le format du package de symboles. Si « Symbols. nupkg », un package de symboles hérités est créé avec une extension *. Symbols. nupkg* contenant des fichiers PDB, des dll et d’autres fichiers de sortie. Si « snupkg », un package de symboles snupkg est créé et contient les fichiers PDB portables. La valeur par défaut est « Symbols. nupkg ». |
| NoPackageAnalysis | Spécifie que `pack` ne doit pas exécuter l’analyse du package après la génération du package. |
| MinClientVersion | Spécifie la version minimale du client NuGet qui peut installer ce package, appliquée par nuget.exe et le gestionnaire de package Visual Studio. |
| IncludeBuildOutput | Cette valeur booléenne spécifie si les assemblys de sortie de la génération doivent être empaquetés dans le fichier *. nupkg* ou non. |
| IncludeContentInPack | Cette valeur booléenne spécifie si tous les éléments dont le type `Content` est sont inclus automatiquement dans le package résultant. Par défaut, il s’agit de `true`. |
| BuildOutputTargetFolder | Spécifie le dossier où placer les assemblys de sortie. Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif. Pour plus d’informations, consultez [assemblys de sortie](#output-assemblies). |
| ContentTargetFolders | Spécifie l’emplacement par défaut où tous les fichiers de contenu doivent être placés si `PackagePath` n’est pas spécifié pour eux. La valeur par défaut est « content;contentFiles ». Pour plus d’informations, consultez [Inclusion de contenu dans un package](#including-content-in-a-package). |
| NuspecFile | Chemin relatif ou absolu du fichier *.nuspec* utilisé pour la compression. S’il est spécifié, il est utilisé **exclusivement** pour les informations de Packaging, et toutes les informations contenues dans les projets ne sont pas utilisées. Pour plus d’informations, consultez [compression à l’aide d’un. NuSpec](#packing-using-a-nuspec). |
| NuspecBasePath | Chemin de base pour le fichier *.nuspec*. Pour plus d’informations, consultez [compression à l’aide d’un. NuSpec](#packing-using-a-nuspec). |
| NuspecProperties | Liste de paires clé=valeur séparées par un point-virgule. Pour plus d’informations, consultez [compression à l’aide d’un. NuSpec](#packing-using-a-nuspec). |

## <a name="pack-scenarios"></a>Scénarios avec pack

### <a name="suppress-dependencies"></a>Supprimer les dépendances

Pour supprimer les dépendances de package du package NuGet généré, affectez `SuppressDependenciesWhenPacking` la valeur à `true` qui autorisera l’ignorance de toutes les dépendances du fichier nupkg généré.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` est déconseillé en faveur de la [`PackageIcon`](#packageicon) propriété. À compter de NuGet 5,3 et de Visual Studio 2019 version 16,3, `pack` déclenche l’avertissement [NU5048](./errors-and-warnings/nu5048.md) si les métadonnées de package spécifient uniquement `PackageIconUrl` .

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> Pour maintenir la compatibilité descendante avec les clients et les sources qui ne sont pas encore prises en charge `PackageIcon` , spécifiez à la fois `PackageIcon` et `PackageIconUrl` . Visual Studio prend en charge `PackageIcon` les packages provenant d’une source basée sur un dossier.

#### <a name="packing-an-icon-image-file"></a>Compression d’un fichier image d’icône

Lors de la compression d’un fichier image icône, utilisez `PackageIcon` la propriété pour spécifier le chemin d’accès du fichier d’icône, relatif à la racine du package. En outre, assurez-vous que le fichier est inclus dans le package. La taille du fichier image est limitée à 1 Mo. Les formats de fichiers pris en charge sont JPEG et PNG. Nous recommandons une résolution d’image de 128 x 128.

Par exemple :

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Exemple d’icône de package](https://github.com/NuGet/Samples/tree/master/PackageIconExample).

Pour l’équivalent NuSpec, consultez la [référence NuSpec pour l’icône](nuspec.md#icon).

### <a name="output-assemblies"></a>Assemblys de sortie

`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`. Les fichiers de sortie qui sont copiés dépendent de ce que fournit MSBuild à partir de la cible `BuiltOutputProjectGroup`.

Il existe deux propriétés MSBuild que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler la destination des assemblys de sortie :

- `IncludeBuildOutput` : valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.
- `BuildOutputTargetFolder` : spécifie le dossier dans lequel les assemblys de sortie doivent être placés. Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.

### <a name="package-references"></a>Références de package

Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Références entre projets

Les références entre projets sont considérées par défaut comme des références de package nuget, par exemple :

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Ajout de contenu dans un package

Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`. Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Si vous souhaitez copier tout le contenu uniquement vers des dossiers racines spécifiques (et non vers `content` et `contentFiles`), vous pouvez utiliser la propriété MSBuild `ContentTargetFolders` qui a pour valeur par défaut « content;contentFiles », mais peut être définie sur tout autre nom de dossier. Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.

`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule. La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package. Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Il existe également une propriété MSBuild `$(IncludeContentInPack)` qui a pour valeur par défaut `true`. Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.

D’autres métadonnées spécifiques à pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` qui définissent les valeurs ```CopyToOutput``` et ```Flatten``` sur l’entrée ```contentFiles``` dans le fichier nuspec de sortie.

> [!Note]
> Outre les éléments de contenu, les métadonnées `<Pack>` et `<PackagePath>` peuvent aussi être définies sur des fichiers avec l’action de génération Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.
>
> Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.

### <a name="includesymbols"></a>IncludeSymbols

Quand vous utilisez `MSBuild -t:pack -p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.

### <a name="includesource"></a>IncludeSource

Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`. Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu. La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.

Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Compression d’une expression de licence ou d’un fichier de licence

Lorsque vous utilisez une expression de licence, utilisez la `PackageLicenseExpression` propriété. Pour obtenir un exemple, consultez [exemple d’expression de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Pour en savoir plus sur les expressions de licence et les licences acceptées par NuGet.org, consultez [métadonnées de licence](nuspec.md#license).

Lors de la compression d’un fichier de licence, utilisez `PackageLicenseFile` la propriété pour spécifier le chemin d’accès du package, relatif à la racine du package. En outre, assurez-vous que le fichier est inclus dans le package. Par exemple :

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Pour obtenir un exemple, consultez [exemple de fichier de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

> [!NOTE]
> Seul un de `PackageLicenseExpression` , `PackageLicenseFile` et `PackageLicenseUrl` peut être spécifié à la fois.

### <a name="packing-a-file-without-an-extension"></a>Compression d’un fichier sans extension

Dans certains scénarios, par exemple lors de la compression d’un fichier de licence, vous souhaiterez peut-être inclure un fichier sans extension.
Pour des raisons historiques, NuGet & MSBuild traitent les chemins d’accès sans extension comme répertoires.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Fichier sans exemple d’extension](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).
### <a name="istool"></a>IsTool

Lors de l’utilisation de `MSBuild -t:pack -p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`. Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.

### <a name="packing-using-a-nuspec"></a>Compression à l’aide d’un fichier .nuspec

Bien qu’il soit recommandé d’inclure à la place [toutes les propriétés](../reference/msbuild-targets.md#pack-target) qui se trouvent généralement dans le fichier du `.nuspec` fichier projet, vous pouvez choisir d’utiliser un `.nuspec` fichier pour compresser votre projet. Pour un projet de type non-SDK qui utilise `PackageReference` , vous devez effectuer `NuGet.Build.Tasks.Pack.targets` l’importation afin que la tâche Pack puisse être exécutée. Vous devez toujours restaurer le projet avant de pouvoir compresser un fichier NuSpec. (Un projet de type SDK comprend les cibles Pack par défaut.)

La version cible du .NET Framework du fichier projet n’est pas pertinente et n’est pas utilisée lors de la compression d’un NuSpec. Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :

1. `NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.
1. `NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule. En raison du mode de fonctionnement de l’analyse de ligne de commande MSBuild, plusieurs propriétés doivent être spécifiées comme suit : `-p:NuspecProperties="key1=value1;key2=value2"`.  
1. `NuspecBasePath` : chemin de base pour le fichier `.nuspec`.

Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Notez que le compactage d’un NuSpec à l’aide de dotnet.exe ou de MSBuild permet également de générer le projet par défaut. Cela peut être évité en passant ```--no-build``` la propriété à dotnet.exe, qui est l’équivalent du paramètre ```<NoBuild>true</NoBuild> ``` dans votre fichier projet, ainsi que le paramètre ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` dans le fichier projet.

Voici un exemple de fichier *. csproj* pour compresser un fichier NuSpec :

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Points d’extension avancés pour créer un package personnalisé

La `pack` cible fournit deux points d’extension qui s’exécutent dans la build interne du Framework cible. Les points d’extension prennent en charge l’inclusion de contenu et d’assemblys spécifiques au Framework cible dans un package :

- `TargetsForTfmSpecificBuildOutput` cible : à utiliser pour les fichiers contenus dans le `lib` dossier ou dans un dossier spécifié à l’aide de `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` cible : à utiliser pour les fichiers en dehors de `BuildOutputTargetFolder` .

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Écrivez une cible personnalisée et spécifiez-la comme valeur de la `$(TargetsForTfmSpecificBuildOutput)` propriété. Pour tous les fichiers qui doivent être placés dans `BuildOutputTargetFolder` (lib par défaut), la cible doit écrire ces fichiers dans ItemGroup `BuildOutputInPackage` et définir les deux valeurs de métadonnées suivantes :

- `FinalOutputPath`: Le chemin d’accès absolu du fichier ; s’il n’est pas fourni, l’identité est utilisée pour évaluer le chemin source.
- `TargetPath`: (Facultatif) définit le moment où le fichier doit être placé dans un sous-dossier au sein de `lib\<TargetFramework>` , comme les assemblys satellites qui se trouvent dans leurs dossiers de culture respectifs. La valeur par défaut est le nom du fichier.

Exemple :

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Écrivez une cible personnalisée et spécifiez-la comme valeur de la `$(TargetsForTfmSpecificContentInPackage)` propriété. Pour tous les fichiers à inclure dans le package, la cible doit écrire ces fichiers dans ItemGroup `TfmSpecificPackageFile` et définir les métadonnées facultatives suivantes :

- `PackagePath`: Chemin d’accès où le fichier doit être généré dans le package. NuGet émet un avertissement si plusieurs fichiers sont ajoutés au même chemin d’accès de package.
- `BuildAction`: Action de génération à assigner au fichier, obligatoire uniquement si le chemin d’accès du package se trouve dans le `contentFiles` dossier. La valeur par défaut est « None ».

Exemple :
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>Cible restore

`MSBuild -t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :

1. Lire toutes les références entre projets
1. Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework
1. Passer des données MSBuild à NuGet.Build.Tasks.dll
1. Exécuter la restauration
1. Télécharger des packages
1. Écrire le fichier de ressources, les cibles et les propriétés

La `restore` cible fonctionne pour les projets utilisant le format PackageReference.
`MSBuild 16.5+` prend également [en charge](#restoring-packagereference-and-packagesconfig-with-msbuild) le `packages.config` format.

> [!NOTE]
> La `restore` cible ne [doit pas être exécutée](#restoring-and-building-with-one-msbuild-command) en association avec la `build` cible.

### <a name="restore-properties"></a>Propriétés de restauration

Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet. Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `-p:` (consultez Exemples ci-dessous).

| Propriété | Description |
|--------|--------|
| RestoreSources | Liste de sources de packages séparées par un point-virgule. |
| RestorePackagesPath | Chemin du dossier de packages de l’utilisateur. |
| RestoreDisableParallel | Limite les téléchargements à un à la fois. |
| RestoreConfigFile | Chemin à un fichier `Nuget.Config` à appliquer. |
| RestoreNoCache | Si la valeur est true, évite d’utiliser des packages mis en cache. Consultez [gestion des dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Si la valeur est true, ignore les sources de packages défectueuses ou manquantes. |
| RestoreFallbackFolders | Dossiers de secours, utilisés de la même façon que le dossier des packages de l’utilisateur est utilisé. |
| RestoreAdditionalProjectSources | Sources supplémentaires à utiliser pendant la restauration. |
| RestoreAdditionalProjectFallbackFolders | Dossiers de secours supplémentaires à utiliser lors de la restauration. |
| RestoreAdditionalProjectFallbackFoldersExcludes | Exclut les dossiers de secours spécifiés dans `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Chemin d’accès à `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus. |
| RestoreUseSkipNonexistentTargets  | Lorsque les projets sont collectés via MSBuild, il détermine s’ils sont collectés à l’aide de l' `SkipNonexistentTargets` optimisation. Si la valeur n’est pas définie, la valeur par défaut est `true` . La conséquence est un comportement de basculement rapide lorsque les cibles d’un projet ne peuvent pas être importées. |
| MSBuildProjectExtensionsPath | Dossier de sortie, avec comme valeur par défaut `BaseIntermediateOutputPath` et le `obj` dossier. |
| RestoreForce | Dans les projets basés sur PackageReference, force la résolution de toutes les dépendances même si la dernière restauration a réussi. La spécification de cet indicateur est semblable à la suppression du `project.assets.json` fichier. Cela ne contourne pas le cache http. |
| RestorePackagesWithLockFile | Opte pour l’utilisation d’un fichier de verrouillage. |
| RestoreLockedMode | Exécutez la restauration en mode verrouillé. Cela signifie que la restauration ne réévaluera pas les dépendances. |
| NuGetLockFilePath | Emplacement personnalisé pour le fichier de verrouillage. L’emplacement par défaut est à côté du projet et est nommé `packages.lock.json` . |
| RestoreForceEvaluate | Force la restauration à recalculer les dépendances et à mettre à jour le fichier de verrouillage sans aucun avertissement. |
| RestorePackagesConfig | Commutateur d’abonnement qui restaure des projets avec packages.config. Prise en charge avec `MSBuild -t:restore` uniquement. |
| RestoreUseStaticGraphEvaluation | Un commutateur d’abonnement pour utiliser l’évaluation MSBuild de graphe statique au lieu de l’évaluation standard. L’évaluation du graphique statique est une fonctionnalité expérimentale qui est beaucoup plus rapide pour les grandes pensions et les solutions. |

#### <a name="examples"></a>Exemples

Ligne de commande :

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

Fichier projet :

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Sorties de restauration

La restauration crée les fichiers suivants dans le dossier `obj` de build :

| Fichier | Description |
|--------|--------|
| `project.assets.json` | Contient le graphique de dépendance de toutes les références de package. |
| `{projectName}.projectFileExtension.nuget.g.props` | Références à des propriétés MSBuild contenues dans des packages |
| `{projectName}.projectFileExtension.nuget.g.targets` | Références à des cibles MSBuild contenues dans des packages |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Restauration et génération à l’aide d’une commande MSBuild

En raison du fait que NuGet peut restaurer des packages qui déplacent des cibles et des props MSBuild, les évaluations de la restauration et de la build sont exécutées avec des propriétés globales différentes.
Cela signifie que les éléments suivants auront un comportement imprévisible et souvent incorrect.

```cli
msbuild -t:restore,build
```

 Au lieu de cela, l’approche recommandée est la suivante :

```cli
msbuild -t:build -restore
```

La même logique s’applique à d’autres cibles similaires à celles de `build` .

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a>Restauration de PackageReference et packages.config avec MSBuild

Avec MSBuild 16,5 +, packages.config sont également pris en charge pour `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` la restauration est disponible uniquement avec `MSBuild 16.5+` , et non avec `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Restauration avec évaluation de graphe statique MSBuild

> [!NOTE]
> Avec MSBuild 16,6 +, NuGet a ajouté une fonctionnalité expérimentale pour utiliser l’évaluation de graphique statique à partir de la ligne de commande, ce qui améliore considérablement le temps de restauration pour les référentiels volumineux.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Vous pouvez également l’activer en définissant la propriété dans un répertoire. Build. props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> À compter de Visual Studio 2019. x et NuGet 5. x, cette fonctionnalité est considérée comme expérimentale et s’abonne. Pour plus d’informations sur le moment où cette fonctionnalité sera activée par défaut, suivez [NuGet/9803](https://github.com/NuGet/Home/issues/9803) .

La restauration de graphiques statiques modifie la partie MSBuild de la restauration, la lecture et l’évaluation du projet, mais pas l’algorithme de restauration ! L’algorithme de restauration est le même pour tous les outils NuGet (NuGet.exe, MSBuild.exe, dotnet.exe et Visual Studio).

Dans très peu de scénarios, la restauration de graphiques statiques peut se comporter différemment de la restauration en cours et certains PackageReferences ou références déclarés peuvent être manquants.

Pour faciliter l’utilisation de la migration vers la restauration de graphiques statiques, envisagez d’exécuter :

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet ne *doit signaler aucune modification* . Si vous voyez une anomalie, veuillez envoyer un problème à [NuGet/](https://github.com/nuget/home/issues/new)à la page d’hébergement.

### <a name="replacing-one-library-from-a-restore-graph"></a>Remplacement d’une bibliothèque à partir d’un graphique de restauration

Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix. Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
