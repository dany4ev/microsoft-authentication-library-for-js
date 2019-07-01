
Microsoft Authentication Library for Electron Proof of Concept
==============================================================

The MSAL library for Electron enables cross-platform Electron desktop applications to authenticate users using [Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-overview) work and school accounts (AAD) as well as Microsoft personal accounts (MSA). It also enables your Electron app to get tokens to access [Microsoft Cloud](https://cloud.microsoft.com) services such as [Microsoft Graph](https://graph.microsoft.io).

## Installation

Using NPM:

```bash
npm install msal-electron-poc
```

## What To Expect From This Library

At present, `msal-electron-poc` is intended to be a proof of concept library in providing authentication to Electron applications using OAuth 2.0's Authorization Code Grant flow and Azure Active Directory. 

***As such, this library is not recommended for serious projects or applications intended for production.***

## OAuth 2.0 and the Authorization Code Flow

MSAL Electron implements the [Authorization Code Grant Flow](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow), as defined by the OAuth 2.0 protocol and is [OpenID](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-protocols-oidc) compliant.

Our goal is that the library abstracts enough of the protocol away so that you can get 'plug and play' authentication, but it is important to know and understand the auth code flow from a security perspective.

The auth code flow runs in the context of a native client (a client running directly on a user's device), which falls under the definition of a public client in the OAuth 2.0 spec.

As opposed to confidential clients, public clients cannot guarantee the confidentiality of their credentials given the environment they operate in. In short, the auth code grant is designed as a specific solution to more secure authentication for this kind of application.

For more information on the concepts related to the Auth Code Grant flow, refer to the [official RFC on OAuth 2.0](https://tools.ietf.org/html/rfc6749#section-1.3.1).


## Prerequisites

Before using MSAL Electron you will need to [register an application in Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) to get a valid `clientId` for configuration, and to register the routes that your app will accept redirect traffic on.

You will need the following information in order to configure `msal-electron` to work with your AAD application:

+ Tenant ID
+ Client ID
+ Authority
+ Redirect URI
    + You must set the Redirect URI on the AAD App yourself.
    + `msal-electron-poc` uses custom schemes to register a custom file protocol to listen for redirect responses. We recommend you register a Native/Mobile Redirect Address with the form "myappname://authentication"
+ A set of scopes you will be requesting the user's authorization on (i.e. user.read for Microsoft Graph API). Read more about scopes [here](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent).

## License

Copyright (c) Microsoft Corporation.  All rights reserved. Licensed under the MIT License (the "License");

## We Value and Adhere to the Microsoft Open Source Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.