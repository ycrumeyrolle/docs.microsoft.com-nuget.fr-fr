---
title: Commande de configuration de l’interface CLI NuGet
description: Référence pour la commande de configuration de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433316"
---
# <a name="config-command-nuget-cli"></a>commande config (interface CLI NuGet)

**S’applique à:** toutes les &bullet; **versions prises en charge**: toutes

Obtient ou définit les valeurs de configuration NuGet. Pour une utilisation supplémentaire, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md). Pour plus d’informations sur les noms de clé autorisés, reportez-vous à la [Référence du fichier de configuration NuGet](../nuget-config-file.md).

## <a name="usage"></a>Usage

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

où `<name>` et`<value>` spécifient une paire clé-valeur à définir dans la configuration. Vous pouvez spécifier autant de paires que vous le souhaitez. Pour supprimer une valeur, spécifiez le nom et `=` le signe, mais aucune valeur.

Pour les noms de clé autorisés, consultez la [Référence du fichier de configuration NuGet](../nuget-config-file.md).

Dans NuGet 3.4 +, `<value>` peut utiliser des [variables d’environnement](cli-ref-environment-variables.md).

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AsPath | Retourne la valeur de configuration sous la forme d’un `-Set` chemin d’accès, ignoré lorsque est utilisé. |
| ConfigFile | Fichier de configuration NuGet à modifier. S’il n’est pas spécifié, le fichier par`%AppData%\NuGet\NuGet.Config` défaut est utilisé ( `~/.config/NuGet/NuGet.Config` Windows) ou (Mac/ `~/.nuget/NuGet/NuGet.Config` Linux) ou (varie selon la distribution du système d’exploitation).|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemples

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```