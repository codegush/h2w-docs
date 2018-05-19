---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - cURL

toc_footers:
  - <a href='http://hate2wait.io'>hate2wait Homepage</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the hate2wait API! Use this API to manage a queue or clients using hate2wait QMS.

You can view code examples in the dark area to the right.

Most hate2wait API endpoints require an API key in the HTTP header with each request. See Authentication on how to get your a API key.

## Requirements

You need an account with hate2wait to use this API. Please sign up on the hate2wait Dashboard

Your queue management system needs to be able to send HTTP requests to hate2wait via the internet to update information about your waitlist (like estimated wait time, services, locations, online availability etc.)

## Basics

The hate2wait API V2 is a completely RESTful. Requests to and responses from the API are formatted as JSON following the recommendations of the of the [JSON API specification](http://jsonapi.org/).


# Authentication

<aside class="notice">
You will need to set an AUTHORIZATION header with almost every request to this API. A few endpoints allow unauthenticated access or (like registering user, creating user sessions etc.) might expect special tokens.
</aside>

Obtain an API key by calling a login endpoint (see below). If successful, the response will contain a token string.

Once you have a token, set the HTTP header named AUTHORIZATION: Bearer [token] when you call another endpoint. This will work until the expiry time(determined by admin). At that time, you'll need to call a login endpoint again to obtain a new token.

`Authorization: Bearer [token]`

## Login using mobile app/browser client

> Authenticated request

```shell
curl 'https://api.hate2wait.io/api/v1/login' \
     -H 'Content-Type: application/json' \
     -X POST -d @- << EOF
{
  "email": "[email]",
  "password": "[password]"
}
EOF
```

> Response format

```shell
{
  token: [token]
}
```

This endpoint does not require a token itself.

hate2wait uses API token to allow access to the API. You need to sign up for an account at Administration Dashboard in order to use the Login Dashboard User endpoint.

This endpoint does not require an API key itself.

It returns the created token as a JSON hash.

Parameter | Description
--------- | -----------
email | Your email address
password | Your password

### HTTP Request

`POST https://api.hate2wait.io/api/v1/login`

# User

User is an entity, who uses this application and can have server roles based on access given.

## Registeration

> Authenticated request

```shell
curl 'https://api.hate2wait.io/api/v1/users' \
     -H 'Content-Type: application/json' \
     -X POST -d @- << EOF
{
  "name": "[name]",
  "email": "[email]",
  "password": "[password]",
  "password_confirmation": "[password_confirmation]"
}
EOF
```

> Response format

```shell
{}
```

This endpoint does not require a token itself. It is used for registering a new user with name, email and password.

Parameter | Description
--------- | -----------
name | Your name
email | Your email address
password | Password
password_confirmation | Repeat the same password

### HTTP Request

`POST https://api.hate2wait.io/api/v1/users`

## Verify email

This endpoint will be used from user's email to verify the account.

> Authenticated request

```shell
curl 'https://api.hate2wait.io/api/v1/users/verify_email' \
     -H 'Content-Type: application/json' \
     -X GET -d @- << EOF
{
  "email": "[email]",
  "email_verification_token": "[email_verification_token]"
}
EOF
```

> Response format

```shell
The response will issue a redirection to the requesting client.
```

Parameter | Description
--------- | -----------
email | Email
email_verification_token | Email verification token

### HTTP Request

`GET https://api.hate2wait.io/api/v1/verify_email`

## Profile

This endpoint will return logged in user's profile

> Authenticated request

```shell
curl 'https://api.hate2wait.io/api/v1/users/profile' \
     -H 'Content-Type: application/json' \
     -H 'AUTHORIZATION: Bearer [token]' \
     -X GET -d @- << EOF
EOF
```

> Response format

```shell
{
  "id": "id",
  "name": "name",
  "email": "email",
  "phone_number": "phone_number"
}
```

### HTTP Request

`GET https://api.hate2wait.io/api/v1/profile`

# Reset password

## Create

This endpoint will do an email to the user, who want's to reset his account password.

> Authenticated request

```shell
curl 'https://api.hate2wait.io/api/v1/users/profile' \
     -H 'Content-Type: application/json' \
     -X POST -d @- << EOF
{
  "email": "[email]"
}
EOF
```

> Response format

```shell
{}
```

### HTTP Request

`POST https://api.hate2wait.io/api/v1/password_resets`

## Update

This endpoint will get active when a user tries to reset password from app/desktop client.


> Authenticated request

```shell
curl 'https://api.hate2wait.io/api/v1/users/profile' \
     -H 'Content-Type: application/json' \
     -X PUT -d @- << EOF
{
  "email": "[email]",
  "reset_token": "[reset_token]",
  "password": "[password]",
  "password_confirmation": "[password_confirmation]",
}
EOF
```

> Response format

```shell
{}
```

### HTTP Request

`PUT https://api.hate2wait.io/api/v1/password_resets`

