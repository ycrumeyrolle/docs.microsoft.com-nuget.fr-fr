---
title: Installer et utiliser un package NuGet dans Visual Studio
description: Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775525"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Démarrage rapide : installer et utiliser un package dans Visual Studio (Windows uniquement)

Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets. Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md). Les packages sont installés dans un projet Visual Studio à l’aide du gestionnaire de package NuGet, de la [console du gestionnaire de package](../consume-packages/install-use-packages-powershell.md)ou de l' [interface CLI dotnet](install-and-use-a-package-using-the-dotnet-cli.md). Cet article explique le processus avec le package [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) bien connu et un projet Windows Presentation Foundation (WPF). Le même processus s’applique à n’importe quel autre projet .NET ou .NET Core.

Une fois l’installation terminée, reportez-vous au package dans le code `using <namespace>` où \<namespace\> est spécifique au package que vous utilisez. Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.

> [!Tip]
> **Commencez avec NuGet.org**: la navigation *NuGet.org* est la manière dont les développeurs .net recherchent généralement les composants qu’ils peuvent réutiliser dans leurs propres applications. Vous pouvez effectuer une recherche directement dans *NuGet.org* , ou Rechercher et installer des packages dans Visual Studio, comme indiqué dans cet article. Pour obtenir des informations générales, consultez [Rechercher et évaluer des packages NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Prérequis

- Visual Studio 2019 avec la charge de travail Développement .NET Desktop.

Vous pouvez installer l’édition Community 2019 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise.

Si vous utilisez Visual Studio pour Mac, consultez [installer et utiliser un package dans Visual Studio pour Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Création d’un projet

Les packages NuGet peuvent être installés dans n’importe quel projet .NET, à condition qu’ils prennent en charge la même version cible de .NET Framework que le projet.

Pour cette procédure pas à pas, utilisez une application WPF simple. Créez un projet dans Visual Studio à l’aide de **fichier**  >  **nouveau projet**, en tapant **.net** dans la zone de recherche, puis en sélectionnant l' **application WPF (.NET Framework)**. Cliquez sur **Suivant**. Acceptez les valeurs par défaut pour **Framework** quand vous y êtes invité.

Visual Studio crée le projet qui s’ouvre dans l’Explorateur de solutions.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Ajouter le package NuGet Newtonsoft.Json

Pour installer le package, vous pouvez utiliser l’interface utilisateur du gestionnaire de package NuGet ou la console du gestionnaire de package. Quand vous installez un package, NuGet enregistre la dépendance dans votre fichier projet ou dans un fichier `packages.config` (en fonction du format du projet). Pour plus d’informations, consultez [Vue d’ensemble et flux de consommation des packages](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Gestionnaire de package NuGet

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références** et choisissez **Gérer les packages NuGet**.

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use-02-ManageNuGetPackages.png)

1. Choisissez « nuget.org » comme **Source du package**, sélectionnez l’onglet **Parcourir**, recherchez **Newtonsoft.Json**, sélectionnez-le dans la liste, puis sélectionnez **Installer** :

    ![Recherche du package Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    Si vous souhaitez plus d’informations sur le gestionnaire de package NuGet, consultez [Installer et gérer des packages avec Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Acceptez toutes les invites de licence.

1. (Visual Studio 2017 uniquement) Si vous êtes invité à sélectionner un format de gestion de package, sélectionnez **PackageReference dans le fichier projet** :

    ![Sélectionner un format de gestion des packages](media/QS_Use-03b-SelectFormat.png)

1. Si vous êtes invité à vérifier les modifications, sélectionnez **OK**.

### <a name="package-manager-console"></a>Console du Gestionnaire de package

1. Sélectionnez la   >  commande de menu de la console Gestionnaire de **package NuGet** outils gestionnaire de package NuGet  >   .

1. Une fois la console ouverte, vérifiez que la liste déroulante **Projet par défaut** affiche le projet dans lequel vous souhaitez installer le package. Si la solution ne contient qu’un seul projet, il est déjà sélectionné.

    ![Sélectionner un projet pour le package](media/QS_Use-08-Console1.png)

1. Entrez la commande `Install-Package Newtonsoft.Json` (consultez [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). La fenêtre de la console affiche la sortie de la commande. Les erreurs indiquent généralement que le package n’est pas compatible avec le framework cible du projet.

   Si vous souhaitez plus d’informations sur la console du gestionnaire de package, consultez [Installer et gérer des packages avec la console du gestionnaire de package](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Utiliser l’API Newtonsoft.Json dans l’application

Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.

1. Ouvrez `MainWindow.xaml` et remplacez l’élément `Grid` existant par l’élément suivant :

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Ouvrez le fichier `MainWindow.xaml.cs` (situé sous le nœud `MainWindow.xaml` dans l’Explorateur de solutions), puis insérez le code suivant dans la classe `MainWindow` :

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Bien que vous ayez ajouté le package Newtonsoft.Json au projet, des tildes rouges s’affichent sous `JsonConvert`, car vous avez besoin d’une instruction `using` en haut du fichier de code :

    ```cs
    using Newtonsoft.Json;
    ```

1. Générez et exécutez l’application en appuyant sur F5 ou en sélectionnant **Déboguer**  >  **Démarrer le débogage**:

    ![Sortie initiale de l’application WPF](media/QS_Use-06-AppStart.png)

1. Cliquez sur le bouton pour remplacer le contenu du TextBlock par du texte JSON :

    ![Sortie de l’application WPF après un clic sur le bouton](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Vidéo connexe

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Recherchez d’autres vidéos NuGet sur [Channel 9](https://channel9.msdn.com/Series/NuGet-101) et [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Étapes suivantes

Félicitations pour l’installation et l’utilisation de votre premier package NuGet !

> [!div class="nextstepaction"]
> [Installer et gérer des packages à l’aide de Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Installer et gérer des packages à l’aide de la Console du Gestionnaire de package](../consume-packages/install-use-packages-powershell.md)

Pour explorer plus en détail ce que NuGet a à offrir, sélectionnez les liens ci-dessous.

- [Vue d’ensemble et flux de travail de consommation de package](../consume-packages/overview-and-workflow.md)
- [Recherche et sélection de packages](../consume-packages/finding-and-choosing-packages.md)
- [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md)
