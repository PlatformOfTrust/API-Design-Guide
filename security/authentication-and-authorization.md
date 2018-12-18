# Authentication and authorization

REST APIs should be stateless. Every request should be self-sufficient and must be fulfilled without knowledge of the prior request. This happens in the case of Authorizing a user action.

Previously, developers stored user information in server-side sessions, which is not a scalable approach. For that reason, every request should contain all the information of a user \(if it’s a secure API\), instead of relying on previous requests.

This doesn’t limit APIs to a user as an authorized person, as it allows service-to-service authorization as well. For user authorization, JWT \(JSON Web Token\) with OAuth2 provides a way to achieve this. Additionally, for service-to-service communication, try to have the encrypted API-key passed in the header. 

#### Use Access and Refresh Tokens <a id="9549"></a>

Modern stateless, RESTful APIs implement authentication with tokens. This eliminates the need to handle sessions and cookies on a now stateless server, and makes it really easy to debug network requests by simply utilising the `Authorization` header \(or even an `access_token` query param\).

**Access Tokens**

The access token is used for authenticating all future API requests, has a short life span and can’t be revoked\*.

**Refresh Tokens**

The refresh token is returned in the initial login response, but it is hashed and stored in the database with an expiry timestamp and relationship to the user. This acts as a long-life, password-like secret token, which can be used to request a new short-life JWT access tokens. Refresh tokens also extend their life every time they are used for renewal, meaning that a user doesn’t need to log in again if they continually use the service.
