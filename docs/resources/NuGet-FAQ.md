---
title: Questions fréquentes (FAQ) sur NuGet
description: Questions courantes et réponses sur l’utilisation de NuGet sur la ligne de commande et dans Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: be24660d05f34242e45f223e2248b943ecc38616
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699660"
---
# <a name="nuget-frequently-asked-questions"></a>Questions fréquentes (FAQ) sur NuGet

Pour parcourir les questions fréquemment posées à propos de NuGet.org, notamment les questions relatives aux comptes NuGet.org, consultez [Questions fréquentes (FAQ) sur NuGet.org](../nuget-org/nuget-org-faq.md).

**Quels sont les éléments nécessaires pour exécuter NuGet ?**

Toutes les informations relatives à l’interface utilisateur et aux outils en ligne de commande sont disponibles dans le [guide d’installation](../install-nuget-client-tools.md).

**NuGet prend-il en charge Mono ?**

L’outil en ligne de commande, `nuget.exe`, génère et s’exécute sous Mono 3.2+ et peut créer des packages dans Mono.

Bien que `nuget.exe` fonctionne entièrement sur Windows, il existe des problèmes connus sur Linux et OS X. Consultez [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) (Problèmes Mono) sur GitHub.

Un [client graphique](https://github.com/mrward/monodevelop-nuget-addin) est disponible en guise de complément pour MonoDevelop.

**Comment puis-je déterminer ce que contient un package et s’il est stable et utile pour mon application ?**

La principale source d’apprentissage sur un package est sa page d’annonce sur nuget.org (ou sur un autre flux privé). Chaque page de package sur nuget.org inclut une description du package, son historique des versions et les statistiques d’utilisation. La section **Info** sur la page de package contient également un lien vers le site web du projet où vous trouvez généralement de nombreux exemples et autres documentations pour vous aider à découvrir comment le package est utilisé.

Pour plus d’informations, consultez [Recherche et sélection des packages](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet dans Visual Studio

**Comment NuGet est-il pris en charge dans les différents produits Visual Studio ?**

- Visual Studio sur Windows prend en charge [l’interface utilisateur du Gestionnaire de package](../consume-packages/install-use-packages-visual-studio.md) et la [console du Gestionnaire de package](../consume-packages/install-use-packages-powershell.md).
- Visual Studio pour Mac offre des fonctionnalités NuGet intégrées, comme décrit dans [Inclusion d’un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (toutes les plateformes) n’a pas d’intégration directe de NuGet. Utilisez l' [interface CLI NuGet](../reference/nuget-exe-cli-reference.md) ou l' [interface CLI dotnet](../reference/dotnet-commands.md).
- Azure DevOps fournit [une étape de la génération pour restaurer des packages NuGet](/vsts/build-release/tasks/package/nuget). Vous pouvez également [héberger des flux de packages NuGet privés sur Azure DevOps](/azure/devops/artifacts/nuget/publish).

**Comment vérifier la version exacte des outils NuGet qui sont installés ?**

Dans Visual Studio, utilisez la commande **Aide > À propos de Microsoft Visual Studio** et examinez la version affichée en regard de **Gestionnaire de package NuGet**.

Vous pouvez également lancer la console du Gestionnaire de package (**Outils > Gestionnaire de package NuGet > Console du Gestionnaire de package**), puis entrer `$host` pour afficher des informations sur NuGet, notamment la version.

**Quels sont les langages de programmation pris en charge par NuGet ?**

En règle générale, NuGet fonctionne pour les langages .NET et est conçu pour intégrer les bibliothèques .NET dans un projet. Comme il prend également en charge MSBuild et Visual Studio Automation dans certains types de projets, il prend aussi en charge d’autres projets et langages à des degrés divers.

La version la plus récente de NuGet prend en charge C#, Visual Basic, F#, WiX et C++.

**Quels sont les modèles de projet pris en charge par NuGet ?**

NuGet prend totalement en charge de nombreux modèles de projet tels que Windows, Web, Cloud, SharePoint, Wix, etc.

**Comment mettre à jour les packages qui font partie de modèles Visual Studio ?**

Accédez à l’onglet **Mises à jour** dans l’interface utilisateur du Gestionnaire de package et sélectionnez **Mettre à jour tout**, ou utilisez la [commande `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) à partir de la console du Gestionnaire de package.

Pour mettre à jour le modèle lui-même, vous devez mettre à jour manuellement le dépôt du modèle. Consultez le [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) à ce sujet. Notez que cette opération est effectuée à vos risques et périls, étant donné que les mises à jour manuelles peuvent endommager le modèle si les dernières versions de toutes les dépendances ne sont pas compatibles entre elles.

**Puis-je utiliser NuGet en dehors de Visual Studio ?**

Oui, NuGet fonctionne directement à partir de la ligne de commande. Consultez le [guide d’installation](../install-nuget-client-tools.md) et les [informations de référence sur l’interface de ligne de commande](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Ligne de commande NuGet

**Comment obtenir la dernière version de l’outil en ligne de commande NuGet ?**

Consultez le [guide d’installation](../install-nuget-client-tools.md). Pour vérifier la version actuelle installée de l'outil, utilisez `nuget help`.

**Quelle est la licence pour nuget.exe ?**

Vous êtes autorisé à redistribuer nuget.exe selon les termes de la licence du MIT. Vous êtes responsable de la mise à jour et de la maintenance de toutes les copies de nuget.exe que vous souhaitez redistribuer.

**Est-il possible d’étendre l’outil en ligne de commande NuGet ?**

Oui, vous pouvez ajouter des commandes personnalisées à `nuget.exe`, comme le décrit le [billet de blog de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Console du Gestionnaire de package NuGet (Visual Studio sur Windows)

**Comment accéder à l’objet DTE dans la console du Gestionnaire de package ?**

L’objet de niveau supérieur dans le modèle objet automation Visual Studio est appelé objet DTE (Development Tools Environment). La console le fournit par le biais d’une variable nommée `$DTE`. Pour plus d’informations, consultez [Vue d’ensemble du modèle Automation](/visualstudio/extensibility/internals/automation-model-overview) dans la documentation de l’extensibilité de Visual Studio.

**J’essaie d’effectuer un cast de la variable $DTE en type DTE2, mais j’obtiens une erreur : impossible de convertir la valeur « EnvDTE. DTEClass » de type « EnvDTE. DTEClass » en type « EnvDTE80. DTE2 ». Qu'est-ce qui ne va pas?**

Il s’agit d’un problème connu lié à la façon dont PowerShell interagit avec un objet COM. Essayez ce qui suit :

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` est une fonction d’assistance ajoutée par l’hôte PowerShell NuGet.

## <a name="creating-and-publishing-packages"></a>Création et publication de packages

**Comment répertorier mon package dans un flux ?**

Consultez [Création et publication d’un package](../quickstart/create-and-publish-a-package-using-visual-studio.md).

**Je dispose de plusieurs versions de ma bibliothèque qui ciblent différentes versions du .NET Framework. Comment faire créer un package unique qui prend en charge cette solution ?**

Consultez [Prise en charge de plusieurs versions et profils du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Comment définir mon propre dépôt ou flux ?**

Consultez la [vue d’ensemble de l’hébergement des packages](../hosting-packages/overview.md).

**Comment charger des packages sur mon flux NuGet en bloc ?**

Consultez [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (Publication de packages NuGet en bloc) (jeffhandly.com).

## <a name="working-with-packages"></a>Utilisation des packages

**Est-il possible d’installer des packages NuGet sans connexion Internet ?**

Oui, consultez le billet de Blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Comment installer des packages dans un autre emplacement que le dossier de packages par défaut ?**

Définissez le [`repositoryPath`](../reference/nuget-config-file.md#config-section) paramètre dans `Nuget.Config` à l’aide de `nuget config -set repositoryPath=<path>` .

**Comment éviter d’ajouter le dossier de packages NuGet dans le contrôle de code source ?**

Affectez [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) à dans la valeur `Nuget.Config` `true` . Cette clé, qui fonctionne au niveau de la solution, doit être ajoutée au fichier `$(Solutiondir)\.nuget\Nuget.Config`. L’activation de la restauration des packages à partir de Visual Studio crée ce fichier automatiquement.

**Comment désactiver la restauration des packages ?**

Consultez [Activation et désactivation de la restauration des packages](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**Quand j’installe un package local avec des dépendances distantes, j’obtiens un message indiquant qu’il est impossible de résoudre une erreur de dépendance. Pourquoi ?**

Vous devez sélectionner la source **Tous** durant l’installation d’un package local dans le projet. Cette option regroupe tous les flux au lieu d’en utiliser un seul. Cette erreur est liée au fait que les utilisateurs d’un dépôt local souhaitent souvent éviter d’installer accidentellement un package distant en raison de stratégies d’entreprise.

**J’ai plusieurs projets dans le même dossier ; comment utiliser des fichiers packages.config distincts pour chaque projet ?**

Dans la plupart des projets où des projets distincts se trouvent dans des dossiers séparés, ce n’est pas un problème, car NuGet identifie les fichiers `packages.config` dans chaque projet. Si vous utilisez NuGet 3.3+ et que plusieurs projets se trouvent dans le même dossier, vous pouvez insérer le nom du projet dans les noms de fichier `packages.config` et utiliser le modèle `packages.{project-name}.config` ; NuGet utilise alors ce fichier.

Cela n’est pas un problème si vous utilisez PackageReference, car chaque fichier de projet contient sa propre liste de dépendances.

**Je ne vois pas nuget.org dans la liste des dépôts ; comment le récupérer ?**

- Ajoutez `https://api.nuget.org/v3/index.json` à votre liste de sources, ou
- Supprimez `%appdata%\.nuget\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) et laissez NuGet le recréer.

**J’ai effectué une migration vers PackageReference, pourquoi ma Build échoue- `This project references NuGet package(s) that are missing on this computer.` t-elle ?**

Dans packages.config projets, quand un package avec `build` props ou cibles a été installé, NuGet ajoute une `EnsureNuGetPackageBuildImports` cible pour vérifier que le contenu des packages MSBuild a été importé avant la génération.
Si le `target` a été modifié manuellement, NuGet peut ne pas être en mesure de détecter qu’il a besoin d’être supprimé lors de la migration.

Si votre projet est `PackageReference` et que vous avez toujours cette cible dans le fichier projet, vous devez pouvoir la supprimer en toute sécurité.
