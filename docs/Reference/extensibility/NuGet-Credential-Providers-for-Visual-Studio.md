---
title: "Fournisseurs d’informations d’identification de NuGet pour Visual Studio | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "Fournisseurs d’informations d’identification de NuGet auprès de flux en implémentant l’interface IVsCredentialProvider dans une extension Visual Studio."
keywords: "Fournisseurs d’informations d’identification de NuGet, auprès de l’alimentation, auprès de la galerie, extension de visual studio NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="6057e-104">L’authentification des flux avec des fournisseurs d’informations d’identification de NuGet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6057e-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="6057e-105">L’Extension NuGet Visual Studio 3.6 et + prend en charge les fournisseurs d’informations d’identification, qui permettent de NuGet travailler avec des flux authentifiés.</span><span class="sxs-lookup"><span data-stu-id="6057e-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="6057e-106">Après avoir installé un fournisseur d’informations d’identification de NuGet pour Visual Studio, l’extension NuGet Visual Studio va automatiquement acquérir et actualiser les informations d’identification pour un flux authentifié en tant que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6057e-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="6057e-107">Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="6057e-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="6057e-108">Fournisseurs d’informations d’identification de NuGet pour Visual Studio doit être installés comme une extension de Visual Studio standard et nécessitera [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (actuellement en version préliminaire) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6057e-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="6057e-109">Fournisseurs d’informations d’identification de NuGet pour Visual Studio fonctionnent uniquement dans Visual Studio (et non dans dotnet restauration ou nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="6057e-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="6057e-110">Pour les fournisseurs d’informations d’identification avec nuget.exe, consultez [nuget.exe fournisseurs d’informations d’identification](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="6057e-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="6057e-111">Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6057e-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="6057e-112">Il existe un fournisseur d’informations d’identification intégré de l’extension Visual Studio NuGet pour prendre en charge de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6057e-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="6057e-113">L’Extension NuGet Visual Studio utilise interne `VsCredentialProviderImporter` qui analyse également pour les fournisseurs d’informations d’identification du plug-in.</span><span class="sxs-lookup"><span data-stu-id="6057e-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="6057e-114">Ces fournisseurs d’informations d’identification du plug-in doivent être détectables comme une exportation MEF de type `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="6057e-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="6057e-115">Fournisseurs d’informations d’identification du plug-in disponibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6057e-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="6057e-116">Fournisseur d’informations d’identification MyGet pour Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6057e-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="6057e-117">Création d’un fournisseur d’informations d’identification de NuGet pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6057e-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="6057e-118">L’Extension NuGet Visual Studio 3.6 et + implémente un CredentialService interne qui est utilisée pour acquérir des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="6057e-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="6057e-119">Le CredentialService a une liste de fournisseurs d’informations d’identification intégrés et plug-in.</span><span class="sxs-lookup"><span data-stu-id="6057e-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="6057e-120">Chaque fournisseur est testé séquentiellement jusqu'à ce que les informations d’identification sont acquis.</span><span class="sxs-lookup"><span data-stu-id="6057e-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="6057e-121">Pendant l’acquisition d’informations d’identification, le service d’informations d’identification va essayer de fournisseurs d’informations d’identification dans l’ordre suivant, l’arrêt dès que les informations d’identification sont acquis :</span><span class="sxs-lookup"><span data-stu-id="6057e-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="6057e-122">Informations d’identification seront extraites à partir des fichiers de configuration NuGet (à l’aide de la fonction intégrée `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="6057e-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="6057e-123">Si la source du package est sur Visual Studio Team Services, le `VisualStudioAccountProvider` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="6057e-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="6057e-124">Tous les autres fournisseurs d’informations d’identification du plug-in sont testés séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="6057e-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="6057e-125">Si aucune information d’identification n’ont été acquis, l’utilisateur sera invité pour les informations d’identification à l’aide d’une boîte de dialogue de l’authentification de base standard.</span><span class="sxs-lookup"><span data-stu-id="6057e-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="6057e-126">Implémentation de IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="6057e-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="6057e-127">Pour créer un fournisseur d’informations d’identification de NuGet pour Visual Studio, créez une Extension Visual Studio qui expose une implémentation d’exportation MEF publique le `IVsCredentialProvider` tapez et adhère aux principes décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6057e-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="6057e-128">Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="6057e-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="6057e-129">Chaque fournisseur d’informations d’identification de NuGet pour Visual Studio doit :</span><span class="sxs-lookup"><span data-stu-id="6057e-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="6057e-130">Déterminer si elle peut fournir des informations d’identification pour l’URI cible avant de lancer l’acquisition des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="6057e-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="6057e-131">Si le fournisseur ne peut pas fournir les informations d’identification pour la source ciblée, elle doit retourner `null`.</span><span class="sxs-lookup"><span data-stu-id="6057e-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="6057e-132">Si le fournisseur gère les demandes pour l’URI cible, mais ne peut pas fournir les informations d’identification, une exception doit être levée.</span><span class="sxs-lookup"><span data-stu-id="6057e-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="6057e-133">Un fournisseur d’informations d’identification NuGet personnalisé pour Visual Studio doit implémenter la `IVsCredentialProvider` interface disponible dans le [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="6057e-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="6057e-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="6057e-134">GetCredentialAsync</span></span>

| <span data-ttu-id="6057e-135">Paramètre d’entrée</span><span class="sxs-lookup"><span data-stu-id="6057e-135">Input Parameter</span></span> |<span data-ttu-id="6057e-136">Description</span><span class="sxs-lookup"><span data-stu-id="6057e-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="6057e-137">Uri de l’URI</span><span class="sxs-lookup"><span data-stu-id="6057e-137">Uri uri</span></span> | <span data-ttu-id="6057e-138">L’Uri de source de package pour lequel les informations d’identification sont demandées.</span><span class="sxs-lookup"><span data-stu-id="6057e-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="6057e-139">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="6057e-139">IWebProxy proxy</span></span> | <span data-ttu-id="6057e-140">Proxy Web à utiliser lors de la communication sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="6057e-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="6057e-141">Null s’il n’existe aucune authentification proxy configurée.</span><span class="sxs-lookup"><span data-stu-id="6057e-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="6057e-142">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="6057e-142">bool isProxyRequest</span></span> | <span data-ttu-id="6057e-143">True si cette demande est pour obtenir des informations d’identification de l’authentification proxy.</span><span class="sxs-lookup"><span data-stu-id="6057e-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="6057e-144">Si l’implémentation n’est pas valide pour l’acquisition d’informations d’identification de proxy, null doit être retourné.</span><span class="sxs-lookup"><span data-stu-id="6057e-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="6057e-145">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="6057e-145">bool isRetry</span></span> | <span data-ttu-id="6057e-146">True si les informations d’identification ont été précédemment demandées pour cet Uri, mais les informations d’identification fournies ne permettait pas autorisé à accéder.</span><span class="sxs-lookup"><span data-stu-id="6057e-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="6057e-147">bool non interactif</span><span class="sxs-lookup"><span data-stu-id="6057e-147">bool nonInteractive</span></span> | <span data-ttu-id="6057e-148">Si la valeur est true, le fournisseur d’informations d’identification doit supprimer toutes les invites utilisateur et utilisez à la place des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="6057e-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="6057e-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="6057e-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="6057e-150">Ce jeton d’annulation doit être vérifié pour déterminer si les informations d’identification demande à l’opération a été annulée.</span><span class="sxs-lookup"><span data-stu-id="6057e-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |
  
<span data-ttu-id="6057e-151">**Valeur de retour**: un objet informations d’identification qui implémente le [ `System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span><span class="sxs-lookup"><span data-stu-id="6057e-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span></span>