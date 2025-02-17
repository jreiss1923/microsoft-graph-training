---
ms.localizationpriority: medium
---

<!-- markdownlint-disable MD041 -->

In this section you will add app-only authentication to the application. This is required to obtain the necessary OAuth access token to call the Microsoft Graph.

## Configure Graph client for app-only authentication

In this section you will use the `GuzzleHttp\Client` class to request an access token by using the [client credentials flow](/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow).

1. Create a new file in the root directory of your project named **GraphHelper.php**. Add the following code.

    ```php
    <?php
    use Microsoft\Graph\Graph;
    use Microsoft\Graph\Http;
    use Microsoft\Graph\Model;
    use GuzzleHttp\Client;

    class GraphHelper {
    }
    ?>
    ```

1. Add the following code to the `GraphHelper` class.

    :::code language="php" source="../src/app-auth/graphapponlytutorial/GraphHelper.php" id="AppOnlyAuthConfigSnippet":::

1. Replace the empty `initializeGraph` function in **main.php** with the following.

    :::code language="php" source="../src/app-auth/graphapponlytutorial/main.php" id="InitializeGraphSnippet":::

This code loads information from the .env file, and initializes two properties, a `Client` object and a `Graph` object. The `Client` object will be used to request an access token, and the `Graph` object will be used to make calls to Microsoft Graph.

## Test the client credentials flow

Next, add code to get an access token from the `GraphHelper`.

1. Add the following function to the `GraphHelper` class.

    :::code language="php" source="../src/app-auth/graphapponlytutorial/GraphHelper.php" id="GetAppOnlyTokenSnippet":::

1. Replace the empty `displayAccessToken` function in **main.php** with the following.

    :::code language="php" source="../src/app-auth/graphapponlytutorial/main.php" id="DisplayAccessTokenSnippet":::

1. Build and run the app. Enter `1` when prompted for an option. The application displays a URL and device code.

    ```bash
    $ php main.php

    PHP Graph Tutorial

    Please choose one of the following options:
    0. Exit
    1. Display access token
    2. List users
    3. Make a Graph call
    1
    App-only token: eyJ0eXAiOiJKV1QiLCJub25jZSI6IlVDTzRYOWtKYlNLVjVkRzJGenJqd2xvVUcwWS...
    ```

    [!INCLUDE [token-debug-tip](../../shared/app-token-debug-tip.md)]
