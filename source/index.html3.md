---
title: HeySasha V1 API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href=''>Sign Up for a Developer Key</a>
  - <a href=''>Documentation Powered by HeySasha</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the HeySasha API! You can use our API to access HeySasha endpoints, which can get information on various data in our database.

Current API domain is [API](http://45.62.96.157:8000). Feel free to try it.

If any bug report, please mail [Me](mailto: kfclts@gmail.com).

# Authentication
## Login

> Example Request Body

```json
{
  "email": "kfc@heysasha.com",
  "password": "opwqer"
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjb21wYW55SWQiOjEsInVzZXJJZCI6MSwidXNlclJvbGUiOiJyb290IiwiaWF0IjoxNTU5NTU0NjUwLCJleHAiOjE1NTk1NjU0NTB9.hioKNZnAstYk8QRHJf-djiwK7kjr6Pjn8isc9W7_eyM",
    "userId": "1",
    "companyId": "1"
  }
}
```

```shell
# With shell, you can just pass the correct header with each request
# Make sure to replace <API_TOKEN> with your API key.
curl "api_endpoint_here"
  -H "Authorization: bearer <API_TOKEN>
```

<!-- ```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
``` -->

Heysasha uses API token to allow access to the API. You can grant a new API token at our login API.

### HTTP Request
<span class="method-post">POST</span> `/v1/auth/login`


Heysasha expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: bearer <API_TOKEN>`

<aside class="notice">
You must replace <code>&lt;API_TOKEN&gt;</code> with your personal API key.
</aside>

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
email | TRUE | email format
password | TRUE | At least 8 digits, letters and numbers included.

### Access Permission
Role | Scope
---- | -----
Root | Full permission.
Admin | Full permission.
User  | Full permission.

## Forget Password
> Example Request Body

```json
{
  "email": "kfc@heysasha.com"
}
```

> Example Response Body

```json
{
    "TBD": "TBD"
}
```

### HTTP Request
<span class="method-post">POST</span> `/v1/auth/forget`

# Companies
## Get All Companies
<!-- > Example Request Body -->

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "englishName": "HeySasha",
        "localName": "三洨",
        "address": "Taipei City",
        "email": "info@heysasha.com",
        "phone": "027877878",
        "fax": "027877788",
        "vatNumber": "234569876",
        "taxRate": 0.05,
        "discount": 0.30,
        "image": "",
        "createdAt": "1559927053",
        "updatedAt": "1559927053"
      },
      {
        "id": "2",
        "englishName": "Google",
        "localName": "谷歌",
        "address": "New Taipei City",
        "email": "sales@google.com",
        "phone": "+1288888888",
        "fax": "+13989999999",
        "vatNumber": "88888888",
        "taxRate": 0.0,
        "discount": 0.60,
        "image": "32image",
        "createdAt": "1559927053",
        "updatedAt": "1559927053"
      }
    ]
  }
}
```
This endpoint retrieves all companies.
### HTTP Request
<span class="method-get">GET</span> `/v1/companies`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
sortBy | id | TBD.
filterBy | N/A | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Full permission.
Admin | Forbidden
User  | Forbidden

## Create a Company

> Example Request Body

```json
{
  "data": {
    "englishName": "HeySasha",
    "localName": "三洨",
    "address": "Taipei City",
    "email": "info@heysasha.com",
    "phone": "027877878",
    "fax": "027877788",
    "vatNumber": "234569876",
    "taxRate": 0.05,
    "discount": 0.30,
    "image": ""
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "englishName": "HeySasha",
    "localName": "三洨",
    "address": "Taipei City",
    "email": "info@heysasha.com",
    "phone": "027877878",
    "fax": "027877788",
    "vatNumber": "234569876",
    "taxRate": 0.05,
    "discount": 0.30,
    "image": "",
    "createdAt": "1559927053",
    "updatedAt": "1559927053"
  }
}
```

This endpoint creates a company.
### HTTP Request
<span class="method-post">POST</span> `/v1/companies`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
englishName | TRUE |
localName | TRUE |
address | TRUE |
email | TRUE |
phone | TRUE |
fax | TRUE |
vatNumber | TRUE |
taxRate | TRUE |
discount | TRUE |
image | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Full permission.
Admin | Forbidden.
User  | Forbidden.

## Get a Specific Company

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "englishName": "HeySasha",
    "localName": "三洨",
    "address": "Taipei City",
    "email": "info@heysasha.com",
    "phone": "027877878",
    "fax": "027877788",
    "vatNumber": "234569876",
    "taxRate": "5%",
    "discount": "30%",
    "image": "",
    "createdAt": "1559927161",
    "updatedAt": "1559927161"
  }
}
```

This endpoint retrieves a specific company.
### HTTP Request
<span class="method-get">GET</span> `/v1/companies/:companyId`

### Access Permission
Role | Scope
---- | -----
Root | Full permission
Admin | Can only retrieve company which <code>id</code> same as admin's <code>companyId</code>.
User  | Can only retrieve company which <code>id</code> same as user's <code>companyId</code>.

<aside class="warning">
If you are not rooot, no matter the <code>&lt;companyId&gt;</code> you pass at url prameter, you can only get the company which <code>&lt;companyId&gt;</code> same as yours
</aside>


## Update a Specific Company

> Example Request Body

```json
{
  "data": {
    "localName": "莎夏"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "englishName": "HeySasha",
    "localName": "莎夏",
    "address": "Taipei City",
    "email": "info@heysasha.com",
    "phone": "027877878",
    "fax": "027877788",
    "vatNumber": "234569876",
    "taxRate": 0.05,
    "discount": 0.30,
    "image": "",
    "createdAt": "1559927161",
    "updatedAt": "1559927161"
  }
}
```

This endpoint updates a specific company.
### HTTP Request
<span class="method-patch">PATCH</span>`/v1/companies/:companyId`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
englishName | TRUE |
localName | TRUE |
address | TRUE |
email | TRUE |
phone | TRUE |
fax | TRUE |
vatNumber | TRUE |
taxRate | TRUE |
discount | TRUE |
image | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Full permission.
Admin | Can only updates company which <code>id</code> same as admin's <code>companyId</code>.
User  | Forbidden.

## Delete a Specific Company

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  }
}
```

This endpoint deletes a specific company.
### HTTP Request
<span class="method-delete">DELETE</span>`/v1/companies/:companyId`

### Access Permission
Role | Scope
---- | -----
Root | Full permission.
Admin | Can only retrieve company which <code>id</code> same as admin's <code>companyId</code>.
User  | Can only retrieve company which <code>id</code> same as user's <code>companyId</code>.


## Get Users from a Specific Company

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "firstName": "Kuan",
        "middleName": "",
        "lastName": "Chang",
        "password": "12345",
        "email": "kuanc@heysasha.com",
        "phone": "028765432",
        "mobile": "+886952318999",
        "fax": "",
        "image": "K",
        "title": "CTO",
        "companyId": "2",
        "updatedAt": "1559927161",
        "createdAt": "1559927161"
      },
      {
        "id": "2",
        "firstName": "Frenk",
        "middleName": "",
        "lastName": "Wu",
        "password": "12345",
        "email": "frankw@heysasha.com",
        "phone": "023456789",
        "mobile": "+886919326222",
        "fax": "023456788",
        "image": "F",
        "title": "CMO",
        "companyId": "1",
        "updatedAt": "1559927161",
        "createdAt": "1559927161"
      }
    ]
  }
}
```

This endpoint get usesr from a specific company.
### HTTP Request
<span class="method-get">GET</span>`/v1/companies/:companyId/users`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Full permission.
Admin | Forbidden.
User  | Forbidden.



## Create a User for a Specific Company

> Example Request Body

```json
{
  "data": {
    "firstName": "Kuan",
    "middleName": "",
    "lastName": "Chang",
    "password": "12345",
    "email": "kuanc@heysasha.com",
    "phone": "028765432",
    "mobile": "+886952318999",
    "fax": "",
    "image": "K",
    "title": "CTO"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 201,
    "message": "Created"
  },
  "data": {
    "id": "1",
    "firstName": "Kuan",
    "middleName": "",
    "lastName": "Chang",
    "password": "12345",
    "email": "kuanc@heysasha.com",
    "phone": "028765432",
    "mobile": "+886952318999",
    "fax": "",
    "image": "K",
    "title": "CTO",
    "companyId": "2",
    "role": "admin",
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```

This endpoint create a user for a specific company.
### HTTP Request
<span class="method-post">POST</span>`/v1/companies/:companyId/users`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
firstName | TRUE |
middleName | TRUE |
lastName | TRUE |
password | TRUE |
email | TRUE |
phone | TRUE |
mobile | TRUE |
fax | TRUE |
image | TRUE |
title | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Full permission.
Admin | Forbidden.
User  | Forbidden.
<!-- ## Get a Specific User from a Specific Company
## Update a Specific User from a Specific Company
## Delete a Specific User from a Specific Company

## Get Accounts from a Specific Company
## Create an Account for a Specific Company
## Get a Specific Account from a Specific Company
## Update a Specific Account from a Specific Company
## Delete a Specific Account from a Specific Company

## Get Contacts from a Specific Company
## Create a Contact for a Specific Company
## Get a Specific Contact from a Specific Company
## Update a Specific Contact from a Specific Company
## Delete a Specific Contact from a Specific Company

## Get Projects from a Specific Company
## Create a Project for a Specific Company
## Get a Specific Project from a Specific Company
## Update a Specific Project from a Specific Company
## Delete a Specific Project from a Specific Company

## Get Quotations of a Specific Projects from a Specific Company

## Get Quotations from a Specific Company
## Create a Quotation for a Specific Company
## Get a Specific Quotation from a Specific Company
## Update a Specific Quotation from a Specific Company
## Delete a Specific Quotation from a Specific Company

## Get Products of a Specific Quotation from a Specific Company

## Get Products from a Specific Company
## Create a Product for a Specific Company
## Get a Specific Product from a Specific Company
## Update a Specific Product from a Specific Company
## Delete a Specific Product from a Specific Company -->

# Users

## Get Me

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "3",
    "firstName": "Kong",
    "middleName": "",
    "lastName": "Gong",
    "password": "$2a$12$7uHqDmqEw9gAcdr9GZwzfeQcqCAzzx1mbwGQ/uJtrFkMyyDwWjb4m",
    "email": "3@gm.co",
    "phone": "028765432",
    "mobile": "+886952318999",
    "fax": "",
    "image": "K",
    "title": "CTO",
    "role": "admin",
    "createdAt": "1559927161",
    "updatedAt": "1559927161",
    "hierarchyLevel": 2,
    "parentId": "1",
    "companyId": "2"
  }
}
```
This endpoint retrieves user's profile.
### HTTP Request
<span class="method-get">GET</span> `/v1/users/me`

### Access Permission
Role | Scope
---- | -----
Root | Full permission.
Admin | Full permission
User  | Full permission

## Get All Users

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "firstName": "Kuan",
        "middleName": "",
        "lastName": "Chang",
        "password": "12345",
        "email": "kuanc@heysasha.com",
        "phone": "028765432",
        "mobile": "+886952318999",
        "fax": "",
        "image": "K",
        "title": "CTO",
        "role": "user",
        "updatedAt": "1559927161",
        "createdAt": "1559927161",
        "hierarchyLevel": 2,
        "parentId": "1",
        "companyId": "2"
      },{
        "id": "2",
        "firstName": "Frenk",
        "middleName": "",
        "lastName": "Wu",
        "password": "12345",
        "email": "frankw@heysasha.com",
        "phone": "023456789",
        "mobile": "+886919326222",
        "fax": "023456788",
        "image": "F",
        "title": "CMO",
        "role": "user",
        "updatedAt": "1559927161",
        "createdAt": "1559927161",
        "hierarchyLevel": 2,
        "parentId": "1",
        "companyId": "2"
      }
    ]
  }
}
```

This endpoint retrieves all users.
### HTTP Request
<span class="method-get">GET</span> `/v1/users`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can retrieve users which <code>companyId</code> same as admin's.
User  | Full permission, can retrieve users with <code>companyId</code> same user's.

## Create a User

> Example Request Body

```json
{
  "data": {
    "firstName": "Kuan",
    "middleName": "",
    "lastName": "Chang",
    "password": "12345",
    "email": "kuanc@heysasha.com",
    "phone": "028765432",
    "mobile": "+886952318999",
    "fax": "",
    "image": "K",
    "title": "CTO",
    "parentId": "3"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 201,
    "message": "Created"
  },
  "data": {
    "id": "1",
    "firstName": "Kuan",
    "middleName": "",
    "lastName": "Chang",
    "password": "12345",
    "email": "kuanc@heysasha.com",
    "phone": "028765432",
    "mobile": "+886952318999",
    "fax": "",
    "image": "K",
    "title": "CTO",
    "role": "user",
    "updatedAt": "1559927161",
    "createdAt": "1559927161",
    "hierarchyLevel": 2,
    "parentId": "1",
    "companyId": "2"
  }
}
```

This endpoint creates a user.
### HTTP Request
<span class="method-post">POST</span> `/v1/users`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
firstName | TRUE |
middleName | TRUE |
lastName | TRUE |
password | TRUE |
email | TRUE |
phone | TRUE |
mobile | TRUE |
fax | TRUE |
image | TRUE |
title | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Creates user with admin's <code>companyId</code>.
User  | Forbidden.

## Get a Specific User

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "2",
    "firstName": "Frenk",
    "middleName": "",
    "lastName": "Wu",
    "password": "12345",
    "email": "frankw@heysasha.com",
    "phone": "023456789",
    "mobile": "+886919326222",
    "fax": "023456788",
    "image": "F",
    "title": "CMO",
    "role": "user",
    "updatedAt": "21559927161",
    "createdAt": "1559927161",
    "hierarchyLevel": 2,
    "parentId": "1",
    "companyId": "2"
  }
}
```

This endpoint retrieves a specific user.
### HTTP Request
<span class="method-get">GET</span> `/v1/users/:userId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can retrieve user which <code>companyId</code> same as admin's.
User  | Full permission, can retrieve user which <code>companyId</code> same as user's.

## Update a Specific User

> Example Request Body

```json
{
  "data": {
    "firstName": "Frank"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "2",
    "firstName": "Frank",
    "middleName": "",
    "lastName": "Wu",
    "password": "12345",
    "email": "frankw@heysasha.com",
    "phone": "023456789",
    "mobile": "+886919326222",
    "fax": "023456788",
    "image": "F",
    "title": "CMO",
    "role": "user",
    "updatedAt": "1559927161",
    "createdAt": "1559927161",
    "hierarchyLevel": 2,
    "parentId": "1",
    "companyId": "2"
  }
}
```

This endpoint updates a specific user.
### HTTP Request
<span class="method-patch">PATCH</span>`/v1/users/:userId`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
firstName | TRUE |
middleName | TRUE |
lastName | TRUE |
password | TRUE |
email | TRUE |
phone | TRUE |
mobile | TRUE |
fax | TRUE |
image | TRUE |
title | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can update users which <code>companyId</code> same as admin's .
User  | Can only updates user which <code>id</code> same as user's.


## Delete a Specific User

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "ok"
  }
}
```

This endpoint deletes a specific user.
### HTTP Request
<span class="method-delete">DELETE</span>`/v1/users/:userId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can delete user which <code>companyId</code> same as admin's.
User  | Forbidden.

<aside class="warning">
You cannot delete admin.
</aside>

## Get Accounts from a Specific User

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "localName": "11 localName",
        "englishName": "22 englishName",
        "address": "33 address",
        "email": "44 email",
        "phone": "55 phone",
        "fax": "66 fax",
        "vatNumber": "77 vatNumber",
        "discount": "88 discount",
        "image": "99 image",
        "userId": "9",
        "companyId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "localName": "1 localName",
        "englishName": "2 englishName",
        "address": "3 address",
        "email": "4 email",
        "phone": "5 phone",
        "fax": "6 fax",
        "vatNumber": "7 vatNumber",
        "discount": "8 discount",
        "image": "9 image",
        "userId": "9",
        "companyId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves accounts from a specific user.
### HTTP Request
<span class="method-get">GET</span> `/v1/user/:userId/accounts`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve acounts which <code>companyId</code> same as admin's.
User  | Forbidden.

## Get Contacts from a Specific User

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "firstName": "11 firstName",
        "middleName": "22 middleName",
        "lastName": "33 lastName",
        "email": "44 email",
        "phone": "55 phone",
        "mobile": "66 mobile",
        "fax": "77 fax",
        "image": "88 image",
        "title": "99 title",
        "accountId": "3",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "firstName": "1 firstName",
        "middleName": "2 middleName",
        "lastName": "3 lastName",
        "email": "4 email",
        "phone": "5 phone",
        "mobile": "6 mobile",
        "fax": "7 fax",
        "image": "8 image",
        "title": "9 title",
        "accountId": "3",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves all contacts from a specific user.
### HTTP Request
<span class="method-get">GET</span> `/v1/users/:userId/contacts`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve contacts which <code>companyId</code> same as admin's.
User  | Forbidden.

## Get Projects from a Specific User

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "localName": "11 localName",
        "englishName": "22 englishName",
        "winRate": "33 winRate",
        "status": "44 status",
        "description": "55 description",
        "loseReason": "66 loseReason",
        "established": "77 established",
        "closed": "88 closed",
        "forecast": "99 forecast",
        "contactId": "2",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "localName": "1 localName",
        "englishName": "2 englishName",
        "winRate": "3 winRate",
        "status": "4 status",
        "description": "5 description",
        "loseReason": "6 loseReason",
        "established": "7 established",
        "closed": "8 closed",
        "forecast": "9 forecast",
        "contactId": "2",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```
This endpoint retrieves projects from a specific user.
### HTTP Request
<span class="method-get">GET</span> `/v1/users/:userId/projects`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve projects which <code>companyId</code> same as admin's.
User  | Forbidden.

## Get Quotations from a Specific User

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "number": "11 number",
        "openDate": "22 openDate",
        "expiredDate": "33 expiredDate",
        "vatExcluded": "44 vatExcluded",
        "taxPercent": "55 taxPercent",
        "shipmentFee": "66 shipmentFee",
        "currency": "77 currency",
        "totalPrice": "88 totalPrice",
        "description": "99 description",
        "totalMargin": "1010 totalMargin",
        "projectId": "6",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "number": "1 number",
        "openDate": "2 openDate",
        "expiredDate": "3 expiredDate",
        "vatExcluded": "4 vatExcluded",
        "taxPercent": "5 taxPercent",
        "shipmentFee": "6 shipmentFee",
        "currency": "7 currency",
        "totalPrice": "8 totalPrice",
        "description": "9 description",
        "totalMargin": "10 totalMargin",
        "projectId": "6",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves quotations from a specific user.
### HTTP Request
<span class="method-get">GET</span> `/v1/users/:userId/quotations`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve quotations which <code>companyId</code> same as admin's.
User  | Forbidden.

## Get Members of Specific Users

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "firstName": "Kuan",
        "middleName": "",
        "lastName": "Chang",
        "password": "12345",
        "email": "kuanc@heysasha.com",
        "phone": "028765432",
        "mobile": "+886952318999",
        "fax": "",
        "image": "K",
        "title": "CTO",
        "role": "user",
        "updatedAt": "1559927161",
        "createdAt": "1559927161",
        "hierarchyLevel": 2,
        "parentId": "3",
        "companyId": "2"
      },{
        "id": "2",
        "firstName": "Frenk",
        "middleName": "",
        "lastName": "Wu",
        "password": "12345",
        "email": "frankw@heysasha.com",
        "phone": "023456789",
        "mobile": "+886919326222",
        "fax": "023456788",
        "image": "F",
        "title": "CMO",
        "role": "user",
        "updatedAt": "1559927161",
        "createdAt": "1559927161",
        "hierarchyLevel": 2,
        "parentId": "3",
        "companyId": "2"
      }
    ]
  }
}
```

This endpoint retrieves members from a specific user.
### HTTP Request
<span class="method-get">GET</span> `/v1/users/:userId/members`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve quotations which <code>companyId</code> same as admin's.
User  | Forbidden.

# Accounts

## Get All Accounts

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "localName": "11 localName",
        "englishName": "22 englishName",
        "address": "33 address",
        "email": "44 email",
        "phone": "55 phone",
        "fax": "66 fax",
        "vatNumber": "77 vatNumber",
        "discount": "88 discount",
        "image": "99 image",
        "userId": "9",
        "companyId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "localName": "1 localName",
        "englishName": "2 englishName",
        "address": "3 address",
        "email": "4 email",
        "phone": "5 phone",
        "fax": "6 fax",
        "vatNumber": "7 vatNumber",
        "discount": "8 discount",
        "image": "9 image",
        "userId": "9",
        "companyId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves all accounts.
### HTTP Request
<span class="method-get">GET</span> `/v1/accounts`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can retrieve acounts which <code>companyId</code> same as admin's.
User  | Retrieves acounts which <code>userId</code> same as user's and the descendants of user.

## Create an Account

> Example Request Body

```json
{
  "data": {
    "localName": "1 localName",
    "englishName": "2 englishName",
    "address": "3 address",
    "email": "4 email",
    "phone": "5 phone",
    "fax": "6 fax",
    "vatNumber": "7 vatNumber",
    "discount": "8 discount",
    "image": "9 image",
    "userId": "9"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "localName": "1 localName",
    "englishName": "2 englishName",
    "address": "3 address",
    "email": "4 email",
    "phone": "5 phone",
    "fax": "6 fax",
    "vatNumber": "7 vatNumber",
    "discount": "8 discount",
    "image": "9 image",
    "userId": "9",
    "companyId": "2",
    "createdAt": "1559927161",
    "updatedAt": "1559927161"
  }
}
```

This endpoint creates an account.
### HTTP Request
<span class="method-post">POST</span> `/v1/accounts`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
localName | TRUE |
englishName | TRUE |
address | TRUE |
email | TRUE |
phone | TRUE |
fax | TRUE |
vatNumber | TRUE |
discount | TRUE |
image | TRUE |
userId | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can assign <code>userId</code> to a specific user.
User  | Full permission, but cannot assign <code>userId</code> to a specific users.

<aside class="notice">If you are not admin, but trying to store <code>userId</code> inside request body, the server will ignore it.</aside>

## Get a Specific Account

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "localName": "1 localName",
    "englishName": "2 englishName",
    "address": "3 address",
    "email": "4 email",
    "phone": "5 phone",
    "fax": "6 fax",
    "vatNumber": "7 vatNumber",
    "discount": "8 discount",
    "image": "9 image",
    "userId": "9",
    "companyId": "2",
    "createdAt": "1559927161",
    "updatedAt": "1559927161"
  }
}
```

This endpoint retrieves a specific account.
### HTTP Request
<span class="method-get">GET</span> `/v1/accounts/:accountId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve account which <code>companyId</code> same as admin's.
User  | Retrieves acount which <code>userId</code> same as user's and the descendants of user.

## Update a Specific Account

> Example Request Body

```json
{
  "data": {
    "localName": "廣達",
    "englishName": "Quanta"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "localName": "廣達",
    "englishName": "Quanta",
    "address": "3 address",
    "email": "4 email",
    "phone": "5 phone",
    "fax": "6 fax",
    "vatNumber": "7 vatNumber",
    "discount": "8 discount",
    "image": "9 image",
    "userId": "9",
    "companyId": "2",
    "createdAt": "1559927161",
    "updatedAt": "1559927161"
  }
}
```

This endpoint updates a specific account.
### HTTP Request
<span class="method-patch">PATCH</span> `/v1/accounts/:accountId`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
localName | TRUE |
englishName | TRUE |
address | TRUE |
email | TRUE |
phone | TRUE |
fax | TRUE |
vatNumber | TRUE |
discount | TRUE |
image | TRUE |
userId | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full Permission, can update an account which <code>companyId</code> same as admin's.
User  | Can only update account which <code>userId</code> same as user's, and cannot change <code>userId</code>.

<aside class="notice">If you are not admin, but trying to store <code>userId</code> inside request body, the server will ignore it.</aside>

## Delete a Specific Account

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "ok"
  }
}
```

This endpoint deletes a specific account.
### HTTP Request
<span class="method-delete">DELETE</span>`/v1/accounts/:accountId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Can delete acount which <code>companyId</code> same as admin's.
User  | Forbidden.

## Get Contacts from a Specific Account

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "firstName": "11 firstName",
        "middleName": "22 middleName",
        "lastName": "33 lastName",
        "email": "44 email",
        "phone": "55 phone",
        "mobile": "66 mobile",
        "fax": "77 fax",
        "image": "88 image",
        "title": "99 title",
        "accountId": "1",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "firstName": "1 firstName",
        "middleName": "2 middleName",
        "lastName": "3 lastName",
        "email": "4 email",
        "phone": "5 phone",
        "mobile": "6 mobile",
        "fax": "7 fax",
        "image": "8 image",
        "title": "9 title",
        "accountId": "1",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves contacts from a specific account.
### HTTP Request
<span class="method-get">GET</span>`/v1/accounts/:accountId/contacts`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve contacts which <code>companyId</code> same as admin's.
User  | Retrieves contacts which <code>userId</code> same as user's and descendants of the user.

## Get Projects from a Specific Account

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "localName": "11 localName",
        "englishName": "22 englishName",
        "winRate": "33 winRate",
        "status": "44 status",
        "description": "55 description",
        "loseReason": "66 loseReason",
        "established": "77 established",
        "closed": "88 closed",
        "forecast": "99 forecast",
        "contactId": "2",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "localName": "1 localName",
        "englishName": "2 englishName",
        "winRate": "3 winRate",
        "status": "4 status",
        "description": "5 description",
        "loseReason": "6 loseReason",
        "established": "7 established",
        "closed": "8 closed",
        "contactId": "2",
        "userId": "2",
        "forecast": "9 forecast",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves projects from a specific account.
### HTTP Request
<span class="method-get">GET</span>`/v1/accounts/:accountId/projects`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve projects which <code>companyId</code> same as admin's.
User  | Retrieves projects which <code>userId</code> same as user's and the descendants of user.

## Get Quotations from a Specific Account

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "number": "11 number",
        "openDate": "22 openDate",
        "expiredDate": "33 expiredDate",
        "vatExcluded": "44 vatExcluded",
        "taxPercent": "55 taxPercent",
        "shipmentFee": "66 shipmentFee",
        "currency": "77 currency",
        "totalPrice": "88 totalPrice",
        "description": "99 description",
        "totalMargin": "1010 totalMargin",
        "projectId": "6",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "number": "1 number",
        "openDate": "2 openDate",
        "expiredDate": "3 expiredDate",
        "vatExcluded": "4 vatExcluded",
        "taxPercent": "5 taxPercent",
        "shipmentFee": "6 shipmentFee",
        "currency": "7 currency",
        "totalPrice": "8 totalPrice",
        "description": "9 description",
        "totalMargin": "10 totalMargin",
        "projectId": "6",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves quotations from a specific account.
### HTTP Request
<span class="method-get">GET</span>`/v1/accounts/:accountId/quotations`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve quotations which <code>companyId</code> same as admin's.
User  | Retrieves quotations which <code>userId</code> same as user's and the descendants of user.

# Contacts

## Get All Contacts

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "firstName": "11 firstName",
        "middleName": "22 middleName",
        "lastName": "33 lastName",
        "email": "44 email",
        "phone": "55 phone",
        "mobile": "66 mobile",
        "fax": "77 fax",
        "image": "88 image",
        "title": "99 title",
        "accountId": "3",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "firstName": "1 firstName",
        "middleName": "2 middleName",
        "lastName": "3 lastName",
        "email": "4 email",
        "phone": "5 phone",
        "mobile": "6 mobile",
        "fax": "7 fax",
        "image": "8 image",
        "title": "9 title",
        "accountId": "3",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves all contacts.
### HTTP Request
<span class="method-get">GET</span> `/v1/contacts`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve contacts which <code>companyId</code> same as admin's.
User  | Retrieves contacts which <code>userId</code> same as user's and descendants of the user.

## Create a Contact

> Example Request Body

```json
{
  "data": {
    "firstName": "1 firstName",
    "middleName": "2 middleName",
    "lastName": "3 lastName",
    "email": "4 email",
    "phone": "5 phone",
    "mobile": "6 mobile",
    "fax": "7 fax",
    "image": "8 image",
    "title": "9 title",
    "accountId": "3"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 201,
    "message": "Created"
  },
  "data": {
    "id": "1",
    "firstName": "1 firstName",
    "middleName": "2 middleName",
    "lastName": "3 lastName",
    "email": "4 email",
    "phone": "5 phone",
    "mobile": "6 mobile",
    "fax": "7 fax",
    "image": "8 image",
    "title": "9 title",
    "accountId": "3",
    "userId": "2",
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```

This endpoint creates a contacts.
### HTTP Request
<span class="method-post">POST</span> `/v1/contacts`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
firstName | TRUE |
middleName | TRUE |
lastName | TRUE |
email | TRUE |
phone | TRUE |
mobile | TRUE |
fax | TRUE |
image | TRUE |
title | TRUE |
accountId | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can create contact with admin's <code>companyId</code>.
User  | Creates contact for an account which <code>accountId</code> exist in user's and descendants of the user.

<aside class="notice">If you are not admin, but trying to store <code>userId</code> inside request body, the server will ignore it.</aside>

## Get a Specific Contact

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "firstName": "1 firstName",
    "middleName": "2 middleName",
    "lastName": "3 lastName",
    "email": "4 email",
    "phone": "5 phone",
    "mobile": "6 mobile",
    "fax": "7 fax",
    "image": "8 image",
    "title": "9 title",
    "accountId": "3",
    "userId": "2",
    "createdAt": "1559927161",
    "updatedAt": "1559927161"
  }
}
```

This endpoint retrieves a specific contacts.
### HTTP Request
<span class="method-get">GET</span> `/v1/contacts/:contactId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve contact which <code>companyId</code> same as admin's.
User  | Retrieves contact which <code>userId</code> same as user's and descendants of the user.

## Update a Specific Contact

> Example Request Body

```json
{
  "data": {
    "firstName": "Barry Lam"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "firstName": "Barry Lam",
    "middleName": "22 middleName",
    "lastName": "33 lastName",
    "email": "44 email",
    "phone": "55 phone",
    "mobile": "66 mobile",
    "fax": "77 fax",
    "image": "88 image",
    "title": "99 title",
    "accountId": "3",
    "userId": "2",
    "createdAt": "1559927161",
    "updatedAt": "1559927161"
  }
}
```

This endpoint updates a specific contact.
### HTTP Request
<span class="method-patch">PATCH</span> `/v1/contacts/:contactId`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
firstName | TRUE |
middleName | TRUE |
lastName | TRUE |
email | TRUE |
phone | TRUE |
mobile | TRUE |
fax | TRUE |
image | TRUE |
title | TRUE |
accountId | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full Permission, can updates an account which <code>companyId</code> same as admin's.
User  | Can only update account which <code>userId</code> same as user's, and cannot change <code>userId</code>.

<aside class="notice">If you are not admin, but trying to store <code>userId</code> inside request body, the server will ignore it.</aside>

## Delete a Specific Contact

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "ok"
  }
}
```

This endpoint deletes a specific contact.
### HTTP Request
<span class="method-delete">DELETE</span>`/v1/contacts/:contactId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Can delete contact which <code>companyId</code> same as admin's.
User  | Forbidden.

# Projects

## Get All Projects

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "localName": "11 localName",
        "englishName": "22 englishName",
        "winRate": "33 winRate",
        "status": "44 status",
        "description": "55 description",
        "loseReason": "66 loseReason",
        "established": "77 established",
        "closed": "88 closed",
        "forecast": "99 forecast",
        "contactId": "2",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "localName": "1 localName",
        "englishName": "2 englishName",
        "winRate": "3 winRate",
        "status": "4 status",
        "description": "5 description",
        "loseReason": "6 loseReason",
        "established": "7 established",
        "closed": "8 closed",
        "forecast": "9 forecast",
        "contactId": "2",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

This endpoint retrieves all projects.
### HTTP Request
<span class="method-get">GET</span> `/v1/projects`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieves projects which <code>companyId</code> same as admin's.
User  | Retrieve projects which <code>userId</code> same as user's and descendants of the user.

## Create a Project

> Example Request Body

```json
{
  "data": {
    "localName": "1 localName",
    "englishName": "2 englishName",
    "winRate": "3 winRate",
    "status": "4 status",
    "description": "5 description",
    "loseReason": "6 loseReason",
    "established": "7 established",
    "closed": "8 closed",
    "forecast": "9 forecast",
    "contactId": "2"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 201,
    "message": "Created"
  },
  "data": {
    "id": "1",
    "localName": "1 localName",
    "englishName": "2 englishName",
    "winRate": "3 winRate",
    "status": "4 status",
    "description": "5 description",
    "loseReason": "6 loseReason",
    "established": "7 established",
    "closed": "8 closed",
    "forecast": "9 forecast",
    "contactId": "2",
    "userId": "2",
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```

This endpoint creates a projects.
### HTTP Request
<span class="method-post">POST</span> `/v1/projects`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
localName | TRUE |
englishName | TRUE |
winRate | TRUE |
status | TRUE |
description | TRUE |
loseReason | TRUE |
established | TRUE |
closed | TRUE |
forecast | TRUE |
contactId | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can create project which with admin's <code>companyId</code>.
User  | Create project with his/her <code>userId</code>.

<aside class="notice">If you are not admin, but trying to store <code>userId</code> inside request body, the server will ignore it.</aside>

## Get a Specific Project

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "localName": "1 localName",
    "englishName": "2 englishName",
    "winRate": "3 winRate",
    "status": "4 status",
    "description": "5 description",
    "loseReason": "6 loseReason",
    "established": "7 established",
    "closed": "8 closed",
    "forecast": "9 forecast",
    "contactId": "2",
    "userId": "2",
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```

This endpoint retrieves a specific project.
### HTTP Request
<span class="method-get">GET</span>`/v1/projects/:projectId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve project which <code>companyId</code> same as admin's.
User  | Retrieve project which <code>userId</code> same as user's and descendants of the user.

## Update a Specific Project

> Example Request Body

```json
{
  "data": {
    "localName": "1Billion"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "localName": "1Billion",
    "englishName": "2 englishName",
    "winRate": "3 winRate",
    "status": "4 status",
    "description": "5 description",
    "loseReason": "6 loseReason",
    "established": "7 established",
    "closed": "8 closed",
    "forecast": "9 forecast",
    "contactId": "2",
    "userId": "2",
    "updatedAt": "1559927053",
    "createdAt": "1559927053"
  }
}
```

This endpoint updates a specific project.
### HTTP Request
<span class="method-patch">PATCH</span>`/v1/projects/:projectId`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
localName | TRUE |
englishName | TRUE |
winRate | TRUE |
status | TRUE |
description | TRUE |
loseReason | TRUE |
established | TRUE |
closed | TRUE |
forecast | TRUE |
contactId | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can update project which <code>companyId</code> same as admin's.
User  | Updates project which <code>userId</code> same as user's.

<aside class="notice">If you are not admin, but trying to store <code>userId</code> inside request body, the server will ignore it.</aside>

## Delete a Specific Project

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "ok"
  }
}
```

This endpoint deletes a specific project.
### HTTP Request
<span class="method-delete">DELETE</span>`/v1/projects/:projectId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can updates projects which <code>companyId</code> same as admin's.
User  | Forbidden.

## Get Quotations from a Specific Project

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "number": "11 number",
        "openDate": "22 openDate",
        "expiredDate": "33 expiredDate",
        "vatExcluded": "44 vatExcluded",
        "taxPercent": "55 taxPercent",
        "shipmentFee": "66 shipmentFee",
        "currency": "77 currency",
        "totalPrice": "88 totalPrice",
        "description": "99 description",
        "totalMargin": "1010 totalMargin",
        "projectId": "6",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "number": "1 number",
        "openDate": "2 openDate",
        "expiredDate": "3 expiredDate",
        "vatExcluded": "4 vatExcluded",
        "taxPercent": "5 taxPercent",
        "shipmentFee": "6 shipmentFee",
        "currency": "7 currency",
        "totalPrice": "8 totalPrice",
        "description": "9 description",
        "totalMargin": "10 totalMargin",
        "projectId": "6",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves quotations from a specific project.
### HTTP Request
<span class="method-get">GET</span>`/v1/projects/:projectId/quotations`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve quotations which <code>companyId</code> same as admin's.
User  | Retrieves quotations which <code>userId</code> same as user's and descendants of the user.

# Quotations

## Get All Quotations

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "number": "11 number",
        "openDate": "22 openDate",
        "expiredDate": "33 expiredDate",
        "vatExcluded": "44 vatExcluded",
        "taxPercent": "55 taxPercent",
        "shipmentFee": "66 shipmentFee",
        "currency": "77 currency",
        "totalPrice": "88 totalPrice",
        "description": "99 description",
        "totalMargin": "1010 totalMargin",
        "projectId": "6",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "number": "1 number",
        "openDate": "2 openDate",
        "expiredDate": "3 expiredDate",
        "vatExcluded": "4 vatExcluded",
        "taxPercent": "5 taxPercent",
        "shipmentFee": "6 shipmentFee",
        "currency": "7 currency",
        "totalPrice": "8 totalPrice",
        "description": "9 description",
        "totalMargin": "10 totalMargin",
        "projectId": "6",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves all quotations.
### HTTP Request
<span class="method-get">GET</span> `/v1/quotations`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve quotations which <code>companyId</code> same as admin's.
User  | Retrieves quotations which <code>userId</code> same as user's and descendants of the user.

## Create a Quotation

> Example Request Body

```json
{
    "data": {
        "number": "1 number",
        "openDate": "2 openDate",
        "expiredDate": "3 expiredDate",
        "vatExcluded": "4 vatExcluded",
        "taxPercent": "5 taxPercent",
        "shipmentFee": "6 shipmentFee",
        "currency": "7 currency",
        "totalPrice": "8 totalPrice",
        "description": "9 description",
        "totalMargin": "10 totalMargin",
        "projectId": 4,
        "productList": [
            {
                "id": 3,
                "quantity": "2",
                "previousPrice": "200",
                "previousPriceMargin": "20%",
                "sellPrice": "300",
                "sellPriceMargin": "120%",
                "minPrice": "150",
                "minPriceMargin": "10%"
            },
            {
                "id": 4,
                "quantity": "2",
                "previousPrice": "100",
                "previousPriceMargin": "20%",
                "sellPrice": "200",
                "sellPriceMargin": "120%",
                "minPrice": "150",
                "minPriceMargin": "10%"
            }
        ]
    }
}
```

> Example Response Body

```json
{
    "status": {
        "status": 200,
        "message": "OK"
    },
    "data": {
        "id": 34,
        "number": "1 number",
        "openDate": "2 openDate",
        "expiredDate": "3 expiredDate",
        "vatExcluded": "4 vatExcluded",
        "taxPercent": "5 taxPercent",
        "shipmentFee": "6 shipmentFee",
        "currency": "7 currency",
        "totalPrice": "8 totalPrice",
        "description": "9 description",
        "totalMargin": "10 totalMargin",
        "createdAt": "1560241424",
        "updatedAt": "1560241424",
        "companyId": 2,
        "userId": 4,
        "projectId": 4,
        "productList": [
            {
                "id": 3,
                "model": "3",
                "description": "2 description",
                "cost": "3 cost",
                "standardPrice": "4 standardPrice",
                "margin": "5 margin",
                "image": "6 image",
                "standard": true,
                "createdAt": "1560231177",
                "updatedAt": "1560231177",
                "companyId": 2,
                "userId": 2,
                "quotationProduct": {
                    "id": 35,
                    "userDefinedFieldName": null,
                    "quantity": "2",
                    "previousPrice": "200",
                    "previousPriceMargin": "20%",
                    "sellPrice": "300",
                    "sellPriceMargin": "120%",
                    "minPrice": "150",
                    "minPriceMargin": "10%",
                    "createdAt": "1560241424",
                    "updatedAt": "1560241424",
                    "quotationId": 34,
                    "productId": 3
                }
            },
            {
                "id": 4,
                "model": "4",
                "description": "2 description",
                "cost": "3 cost",
                "standardPrice": "4 standardPrice",
                "margin": "5 margin",
                "image": "6 image",
                "standard": true,
                "createdAt": "1560231177",
                "updatedAt": "1560231177",
                "companyId": 2,
                "userId": 2,
                "quotationProduct": {
                    "id": 36,
                    "userDefinedFieldName": null,
                    "quantity": "3",
                    "previousPrice": "100",
                    "previousPriceMargin": "20%",
                    "sellPrice": "200",
                    "sellPriceMargin": "120%",
                    "minPrice": "150",
                    "minPriceMargin": "10%",
                    "createdAt": "1560241424",
                    "updatedAt": "1560241424",
                    "quotationId": 34,
                    "productId": 4
                }
            }
        ]
    }
}
```

This endpoint creates a quotation.
### HTTP Request
<span class="method-post">POST</span> `/v1/quotations`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
number | TRUE |
openDate | TRUE |
expiredDate | TRUE |
vatExcluded | TRUE |
taxPercent | TRUE |
shipmentFee | TRUE |
currency | TRUE |
totalPrice | TRUE |
description | TRUE |
totalMargin | TRUE |
projectId | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can create quotation which <code>companyId</code> same as admin's.
User  | Creates quotation which <code>userId</code> same as user's and descendants of the user.

<aside class="notice">If you are not admin, but trying to store <code>userId</code> inside request body, the server will ignore it.</aside>

## Get a Specific Quotation

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "number": "1 number",
    "openDate": "2 openDate",
    "expiredDate": "3 expiredDate",
    "vatExcluded": "4 vatExcluded",
    "taxPercent": "5 taxPercent",
    "shipmentFee": "6 shipmentFee",
    "currency": "7 currency",
    "totalPrice": "8 totalPrice",
    "description": "9 description",
    "totalMargin": "10 totalMargin",
    "projectId": "6",
    "userId": "2",
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```

This endpoint retrieves a specific quotation.
### HTTP Request
<span class="method-get">GET</span>`/v1/quotations/:quotationId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve quotation which <code>companyId</code> same as admin's.
User  | Retrieves quotation which <code>userId</code> same as user's and descendants of the user.

## Update a Specific Quotation

> Example Request Body

```json
{
  "data": {
    "number": "12345678"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "number": "12345678",
    "openDate": "2 openDate",
    "expiredDate": "3 expiredDate",
    "vatExcluded": "4 vatExcluded",
    "taxPercent": "5 taxPercent",
    "shipmentFee": "6 shipmentFee",
    "currency": "7 currency",
    "totalPrice": "8 totalPrice",
    "description": "9 description",
    "totalMargin": "10 totalMargin",
    "projectId": "6",
    "userId": "2",
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```
This endpoint updates a specific quotation.
### HTTP Request
<span class="method-patch">PATCH</span> `/v1/quotations/:quotationId`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
number | TRUE |
openDate | TRUE |
expiredDate | TRUE |
vatExcluded | TRUE |
taxPercent | TRUE |
shipmentFee | TRUE |
currency | TRUE |
totalPrice | TRUE |
description | TRUE |
totalMargin | TRUE |
projectId | TRUE |

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Frobidden.
User  | Forbidden.

<aside class="warning">Once the quotaion has been created, no one can modify it.</aside>

## Delete a Specific Quotation

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "ok"
  }
}
```

This endpoint deletes a specific quotation.
### HTTP Request
<span class="method-delete">DELETE</span>`/v1/quotations/:quotationId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can delete quotations which <code>companyId</code> same as admin's.
User  | Forbidden

## Get Products from a Specific Quotation

> Example Response Body Field TBD TBD

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "model": "11 model",
        "description": "22 description",
        "cost": "33 cost",
        "standardPrice": "44 standardPrice",
        "margin": "55 margin",
        "image": "66 image",
        "standard": true,
        "companyId": "1",
        "userId": "5",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "model": "1 model",
        "description": "2 description",
        "cost": "3 cost",
        "standardPrice": "4 standardPrice",
        "margin": "5 margin",
        "image": "6 image",
        "standard": false,
        "companyId": "1",
        "userId": "5",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves products from a specific quotation.
### HTTP Request
<span class="method-get">GET</span>`/v1/quotations/:quotationId/products`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve products which <code>companyId</code> same as admin's.
User  | Retrieves products which <code>userId</code> same as user's and descendants of the user, or the products which <code>companyId</code> same as user's, <code>userId</code> same as user's.

# Products

## Get All Products

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "list": [
      {
        "id": "1",
        "model": "11 model",
        "description": "22 description",
        "cost": "33 cost",
        "standardPrice": "44 standardPrice",
        "margin": "55 margin",
        "image": "66 image",
        "standard": true,
        "companyId": "1",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      },
      {
        "id": "2",
        "model": "1 model",
        "description": "2 description",
        "cost": "3 cost",
        "standardPrice": "4 standardPrice",
        "margin": "5 margin",
        "image": "6 image",
        "standard": false,
        "companyId": "1",
        "userId": "2",
        "createdAt": "1559927161",
        "updatedAt": "1559927161"
      }
    ]
  }
}
```

This endpoint retrieves all products.
### HTTP Request
<span class="method-get">GET</span> `/v1/products`

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
TBD | false | TBD.
TBD | true | TBD.

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve products which <code>companyId</code> same as admin's.
User  | Retrieves products which <code>userId</code> same as user's and descendants of the user, or the products which <code>companyId</code> same as user's, <code>userId</code> same as user's.

## Create a Product

> Example Request Body

```json
{
  "data": {
    "model": "1 model",
    "description": "2 description",
    "cost": "3 cost",
    "standardPrice": "4 standardPrice",
    "margin": "5 margin",
    "image": "6 image",
    "userId": "5",
    "standard": true
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 201,
    "message": "Created"
  },
  "data": {
    "id": "1",
    "model": "1 model",
    "description": "2 description",
    "cost": "3 cost",
    "standardPrice": "4 standardPrice",
    "margin": "5 margin",
    "image": "6 image",
    "companyId": "1",
    "userId": "5",
    "standard": true,
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
model | TRUE |
description | TRUE |
cost | TRUE |
standardPrice | TRUE |
margin | TRUE |
image | TRUE |
userId | TRUE |
standard | TRUE | Boolean

This endpoint creates a product.
### HTTP Request
<span class="method-post">POST</span> `/v1/products/`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can create product with admin's <code>companyId</code>.
User  | Full permission, can create product with user's <code>companyId</code>.s.

<aside class="notice">If you create a product and set <code>standard</code> to <code>false</code> in request body, only you and your ancestors can view the product</aside>

## Get a Specific Product

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "model": "1 model",
    "description": "2 description",
    "cost": "3 cost",
    "standardPrice": "4 standardPrice",
    "margin": "5 margin",
    "image": "6 image",
    "standard": true,
    "companyId": "1",
    "userId": "5",
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```

This endpoint retrieves a specific product.
### HTTP Request
<span class="method-get">GET</span> `/v1/products/:productId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can rerieve product which <code>companyId</code> same as admin's.
User  | Retrieves product which <code>userId</code> same as user's and descendants of the user, or the products which <code>companyId</code> same as user's, <code>userId</code> same as user's.

## Update a Specific Product

> Example Request Body

```json
{
  "data": {
    "model": "iPhone XXXXXXXXSR"
  }
}
```

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "OK"
  },
  "data": {
    "id": "1",
    "model": "iPhone XXXXXXXXSR",
    "description": "2 description",
    "cost": "3 cost",
    "standardPrice": "4 standardPrice",
    "margin": "5 margin",
    "image": "6 image",
    "standard": true,
    "companyId": "1",
    "userId": "1",
    "updatedAt": "1559927161",
    "createdAt": "1559927161"
  }
}
```

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
model | TRUE |
description | TRUE |
cost | TRUE |
standardPrice | TRUE |
margin | TRUE |
image | TRUE |
userId | TRUE |
standard | TRUE | Boolean

This endpoint updates a specific product.
### HTTP Request
<span class="method-patch">PATCH</span>`/v1/products/:productId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can update product which <code>companyId</code> same as admin's.
User  | Updates product which <code>userId</code> same as user's and descendants of the user, or the products which <code>companyId</code> same as user's, <code>userId</code> same as user's.

## Delete a Specific Product

> Example Response Body

```json
{
  "status": {
    "status": 200,
    "message": "ok"
  }
}
```

This endpoint deletes a specific product.
### HTTP Request
<span class="method-delete">DELETE</span>`/v1/products/:productId`

### Access Permission
Role | Scope
---- | -----
Root | Forbidden.
Admin | Full permission, can delete product which <code>companyId</code> same as admin's.
User  | Forbidden.

<!-- # Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
 -->
