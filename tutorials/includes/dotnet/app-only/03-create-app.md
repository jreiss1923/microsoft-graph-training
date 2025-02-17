---
ms.localizationpriority: medium
---

<!-- markdownlint-disable MD002 MD041 -->

Begin by creating a new .NET console project using the [.NET CLI](/dotnet/core/tools/).

1. Open your command-line interface (CLI) in a directory where you want to create the project. Run the following command.

    ```dotnetcli
    dotnet new console -o GraphAppOnlyTutorial
    ```

1. Once the project is created, verify that it works by changing the current directory to the **GraphTutorial** directory and running the following command in your CLI.

    ```dotnetcli
    dotnet run
    ```

    If it works, the app should output `Hello, World!`.

## Install dependencies

Before moving on, add some additional dependencies that you will use later.

- [.NET configuration packages](/dotnet/core/extensions/configuration) to read application configuration from **appsettings.json**.
- [Azure Identity client library for .NET](https://www.nuget.org/packages/Azure.Identity)  to authenticate the user and acquire access tokens.
- [Microsoft Graph .NET client library](https://github.com/microsoftgraph/msgraph-sdk-dotnet) to make calls to the Microsoft Graph.

Run the following commands in your CLI to install the dependencies.

```Shell
dotnet add package Microsoft.Extensions.Configuration.Binder
dotnet add package Microsoft.Extensions.Configuration.Json
dotnet add package Microsoft.Extensions.Configuration.UserSecrets
dotnet add package Azure.Identity
dotnet add package Microsoft.Graph
```

## Load application settings

In this section you'll add the details of your app registration to the project.

1. Create a file in the **GraphAppOnlyTutorial** directory named **appsettings.json** and add the following code.

    :::code language="json" source="../src/app-auth/GraphAppOnlyTutorial/appsettings.json":::

1. Update the values according to the following table.

    | Setting | Value |
    |---------|-------|
    | `clientId` | The client ID of your app registration |
    | `tenantId` | The tenant ID of your organization. |

    > [!TIP]
    > Optionally, you can set these values in a separate file named **appsettings.Development.json**.

1. Add your client secret to the [.NET Secret Manager](/aspnet/core/security/app-secrets). In your command-line interface, change the directory to the location of **GraphAppOnlyTutorial.csproj** and run the following commands, replacing *&lt;client-secret&gt;* with your client secret.

    ```dotnetcli
    dotnet user-secrets init
    dotnet user-secrets set settings:clientSecret <client-secret>
    ```

1. Update **GraphAppOnlyTutorial.csproj** to copy **appsettings.json** to the output directory. Add the following code between the `<Project>` and `</Project>` lines.

    ```xml
    <ItemGroup>
      <None Include="appsettings*.json">
        <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      </None>
    </ItemGroup>
    ```

1. Create a file in the **GraphAppOnlyTutorial** directory named **Settings.cs** and add the following code.

    :::code language="csharp" source="../src/app-auth/GraphAppOnlyTutorial/Settings.cs" id="SettingsSnippet":::

## Design the app

In this section you will create a simple console-based menu.

1. Open **./Program.cs** and replace its entire contents with the following code.

    :::code language="csharp" source="../src/app-auth/GraphAppOnlyTutorial/Program.cs" id="ProgramSnippet":::

1. Add the following placeholder methods at the end of the file. You'll implement them in later steps.

    ```csharp
    void InitializeGraph(Settings settings)
    {
        // TODO
    }

    async Task DisplayAccessTokenAsync()
    {
        // TODO
    }

    async Task ListUsersAsync()
    {
        // TODO
    }

    async Task MakeGraphCallAsync()
    {
        // TODO
    }
    ```

This implements a basic menu and reads the user's choice from the command line.
