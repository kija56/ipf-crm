---
title: iPF UZO API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript: Javascript

toc_footers:
  - <a href='#'>Contact Developers for more information</a>
  

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the iPF UZO API
---

# Introduction

Welcome to the ***iPF UZO API!*** You can use this API to access UZO API endpoints, which can get information on various users,pipelines, deals, contacts, appointments, and more other information in our database.

We have language bindings in Shell and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: uzo token"
```

```javascript
const uzo = require('uzo');

let api = uzo.authorize('Bearer' 'uzo token');
```

> Make sure to replace `uzo token` with your valid authentication token.

iPF UZO API uses **Bearer authentication** (also called *token authentication*) to allow access to the API

iPF UZO API expects for the Authorization token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer <uzo token>`

<aside class="notice">
You must replace <code>uzo token</code> with your authorization token.
</aside>

# Users

## Get All Non Staff Users

```shell
curl "http://example.com/api/v1/users" \
  -H "Authorization: uzo token"
```

```javascript
const uzo = require('uzo');

let api = uzo.authorize(Bearer + ' ' +'uzo token');
let users = api.uzo.get();
```

> The above command returns JSON structured like this:

```json
  {
    "userMessage": "Staffs retrieved successfully...",
    "pagination": {
        "currentPage": 1,
        "perPage": 15,
        "totalPages": 1,
        "totalRows": 1
    },
    "data": [
        {
            "_id": "61efa6369f2280267ab96cee",
            "type": "user",
            "status": 1,
            "firstTimeLoginFlag": 0,
            "email": "example2@gmail.com",
            "password": "$2a$10$skfrmidNzkItqpSAZTNEi.UF2NK5XOyR/gt6oz5w4o/OQNudFJkHy",
            "firstName": "Kija",
            "lastName": "Mabula",
            "middleName": "Mayunga",
            "phoneNumber": "0758094352",
            "createdAt": "2022-01-25T07:26:46.772Z",
            "updatedAt": "2022-01-25T07:26:46.772Z",
            "__v": 0,
            "role": [],
            "semifullName": "Kija Mabula",
            "fullName": "Kija Mayunga Mabula"
        }
        {
            "_id": "61efa6369f2280267ab96cef",
            "type": "user",
            "status": 1,
            "firstTimeLoginFlag": 0,
            "email": "example@gmail.com",
            "password": "$2a$10$skfrmidNzkItqpSAZTNEi.UF2NK5XOyR/gt6oz5w4o/OQNudFJkHy",
            "firstName": "John",
            "lastName": "Gerald",
            "middleName": "Doe",
            "phoneNumber": "075809433",
            "createdAt": "2022-01-25T07:26:46.772Z",
            "updatedAt": "2022-01-25T07:26:46.772Z",
            "__v": 0,
            "role": [],
            "semifullName": "John Doe",
            "fullName": "John Gerald Doe"
        }
    ]
}
```

This endpoint retrieves all non staff users.

### HTTP Request

`GET http://example.com/api/v1/users`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a user with type `user` is a non staff user!
</aside>

## Get a Specific User

```shell
curl "http://example.com/api/v1/users/61efa6369f2280267ab96cef" \
  -H "Authorization: Bearer token"
```

```javascript
const uzo = require('uzo');

let api = uzo.authorize('token');
let max = api.users.get(2);
```

> The above command returns JSON structured like this:

```json
{
    "_id": "61efa6369f2280267ab96cee",
    "firstName": "Kija",
    "lastName": "Mabula",
    "middleName": "Mayunga",
    "email": "kijamabula2@gmail.com",
    "phoneNumber": "0758094352",
    "type": "user",
    "status": 1,
    "createdAt": "2022-01-25T07:26:46.772Z",
    "updatedAt": "2022-01-25T07:26:46.772Z"
}
```

This endpoint retrieves a specific user.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```shell
curl "http://example.com/api/v1/users/2" \
  -X DELETE \
  -H "Authorization: Bearer token"
```

```javascript
const uzo = require('uzo');

let api = uzo.authorize('Bearer token');
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

`DELETE http://example.com/api/v1/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to delete
