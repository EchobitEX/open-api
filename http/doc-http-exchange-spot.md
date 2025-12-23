# Spot Trading

## GET Spot Asset List

GET /uapi/spot/v1/property/get

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "tokenId": "BTC",
      "tokenName": "BTC",
      "positionLock": "0",
      "totalValue": "0.037780008",
      "useable": "0.037780008",
      "uTotalValue": "3531.67"
    },
    {
      "tokenId": "SEI",
      "tokenName": "SEI",
      "positionLock": "0",
      "totalValue": "2.996",
      "useable": "2.996",
      "uTotalValue": "4.49"
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
|»» tokenId|string|Yes|Token ID|
|»» tokenName|string|Yes|Token name|
|»» positionLock|string|Yes|Locked amount|
|»» totalValue|string|Yes|Total|
|»» userable|string|Yes|Available|
|»» uTotalValue|string|Yes|Total (USD equivalent)|
|»» todayPnl|string|Yes|Today's PnL|

## POST Place Order

POST /uapi/spot/v1/order

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|symbolId|query|string| No |Symbol ID|
|side|query|integer| Yes |1-buy, 2-sell|
|type|query|integer| Yes |1-limit, 2-market|
|quantity|query|string| Yes |Quantity|
|price|query|string| Yes |Price|
|clientOrderId|query|string| Yes |Client order ID, prefix `uapi_`|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

#### Details

**quantity**: Quantity
<pre>
Buy (side = 1):
      type = 1 limit, quantity unit is base token
      type = 2 market, quantity unit is USDT
Sell (side = 2):
      type = 1 limit, quantity unit is base token
      type = 2 market, quantity unit is base token
</pre>

**clientOrderId**: Client order id, fixed prefix `uapi_`
Example: uapi_MnwkeCGHqGGdg6SfLtXrsltMex27vkh8

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": {
    "time": 1749110819716,
    "orderId": "1966078487560293376",
    "userId": null,
    "aid": null,
    "clientOrderId": "uapi_MnwkeCGHqGGdg6SfLtXrsltMex27vkh8",
    "symbolId": "ETHUSDT",
    "basicTokenId": "ETH",
    "pricingTokenId": "USDT",
    "orderPrice": "0",
    "originQuantity": "100",
    "executedQuantity": "0",
    "executedAmount": "0",
    "averagePrice": "0",
    "orderType": 2,
    "side": 1,
    "feeInfoList": [],
    "orderStatus": 2,
    "noExecutedQty": null,
    "amount": null,
    "margin": null,
    "updateTime": 1749110819716,
    "quotePrice": null,
    "remark": null
  }
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
|» data|object|Yes|payload|
|»» time|number|Yes|Order time|
|»» orderId|string|Yes|Order ID|
|»» symbolId|string|Yes|Symbol ID|
|»» basicTokenId|string|Yes|Base token ID|
|»» pricingTokenId|string|Yes|Quote token ID|
|»» orderPrice|string|Yes|Order price|
|»» originQuantity|string|Yes|Original quantity|
|»» executedQuantity|string|Yes|Executed quantity|
|»» executedAmount|string|Yes|Executed amount|
|»» averagePrice|string|Yes|Average price|
|»» orderType|integer|Yes|1-limit, 2-market|
|»» side|integer|Yes|1-buy, 2-sell|
|»» feeInfoList|[object]|Yes|Fees|
|»»» feeTokenId|string|Yes|Fee token ID|
|»»» feeTokenName|string|Yes|Fee token name|
|»»» fee|string|Yes|Fee|
|»» orderStatus|integer|Yes|Order status: created(0), partial(1), filled(2), canceled(4)|
|»» updateTime|number|Yes|Update time|

## POST Cancel Order

POST /uapi/spot/v1/order/cancel

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|orderId|query|number| No |Order ID (either/or)|
|clientOrderId|query|string| No |Client order ID (either/or)|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

#### Details

**clientOrderId**: Client order id, prefix `uapi_`  
Example: uapi_MnwkeCGHqGGdg6SfLtXrsltMex27vkh8

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": {
    "status": true
  }
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
|» data|object|Yes|payload|
|»» status|boolean|Yes|true if success|

## GET Trade History

GET /uapi/spot/v1/order/history/trades

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|symbolId|query|string| No |Symbol ID; default empty string|
|fromId|query|integer| No |Start order ID; default empty string|
|endId|query|integer| No |End order ID; default empty string|
|startTime|query|number| No |Start time, timestamp, e.g. 1731919343452|
|endTime|query|number| No |End time, timestamp, e.g. 1731919343452|
|pageSize|query|string| No |Page size, default 20|
|orderSide|query|integer| No |0:all 1:buy 2:sell|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1731919343452,
      "tradeId": 1821865932600995800,
      "orderId": 1821865922215899100,
      "symbolId": "BTCUSDT",
      "basicTokenId": "BTC",
      "pricingTokenId": "USDT",
      "tradePrice": "91836.49",
      "tradeQuantity": "0.01",
      "tradeAmount": "0.01",
      "costCoinId": "BTC",
      "cost": "0.00001",
      "tradeType": 1,
      "side": 1
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
|»» time|number|Yes|time|
|»» tradeId|string|Yes|trade ID|
|»» orderId|string|Yes|order ID|
|»» symbolId|string|Yes|symbol ID|
|»» basicTokenId|string|Yes|base token ID|
|»» pricingTokenId|string|Yes|quote token ID|
|»» tradePrice|string|Yes|price|
|»» tradeQuantity|string|Yes|quantity|
|»» tradeAmount|string|Yes|amount|
|»» costTokenId|string|Yes|fee token ID|
|»» cost|string|Yes|fee|
|»» tradeType|integer|Yes|1: limit 2: market|
|»» side|integer|Yes|1: buy 2: sell|

## GET Current Orders (regular)

GET /uapi/spot/v1/order/current/orders

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|symbolId|query|string| No |Symbol ID; default empty string|
|fromId|query|integer| No |Start order ID; default empty string|
|endId|query|integer| No |End order ID; default empty string|
|startTime|query|number| No |Start time, timestamp, e.g. 1731919343452|
|endTime|query|number| No |End time, timestamp, e.g. 1731919343452|
|orderType|query|integer| No |1: limit 2: market|
|orderSide|query|integer| No |0:all 1:buy 2:sell|
|pageSize|query|string| No |Page size, default 20|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1732784241710,
      "orderId": 1829121224770324200,
      "symbolId": "BTCUSDT",
      "basicTokenId": "BTC",
      "pricingTokenId": "USDT",
      "orderPrice": "93400.04",
      "originQuantity": "0.01",
      "executedQuantity": "0",
      "executedAmount": "0",
      "averagePrice": "0",
      "orderType": 1,
      "side": 1,
      "feeInfoList": [],
      "orderStatus": 1,
      "updateTime": 1732784241735
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
|»» time|number|Yes|time|
|»» orderId|string|Yes|order ID|
|»» symbolId|string|Yes|symbol ID|
|»» basicTokenId|string|Yes|base token ID|
|»» pricingTokenId|string|Yes|quote token ID|
|»» orderPrice|string|Yes|price|
|»» originQuantity|string|Yes|quantity|
|»» executedQuantity|string|Yes|executed quantity|
|»» executedAmount|string|Yes|executed amount|
|»» averagePrice|string|Yes|average price|
|»» orderType|integer|Yes|1: limit 2: market|
|»» side|integer|Yes|1: buy 2: sell|
|»» orderStatus|integer|Yes|0: created 1: partial 2: filled 4: canceled|
|»» updateTime|number|Yes|update time|

## GET Order History (regular)

GET /uapi/spot/v1/order/history/orders

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|symbolId|query|string| No |Symbol ID; default empty string|
|fromId|query|integer| No |Start order ID; default empty string|
|endId|query|integer| No |End order ID; default empty string|
|startTime|query|number| No |Start time, timestamp, e.g. 1731919343452|
|endTime|query|number| No |End time, timestamp, e.g. 1731919343452|
|orderType|query|integer| No |1: limit 2: market|
|orderSide|query|integer| No |0:all 1:buy 2:sell|
|pageSize|query|string| No |Page size, default 20|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1731919348767,
      "orderId": 1821865976926400500,
      "symbolId": "BTCUSDT",
      "basicTokenId": "BTC",
      "pricingTokenId": "USDT",
      "orderPrice": "91836.49",
      "originQuantity": "0.01",
      "executedQuantity": "0",
      "executedAmount": "0",
      "averagePrice": "0",
      "orderType": 1,
      "side": 1,
      "feeInfoList": [],
      "orderStatus": 1,
      "updateTime": 1731919362611
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
|» msg|string|true|Response message, when code = 0, message = "success"; when code != 0, shows error reason|
|» code|string|true|Response status code, 0-success, non-0-failure|
|» data|[object]|true|none|
|»» time|number|true|time|
|»» orderId|string|true|order ID|
|»» symbolId|string|true|symbol ID|
|»» basicTokenId|string|true|base token ID|
|»» pricingTokenId|string|true|quote token ID|
|»» orderPrice|string|true|price|
|»» originQuantity|string|true|quantity|
|»» executedQuantity|string|true|executed quantity|
|»» executedAmount|string|true|executed amount|
|»» averagePrice|string|true|average price|
|»» orderType|integer|true|1: limit 2: market|
|»» side|integer|true|1: buy 2: sell|
|»» orderStatus|integer|true|0: created 1: partial 2: filled 4: canceled|
|»» updateTime|number|true|update time|

## GET Order Trade Details

GET /uapi/spot/v1/order/trade/details

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|orderId|query|number| No |Order ID|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1725611320855,
      "tradeId": 1768950403670481700,
      "orderId": 1768950382573132500,
      "symbolId": "BTCUSDT",
      "basicTokenId": "BTC",
      "pricingTokenId": "USDT",
      "tradePrice": "55786",
      "tradeQuantity": "0.00045",
      "tradeAmount": "25.1037",
      "costTokenId": "BTC",
      "cost": "0.00000045",
      "tradeType": 1,
      "side": 1
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
|»» time|number|Yes|time|
|»» tradeId|string|Yes|trade ID|
|»» orderId|string|Yes|order ID|
|»» symbolId|string|Yes|symbol ID|
|»» basicTokenId|string|Yes|base token ID|
|»» pricingTokenId|string|Yes|quote token ID|
|»» tradePrice|string|Yes|trade price|
|»» tradeQuantity|string|Yes|trade quantity|
|»» tradeAmount|string|Yes|trade amount|
|»» costTokenId|string|Yes|fee token|
|»» cost|string|Yes|fee|
|»» tradeType|integer|Yes|1: limit 2: market|
|»» side|integer|Yes|1: buy 2: sell|
