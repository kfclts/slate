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
    "userId": "04885878-13ea-44df-bcf1-bde17c6ed59d",
    "companyId": "4491eb60-6569-4faf-9039-3653723d5ccf"
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

## Forget Password `Not Implement`
> Example Request Body

```json
{
  "email": "kfc@heysasha.com"
}
```

> Example Response Body

```json
{
    "userId": "04885878-13ea-44df-bcf1-bde17c6ed59d",
    "reset_email":"https://api.heysasha.com/QWEQ!@#1213fjslfkjqweQW"
}
```

### HTTP Request
<span class="method-post">POST</span> `/v1/auth/forget_password`

### Request Body Parameters
Parameter | Required | Validation
--------- | ----------- | -----------
email | TRUE | email format

### Access Permission
Role | Scope
---- | ----- 
Root | Full permission.
Admin | Full permission.
User  | Full permission.

