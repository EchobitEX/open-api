# Common APIs

## GET Server Time

GET /uapi/time

### Request Parameters

none

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": 1753689760366
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
|» data|integer|Yes|Server timestamp|

## GET Spot Symbol List

GET /uapi/spot/list

### Request Parameters

none

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "symbolId": "BTCUSDT",
      "baseTokenId": "BTC",
      "baseTokenName": "BTC",
      "quoteTokenId": "USDT",
      "quoteTokenName": "USDT",
      "baseTokenPrecision": "0.00001",
      "quoteTokenPrecision": "0.01",
      "minTradeQuantity": "0.0012",
      "minTradeAmount": "20",
      "minPricePrecision": "0.1",
      "depthInfo": "0.1,1,10,100",
      "allowTradeState": true,
      "showState": true,
      "showDate": 1604758562000,
      "type": 1,
      "tagIds": [
        1591362791639015000
      ],
      "iconUrl": "https://static.echobit.com/static/data/jl_J0MJwCEs9NPGkvURKb2a9yUySXGb8ABP2dXNiVfk.png"
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

| Name                   | Type     |Required|Description|
|------------------------|----------|---|---|
| » code                 | string   |Yes|Response status code, 0-success, non-0-failure|
| » msg                  | string   |Yes|Response message, when code = 0, message = "success"; when code != 0, shows error reason|
| » data                 | [object] |Yes|payload|
| »» symbolId            | string   |Yes|Symbol ID|
| »» baseTokenId         | string   |Yes|Base token ID|
| »» baseTokenName       | string   |Yes|Base token name|
| »» quoteTokenId        | string   |Yes|Quote token ID|
| »» quoteTokenName      | string   |Yes|Quote token name|
| »» baseTokenPrecision  | string   |Yes|Base token precision|
| »» quoteTokenPrecision | string   |Yes|Quote token precision|
| »» minTradeQuantity    | string   |Yes|Minimum trade quantity|
| »» minTradeAmount      | string   |Yes|Minimum trade amount|
| »» minPricePrecision   | string   |Yes|Minimum price precision|
| »» depthInfo           | string   |Yes|Merged depth|
| »» allowTradeState     | boolean  |Yes|Whether trading is allowed|
| »» showState           | boolean  |Yes|Display state|
| »» showDate            | number   |Yes|Listing time|
| »» type                | integer  |Yes|Type: 1-spot, 4-futures|
| »» tagIds              | [number] |Yes|Tag IDs|
| »» iconUrl             | string   |Yes|Token logo|

## GET Futures Symbol List

GET /uapi/contract/list

### Request Parameters

none

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "symbolId": "BTC-SWAP-USDT",
      "baseTokenId": "BTC",
      "quoteTokenId": "USDT",
      "baseTokenPrecision": "1",
      "quoteTokenPrecision": "0.0001",
      "minTradeQuantity": "1",
      "minTradeAmount": "20",
      "minPricePrecision": "0.1",
      "depthInfo": "0.1,1,10,100",
      "baseId": 1,
      "showState": true,
      "showDate": 1604742313403,
      "type": 4,
      "tagIds": [
        1591362791639015000
      ],
      "iconUrl": "https://static.echobit.com/static/data/jl_J0MJwCEs9NPGkvURKb2a9yUySXGb8ABP2dXNiVfk.png",
      "tokenId": "BTC-SWAP-USDT",
      "multiplier": "0.0001",
      "riskLimitList": [
        {"id": "1000008990", "amount": "10000.0", "maintainRate": "0.0025", "initialRate": "0.005", "side": 2},
        {"id": "1000001005", "amount": "80000.0", "maintainRate": "0.004", "initialRate": "0.008", "side": 2},
        {"id": "1000000665", "amount": "360000.0", "maintainRate": "0.005", "initialRate": "0.01", "side": 2},
        {"id": "1000000670", "amount": "1200000.0", "maintainRate": "0.01", "initialRate": "0.02", "side": 2},
        {"id": "1000000675", "amount": "5000000.0", "maintainRate": "0.025", "initialRate": "0.05", "side": 2},
        {"id": "1000001360", "amount": "10000000.0", "maintainRate": "0.05", "initialRate": "0.1", "side": 2},
        {"id": "1000002145", "amount": "15000000.0", "maintainRate": "0.1", "initialRate": "0.2", "side": 2}
      ],
      "crossRiskLimitList": [
        {"id": "1000008995", "amount": "10000.0", "maintainRate": "0.0025", "initialRate": "0.005", "side": 2},
        {"id": "1000001525", "amount": "80000.0", "maintainRate": "0.004", "initialRate": "0.008", "side": 2},
        {"id": "1000001510", "amount": "360000.0", "maintainRate": "0.005", "initialRate": "0.01", "side": 2},
        {"id": "1000001515", "amount": "1200000.0", "maintainRate": "0.01", "initialRate": "0.02", "side": 2},
        {"id": "1000001520", "amount": "5000000.0", "maintainRate": "0.025", "initialRate": "0.05", "side": 2},
        {"id": "1000001530", "amount": "10000000.0", "maintainRate": "0.05", "initialRate": "0.1", "side": 2},
        {"id": "1000002150", "amount": "15000000.0", "maintainRate": "0.1", "initialRate": "0.2", "side": 2}
      ],
      "marketPriceScope": ["-0.001", "0.001"],
      "indexId": "BTCUSDT",
      "marginPrecision": "0.0001"
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

| Name                   | Type      | Required |Description|
|------------------------|-----------|----------|---|
| » code                 | string    | Yes      |Response status code, 0-success, non-0-failure|
| » msg                  | string    | Yes      |Response message, when code = 0, message = "success"; when code != 0, shows error reason|
| » data                 | [object]  | Yes      |payload|
| »» symbolId            | string    | true     |Symbol ID|
| »» baseTokenId         | string    | true     |Base token ID|
| »» quoteTokenId        | string    | true     |Quote token ID|
| »» baseTokenPrecision  | string    | true     |Base token precision|
| »» quoteTokenPrecision | string    | true     |Quote token precision|
| »» minTradeQuantity    | string    | true     |Minimum trade quantity|
| »» minTradeAmount      | string    | true     |Minimum trade amount|
| »» minPricePrecision   | string    | true     |Minimum price precision|
| »» depthInfo           | string    | true     |Merged depth|
| »» iconUrl             | string    | true     |Token logo|
| »» baseId              | integer   | true     |Contract type: 0 UNKNOW; 1 LIVE_USDT; 2 CONTRACT_SIMULATION; 3 FOREIGN_EXCHANGE; 4 FOREIGN_EXCHANGE_SIMULATION; 5 STOCK_INDEX|
| »» showState           | boolean   | true     |Display state|
| »» showDate            | integer   | true     |Listing time|
| »» type                | integer   | true     |Type: 1-spot, 4-futures|
| »» tagIds              | [integer] | true     |Tag IDs|
| »» tokenId             | string    | true     |Futures name|
| »» multiplier          | string    | true     |Contract multiplier|
| »» riskLimitList       | [object]  | true     |Cross margin risk limits|
| »»» id                 | string    | true     |Risk limit ID|
| »»» amount             | string    | true     |Limit amount|
| »»» maintainRate       | string    | true     |Maintenance margin rate|
| »»» initialRate        | string    | true     |Initial margin rate|
| »»» side               | integer   | true     |1: BUY_OPEN, 2: SELL_OPEN|
| »» crossRiskLimitList  | [object]  | true     |Isolated margin risk limits|
| »»» id                 | string    | true     |Risk limit ID|
| »»» amount             | string    | true     |Limit amount|
| »»» maintainRate       | string    | true     |Maintenance margin rate|
| »»» initialRate        | string    | true     |Initial margin rate|
| »»» side               | integer   | true     |1: BUY_OPEN, 2: SELL_OPEN|
| »» marketPriceScope    | [string]  | true     |Market price range|
| »» indexId             | string    | true     |Index symbol|
| »» marginPrecision     | string    | true     |Margin precision|
