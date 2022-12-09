---
layout: default
title: QuickStart API Tutorial
nav_order: 50
---
# QuickStart API Tutorial

Integration Manager is an entirely API-driven platform. Every function avaialble via the UI is also available as an API (and more!).

Open API specs for Integration Manager APIs are located here: [https://api.im.actiandatacloud.com/v2/apidocs/](https://api.im.actiandatacloud.com/v2/apidocs/)

## Step 1: Retrieve an Access Token
```
POST https://localhost:8080/api/login
Content-Type: application/json

{
    "username": "[username]",
    "password": "[password text]"
}
```
Response:
```
{
    "access_token": [access token value],
    "token_type": "bearer",
    "refresh_token": [refresh token value],
    "expires_in": 36000
}
```

## Step 2: Create a JobConfig
```
POST https://localhost:8080/api/jobconfigs
Authorization: Bearer [access token value]
Content-Type: application/json

{
    "active": true,
    "name": "sample config",
    "description": "this is sample config created from API"
}
```
Response:
```
{
    "id": "44",
    "active": true,
    "name": "sample config",
    "description": "this is sample config created from API",
    "href": "http://localhost:8080/api/jobconfigs/44",
    "user": {
        "id": "1",
        "name": "admin",
        "href": "http://localhost:8080/api/users/1"
    },
    "created": "Apr 12, 2019 12:40:51 PM",
    "createdByUser": {
        "id": "1",
        "name": "admin",
        "href": "http://localhost:8080/api/users/1"
    },
    "lastModified": "Apr 12, 2019 12:40:51 PM",
    "lastModifiedByUser": {
        "id": "1",
        "name": "admin",
        "href": "http://localhost:8080/api/users/1"
    }
}
```

## Step 3: Upload an Integration Package
```
POST https://localhost:8080/api/jobconfigs/44/files
Authorization: Bearer [access token value]
Content-Type: multipart/form-data

key=samplePackage.djar
file="C:\packages\samplePackage.djar"
```
Response:
```
{
    "name": "samplePackage.djar",
    "href": "http://localhost:8080/api/jobconfigs/44/files/samplePackage.djar",
    "metadata": {
        "size": 5732,
        "lastModified": "Apr 12, 2019 1:32:52 PM"
    }
}
```

## Step 4: Update the JobConfig with Package Name and Entry Point
```
PUT https://localhost:8080/api/jobconfigs/44
Authorization: Bearer [access token value]
Content-Type: multipart/form-data

{
    "active": true,
    "name": "sample config",
    "description": "this is sample config created from API"
	"runtimeConfig": {
		"packageName": "samplePackage.djar",
		"entryPoint": "integrateXYZ.process"
	}
}
```
Response:
```
{
    "id": "44",
    "active": true,
    "name": "sample config",
    "description": "this is sample config created from API",
    "href": "http://localhost:8080/api/jobconfigs/44",
	"runtimeConfig": {
		"packageName": "samplePackage.djar",
		"entryPoint": "integrateXYZ.process",
        "packagePrefix": "configuration\\44",
        "packageArtifactOverride": false
	}
    "user": {
        "id": "1",
        "name": "admin",
        "href": "http://localhost:8080/api/users/1"
    },
    "created": "Apr 12, 2019 12:40:51 PM",
    "createdByUser": {
        "id": "1",
        "name": "admin",
        "href": "http://localhost:8080/api/users/1"
    },
    "lastModified": "Apr 12, 2019 12:40:51 PM",
    "lastModifiedByUser": {
        "id": "1",
        "name": "admin",
        "href": "http://localhost:8080/api/users/1"
    }
}
```

## Step 5: Run the JobConfig
```
POST https://localhost:8080/api/jobconfigs/44/jobs
Authorization: Bearer [access token value]
Content-Type: application/json
```
Response:
```
{
    "href": "http://localhost:8080/api/jobs/3845bf5-6504-48dc-ab1e",
    "id": "3845bf5-6504-48dc-ab1e",
    "scheduled": "Apr 12, 2019 2:41:41 PM",
    "status": "QUEUED",
    "finalDestinationId": "1",
    "jobConfig": {
        "id": "44",
        "name": "sample config",
        "href": "http://localhost:8080/api/jobconfigs/44"
    },
    "submittedByUser": {
        "id": "1",
        "name": "admin",
        "href": "http://localhost:8080/api/users/1"
    }
}  
```