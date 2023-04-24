---
layout: post
title: Azure and MS Graph Email Import
author: jesse.wolcott
---

Many applications import email from O365 mailboxes using MS Graph. This document aims to assist in that setup process.

1. Verify that your email mailbox exists and is in O365. O365 cannot access on-prem mailboxes with Graph.
2. Go to https://portal.azure.com
3. Go to Azure Active Directory, then App Registrations
4. Click "New Registration", enter the user-facing name of the app that makes sense
    - Fill out https://login.microsoftonline.com/common/oauth2/nativeclient for the redirect URI (if your application does not specify)
5. From the left-hand pane under the Manage heading, click Certificates & secrets.
6. Under Client secrets, click + New client secret
	- Enter an appropriate description
	- Set an appropriate Expiration setting for the secret
	- Click Add
7. Record the value of the Secret as this will be needed during Mailbox Importer Account configuration.
8. From the left-hand pane under the Manage heading, click API permissions
    - Click the + Add a permission button
    - Click Microsoft Graph at the top of the page that flies out
    - Choose Application permissions
    - Navigate to Mail and expand it
    - Check Mail.ReadWrite
    - Check Mail.ReadBasic
    - Check Mail.ReadBasic.All
    - Check MailboxSettings.Read
    - Check User.Read
    - Click Add permissions
9. Grant admin consent for the app registration
10. Click on App Registrations, then Endpoints 
    - Record OAuth 2.0 authorization endpoint (v2) (but its probably https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize )
    - Record OAuth 2.0 token endpoint (v2) (but its probably https://login.microsoftonline.com/{tenant}/v2.0/token )
11. Record the Application (client) ID
    - **NOTE:** At this point, your app can access literally everyones mailbox. 
13. Create a mail-enabled security group and add your mailbox to it. 
14. Wait for replication to Azure and verify that your user mailbox is a member in the syncronized group
15. Run the script located here: [New-AppPolicy.ps1](https://github.com/jessewolcott/InfrastructureScripts/blob/main/New-AppPolicy.ps1) with your values entered
16. With your Exchange Online session connected (part of the script above), you can change '$CreatePolicy' to 'No', and '$TestPolicy' to 'Yes' and enter a user to check.

## Nightingale Testing

Nightingale is a REST client that we can use to test MS Graph calls in real time (instead of using applications individual built-in testing mechanisms which are often terrible). You can install it from the Company Portal.

To test if your application is able to access email (and verify that it is limited to only the email you specify), open Nightingale, and make sure you have the following info:

- Grant type: Client Credentials
- Client ID (Azure calls this AppId):
- Client Secret:
- Access Token URL: https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
- Scope: https://graph.microsoft.com/.default

Create a new Request, under the "Auth" header, and choose "OAuth 2.0". Enter all the info above, and click "Get new token". If that doesn't work, make sure your secret and AppId are correct.

After you've received a token, in the top bar, enter ```https://graph.microsoft.com/v1.0/Users/user@domain.com/mailFolders/Inbox/messages``` and hit ```Send```. Your results in the bottom pane will give you feedback. Change ```user@domain.com``` to whatever your email is. If there is no email, you'll see something like:
```JSON
{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('user%40domain.com')/mailFolders('Inbox')/messages",
  "value": []
}
```

If there is email, you'll see it in JSON form. You can also get informative errors like "Resource not found" (which means your mailbox isn't on O365) or "Access denied" (which is self-explanatory).

###  Resources
https://www.azure365pro.com/access-specific-office-365-mailbox-using-microsoft-graph/

