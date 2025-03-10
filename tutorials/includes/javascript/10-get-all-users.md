---
ms.localizationpriority: medium
---

<!-- markdownlint-disable MD041 -->

In this section you will add the ability to list all users in your Azure Active Directory using app-only authentication. This section is optional, and requires completion of [Optional: configure app-only authentication](?tutorial-step=2) and [Optional: add app-only authentication](?tutorial-step=8). These steps can only be completed with a work or school account.

> [!div class="nextstepaction"]
> [I don't need app-only, skip to the end](?tutorial-step=10)

1. Open **graphHelper.js** and add the following function.

    :::code language="javascript" source="./src/demo/graphtutorial/graphHelper.js" id="GetUsersSnippet":::

1. Replace the empty `listUsersAsync` function in **index.js** with the following.

    :::code language="javascript" source="./src/demo/graphtutorial/index.js" id="ListUsersSnippet":::

1. Run the app, sign in, and choose option 4 to list users.

    ```Shell
    [1] Display access token
    [2] List my inbox
    [3] Send mail
    [4] List users (requires app-only)
    [5] Make a Graph call
    [0] Exit

    Select an option [1...5 / 0]: 4
    User: Adele Vance
      ID: 05fb57bf-2653-4396-846d-2f210a91d9cf
      Email: AdeleV@contoso.com
    User: Alex Wilber
      ID: a36fe267-a437-4d24-b39e-7344774d606c
      Email: AlexW@contoso.com
    User: Allan Deyoung
      ID: 54cebbaa-2c56-47ec-b878-c8ff309746b0
      Email: AllanD@contoso.com
    User: Bianca Pisani
      ID: 9a7dcbd0-72f0-48a9-a9fa-03cd46641d49
      Email: NO EMAIL
    User: Brian Johnson (TAILSPIN)
      ID: a8989e40-be57-4c2e-bf0b-7cdc471e9cc4
      Email: BrianJ@contoso.com

    ...

    More users available? true
    ```

## Code explained

Consider the code in the `getUsersAsync` function. It is very similar to the code in `getInboxAsync`:

- It gets a collection of users
- It uses `select` to request specific properties
- It uses `top` to limit the number of users returned
- It uses `orderBy` to sort the response

The key difference is that this code uses the `_appClient`, not the `_userClient`. Both clients use the same syntax and request builders, but were configured with different credentials.
