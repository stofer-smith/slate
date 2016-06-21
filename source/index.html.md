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
> ###API Endpoint --- https://api.capturehighered.net

> Creating a prospect with the HTTP Library...

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
    -H "Content-Type: application/json"
    -d '{"first_name":"Jack","last_name":"Smith","email":"j.smith@example.com"}'
```
```php
<?php
$client = new Capture\API\Client($jwt.placeholder);
$client->authorize();
$prospects = $client->createProspects(['first_name'=>"Jack",'last_name'=>"Smith",'email'=>"j.smith@example.com"]);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.create(['first_name'=>"Jack",'last_name'=>"Smith",'email'=>"j.smith@example.com"])
```
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
    -H "Content-Type: application/json"
    -d '{"address_1":"124 State St.",...}'
```
```php
<?php
$client = new Capture\API\Client($jwt.placeholder);
$client->authorize();
$prospects = $client->updateProspects(321, ['address_1'=>"124 State St.",...]);
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.update(321, ['address_1'=>"124 State St.",...])
```
>The Update and Create endpoints will both return JSON similar to the following,
with the exception that the url, result, and message will vary accordingly.

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
The Capture Prospect API is organized around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application (though you should never expose your secret API key in any public website's client-side code).

JSON is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.
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
    -H "Authorization: bearer jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client($jwt.placeholder);
$client->authorize();
$prospects = $client->getProspects();
```
```ruby
require 'capture-api'

api = Capture::APIClient.authorize!('jwt.placeholder')
api.prospects.get
```
> ####Make sure to replace `jwt.placeholder` with your Token.

Authenticate your account when using the API by including your secret API key in the request. You will receive your API key from us. Your client application will then submit it to https://api.capturehighered.com/authenticate and receive back a JSON Web Token(JWT). Your JWT carries many privileges, so be sure to keep them secret! Do not share your secret JWT or Token in publicly accessible areas such GitHub, client-side code, and so forth. For the most part only your API client will know your Token, because the client will get it from the authentication page and use it when calling protected end points.

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
$client = new Capture\API\Client($jwt.placeholder);
$client->authorize();
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
  "object": "list",
  "url": "/v1/prospects",
  "data": [
    {
      "id": 1
    },
    {
      "id": 2
    },
    {
        ...
    },
    {
      "id": N
    }
  ]
}
```
Default returns only the Prospect IDs for all prospects, or a subgroup of prospects.

The auto-pagination feature is specific to Capture's libraries and cannot be used directly with curl.

### Returns

This endpoint retrieves all prospects.

### HTTP Request

`GET http://api.capturehighered.net/v1/prospects`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_prospects | true | If set to false, the result will not include prospect information.
available | true | If set to false, the result will include prospects that have already been enrolled.

## Get a Specific Prospect
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
    -H "Authorization: bearer jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client($jwt.placeholder);
$client->authorize();
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
    "id": 321,
    "pool_id": null,
    "campaign_id": null,
    "campaign_list_id": 1,
    "source_id": 0,
    "client_prospect_id": "5",
    "prospect_status_id": 1,
    "prospect_disposition_id": 2,
    "first_name": "Joe",
    "last_name": "Jones",
    "mi": null,
    "email": "email@example.com",
    "home_phone": null,
    "cell_phone": null,
    "can_text": 0,
    "address_1": "123 Old Street",
    "address_2": null,
    "city": "Louisville",
    "state": 18,
    "zip": "40204",
    "addr_verified": 0,
    "lob_addr_id": null,
    "gender": null,
    "dob": null,
    "info_high_school_id": "000001",
    "ethnicity_id": null,
    "cluster_id": 0,
    "upload_id": 0,
    "update_id": 0,
    "url": "jjones",
    "passcode": "test",
    "parent_passcode": "test",
    "distance": null,
    "source_interest_id": "2",
    "capture_interest_id": 6,
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
    "matrix_cell_id": 0,
    "matrix_cell_code": "",
    "award": null,
    "award_type": "",
    "order_no": null,
    "country": null,
    "first_gen": null,
    "mobility": null,
    "mobility_perc": null,
    "inst_type": null,
    "inst_type_perc": null,
    "selectivity": null,
    "selectivity_perc": null,
    "inst_size": null,
    "inst_size_perc": null,
    "custom_fields": null,
    "parent_email": null,
    "parent_last_name": null,
    "parent_first_name": null,
    "created_at": "2016-06-10T15:42:28.000Z",
    "updated_at": "2016-06-10T15:42:28.000Z",
    "deleted_at": null,
    "nfa": 0,
    "retargeted": 0,
    "withdrawn": 0,
    "cancelled": 0,
    "wl_admit": 0,
    "status_updated": "0000-00-00",
    "from_form": 0,
    "client_prospect": 0,
    "tracking_identifier": null,
    "emails_sent": 0,
    "emails_opened": 0,
    "emails_clicked": 0
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

## Create a New Prospect

Creates a new prospect object.

```shell
In a single line, the curl command would be:
a) If sending form data:
curl "https://api.capturehighered.net/v1/prospects"
    -X POST
    -H "Content-Type: multipart/form-data;"
    -H "Authorization: Bearer jwt.placeholder"
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
$client = new Capture\API\Client($jwt.placeholder);
$client->authorize();
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
  "result": "new prospect created",
  "data": [
    {
      "id": 15,
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
      "address_1": null,
      "address_2": null,
      "city": null,
      "state": null,
      "zip": null,
      "addr_verified": 0,
      "lob_addr_id": null,
      "gender": null,
      "dob": null,
      "info_high_school_id": null,
      "ethnicity_id": null,
      "cluster_id": 0,
      "upload_id": 0,
      "update_id": 0,
      "url": "",
      "passcode": "",
      "parent_passcode": "",
      "distance": null,
      "source_interest_id": null,
      "capture_interest_id": null,
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
      "matrix_cell_id": 0,
      "matrix_cell_code": "",
      "award": null,
      "award_type": "",
      "order_no": null,
      "country": null,
      "first_gen": null,
      "mobility": null,
      "mobility_perc": null,
      "inst_type": null,
      "inst_type_perc": null,
      "selectivity": null,
      "selectivity_perc": null,
      "inst_size": null,
      "inst_size_perc": null,
      "custom_fields": null,
      "parent_email": null,
      "parent_last_name": null,
      "parent_first_name": null,
      "created_at": "0000-00-00 00:00:00",
      "updated_at": "0000-00-00 00:00:00",
      "deleted_at": null,
      "nfa": 0,
      "retargeted": 0,
      "withdrawn": 0,
      "cancelled": 0,
      "wl_admit": 0,
      "status_updated": "0000-00-00",
      "from_form": 0,
      "client_prospect": 0,
      "tracking_identifier": null,
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
    -H "Authorization: Bearer jwt.placeholder"
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
$client = new Capture\API\Client($jwt.placeholder);
$client->authorize();
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
  "result": "prospect updated",
  "message": "(Rows matched: 1  Changed: 1  Warnings: 0",
  "data": [
    {
      "id": 11,
      "pool_id": null,
      "campaign_id": null,
      "campaign_list_id": null,
      "source_id": 0,
      "client_prospect_id": null,
      "prospect_status_id": 1,
      "prospect_disposition_id": null,
      "first_name": "Tester6",
      "last_name": "Test",
      "mi": null,
      "email": "bad_email@example.com",
      "home_phone": null,
      "cell_phone": null,
      "can_text": 0,
      "address_1": "124 State St.",
      "address_2": null,
      "city": null,
      "state": null,
      "zip": null,
      "addr_verified": 0,
      "lob_addr_id": null,
      "gender": null,
      "dob": null,
      "info_high_school_id": null,
      "ethnicity_id": null,
      "cluster_id": 0,
      "upload_id": 0,
      "update_id": 0,
      "url": "",
      "passcode": "",
      "parent_passcode": "",
      "distance": null,
      "source_interest_id": null,
      "capture_interest_id": null,
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
      "matrix_cell_id": 0,
      "matrix_cell_code": "",
      "award": null,
      "award_type": "",
      "order_no": null,
      "country": null,
      "first_gen": null,
      "mobility": null,
      "mobility_perc": null,
      "inst_type": null,
      "inst_type_perc": null,
      "selectivity": null,
      "selectivity_perc": null,
      "inst_size": null,
      "inst_size_perc": null,
      "custom_fields": null,
      "parent_email": null,
      "parent_last_name": null,
      "parent_first_name": null,
      "created_at": "0000-00-00 00:00:00",
      "updated_at": "0000-00-00 00:00:00",
      "deleted_at": null,
      "nfa": 0,
      "retargeted": 0,
      "withdrawn": 0,
      "cancelled": 0,
      "wl_admit": 0,
      "status_updated": "0000-00-00",
      "from_form": 0,
      "client_prospect": 0,
      "tracking_identifier": null,
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
    -H "Authorization: bearer jwt.placeholder"
```
```php
<?php
$client = new Capture\API\Client($jwt.placeholder);
$client->authorize();
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
