---
title: Delegated authorization v/s Federated identity
date: Wed, 02 Mar 2022 17:04:00 +0000
---

Delegated Authority is the ability for a service or application to gain access to a user's resources on their behalf. Delegated Authority allows the owner of a set of resources to delegate access to a designated client application without enabling the client application to impersonate the user.

OAuth 2.0 is an authorization framework that is a process defined for delegated authorization. It allows users to grant a third-party website or application access to the user's protected resources without revealing the users' long-term credentials or identity.

## OAuth 2.0 Key Terminology

A few key terms to get familiar with OAuth:

-   **Resource Owner**: Owner of the data, resources, accounts, etc.
-   **Client**: Third-party application requesting access to resources.
-   **Authorization Server**: The application that identifies the resource owner.
-   **Resource Server**: A service the Client would use on behalf of the resource owner.
-   **Access Token**: An authorization key used between clients and servers to communicate.
-   **Scope**: Level of access requested by an application.

OAuth separates the role of the Client and the resource owner and introduces an authorization layer. The Client uses an access token instead of using the resources owner's credentials to access resources, a string that denotes the lifetime, access & Scope of the token. The resource owner requests access to resources hosted by the resource server with particular issued credentials.

The Client can use the access token to access the protected resources issued by the third party client by an authorization server with the resource owner's approval and hosted by a resource server.

The access tokens generated for authorization through APIs are done using JSON web token (JWT).

OAuth 2.0 consists of different process flow to obtain an access token. These flows are called grant types. Choosing the flow depends on the application use case.

-   **Authorization Code Flow**: Authorization Code flow is the most commonly used web application executed on a server. It is also used by mobile applications using the (PKCE) technique.
-   **Implicit Flow with Form Post**: Implicit Flow with Form Post is used purely for JavaScript-centric applications (Single-Page Applications, React, Angular, Vue, etc.) executing on a user's browser.
-   **Resource Owner Password Flow**: Resource owner password flow is used by highly-trusted applications.
-   **Client Credentials Flow**: Client Credentials Flow is used for machine-to-machine communication.

## OAuth 2.0 Terminology

OAuth 2.0 terminology:

-   **Redirect URI**: The callback URI that the authorization server calls after process completion.
-   **Scope**: This specifies the "scope" of the access to the resource at a granular level, i.e., Is this authorization request to read, edit, delete the resources, etc.
-   **Response Type**: Response type is a reaction that specifies that the Authorization server will provide the Client with an "Authorization Code," therefore, the Client will exchange an access token (using the back-channel).

## Federated Identity

Federated Identity refers to the concept that allows one service provider to authenticate a user using their identity with another service provider. In this scenario, the user can access protected resources on behalf of another party. Federated authentication will allow you to log in to a site or application via your Google or Facebook account.

There are primarily two types of federated identity authentication standards, and both can provide the single sign-on feature.

-   OpenId Connect
-   SAML

### OpenId Connect

OpenId Connect is built over the process flows of OAuth 2.0

In addition to the access token, an id-token is an additional piece produced in JWT format by the authorization server.

If the id token does not provide sufficient information, the user information endpoint is used to fetch more user info.

An initial call to the Authorization Server requires an "OpenID" parameter to be passed within the Scope.

### SAML

SAML stands for Security Assertion Markup Language. SAML is an asynchronous protocol that enables users to access multiple web applications using a single set of login credentials. It passes authentication info between two clients using an identity provider and a web application (service provider) with a particular format. The identity provider and the service provider never directly interact, the browser acts as an agent to carry out all redirections. It is popularly used as an enterprise solution.

#### SAML Workflow:

-   **Identity Provider**: A user logged into a system
-   **Service Provider**: An application that needs to be logged into, for example, Zendesk.

1.  The user accesses the application using a web link.
2.  The application is able to identify the user's origin (by application subdomain, user IP address, etc.) and redirects the user back to the IP, asking for an authentication request.
3.  The user establishes a browser session with the identity provider by logging into the identity provider.
4.  The identity provider creates an authentication response in an XML document, including the user's username or email address, signs it using an X.509 certificate, and posts the information to the service provider.
5.  The service provider retrieves the authentication response and validates it using the certificate fingerprint. The service provider knows the identity provider and has a certificate fingerprint with the browser session open.
6.  The user's identity is established, and the user is provided access to the application.

SAML SSO offers an enhanced user experience where users do not need to maintain multiple credentials for multiple applications. It reduces cost in terms of IT help desk to manage calls.