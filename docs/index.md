# FastAPI-Security

FastAPI-Security is a package that you can use together with [FastAPI](https://fastapi.tiangolo.com/) to easily add authentication and authorization.

## Key features

- Authentication via JWT-based OAuth 2 access tokens and via Basic Auth
- Pydantic-based `User` model for authenticated and anonymous users
- Sub-classable `UserPermission` dependency to check against the `permissions` attribute returned in OAuth 2 access tokens
- Ability to extract user info from access tokens via OpenID Connect

## Current limitations

- Only supports validating access tokens using public keys from a JSON Web Key Set (JWKS) endpoint. I.e. for use with external identity providers such as Auth0 and ORY Hydra.
- Permissions can only be picked up automatically from OAuth2 tokens, from the non-standard `permissions` list attribute (Auth0 provides this, maybe other identity providers as well). For all other use cases, `permission_overrides` must be used. For example if there's a basic auth user called `user1` you can set `permission_overrides={"user1": ["*"]}` to give the user access to all permissions, or `permission_overrides={"user1": ["products:create"]}` to only assign `user1` with the permission `products:create`.

Installation

```
pip install fastapi-security
```

## Usage example

An example app using FastAPI-Security [can be found here](https://github.com/jmagnusson/fastapi-security/tree/main/examples).
