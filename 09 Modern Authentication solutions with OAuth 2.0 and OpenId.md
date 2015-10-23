# Modern Authentication solutions with OAuth 2.0 and OpenId

## Introduction
* many apps
* many devices, applications and services

## OAuth
* developed at Twitter and Ma.gnolia
* delegation of (restricted rights)

## OAuth Roles
* client who tries to access a resource server
* user: resource owner
* authorization server: has access to the user accounts

## Basic Flow
* Client redirects user to the authorization server (redirection) (&scope=...)
  * scopes define the user rights the user wants to get
* Authorization then redirection with an Access Token
* Client provides his access token to the resource server

The client only provides its credentials to the authorization server, never to the resource servers.

## Other flows
* authorization code grand: for server-side web apps
* implicit grant: for single page applications

## Authentication with OAuth 2.0
* Client: request token for reading profile (to the Authorization server)
* Client receives the access token
* Client requests information from the resource server by providing his access token

OAuth only defines the communication between the client and the authorization server.

OpenId connect:
* is an extension to OAuth 2.0
* defines how to use OAuth 2.0 for authentication
* defines how to query user profile
* client also gets ID Token
  * JSON Web Token

Flow with OpenId connect
* client -> auth
* authorization server: provides ID token
* client: provides his id token to the resource server

## JSON Web Tokens
* string consisting of multiple parts
* parts separated by '.'
* encoded with base64
* parts
  * access rights
  * user information (username, email, ...)
  * digital signature

