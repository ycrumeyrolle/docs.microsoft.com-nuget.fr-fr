---
title: Modèle d’URL Détails du package, API NuGet
description: Le modèle d’URL Détails du package permet aux clients d’afficher dans leur interface utilisateur un lien Web vers d’autres détails sur le package
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773949"
---
# <a name="package-details-url-template"></a>Modèle d’URL Détails du package

Il est possible pour un client de créer une URL qui peut être utilisée par l’utilisateur pour afficher plus de détails sur le package dans son navigateur Web. Cela s’avère utile quand une source de package souhaite afficher des informations supplémentaires sur un package qui ne tiennent pas dans l’étendue de ce que l’application cliente NuGet affiche.

La ressource utilisée pour générer cette URL est la `PackageDetailsUriTemplate` ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Contrôle de version

Les `@type` valeurs suivantes sont utilisées :

Valeur @type                     | Notes
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | La version initiale

## <a name="url-template"></a>URL template

L’URL de l’API suivante est la valeur de la `@id` propriété associée à l’une des valeurs de ressource mentionnées ci-dessus `@type` .

## <a name="http-methods"></a>Méthodes HTTP

Bien que le client ne soit pas destiné à effectuer des requêtes sur l’URL des détails du package pour le compte de l’utilisateur, la page Web doit prendre en charge la `GET` méthode pour permettre l’ouverture facile d’une URL cliquée dans un navigateur Web.

## <a name="construct-the-url"></a>Construire l’URL

Avec un ID de package connu et une version, l’implémentation cliente peut construire une URL utilisée pour accéder à une interface Web. L’implémentation du client doit afficher cette URL construite (ou un lien de clic) pour permettre à l’utilisateur d’ouvrir un navigateur Web à l’URL et d’en savoir plus sur le package. Le contenu de la page Détails du package est déterminé par l’implémentation du serveur.

L’URL doit être une URL absolue et le schéma (protocole) doit être HTTPs.

La valeur de `@id` dans l’index de service est une chaîne d’URL contenant l’un des jetons d’espaces réservés suivants :

### <a name="url-placeholders"></a>Espaces réservés d’URL

Nom        | Type    | Obligatoire | Notes
----------- | ------- | -------- | -----
`{id}`      | string  | non       | ID de package pour lequel obtenir des détails
`{version}` | string  | non       | Version du package pour laquelle obtenir des détails

Le serveur doit accepter `{id}` les `{version}` valeurs et avec n’importe quelle casse. En outre, le serveur ne doit pas être sensible à la [normalisation](../concepts/package-versioning.md#normalized-version-numbers)de la version. En d’autres termes, le serveur doit accepter également les versions non normalisées.

Par exemple, le modèle de détails de package de NuGet. org ressemble à ceci :

```http
https://www.nuget.org/packages/{id}/{version}
```

Si l’implémentation du client doit afficher un lien vers les détails du package pour NuGet. version 4.3.0, elle génère l’URL suivante et la fournit à l’utilisateur :

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
