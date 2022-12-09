---
layout: default
title: Scriptable Agent Registration
nav_order: 8
parent: Advanced Topics
---
# Scriptable Agent Registration

## Prerequisite(s):

* Install Integration Agent 3.1.0 or later.
* Enable an API Password for the User registering the Agent.
* Access to an API tool such as Postman, SoapUI, or Curl.

## Step 1: Retrieve an Access Token

```
REQUEST:
POST https://api.im.actiandatacloud.com/v2/api/login

HEADER(S):
Content-Type: application/json

BODY:
{
    "username": "[username]",
    "password": "[password text]"
}
```

```
RESPONSE:
200 OK

{
    "access_token": [access token value],
    "token_type": "bearer",
    "refresh_token": [refresh token value],
    "expires_in": 36000
}
```

## Step 2: Retrieve a User Code

```
REQUEST:
POST https://api.im.actiandatacloud.com/v2/api/device/code?client_id=integration-agent&host=[agent hostname]

HEADER(S):
Authorization: Bearer [access token value]
```

```
RESPONSE:
201 Created

{
    "approved": false,
    "user_code": "[user code]",
    "hostname": "[agent hostname]",
    "device_code": "[device code]",
    "verification_uri_complete": "[verification uri complete]",
    "client_id": "integration-agent",
    "expires_in": 599,
    "interval": 15,
    "owner": {
        "id": "[user id]",
        "name": "[username]"
    }
}
```

## Step 3: Activate Device Code

```
REQUEST:
POST [verification uri complete]

HEADER(S):
Authorization: Bearer [access token value]
```

```
RESPONSE:
200 OK

# Integration Manager Connection Info
im.base-url=[base url]
im.client-id=[client id]
im.client-secret=[client secret]
im.device-code=[device code]
im.user-code=[user code]
```

## Step 4: Update the Agent

Copy and paste connection info into /IntegrationAgent/conf/application.properties file. Make sure to delete/overwrite any existing im.\* values that may be present. Duplicate entries will yield inconsistent results.

Start/restart Agent. It will now register itself.

