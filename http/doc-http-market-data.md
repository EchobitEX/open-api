# Market Data

## GET Spot Tickers - all

GET /uapi/exchange/tickers

<pre>
Market APIs do not require signature.
</pre>

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "t": 1733221981727,
      "s": "JENTUSDT",
      "sn": "JENTUSDT",
      "c": "0.0041788",
      "h": "0.0041788",
      "l": "0.0041788",
      "o": "0.0041788",
      "v": "0",
      "qv": "0",
      "m": "0",
      "f": false
    }
  ]
}
```

### Response

|Status Code|Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Response Schema

Status code **200**

|Name|Type|Required|Description|
|---|---|---|---|
|» msg|string|Yes|Response message, when code = 0, message = "success"; when code != 0, shows error reason|
|» code|string|Yes|Response status code, 0-success, non-0-failure|
|» data|[object]|Yes|payload|
|»» t|integer|Yes|time|
|»» s|string|Yes|symbol ID|
|»» sn|string|Yes|symbol name|
|»» c|string|Yes|close|
|»» h|string|Yes|high|
|»» l|string|Yes|low|
|»» o|string|Yes|open|
|»» v|string|Yes|volume|
|»» qv|string|Yes|quote volume|
|»» m|string|Yes|change|
|»» f|boolean|Yes|isVirtual|

## GET Tickers - all

GET /uapi/exchange/all/tickers

<pre>
Market APIs do not require signature.
</pre>

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "t": 1733221981727,
      "s": "JENTUSDT",
      "sn": "JENTUSDT",
      "c": "0.0041788",
      "h": "0.0041788",
      "l": "0.0041788",
      "o": "0.0041788",
      "v": "0",
      "qv": "0",
      "m": "0",
      "f": false
    }
  ]
}
```

### Response

|Status Code|Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Response Schema

Status code **200**

|Name|Type|Required|Description|
|---|---|---|---|
|» msg|string|Yes|Response message, when code = 0, message = "success"; when code != 0, shows error reason|
|» code|string|Yes|Response status code, 0-success, non-0-failure|
|» data|[object]|Yes|payload|
|»» t|integer|Yes|time|
|»» s|string|Yes|symbol ID|
|»» sn|string|Yes|symbol name|
|»» c|string|Yes|close|
|»» h|string|Yes|high|
|»» l|string|Yes|low|
|»» o|string|Yes|open|
|»» v|string|Yes|volume|
|»» qv|string|Yes|quote volume|
|»» m|string|Yes|change|
|»» f|boolean|Yes|isVirtual|

## GET Ticker - single symbol

GET /uapi/exchange/ticker

<pre>
Market APIs do not require signature.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|symbol|query|string| Yes |Multiple symbols separated by commas|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "t": 1733221982511,
      "s": "BTCUSDT",
      "sn": "BTCUSDT",
      "c": "93400.04",
      "h": "93400.04",
      "l": "93400.04",
      "o": "93400.04",
      "v": "0.01272",
      "qv": "1187.9077308",
      "m": "0",
      "f": false
    }
  ]
}
```

### Response

|Status Code|Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Response Schema

Status code **200**

|Name|Type|Required|Description|
|---|---|---|---|
|» msg|string|Yes|Response message, when code = 0, message = "success"; when code != 0, shows error reason|
|» code|string|Yes|Response status code, 0-success, non-0-failure|
|» data|[object]|Yes|payload|
|»» t|integer|Yes|time|
|»» s|string|Yes|symbol ID|
|»» sn|string|Yes|symbol name|
|»» c|string|Yes|close|
|»» h|string|Yes|high|
|»» l|string|Yes|low|
|»» o|string|Yes|open|
|»» v|string|Yes|volume|
|»» qv|string|Yes|quote volume|
|»» m|string|Yes|change|
|»» f|boolean|Yes|isVirtual|

## GET Recent Trades

GET /uapi/exchange/trades

<pre>
Market APIs do not require signature.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|symbol|query|string| Yes |Multiple symbols separated by commas|
|limit|query|string| Yes |limit|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "v": "1828424451168157697",
      "t": 1732701179821,
      "p": "93393.01",
      "q": "0.00066",
      "f": false,
      "m": false
    }
  ]
}
```

### Response

|Status Code|Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Response Schema

Status code **200**

|Name|Type|Required|Description|
|---|---|---|---|
|» msg|string|Yes|Response message, when code = 0, message = "success"; when code != 0, shows error reason|
|» code|string|Yes|Response status code, 0-success, non-0-failure|
|» data|[object]|Yes|payload|
|»» v|string|Yes|version|
|»» t|integer|Yes|time|
|»» p|string|Yes|price|
|»» q|string|Yes|quantity|
|»» f|boolean|Yes|isVirtual|
|»» m|boolean|Yes|isMaker|

## GET Order Book Depth

GET /uapi/exchange/depth

<pre>
Market APIs do not require signature.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|symbol|query|string| Yes |symbol ID|
|limit|query|string| Yes |limit|
|dumpScale|query|string| No |-1,1,2,3,4  -1 for integer, 1/2/3/4 for decimal places |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "s": "BTCUSDT",
      "t": 1733222252190,
      "v": "405753_1",
      "b": [["93412","0.001"],["93400","0.008614"],["90000","0.001386"],["69550","34.619535"]],
      "a": [["95000","0.056397"],["95000.1","0.044056"]],
      "o": 0
    }
  ]
}
```

### Response

|Status Code|Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Response Schema

Status code **200**

|Name|Type|Required|Description|
|---|---|---|---|
|» msg|string|Yes|Response message, when code = 0, message = "success"; when code != 0, shows error reason|
|» code|string|Yes|Response status code, 0-success, non-0-failure|
|» data|[object]|Yes|payload|
|»» s|string|Yes|symbol ID|
|»» t|integer|Yes|time|
|»» v|string|Yes|version|
|»» b|[array]|Yes|bids; [0]: price, [1]: quantity|
|»» a|[array]|Yes|asks; [0]: price, [1]: quantity|
|»» o|integer|Yes|order|

## GET Klines

GET /uapi/exchange/klines

<pre>
Market APIs do not require signature.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|symbol|query|string| Yes |symbol ID|
|limit|query|string| Yes |limit|
|interval|query|string| Yes |Intervals: 1m,5m,15m,30m,1h,2h,4h,6h,8h,12h,1d,1w,1M|
|to|query|string| No |End timestamp to query to|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "t": 1733211900000,
      "s": "BTCUSDT",
      "sn": "BTCUSDT",
      "c": "93400.04",
      "h": "93400.04",
      "l": "93400.04",
      "o": "93400.04",
      "v": "0"
    }
  ]
}
```

### Response

|Status Code|Meaning|Description|Data Model|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Response Schema

Status code **200**

|Name|Type|Required|Description|
|---|---|---|---|
|» msg|string|Yes|Response message, when code = 0, message = "success"; when code != 0, shows error reason|
|» code|string|Yes|Response status code, 0-success, non-0-failure|
|» data|[object]|Yes|payload|
|»» t|integer|Yes|time|
|»» s|string|Yes|symbol ID|
|»» sn|string|Yes|symbol name|
|»» c|string|Yes|close|
|»» h|string|Yes|high|
|»» l|string|Yes|low|
|»» o|string|Yes|open|
|»» v|string|Yes|volume|
