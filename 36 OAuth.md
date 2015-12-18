# OAuth

## OAuth
Standard for the delegation of restricted rights.
Developed and Twitter and Ma.gnolia.

Used by major vendors: Google, Facebook, Microsoft, ...

## OAuth Roles
* client: wants to access some server called a resource server on behalf of the user
* resource server
* user (resource owner)
* authorization server

## OAuth flow
The client redirects the user to the Authorization server.
The client passes a "scope" variable along, which describes the rights the client wants to have from the user.

The user has to login and the authorization asks the user if he wants to delegate right x and y for client a or b.

If the user agrees, the authorization server generates and provides an "access token" to the client.

The client can then access the resource server and pass it the access token.
The access token gives the client the permission to act on behalf of the user.

## OAuth flows
OAuth supports different flows for different use cases.

Examples:
* authorization code grant
  * for server-side web apps
* implicit grant
  * for single page applications

## Authentication with OAuth 2.0
* client sends a request to the authorization server to request a token for reading the user's profile
* when the client gets the token, it can access the resource server and read the profile of the current user
  * issue: the user profile is not defined by OAuth 2.0

## OpenId Connect (OIDC)
Extension of OAuth 2.0

Defines
* how to use OAuth 2.0 for authentication
* how to query User Profile
* how to get an identity token
  * JWT token with information about the user
    * username, email, company, ...
  * can be signed/encrypted by the authorization server

OpenId Connects eliminates some security holes of OAuth 2.0

## OIDC Flow
* client requests user information to the authorization server
  * it receives an access token (OAuth 2.0 authentication)
  * it receives an identity token containing the user profile information

## Identity Server 3
FOSS solution to provide an authorization server

## Conclusions
* use OAuth 2.0 to delegate rights
* use the implicit grant oauth profile for Single Page Applications
* use OpenId Connect to handle authentication with OAuth 2.0 and get user profiles in a standardized manner
* maintain user accounts centrally
* only the authorization server gets the user credentials
* other services only get tokens
