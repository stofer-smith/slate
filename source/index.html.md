---
title: Capture API Reference

language_tabs:
  - http
  - shell: cURL
  - php: PHP
  - ruby: Ruby

toc_footers:
  - <a href='http://capturehighered.com'>Capture LLC</a>
  - <a href='https://jwt.io/'>JSON Web Token</a>
  - <a href='https://en.wikipedia.org/wiki/Representational_state_transfer'>REST Defined</a>

includes:
  - errors

search: true
---

# Introduction
##Welcome!
> ###API Endpoint --- https://api.capturehighered.net

One of the missions of Capture is to make complex technologies more accessible; we are excited that you have arrived at this site to explore our Application Programming Interface (API) offering. Wether you are a current Capture partner looking to design your own custom integration or you are still evaluating our capabilities, we know you will find our API simple, powerful and flexible.

> Creating a prospect with the HTTP, a PHP Library, or your language of preference...

```http
POST /prospects HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
Content-Length: 30
first_name=Jack&last_name=Smith&email=j.smith@example.com&...
```
```shell
curl "https://api.capturehighered.net/v1/prospects"
    -X POST
    -H "Authorization: JWT jwt.placeholder"
    -d '{"first_name":"Jack","last_name":"Smith","email":"j.smith@example.com"}'
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->createProspects(['first_name'=>"Jack",'last_name'=>"Smith",'email'=>"j.smith@example.com"]);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.create(['first_name'=>"Jack",'last_name'=>"Smith",'email'=>"j.smith@example.com"])
```
###Prospect Focus

All the data in the Capture ecosystem is people related, so it should be no surprise that our API is mostly concerned with people and what they do.  Available methods include the ability locate, read, update, create and delete prospect information over the wire. It is very important to understand that all related data for a prospect record — a prospect’s web traffic, email statistics, dynamic content, custom fields, modeling scores and other detailed items — is accessible via this single robust system. All you need to do is locate a record using your CRM’s unique ID (as one example) and we will send back a comprehensive record for that prospect in one shot. Should you need to modify the record: simply make changes to the record you just retrieved and send it back.

>  Then sending an Update with raw data as JSON...

```http
POST /prospects HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
Content-Length: 30
id=321&address_1=124+State+St.&...
```
```shell
b) If sending raw data as json:
curl "https://api.capturehighered.net/v1/prospects/321"
    -X PUT
    -H "Authorization: JWT jwt.placeholder"
    -d '{"address_1":"124 State St.",...}'
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->updateProspects(321, ['address_1'=>"124 State St.",...]);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.update(321, ['address_1'=>"124 State St.",...])
```
>The Update and Create endpoints will both return JSON similar to the following,
with the exception that the url, result, and message will vary accordingly.

###Based on REST

The Capture Prospect API is organized around the very common Representational State Transfer (REST) design pattern. Our API has predictable, resource-oriented URLs, and uses Hypertext Transfer Protocol (HTTP) response codes to indicate API errors. We use built-in HTTP features like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application (though you should never expose your secret API key in any public website’s client-side code).

JavaScript Object Notation (JSON) is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.

###Bring Your Own Language

Since our API is based on REST, you have a tremendous amount of choice in the language and operating system upon which you will complete your integration. We presently provide examples for raw HTTP, cURL, PHP and Ruby — but we’ve yet to run into a programming language not capable of consuming a standards-based HTTP web service, and some software will support consuming our API out of the box.

```json
{
  "object": "prospect",
  "url": "/v1/prospects/:id",
  "result": "prospect updated",
  "message": "(Rows matched: 1  Changed: 1  Warnings: 0",
  "data": [
    {
      "id": 321,
      "pool_id": null,
      "campaign_id": null,
      "campaign_list_id": null,
      "source_id": 0,
      "client_prospect_id": null,
      "prospect_status_id": 1,
      "prospect_disposition_id": null,
      "first_name": "Jack",
      "last_name": "Smith",
      "mi": null,
      "email": "j.smith@example.com",
      "home_phone": null,
      "cell_phone": null,
      "can_text": 0,
      "address_1": "124 State St.",
      "...":"..."
    }
  ]
}
```
> ###Full Endpoint examples below

# Authentication
> ### To authorize, use this code:

```shell
# With the shell, you can just pass the correct header with each request
curl "https://api.capturehighered.com/v1/authenticate"
    -X POST
    -H "Cache-Control: no-cache"
    -d 'email=example@email.com&password=password'
```
```php
<?php
$jwt.placeholder = new Capture\API\Authenticate($username,$password);
```
```ruby
require 'capture-api'

jwt.placeholder = Capture::APIClient.authenticate!(username,password)
```
```http
POST /authenticate HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Content-Type: application/x-www-form-urlencoded
Host: api.capturehighered.net
Content-Length: 30
email=example@email.com&password=password
```
> Example call after receiving your JWT

```http
GET /prospects HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
```
```shell
curl "https://api.capturehighered.net/v1/prospects"
    -H "Authorization: JWT jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->getProspects();
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.get
```
> ####Make sure to replace `jwt.placeholder` with your Token.

Authenticate your account when using the API by including your secret JSON Web Token(JWT) in the request. You will receive your JWT from us. Your client application will initially submit your username/email and password to https://api.capturehighered.com/authenticate and receive back a JWT. Your JWT carries many privileges, so be sure to keep them secret! Do not share your secret JWT or Token in publicly accessible areas such GitHub, client-side code, and so forth. For the most part only your API client will know your Token, because the client will get it from the authentication page and use it when calling protected end points.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

Capture API expects for the JWT to be included in all API requests to the server in a header that looks like the following:

`Authorization: JWT jwt.placeholder`

<aside class="warning">
You must replace <code>jwt.placeholder</code> with your personal API key. However, this will mainly be handled by the API client code.
</aside>

# Prospects
## Get All Prospects
```http
GET /prospects HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
```
```shell
curl "https://api.capturehighered.net/v1/prospects"
    -H "Authorization: JWT jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->getProspects();
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.get
```
> The above command returns JSON structured like this:

```json
{
  "_metadata": {
    "cursor": 5,
    "per_page": 20,
    "page_count": 9,
    "total_count": 199,
    "Links": [
      {
        "self": "/v1/prospects?cursor=5&per_page=20"
      },
      {
        "first": "/v1/prospects?cursor=0&per_page=20"
      },
      {
        "previous": "/v1/prospects?cursor=4&per_page=20"
      },
      {
        "next": "/v1/prospects?cursor=6&per_page=20"
      },
      {
        "last": "/v1/prospects?cursor=9&per_page=20"
      }
    ]
  },
  "object": "list",
  "url": "/v1/prospects",
  "count": 20,
  "data": [
    {
      "id": 109
    },
    {
      "id": 110
    },
    {
      "id": 111
    },
    "...",
    {
      "id": 128
    }
  ]
}
```
Default returns only the Prospect IDs for all prospects, or a subgroup of prospects.

The auto-pagination feature is specific to Capture's libraries and cannot be used directly with curl.

### Returns

This endpoint retrieves all prospect ids, paginated with cursor, page count, and total counts included.

### HTTP Request

`GET http://api.capturehighered.net/v1/prospects`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_prospects | false | If set to true, the result will include prospect information.
available | true | If set to false, the result will include prospects that have already been enrolled.

## Get a Specific Prospect (By ID)
Retrieves the details of an existing prospect. You need only supply the unique prospect identifier that was returned upon prospect creation.

```http
GET /prospects HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
Content-Length: 30
id=321
```
```shell
curl "https://api.capturehighered.net/v1/prospects/321"
    -H "Authorization: JWT jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->getProspects(321);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.get(321)
```

> The above command returns JSON structured like this:

```json
{
  "object": "prospect",
  "url": "/v1/prospects/:id",
  "count": 1,
  "data": [
    {
        "id": 321,
        "campaign_id": null,
        "campaign_list_id": 1,
        "source_id": 0,
        "client_prospect_id": "5",
        "prospect_status_id": 1,
        "first_name": "Joe",
        "last_name": "Jones",
        "mi": null,
        "email": "email@example.com",
        "home_phone": null,
        "cell_phone": null,
        "address_1": "123 Old Street",
        "address_2": null,
        "city": "Louisville",
        "state": 18,
        "zip": "40204",
        "gender": null,
        "dob": null,
        "ethnicity_id": null,
        "major_1": null,
        "major_2": null,
        "major_3": null,
        "grad_year": null,
        "gpa": null,
        "sat_score": null,
        "act_score": null,
        "score_floor": null,
        "score_ceiling": null,
        "grade_floor": null,
        "grade_ceiling": null,
        "award": null,
        "country": null,
        "parent_email": null,
        "parent_last_name": null,
        "parent_first_name": null,
        "nfa": 0,
        "retargeted": 0,
        "withdrawn": 0,
        "cancelled": 0,
        "wl_admit": 0,
        "emails_sent": 0,
        "emails_opened": 0,
        "emails_clicked": 0
    }
  ]
}
```
### returns

This endpoint returns a specific prospect, or an error if the prospect is not found.

### HTTP Request

`GET https://api.capturehighered.net/v1/prospects/[prospect_id]`

### URL Parameters

Parameter | Description
--------- | -----------
prospect_id | The ID of the prospect to retrieve

## Get a Specific Prospect (By Client ID)
Retrieves the details of an existing prospect by Client ID. You need only supply the unique client prospect identifier from your CRM. This returns a similar json object as getting a specific prospect by id.

```http
GET /prospects/client HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
Content-Length: 30
id=5
```
```shell
curl "https://api.capturehighered.net/v1/prospects/client/5"
    -H "Authorization: JWT jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->getProspects(5, true);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.get(5, true)
```

> The above command returns JSON structured like this:

```json
{
  "object": "prospect",
  "url": "/v1/prospects/client/:client_prospect_id",
  "count": 1,
  "data": [
    {
        "id": 321,
        "campaign_id": null,
        "campaign_list_id": 1,
        "source_id": 0,
        "client_prospect_id": "5",
        "prospect_status_id": 1,
        "first_name": "Joe",
        "last_name": "Jones",
        "mi": null,
        "email": "email@example.com",
        "home_phone": null,
        "cell_phone": null,
        "address_1": "123 Old Street",
        "address_2": null,
        "city": "Louisville",
        "state": 18,
        "zip": "40204",
        "gender": null,
        "dob": null,
        "ethnicity_id": null,
        "major_1": null,
        "major_2": null,
        "major_3": null,
        "grad_year": null,
        "gpa": null,
        "sat_score": null,
        "act_score": null,
        "score_floor": null,
        "score_ceiling": null,
        "grade_floor": null,
        "grade_ceiling": null,
        "award": null,
        "country": null,
        "parent_email": null,
        "parent_last_name": null,
        "parent_first_name": null,
        "nfa": 0,
        "retargeted": 0,
        "withdrawn": 0,
        "cancelled": 0,
        "wl_admit": 0,
        "emails_sent": 0,
        "emails_opened": 0,
        "emails_clicked": 0
    }
  ]
}
```
### returns

This endpoint returns a specific prospect, or an error if the prospect is not found.

### HTTP Request

`GET https://api.capturehighered.net/v1/prospects/client/[client_prospect_id]`

### URL Parameters

Parameter | Description
--------- | -----------
client_prospect_id | The Client(CRM) ID of the prospect to retrieve (required)

## Get a Specific Prospect (By Name)
Retrieves the details of an existing prospect by First and Last Name. You need only supply the first and last name of a prospect. This returns a similar json object as getting a specific prospect by id.

Note: This endpoint may return a list of prospects with matching first and last names

```http
GET /prospects/[first_name]/[last_name] HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
Content-Length: 30
```
```shell
curl "https://api.capturehighered.net/v1/prospects/[first_name]/[last_name]"
    -H "Authorization: JWT jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->getProspectByName($first_name, $last_name);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.getByName(first_name, last_name)
```

> The above command returns JSON structured like this:

```json
{
  "object": "prospect",
  "url": "/v1/prospects/client/:client_prospect_id",
  "count": 1,
  "data": [
    {
        "id": 321,
        "campaign_id": null,
        "campaign_list_id": 1,
        "source_id": 0,
        "client_prospect_id": "5",
        "prospect_status_id": 1,
        "first_name": "Joe",
        "last_name": "Jones",
        "mi": null,
        "email": "email@example.com",
        "home_phone": null,
        "cell_phone": null,
        "address_1": "123 Old Street",
        "address_2": null,
        "city": "Louisville",
        "state": 18,
        "zip": "40204",
        "gender": null,
        "dob": null,
        "ethnicity_id": null,
        "major_1": null,
        "major_2": null,
        "major_3": null,
        "grad_year": null,
        "gpa": null,
        "sat_score": null,
        "act_score": null,
        "score_floor": null,
        "score_ceiling": null,
        "grade_floor": null,
        "grade_ceiling": null,
        "award": null,
        "country": null,
        "parent_email": null,
        "parent_last_name": null,
        "parent_first_name": null,
        "nfa": 0,
        "retargeted": 0,
        "withdrawn": 0,
        "cancelled": 0,
        "wl_admit": 0,
        "emails_sent": 0,
        "emails_opened": 0,
        "emails_clicked": 0
    }
  ]
}
```
### returns

This endpoint returns a specific prospect, or an error if the prospect is not found.

### HTTP Request

`GET https://api.capturehighered.net/v1/prospects/[first_name]/[last_name]`

### URL Parameters

Parameter | Description
--------- | -----------
first_name | The first name of the prospect to retrieve (required)
last_name | The last name of the prospect to retrieve (required)

## Create a New Prospect

Creates a new prospect object.

```shell
In a single line, the curl command would be:
a) If sending form data:
curl "https://api.capturehighered.net/v1/prospects"
    -X POST
    -H "Content-Type: multipart/form-data;"
    -H "Authorization: JWT jwt.placeholder"
    -F "first_name=Jack"
    -F "last_name=Smith"
    -F "email=j.smith@example.com"
```
```shell
b) If sending raw data as json:
curl "https://api.capturehighered.net/v1/prospects"
    -X POST
    -H "Content-Type: application/json"
    -d '{"first_name":"Jack","last_name":"Smith","email":"j.smith@example.com"}'
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->createProspects(['first_name'=>"Jack",'last_name'=>"Smith",'email'=>"j.smith@example.com"]);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.create(['first_name'=>"Jack",'last_name'=>"Smith",'email'=>"j.smith@example.com"])
```
```http
POST /prospects HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
Content-Length: 30
first_name=Jack&last_name=Smith&...
```
> The above command returns the new prospect with JSON structured like this:

```json
{
  "object": "prospect",
  "url": "/v1/prospects/:id",
  "count": 1,
  "data": [
    {
        "id": 15,
        "campaign_id": null,
        "campaign_list_id": 1,
        "source_id": 0,
        "client_prospect_id": "5",
        "prospect_status_id": 1,
        "first_name": "Jack",
        "last_name": "Smith",
        "mi": null,
        "email": "j.smith@example.com",
        "home_phone": null,
        "cell_phone": null,
        "address_1": null,
        "address_2": null,
        "city": null,
        "state": null,
        "zip": null,
        "gender": null,
        "dob": null,
        "ethnicity_id": null,
        "major_1": null,
        "major_2": null,
        "major_3": null,
        "grad_year": null,
        "gpa": null,
        "sat_score": null,
        "act_score": null,
        "score_floor": null,
        "score_ceiling": null,
        "grade_floor": null,
        "grade_ceiling": null,
        "award": null,
        "country": null,
        "parent_email": null,
        "parent_last_name": null,
        "parent_first_name": null,
        "nfa": 0,
        "retargeted": 0,
        "withdrawn": 0,
        "cancelled": 0,
        "wl_admit": 0,
        "emails_sent": 0,
        "emails_opened": 0,
        "emails_clicked": 0
    }
  ]
}
```

### Returns

Returns the prospect object if the update succeeded. Returns an error if update parameters are invalid.

### HTTP Request

`POST https://api.capturehighered.net/v1/prospects/?key1=value1&key2=value2`

### URL Parameters

Parameter | Description
--------- | -----------
first_name | Prospect First Name
last_name | Prospect Last Name
email | Prospect Email address
prospect_status_id | Default 1

## Update a Specific Prospect

Updates the specified prospect by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

```shell
In a single line, the curl command would be:
a) If sending form data:
curl "https://api.capturehighered.net/v1/prospects/[prospect_id]"
    -X PUT
    -H "Content-Type: multipart/form-data;"
    -H "Authorization: JWT jwt.placeholder"
    -F "address_1='124 State St.'"
    -F "..."
```
```shell
b) If sending raw data as json:
curl "https://api.capturehighered.net/v1/prospects/[prospect_id]"
    -X PUT
    -H "Content-Type: application/json"
    -d '{"address_1":"124 State St.",...}'
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->updateProspects($prospect_id, ['address_1'=>"124 State St.",...]);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.update(prospect_id, ['address_1'=>"124 State St.",...])
```
```http
POST /prospects HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
Content-Length: 30
id=[prospect_id]&address_1=124+State+St.&...
```

> The above command returns the updated prospect with JSON structured like this:

```json
{
  "object": "prospect",
  "url": "/v1/prospects/:id",
  "count": 1,
  "data": [
    {
        "id": 15,
        "campaign_id": null,
        "campaign_list_id": 1,
        "source_id": 0,
        "client_prospect_id": "5",
        "prospect_status_id": 1,
        "first_name": "Jack",
        "last_name": "Smith",
        "mi": null,
        "email": "j.smith@example.com",
        "home_phone": null,
        "cell_phone": null,
        "address_1": "124 State St.",
        "address_2": null,
        "city": null,
        "state": null,
        "zip": null,
        "gender": null,
        "dob": null,
        "ethnicity_id": null,
        "major_1": null,
        "major_2": null,
        "major_3": null,
        "grad_year": null,
        "gpa": null,
        "sat_score": null,
        "act_score": null,
        "score_floor": null,
        "score_ceiling": null,
        "grade_floor": null,
        "grade_ceiling": null,
        "award": null,
        "country": null,
        "parent_email": null,
        "parent_last_name": null,
        "parent_first_name": null,
        "nfa": 0,
        "retargeted": 0,
        "withdrawn": 0,
        "cancelled": 0,
        "wl_admit": 0,
        "emails_sent": 0,
        "emails_opened": 0,
        "emails_clicked": 0
    }
  ]
}
```

### Returns

Returns the prospect object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid coupon or an invalid source).

### HTTP Request

`PUT https://api.capturehighered.net/v1/prospects/[prospect_id]?key1=value1&key2=value2`

### URL Parameters

Parameter | Description
--------- | -----------
prospect_id | The ID of the prospect to update
key1 | value1
key2 | value2

## Delete a Specific Prospect

Permanently deletes a prospect.

```shell
curl "https://api.capturehighered.net/v1/prospects/31221"
    -X DELETE
    -H "Authorization: JWT jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$result = $client->deleteProspect(31221);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.destroy(31221)
```
> The above command returns JSON structured like this:

```json
{
  "object": "result",
  "url": "/v1/prospects/:id",
  "result": "prospect deleted",
  "id": "15",
  "data": {
    "fieldCount": 0,
    "affectedRows": 1,
    "insertId": 0,
    "serverStatus": 2,
    "warningCount": 0,
    "message": "",
    "protocol41": true,
    "changedRows": 0
  }
}
```

### Returns

Returns an object with a deleted parameter on success. If the prospect ID does not exist, this call returns an error.
Unlike other objects, deleted prospects can still be retrieved through the API, in order to be able to track the history of prospects but preventing any further operations to be performed.

### HTTP Request

`GET https://api.capturehighered.net/v1/prospects/[prospect_id]`

### URL Parameters

Parameter | Description
--------- | -----------
prospect_id | The ID of the prospect to retrieve


## Get All Prospects Scores
```http
GET /prospects/scores HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.capture-api.1+json
Host: api.capturehighered.net
Authorization: JWT "jwt.placeholder"
```
```shell
curl "https://api.capturehighered.net/v1/prospects/scores"
    -H "Authorization: JWT jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client();
$client->authorize($email,$password);
$prospects = $client->getProspectsScores();
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.getScores
```
> The above command returns JSON structured like this:

```json
{
  "_metadata": {
    "cursor": 1,
    "per_page": 100,
    "page_count": 41,
    "total_count": 4195,
    "Links": [
      {
        "self": "/v1/prospects/scores?cursor=1&per_page=100"
      },
      {
        "first": "/v1/prospects/scores?cursor=0&per_page=100"
      },
      {
        "previous": "/v1/prospects/scores?cursor=0&per_page=100"
      },
      {
        "next": "/v1/prospects/scores?cursor=2&per_page=100"
      },
      {
        "last": "/v1/prospects/scores?cursor=41&per_page=100"
      }
    ]
  },
  "object": "list",
  "url": "/v1/prospects/scores",
  "count": 100,
  "data": [
    {
      "id": 15,
      "campaign_id": null,
      "campaign_list_id": 1,
      "source_id": 0,
      "client_prospect_id": "5",
      "prospect_status_id": 1,
      "first_name": "Jack",
      "last_name": "Smith",
      "mi": null,
      "email": "j.smith@example.com",
      "cai": 16,
      "cai_pct_rank": 0,
      "cai_date": "2016-06-24T00:00:00.000Z",
      "match_date": null,
      "first_visit": null,
      "ces": 44,
      "ces_raw": 52,
      "opens_7": null,
      "clicks_7": null,
      "visits_7": null,
      "pages_7": null,
      "app_page_7": null,
      "visit_page_7": null,
      "duration_7": 261,
      "device_7": 1
    },
    {
      ...
    }
  ]
}    
```

The auto-pagination feature is specific to Capture's libraries and cannot be used directly with curl.

### Returns

This endpoint retrieves all prospects CAI, CES, and Envision Scores.

### HTTP Request

`GET http://api.capturehighered.net/v1/prospects/scores`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
crm_unique_id | Id of prospect in your crm | If set the result will return the score for a specific prospect.
