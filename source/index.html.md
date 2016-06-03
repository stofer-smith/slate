---
title: Capture API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='http://capturehighered.com'>Capture LLC</a>
  - <a href='https://jwt.io/'>JSON Web Token</a>

includes:
  - errors

search: true
---

# Introduction

The Capture Prospect API is organized around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application (though you should never expose your secret API key in any public website's client-side code).

JSON is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.

# Authentication

Authenticate your account when using the API by including your secret API key in the request. You will receive your API key from us. Your client application will then submit it to https://api.capturehighered.com/authenticate and receive back a JSON Web Token(JWT). Your JWT carries many privileges, so be sure to keep them secret! Do not share your secret API keys or JWT in publicly accessible areas such GitHub, client-side code, and so forth. For the most part only your API client will know your JWT, because the client will get it from the authentication page and use it when calling protected end points.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

> To authorize, use this code:

```shell
# With the shell, you can just pass the correct header with each request
curl "https://api.capturehighered.com/v1/authenticate"
    -H "api_key: api_key.placeholder"
```

> Example call after receiving your JWT

```shell
curl "https://api.capturehighered.com/v1/prospects"
    -H "Authorization: bearer jwt.placeholder"
```
> Make sure to replace `api_key.placeholder` with your API key.

Capture API expects for the JWT to be included in all API requests to the server in a header that looks like the following:

`Authorization: bearer jwt.placeholder`

<aside class="notice">
You must replace <code>jwt.placeholder</code> with your personal API key. However, this will mainly be handled by the API client code.
</aside>

# Prospects

## Get All Prospects

Default returns only the Prospect IDs for all prospects, or a subgroup of prospects.

```shell
curl "https://api.capturehighered.com/v1/prospects"
    -H "Authorization: bearer jwt.placeholder"
```

> The above command returns JSON structured like this:

```json
{
  "object": "list",
  "url": "/v1/prospects",
  "data": [
    {
      "id": "321",
      "object": "prospect",
      "first_name": "First",
      "last_name": "Last",
      "description": null,
      "email": "prospect12347@gmail.com",
      "address_city": "Maumee",
      "address_line1": null,
      "address_line2": null,
      "address_state": "OH",
      "address_zip": "43537",
      "country": "US",
      "created_at": 1464974307,
      "updated_at": 1464974307,      
      "metadata": {
      },
      "info_high_school_id": 1234,
      "status": "INQ",
      "web_hist": {
        "object": "list",
        "data": [
          {
            "id": "123",
            "object": "visit",
            "site_id": "198",
            "ip_address": "72.240.147.177",
            "city": "Maumee",
            "state": "OH",
            "country": "US",
            "postal_code": "43537",
            "timezone": "America/New_York",
            "duration_in_seconds": "143",
            "metadata": {
            }
          }
        ],
        "has_more": false,
        "total_count": 1,
        "url": "/v1/prospects/visit/123"
      }
    },
    {...},
    {...}
  ]
}
```
The auto-pagination feature is specific to Capture's libraries and cannot be used directly with curl.

### Returns

This endpoint retrieves all prospects.

### HTTP Request

`GET http://api.capturehighered.com/v1/prospects`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_prospects | false | If set to true, the result will also include prospect information.
available | true | If set to false, the result will include prospects that have already been enrolled.

## Get a Specific Prospect
Retrieves the details of an existing prospect. You need only supply the unique prospect identifier that was returned upon prospect creation.

```shell
curl "https://api.capturehighered.com/v1/prospects/321"
    -H "Authorization: bearer jwt.placeholder"
```

> The above command returns JSON structured like this:

```json
{
  "object": "prospect",
  "url": "/v1/prospects/321",
  "id": "321",
  "first_name": "First",
  "last_name": "Last",
  "description": null,
  "email": "prospect12347@gmail.com",
  "address_city": "Maumee",
  "address_line1": null,
  "address_line2": null,
  "address_state": "OH",
  "address_zip": "43537",
  "country": "US",
  "created_at": 1464974307,
  "updated_at": 1464974307,      
  "metadata": {
  },
  "info_high_school_id": 1234,
  "status": "INQ",
  "web_hist": {
    "object": "list",
    "data": [
      {
        "id": "123",
        "object": "visit",
        "site_id": "198",
        "ip_address": "72.240.147.177",
        "city": "Maumee",
        "state": "OH",
        "country": "US",
        "postal_code": "43537",
        "timezone": "America/New_York",
        "duration_in_seconds": "143",
        "metadata": {
        }
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/prospects/visit/123"
  }
}
```

### returns

This endpoint returns a specific prospect, or an error if the prospect is not found.

### HTTP Request

`GET https://api.capturehighered.com/v1/prospects/[prospect_id]`

### URL Parameters

Parameter | Description
--------- | -----------
prospect_id | The ID of the prospect to retrieve

## Create a New Prospect

Creates a new prospect object.

> In a single line, the curl command would be: a) If sending form data:

```shell
curl "https://api.capturehighered.com/v1/prospects"
    -X POST
    -H "Content-Type: multipart/form-data;"
    -H "Authorization: Bearer jwt.placeholder"
    -F "key1=value1" -F "key2=value2"
```
>b) If sending raw data as json:

```shell
curl "https://api.capturehighered.com/v1/prospects"
    -X POST
    -H "Content-Type: application/json"
    -d '{"key1":"value1", "key2":"value2"}'
```

> The above command returns the new prospect with JSON structured like this:

```json
{
  "object": "prospect",
  "url": "/v1/prospects/321",
  "id": "321",
  "first_name": "First",
  "last_name": "Last",
  "description": null,
  "email": "prospect12347@gmail.com",
  "address_city": "Maumee",
  "address_line1": null,
  "address_line2": null,
  "address_state": "OH",
  "address_zip": "43537",
  "country": "US",
  "created_at": 1464974307,
  "updated_at": 1464974307,      
  "metadata": {
  },
  "info_high_school_id": 1234,
  "status": "INQ"
}
```

### Returns

Returns the prospect object if the update succeeded. Returns an error if update parameters are invalid.

### HTTP Request

`PUT https://api.capturehighered.com/v1/prospects/[prospect_id]?key1=value1&key2=value2`

### URL Parameters

Parameter | Description
--------- | -----------
prospect_id | The ID of the prospect to retrieve
key1 | value1
key2 | value2

## Update a Specific Prospect

Updates the specified prospect by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

> In a single line, the curl command would be: a) If sending form data:

```shell
curl "https://api.capturehighered.com/v1/prospects/[prospect_id]"
    -X PUT
    -H "Content-Type: multipart/form-data;"
    -H "Authorization: Bearer jwt.placeholder"
    -F "description='description change'"
    -F "address_line1='124 State St.'"
```
>b) If sending raw data as json:

```shell
curl "https://api.capturehighered.com/v1/prospects/[prospect_id]"
    -X PUT
    -H "Content-Type: application/json"
    -d '{"description":"description change", "address_line1":"124 State St."}'
```

> The above command returns the updated prospect with JSON structured like this:

```json
{
  "object": "prospect",
  "url": "/v1/prospects/321",
  "id": "321",
  "first_name": "First",
  "last_name": "Last",
  "description": "description change",
  "email": "prospect12347@gmail.com",
  "address_city": "Maumee",
  "address_line1": "124 State St.",
  "address_line2": null,
  "address_state": "OH",
  "address_zip": "43537",
  "country": "US",
  "created_at": 1464974307,
  "updated_at": 1464974307,      
  "metadata": {
  },
  "info_high_school_id": 1234,
  "status": "INQ"
}
```

### Returns

Returns the prospect object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid coupon or an invalid source).

### HTTP Request

`PUT https://api.capturehighered.com/v1/prospects/[prospect_id]?key1=value1&key2=value2`

### URL Parameters

Parameter | Description
--------- | -----------
prospect_id | The ID of the prospect to retrieve
key1 | value1
key2 | value2


## Delete a Specific Prospect

Permanently deletes a prospect.

```shell
curl "https://api.capturehighered.com/v1/prospects/31221"
    -X DELETE
    -H "Authorization: bearer jwt.placeholder"
```

> The above command returns JSON structured like this:

```json
{
  "deleted": true,
  "id": "31221"
}
```

### Returns

Returns an object with a deleted parameter on success. If the prospect ID does not exist, this call returns an error.
Unlike other objects, deleted prospects can still be retrieved through the API, in order to be able to track the history of prospects but preventing any further operations to be performed.

### HTTP Request

`GET https://api.capturehighered.com/v1/prospects/[prospect_id]`

### URL Parameters

Parameter | Description
--------- | -----------
prospect_id | The ID of the prospect to retrieve
