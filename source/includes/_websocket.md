
# Websocket

## Get All DurEXs

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.DurEXs.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.DurEXs.get()
```

```shell
curl "http://example.com/api/DurEXs"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let DurEXs = api.DurEXs.get();
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

This endpoint retrieves all DurEXs.

### HTTP Request

`GET http://example.com/api/DurEXs`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include DurEXs that have already been adopted.

<aside class="success">
Remember — a happy DurEX is an authenticated DurEX!
</aside>

## Get a Specific DurEX

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.DurEXs.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.DurEXs.get(2)
```

```shell
curl "http://example.com/api/DurEXs/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.DurEXs.get(2);
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

This endpoint retrieves a specific DurEX.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/DurEXs/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the DurEX to retrieve

## Delete a Specific DurEX

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.DurEXs.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.DurEXs.delete(2)
```

```shell
curl "http://example.com/api/DurEXs/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.DurEXs.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific DurEX.

### HTTP Request

`DELETE http://example.com/DurEXs/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the DurEX to delete

