---
title: Commande de signature de l’interface CLI NuGet
description: Référence pour la commande de signature NuGet. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327586"
---
# <a name="sign-command-nuget-cli"></a>sign (commande, NuGet CLI)

**S’applique à:** &bullet; **versions prises en charge** pour la création de package: 4.6 +

Signe tous les packages correspondant au premier argument avec un certificat. Le certificat avec la clé privée peut être obtenu à partir d’un fichier ou d’un certificat installé dans un magasin de certificats en fournissant un nom d’objet ou une empreinte numérique.

La signature du package n’est pas encore prise en charge dans .NET Core, sous mono ou sur des plateformes non-Windows.

## <a name="usage"></a>Usage

```cli
nuget sign <package(s)> [options]
```

où `<package(s)>` se trouve un ou `.nupkg` plusieurs fichiers.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| CertificateFingerprint | Spécifie l’empreinte SHA-1 du certificat utilisé pour rechercher le certificat dans un magasin de certificats local. |
| CertificatePassword | Spécifie le mot de passe du certificat, si nécessaire. Si un certificat est protégé par un mot de passe mais qu’aucun mot de passe n’est fourni, la commande vous invite à entrer un mot de passe au moment de l’exécution, sauf si l’option-non interactive est passée. |
| CertificatePath | Spécifie le chemin d’accès au certificat à utiliser pour signer le package. |
| CertificateStoreLocation | Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat. La valeur par défaut est «CurrentUser», le magasin de certificats X. 509 utilisé par l’utilisateur actuel. Cette option doit être utilisée lors de la spécification du certificat via les options-CertificateSubjectName ou-CertificateFingerprint. |
| CertificateStoreName | Spécifie le nom du magasin de certificats X. 509 à utiliser pour rechercher le certificat. La valeur par défaut est «My», le magasin de certificats X. 509 pour les certificats personnels. Cette option doit être utilisée lors de la spécification du certificat via les options-CertificateSubjectName ou-CertificateFingerprint. |
| CertificateSubjectName | Spécifie le nom du sujet du certificat utilisé pour rechercher le certificat dans un magasin de certificats local.  La recherche est une comparaison de chaînes ne respectant pas la casse à l’aide de la valeur fournie, qui recherchera tous les certificats dont le nom d’objet contient cette chaîne, indépendamment des autres valeurs d’objet.  Le magasin de certificats peut être spécifié par les options-CertificateStoreName et-CertificateStoreLocation. |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais. |
| HashAlgorithm | Algorithme de hachage à utiliser pour signer le package. La valeur par défaut est SHA256. |
| Aide | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| OutputDirectory | Spécifie le répertoire dans lequel le package signé doit être enregistré. Par défaut, le package d’origine est remplacé par le package signé. |
| Overwrite | Basculez pour indiquer si la signature actuelle doit être remplacée. Par défaut, la commande échoue si le package a déjà une signature. |
| Timestamper | URL vers un serveur d’horodatage RFC 3161. |
| TimestampHashAlgorithm | Algorithme de hachage à utiliser par le serveur d’horodatage RFC 3161. La valeur par défaut est SHA256. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

## <a name="examples"></a>Exemples

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```