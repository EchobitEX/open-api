# Futures Trading

## POST Create Futures Order

POST /uapi/contract/v1/create

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name            | Location | Type    | Required | Description                                                               |
| --------------- | -------- | ------- | -------- | ------------------------------------------------------------------------- |
| symbolId        | query    | string  | Yes      | Symbol ID                                                                 |
| clientId        | query    | string  | Yes      | Client order ID, prefix `uapi_`                                           |
| side            | query    | integer | Yes      | 1: buy open long 2: sell open short 3: buy close short 4: sell close long |
| type            | query    | integer | Yes      | 1: regular order                                                          |
| price           | query    | string  | No       | Price                                                                     |
| priceType       | query    | integer | Yes      | Price type; 1: input price 5: market price                                |
| touchPrice      | query    | string  | No       | Trigger price                                                             |
| quantity        | query    | string  | Yes      | Quantity                                                                  |
| touchType       | query    | integer | No       | Trigger type: 0-latest 1-index 2-mark                                     |
| inForTime       | query    | string  | No       | GTC, MAKER, IOC, FOK                                                      |
| profitPrice     | query    | string  | No       | Take-profit price                                                         |
| lossPrice       | query    | string  | No       | Stop-loss price                                                           |
| profitTouchType | query    | integer | No       | Take-profit trigger type: 0-latest 1-index 2-mark                         |
| lossTouchType   | query    | integer | No       | Stop-loss trigger type: 0-latest 1-index 2-mark                           |
| stopStatus      | query    | integer | No       | Is TP/SL order (0 no)                                                     |
| backType        | query    | integer | No       | Trailing type                                                             |
| backValue       | query    | string  | No       | Trailing value                                                            |
| X-EC-APIKEY     | header   | string  | Yes      | Apikey, contact support to obtain                                         |

#### Details

- **clientId**: Client order id, fixed prefix `uapi_`
    - Example: uapi_MnwkeCGHqGGdg6SfLtXrsltMex27vkh8
- **stopStatus**: Is TP/SL order (0- no， 1- yes)
    - When `stopStatus = 1`, the order is a take-profit/stop-loss order.
    - At least one trigger method (`profitTouchType` or `lossTouchType`) must be set, and the corresponding price (`profitPrice` or `lossPrice`) must be configured.
> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": true
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name   | Type    | Required | Description                                                                              |
| ------ | ------- | -------- | ---------------------------------------------------------------------------------------- |
| » code | string  | Yes      | Response status code, 0-success, non-0-failure                                           |
| » msg  | string  | Yes      | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data | boolean | Yes      | Success flag                                                                             |

## POST Cancel Futures Order

POST /uapi/contract/v1/cancel

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type    | Required | Description                                                       |
|-------------|----------|---------|----------|-------------------------------------------------------------------|
| clientId    | query    | string  | No       | Client order ID, prefix `uapi_`                                   |
| orderId     | query    | number  | No       | Order ID                                                          |
| type        | query    | integer | No       | Order type 1: regular 2: conditional 3: Take-profit and stop-loss |
| X-EC-APIKEY | header   | string  | Yes      | Apikey, contact support to obtain                                 |

#### Details

- **clientId**: Client order id, fixed prefix `uapi_`
Example: uapi_MnwkeCGHqGGdg6SfLtXrsltMex27vkh8
- **type**: When type=1, you can enter either the `clientID` or the `orderID`,
When type=2 or 3, only `orderId` can be entered

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": true
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name   | Type    | Required | Description                                                                              |
| ------ | ------- | -------- | ---------------------------------------------------------------------------------------- |
| » code | string  | Yes      | Response status code, 0-success, non-0-failure                                           |
| » msg  | string  | Yes      | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data | boolean | Yes      | true                                                                                     |

## POST Set Stop Profit And Loss

POST /uapi/contract/v1/new/profit/loss/set

### Request Parameters

| Name            | Location | Type    | Required | Description                           |
|-----------------|----------|---------|----------|---------------------------------------|
| symbolId        | query    | string  | true     | Symbol ID                             |
| profitPrice     | query    | string  | true     | Take-profit Price                     |
| lossPrice       | query    | string  | true     | Stop-loss Price                       |
| positionDirect  | query    | integer | true     | 1 = Long Position, 0 = Short Position |
| profitTouchType | query    | integer | true     | 0 = Last Traded Price, 2 = Mark Price |
| lossTouchType   | query    | integer | true     | 0 = Last Traded Price, 2 = Mark Price |
| X-EC-APIKEY     | header   | string  | true     | Apikey, contact support to obtain     |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": true
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
|-------------|---------------------------------------------------------|-------------|------------|
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name   | Type    | Required | Description                                                                              |
|--------|---------|----------|------------------------------------------------------------------------------------------|
| » msg  | string  | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » code | string  | true     | Response status code, 0-success, non-0-failure                                           |
| » data | boolean | true     | none                                                                                     |

## GET Query Unfilled Take Profit and Stop Loss Orders for Contracts

GET /uapi/contract/v1/take/profit/stop/loss/current/orders

### Request Parameters

| Name        | Location | Type    | Required | DescriptionNo                                |
|-------------|----------|---------|----------|----------------------------------------------|
| symbolId    | query    | string  | false    | Symbol ID                                    |
| fromId      | query    | integer | false    | Starting order ID;Default 0                  |
| endId       | query    | integer | false    | End order ID;Default 0                       |
| startTime   | query    | integer | false    | Start time;Timestamp, such as 1765956648679  |
| endTime     | query    | integer | false    | End time;Timestamp, such as 1767079844000    |
| limit       | query    | integer | false    | Number of items per page;default 20 ,max 100 |
| X-EC-APIKEY | header   | string  | true     | Apikey, contact support to obtain            |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1734946163513,
      "orderId": 1847256737549172500,
      "aid": 1325347180177789400,
      "clientOrderId": "1734946162964",
      "symbolId": "BTC-SWAP-USDT",
      "basicTokenId": "BTC-SWAP-USDT",
      "pricingTokenId": "USDT",
      "orderPrice": "96879.7",
      "originQuantity": "100",
      "executedQuantity": "0",
      "executedAmount": "0",
      "executedPrice": "",
      "executedOrderId": 0,
      "averagePrice": "0",
      "orderType": 1,
      "side": 2,
      "feeInfoList": [],
      "orderStatus": 0,
      "lever": "100",
      "orderDirection": 0,
      "orderPriceType": 0,
      "touchOffPrice": "",
      "touchOffTime": 0,
      "noExecutedQty": "100",
      "marginLock": "9.6879",
      "intentionType": 0,
      "originalIntentionType": 0,
      "touchOffCondition": 0,
      "closeDirectionType": 0,
      "takeProfitStopLossType": 0,
      "forceCloseOrder": 0,
      "forceCloseOrderType": 0,
      "forceClosePrice": "",
      "pnl": "",
      "cross": 0,
      "inForTime": ""
    }
  ]
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
|-------------|---------------------------------------------------------|-------------|------------|
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                      | Type     | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| » msg                     | string   | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| » code                    | string   | true     | Response status code, 0-success, non-0-failure                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| » data                    | [object] | true     | none                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| »» time                   | integer  | false    | Time                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| »» orderId                | string   | false    | Order ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| »» aid                    | integer  | false    | Account ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| »» clientOrderId          | string   | false    | Client Order ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| »» symbolId               | string   | false    | Symbol ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| »» basicTokenId           | string   | false    | Base token ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| »» pricingTokenId         | string   | false    | Pricing token ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| »» orderPrice             | string   | false    | Price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| »» originQuantity         | string   | false    | Quantity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| »» executedQuantity       | string   | false    | Executed quantity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| »» executedAmount         | string   | false    | Executed amount                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| »» executedPrice          | string   | false    | Executed price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| »» executedOrderId        | string   | false    | Executed order ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| »» averagePrice           | string   | false    | Average price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| »» orderType              | integer  | false    | Order type 1: Ordinary order 2: Planned order                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| »» side                   | integer  | false    | Order direction 1: Buy to open long 2: Sell to open short 3: Buy to close long 4: Sell to close short                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| »» feeInfoList            | [string] | false    | Fee                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| »» orderStatus            | integer  | false    | Order status Ordinary order status 0: Created 1: Partially filled 2: Fully filled 4: Cancelled 8: Rejected Planned order/Take Profit & Stop Loss 11: Created 12: Ordered 13: Rejected 14: Cancelled                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| »» lever                  | string   | false    | Leverage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| »» orderDirection         | integer  | false    | 1: Close position order 0: Open position order                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| »» orderPriceType         | integer  | false    | Original priceType 1: Input price 5: Market price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| »» touchOffPrice          | string   | false    | Trigger price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| »» noExecutedQty          | string   | false    | Unfilled quantity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| »» marginLock             | string   | false    | Margin                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| »» intentionType          | integer  | false    | Original planOrderType STOP_COMMON = 1; // Planned order - Ordinary<br />STOP_LONG_PROFIT = 2; // Planned order - Long position take profit<br />STOP_LONG_LOSS = 3; // Planned order - Long position stop loss<br />STOP_SHORT_PROFIT = 4; // Planned order - Short position take profit<br />STOP_SHORT_LOSS = 5; // Planned order - Short position stop loss<br />STOP_LONG_PROFIT_QUANTITY = 6; // Long position take profit (by batch/quantity)<br />STOP_LONG_LOSS_QUANTITY = 7; // Long position stop loss (by batch/quantity)<br />STOP_SHORT_PROFIT_QUANTITY = 8; // Short position take profit (by batch/quantity)<br />STOP_SHORT_LOSS_QUANTITY = 9; // Short position stop loss (by batch/quantity)         |
| »» originalIntentionType  | integer  | false    | Original originalPlanOrderType STOP_COMMON = 1; // Planned order - Ordinary<br />STOP_LONG_PROFIT = 2; // Planned order - Long position take profit<br />STOP_LONG_LOSS = 3; // Planned order - Long position stop loss<br />STOP_SHORT_PROFIT = 4; // Planned order - Short position take profit<br />STOP_SHORT_LOSS = 5; // Planned order - Short position stop loss<br />STOP_LONG_PROFIT_QUANTITY = 6; // Long position take profit (by batch/quantity)<br />STOP_LONG_LOSS_QUANTITY = 7; // Long position stop loss (by batch/quantity)<br />STOP_SHORT_PROFIT_QUANTITY = 8; // Short position take profit (by batch/quantity)<br />STOP_SHORT_LOSS_QUANTITY = 9; // Short position stop loss (by batch/quantity) |
| »» touchOffCondition      | integer  | false    | Planned order trigger condition type 0: Latest price 1: Index price 2: Mark price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| »» closeDirectionType     | integer  | false    | Planned order take profit/stop loss close type 0: Close only available positions when closing 1: Close all positions when closing                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| »» takeProfitStopLossType | integer  | false    | Take profit/stop loss type 0: Position take profit/stop loss 1: Take profit/stop loss by quantity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| »» forceCloseOrder        | integer  | false    | Whether it is a forced liquidation order 1: Forced liquidation order 2: Non-forced liquidation order                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| »» forceCloseOrderType    | integer  | false    | Forced liquidation order type 0: Non-liquidation order 1: Forced liquidation order during liquidation 2: Reduction order during liquidation                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| »» forceClosePrice        | string   | false    | Forced liquidation price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| »» pnl                    | string   | false    | Profit and loss from execution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| »» cross                  | integer  | false    | Position mode 1: Cross margin 0: Isolated margin                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

## GET Query Contract Historical Take-profit & Stop-loss Orders

GET /uapi/contract/v1/take/profit/stop/loss/history/orders

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type    | Required | Description                                  |
|-------------|----------|---------|----------|----------------------------------------------|
| symbolId    | query    | string  | No       | Symbol ID                                    |
| fromId      | query    | integer | No       | Starting order ID;Default 0                  |
| endId       | query    | integer | No       | End order ID;Default 0                       |
| startTime   | query    | integer | No       | Start time;Timestamp, such as 1765956648679  |
| endTime     | query    | integer | No       | End time;Timestamp, such as 1767079844000    |
| limit       | query    | integer | No       | Number of items per page;default 20 ,max 100 |
| X-EC-APIKEY | header   | string  | true     | Apikey, contact support to obtain            |

Response Example

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1765867025597,
      "orderId": "2106639730397552640",
      "aid": 2076841886199443202,
      "userId": "",
      "clientOrderId": "STOP_LONG_PROFIT_2106639730322256640",
      "symbolId": "ETH-SWAP-USDT",
      "basicTokenId": "ETH-SWAP-USDT",
      "pricingTokenId": "USDT",
      "orderPrice": "3900",
      "originQuantity": "0",
      "executedQuantity": "0",
      "executedAmount": "",
      "executedPrice": "0",
      "executedOrderId": "0",
      "averagePrice": "",
      "orderType": 2,
      "side": 4,
      "feeInfoList": [],
      "orderStatus": 14,
      "lever": "0",
      "orderDirection": 0,
      "orderPriceType": 5,
      "touchOffPrice": "3900",
      "touchOffTime": 0,
      "noExecutedQty": "",
      "marginLock": "",
      "intentionType": 2,
      "originalIntentionType": 2,
      "touchOffCondition": 0,
      "closeDirectionType": 1,
      "takeProfitStopLossType": 0,
      "forceCloseOrder": 0,
      "forceCloseOrderType": 0,
      "forceClosePrice": "",
      "pnl": "",
      "cross": 0,
      "openPositionAvgPrice": "",
      "avgLeverage": 0,
      "updateTime": 1765870030695,
      "remark": "",
      "quotePrice": "2939.6"
    }
  ]
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
|-------------|---------------------------------------------------------|-------------|------------|
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                      | Type     | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|---------------------------|----------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| » msg                     | string   | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| » code                    | string   | true     | Response status code, 0-success, non-0-failure                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| » data                    | [object] | true     | none                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| »» time                   | integer  | false    | Time                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| »» orderId                | string   | false    | Order ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| »» aid                    | integer  | false    | Account ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| »» clientOrderId          | string   | false    | Client Order ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| »» symbolId               | string   | false    | Symbol ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| »» basicTokenId           | string   | false    | Base Token ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| »» pricingTokenId         | string   | false    | Quote Token ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| »» orderPrice             | string   | false    | Order Price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| »» originQuantity         | string   | false    | Original Quantity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| »» executedQuantity       | string   | false    | Executed Quantity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| »» executedAmount         | string   | false    | Executed Amount                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| »» executedPrice          | string   | false    | Executed Price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| »» executedOrderId        | string   | false    | Executed Order ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| »» averagePrice           | string   | false    | Average Price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| »» orderType              | integer  | false    | Order Type: 1 = Regular Order, 2 = Planned Order                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| »» side                   | integer  | false    | Order Side: 1 = Buy Open Long, 2 = Sell Open Short, 3 = Buy Close Long, 4 = Sell Close Short                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| »» feeInfoList            | [string] | false    | Fee Information List                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| »» orderStatus            | integer  | false    | Order Status<br />Regular Order: 0 = Created, 1 = Partially Filled, 2 = Fully Filled, 4 = Cancelled, 8 = Rejected<br />Planned/Take-profit/Stop-loss Order: 11 = Created, 12 = Placed, 13 = Rejected, 14 = Cancelled                                                                                                                                                                                                                                                                                                                                                                         |
| »» lever                  | string   | false    | Leverage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| »» orderDirection         | integer  | false    | Order Direction: 1 = Close Position Order, 0 = Open Position Order                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| »» orderPriceType         | integer  | false    | Original Price Type: 1 = Input Price, 5 = Market Price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| »» touchOffPrice          | string   | false    | Trigger Price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| »» noExecutedQty          | string   | false    | Unexecuted Quantity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| »» marginLock             | string   | false    | Margin Locked                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| »» intentionType          | integer  | false    | Original Plan Order Type:<br />1 = STOP_COMMON (Planned Order - Regular)<br />2 = STOP_LONG_PROFIT (Planned Order - Long Take-profit)<br />3 = STOP_LONG_LOSS (Planned Order - Long Stop-loss)<br />4 = STOP_SHORT_PROFIT (Planned Order - Short Take-profit)<br />5 = STOP_SHORT_LOSS (Planned Order - Short Stop-loss)<br />6 = STOP_LONG_PROFIT_QUANTITY (Long Take-profit by Quantity)<br />7 = STOP_LONG_LOSS_QUANTITY (Long Stop-loss by Quantity)<br />8 = STOP_SHORT_PROFIT_QUANTITY (Short Take-profit by Quantity)<br />9 = STOP_SHORT_LOSS_QUANTITY (Short Stop-loss by Quantity) |
| »» originalIntentionType  | integer  | false    | Original Plan Order Type:<br />1 = STOP_COMMON (Planned Order - Regular)<br />2 = STOP_LONG_PROFIT (Planned Order - Long Take-profit)<br />3 = STOP_LONG_LOSS (Planned Order - Long Stop-loss)<br />4 = STOP_SHORT_PROFIT (Planned Order - Short Take-profit)<br />5 = STOP_SHORT_LOSS (Planned Order - Short Stop-loss)<br />6 = STOP_LONG_PROFIT_QUANTITY (Long Take-profit by Quantity)<br />7 = STOP_LONG_LOSS_QUANTITY (Long Stop-loss by Quantity)<br />8 = STOP_SHORT_PROFIT_QUANTITY (Short Take-profit by Quantity)<br />9 = STOP_SHORT_LOSS_QUANTITY (Short Stop-loss by Quantity) |
| »» touchOffCondition      | integer  | false    | Planned Order Trigger Condition Type: 0 = Last Traded Price, 1 = Index Price, 2 = Mark Price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| »» closeDirectionType     | integer  | false    | Planned Order Take-profit/Stop-loss Close Type: 0 = Close Only Available Position, 1 = Close All Positions                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| »» takeProfitStopLossType | integer  | false    | Take-profit/Stop-loss Type: 0 = Position-based Take-profit/Stop-loss, 1 = Quantity-based Take-profit/Stop-loss                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| »» forceCloseOrder        | integer  | false    | Force Close Flag: 1 = Force Close Order, 2 = Non-force Close Order                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| »» forceCloseOrderType    | integer  | false    | Force Close Order Type: 0 = Non-liquidation Order, 1 = Liquidation Force Close Order, 2 = Liquidation Position Reduction Order                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| »» forceClosePrice        | string   | false    | Force Close Price                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| »» pnl                    | string   | false    | Profit and Loss (P&L)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| »» cross                  | integer  | false    | Margin Mode: 1 = Cross Margin, 0 = Isolated Margin                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |


## GET Query Stop Profit And Loss

GET /uapi/contract/v1/profit/loss/get

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name           | Location | Type    | Required | Description                           |
|----------------|----------|---------|----------|---------------------------------------|
| symbolId       | query    | string  | true     | Symbol ID                             |
| positionDirect | query    | integer | true     | 1 = Long Position, 0 = Short Position |
| X-EC-APIKEY    | header   | string  | true     | Apikey, contact support to obtain     |

Response Example

```json
{
    "msg": "success",
    "code": "0",
    "data": {
        "stopProfit": true,
        "profitPrice": "3800",
        "profitOrderId": 2103892153331752960,
        "profitWebOrderId": "2103892153331752960",
        "profitTouchType": 0,
        "profitCloseType": 1,
        "stopLoss": false,
        "lossPrice": "",
        "lossOrderId": 0,
        "lossWebOrderId": "0",
        "lossTouchType": 0,
        "lossCloseType": 0
    }
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
|-------------|---------------------------------------------------------|-------------|------------|
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                | Type     | Required | Description                                                                              |
|---------------------|----------|----------|------------------------------------------------------------------------------------------|
| » code              | string   | true     | Response status code, 0-success, non-0-failure                                           |
| » msg               | string   | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data              | [object] | true     | none                                                                                     |
| »» stopProfit       | boolean  | true     | Whether to enable take-profit                                                            |
| profitPrice         | string   | true     | Take-profit price                                                                        |
| »» profitOrderId    | long     | true     | Take-profit order ID                                                                     |
| »» profitWebOrderId | string   | true     | Take-profit web-side order ID                                                            |
| »» profitTouchType  | integer  | true     | Take-profit trigger type                                                                 |
| »» profitCloseType  | integer  | true     | Take-profit position closing type                                                        |
| »» stopLoss         | boolean  | true     | Whether to enable stop-loss                                                              |
| »» lossPrice        | string   | true     | Stop-loss price                                                                          |
| »» lossOrderId      | long     | true     | Stop-loss order ID                                                                       |
| »» lossWebOrderId   | string   | true     | Stop-loss web-side order ID                                                              |
| »» lossTouchType    | integer  | true     | Stop-loss trigger type                                                                   |
| »» lossCloseType    | integer  | true     | Stop-loss position closing type                                                          |

## GET Query Stop Profit And Loss By PositionId

GET /uapi/contract/v1/profit/loss/query

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name          | Location | Type    | Required | Description                       |
|---------------|----------|---------|----------|-----------------------------------|
| positionId    | query    | integer | true     | Position ID                       |
| X-EC-APIKEY   | header   | string  | true     | Apikey, contact support to obtain |

Response Example

```json
{
    "msg": "success",
    "code": "0",
    "data": {
        "stopProfit": true,
        "profitPrice": "3800",
        "profitOrderId": 2103892153331752960,
        "profitWebOrderId": "2103892153331752960",
        "profitTouchType": 0,
        "profitCloseType": 1,
        "stopLoss": false,
        "lossPrice": "",
        "lossOrderId": 0,
        "lossWebOrderId": "0",
        "lossTouchType": 0,
        "lossCloseType": 0
    }
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
|-------------|---------------------------------------------------------|-------------|------------|
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                | Type     | Required | Description                                                                              |
|---------------------|----------|----------|------------------------------------------------------------------------------------------|
| » code              | string   | true     | Response status code, 0-success, non-0-failure                                           |
| » msg               | string   | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data              | [object] | true     | none                                                                                     |
| »» stopProfit       | boolean  | true     | Whether to enable take-profit                                                            |
| profitPrice         | string   | true     | Take-profit price                                                                        |
| »» profitOrderId    | long     | true     | Take-profit order ID                                                                     |
| »» profitWebOrderId | string   | true     | Take-profit web-side order ID                                                            |
| »» profitTouchType  | integer  | true     | Take-profit trigger type                                                                 |
| »» profitCloseType  | integer  | true     | Take-profit position closing type                                                        |
| »» stopLoss         | boolean  | true     | Whether to enable stop-loss                                                              |
| »» lossPrice        | string   | true     | Stop-loss price                                                                          |
| »» lossOrderId      | long     | true     | Stop-loss order ID                                                                       |
| »» lossWebOrderId   | string   | true     | Stop-loss web-side order ID                                                              |
| »» lossTouchType    | integer  | true     | Stop-loss trigger type                                                                   |
| »» lossCloseType    | integer  | true     | Stop-loss position closing type                                                          |

## GET Current Positions

GET /uapi/contract/v1/current/position

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type    | Required | Description                         |
| ----------- | -------- | ------- | -------- | ----------------------------------- |
| mode        | query    | integer | No       | Default 2; 0-merged, 1-split, 2-all |
| X-EC-APIKEY | header   | string  | Yes      | Apikey, contact support to obtain   |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "positionId": 1905771681613478700,
      "positionWebId": "1905771681613478656",
      "symbolId": "ETH-SWAP-USDT",
      "symbolName": "ETH-SWAP-USDT",
      "lever": "4.7",
      "totalPosition": "222",
      "valueOfPosition": "8160.942",
      "positionMargin": "1738.850287",
      "minReductionMargin": "1698.021157",
      "entrustMargin": "0",
      "averagePrice": "3678.3",
      "estimateLiquidationPrice": "2902.2",
      "marginRatio": "0.2124",
      "indexPrice": "3677",
      "contractPrice": "3677",
      "availablePosition": "222",
      "availableMargin": "0",
      "positionDirect": 1,
      "realizedProfitLoss": "-4.082913",
      "upnl": "-4.884",
      "coin": "USDT",
      "pnlRatio": "-0.0028",
      "fixedLever": "5",
      "profitLossConfig": {
        "stopProfit": false,
        "profitPrice": "",
        "profitOrderId": 0,
        "profitWebOrderId": "0",
        "profitTouchType": 0,
        "profitCloseType": 0,
        "stopLoss": false,
        "lossPrice": "",
        "lossOrderId": 0,
        "lossWebOrderId": "0",
        "lossTouchType": 0,
        "lossCloseType": 0
      },
      "cross": 0,
      "finishedUpnl": "0",
      "valueOfPositionTotal": "8165.826"
    }
  ]
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                        | Type     | Required | Description                                                                              |
| --------------------------- | -------- | -------- | ---------------------------------------------------------------------------------------- |
| » code                      | string   | Yes      | Response status code, 0-success, non-0-failure                                           |
| » msg                       | string   | Yes      | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data                      | [object] | Yes      | payload                                                                                  |
| »» positionId               | number   | true     | position id                                                                              |
| »» positionWebId            | string   | true     | position id (web)                                                                        |
| »» symbolId                 | string   | true     | futures symbol id                                                                        |
| »» symbolName               | string   | true     | futures symbol name                                                                      |
| »» lever                    | string   | true     | leverage                                                                                 |
| »» totalPosition            | string   | true     | position                                                                                 |
| »» valueOfPosition          | string   | true     | position value (USDT)                                                                    |
| »» positionMargin           | string   | true     | position margin                                                                          |
| »» minReductionMargin       | string   | true     | max reducible margin                                                                     |
| »» entrustMargin            | string   | true     | entrusted margin                                                                         |
| »» averagePrice             | string   | true     | avg open price = cumulative open value / (position * contract multiplier)                |
| »» estimateLiquidationPrice | string   | true     | estimated liquidation price                                                              |
| »» marginRatio              | string   | true     | margin ratio                                                                             |
| »» indexPrice               | string   | true     | index price                                                                              |
| »» contractPrice            | string   | true     | contract price (mark or index by quote-server config)                                    |
| »» availablePosition        | string   | true     | closeable quantity                                                                       |
| »» availableMargin          | string   | true     | available margin                                                                         |
| »» positionDirect           | integer  | true     | 1-long, 0-short                                                                          |
| »» realizedProfitLoss       | string   | true     | realized PnL                                                                             |
| »» upnl                     | string   | true     | unrealized PnL                                                                           |
| »» coin                     | string   | true     | coin unit                                                                                |
| »» pnlRatio                 | string   | true     | return ratio                                                                             |
| »» fixedLever               | string   | true     | fixed leverage (UI)                                                                      |
| »» profitLossConfig         | object   | true     | TP/SL config                                                                             |
| »»» stopProfit              | boolean  | true     | TP enabled                                                                               |
| »»» profitPrice             | string   | true     | TP price                                                                                 |
| »»» profitOrderId           | number   | true     | TP order id                                                                              |
| »»» profitWebOrderId        | string   | true     | TP order id (web)                                                                        |
| »»» profitTouchType         | integer  | true     | TP trigger: 0-latest 1-index 2-mark                                                      |
| »»» profitCloseType         | integer  | true     | TP close: 0-partial closeable 1-close all                                                |
| »»» stopLoss                | boolean  | true     | SL enabled                                                                               |
| »»» lossPrice               | string   | true     | SL price                                                                                 |
| »»» lossTouchType           | integer  | true     | SL trigger: 0-latest 1-index 2-mark                                                      |
| »»» lossOrderId             | number   | true     | SL order id                                                                              |
| »»» lossWebOrderId          | string   | true     | SL order id (web)                                                                        |
| »»» lossCloseType           | integer  | true     | SL close: 0-partial closeable 1-close all                                                |
| »» cross                    | integer  | Yes      | 1-cross, 0-isolated                                                                      |
| »» finishedUpnl             | string   | Yes      | settled unrealized PnL                                                                   |
| »» valueOfPositionTotal     | string   | Yes      | cumulative open value                                                                    |

## GET Current Orders (regular or conditional)

GET /uapi/contract/v1/current/orders

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type    | Required | Description                       |
| ----------- | -------- | ------- | -------- | --------------------------------- |
| symbolId    | query    | string  | No       | Symbol ID; default empty          |
| fromId      | query    | number  | No       | Start ID; default 0               |
| endId       | query    | number  | No       | End ID; default 0                 |
| startTime   | query    | number  | No       | Start time, timestamp             |
| endTime     | query    | number  | No       | End time, timestamp               |
| orderType   | query    | integer | No       | 1: regular 2: conditional         |
| limit       | query    | integer | No       | Page size, default 20             |
| X-EC-APIKEY | header   | string  | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1734946163513,
      "orderId": 1847256737549172500,
      "aid": 1325347180177789400,
      "clientOrderId": "1734946162964",
      "symbolId": "BTC-SWAP-USDT",
      "basicTokenId": "BTC-SWAP-USDT",
      "pricingTokenId": "USDT",
      "orderPrice": "96879.7",
      "originQuantity": "100",
      "executedQuantity": "0",
      "executedAmount": "0",
      "executedPrice": "",
      "executedOrderId": "",
      "averagePrice": "0",
      "orderType": 1,
      "side": 2,
      "feeInfoList": [],
      "orderStatus": 0,
      "lever": "100",
      "orderDirection": 0,
      "orderPriceType": 0,
      "touchOffPrice": "",
      "touchOffTime": 0,
      "noExecutedQty": "100",
      "marginLock": "9.6879",
      "intentionType": 0,
      "originalIntentionType": 0,
      "touchOffCondition": 0,
      "closeDirectionType": 0,
      "takeProfitStopLossType": 0,
      "forceCloseOrder": 0,
      "forceCloseOrderType": 0,
      "forceClosePrice": "",
      "pnl": "",
      "cross": 0,
      "inForTime": ""
    }
  ]
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                      | Type     | Required | Description                                                                                                                                                                                                                        |
| ------------------------- | -------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| » msg                     | string   | Yes      | Response message, when code = 0, message = "success"; when code != 0, shows error reason                                                                                                                                           |
| » code                    | string   | Yes      | Response status code, 0-success, non-0-failure                                                                                                                                                                                     |
| » data                    | [object] | Yes      | payload                                                                                                                                                                                                                            |
| »» time                   | number   | Yes      | time                                                                                                                                                                                                                               |
| »» orderId                | string   | Yes      | order ID                                                                                                                                                                                                                           |
| »» aid                    | number   | Yes      | account ID                                                                                                                                                                                                                         |
| »» clientOrderId          | string   | Yes      | client order ID                                                                                                                                                                                                                    |
| »» symbolId               | string   | Yes      | symbol ID                                                                                                                                                                                                                          |
| »» basicTokenId           | string   | Yes      | base token ID                                                                                                                                                                                                                      |
| »» pricingTokenId         | string   | Yes      | quote token ID                                                                                                                                                                                                                     |
| »» orderPrice             | string   | Yes      | price                                                                                                                                                                                                                              |
| »» originQuantity         | string   | Yes      | quantity                                                                                                                                                                                                                           |
| »» executedQuantity       | string   | Yes      | executed quantity                                                                                                                                                                                                                  |
| »» executedAmount         | string   | Yes      | executed amount                                                                                                                                                                                                                    |
| »» executedPrice          | string   | Yes      | executed price                                                                                                                                                                                                                     |
| »» executedOrderId        | string   | Yes      | executed order ID                                                                                                                                                                                                                  |
| »» averagePrice           | string   | Yes      | average price                                                                                                                                                                                                                      |
| »» orderType              | integer  | Yes      | 1: regular 2: conditional                                                                                                                                                                                                          |
| »» side                   | integer  | Yes      | 1: buy open long 2: sell open short 3: buy close long 4: sell close short                                                                                                                                                          |
| »» feeInfoList            | [string] | Yes      | fees                                                                                                                                                                                                                               |
| »» orderStatus            | integer  | Yes      | regular 0:create 1:partial 2:filled 4:cancel 8:reject; conditional 11:create 12:entrusted 13:rejected 14:canceled                                                                                                                  |
| »» lever                  | string   | Yes      | leverage                                                                                                                                                                                                                           |
| »» orderDirection         | integer  | Yes      | 1: close 0: open                                                                                                                                                                                                                   |
| »» orderPriceType         | integer  | Yes      | 1: input price 5: market price                                                                                                                                                                                                     |
| »» touchOffPrice          | string   | Yes      | trigger price                                                                                                                                                                                                                      |
| »» noExecutedQty          | string   | Yes      | unfilled quantity                                                                                                                                                                                                                  |
| »» marginLock             | string   | Yes      | margin                                                                                                                                                                                                                             |
| »» intentionType          | integer  | Yes      | planned order type (STOP_COMMON=1, STOP_LONG_PROFIT=2, STOP_LONG_LOSS=3, STOP_SHORT_PROFIT=4, STOP_SHORT_LOSS=5, STOP_LONG_PROFIT_QUANTITY=6, STOP_LONG_LOSS_QUANTITY=7, STOP_SHORT_PROFIT_QUANTITY=8, STOP_SHORT_LOSS_QUANTITY=9) |
| »» originalIntentionType  | integer  | Yes      | same as `intentionType`                                                                                                                                                                                                            |
| »» touchOffCondition      | integer  | Yes      | 0: latest 1: index 2: mark                                                                                                                                                                                                         |
| »» closeDirectionType     | integer  | Yes      | 0: close only closeable 1: close all                                                                                                                                                                                               |
| »» takeProfitStopLossType | integer  | Yes      | 0: position TP/SL 1: quantity TP/SL                                                                                                                                                                                                |
| »» forceCloseOrder        | integer  | Yes      | 1: forced close 2: normal                                                                                                                                                                                                          |
| »» forceCloseOrderType    | integer  | Yes      | 0: non-liquidation 1: liquidation close 2: liquidation reduction                                                                                                                                                                   |
| »» forceClosePrice        | string   | Yes      | forced close price                                                                                                                                                                                                                 |
| »» pnl                    | string   | Yes      | P&L                                                                                                                                                                                                                                |
| »» cross                  | integer  | false    | 1: cross 0: isolated                                                                                                                                                                                                               |
| »» quotePrice             | string   | true     | none                                                                                                                                                                                                                               |

## GET Order History (regular or conditional)

GET /uapi/contract/v1/history/orders

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type    | Required | Description                       |
| ----------- | -------- | ------- | -------- | --------------------------------- |
| symbolId    | query    | string  | No       | Symbol ID; default empty          |
| fromId      | query    | number  | No       | Start ID; default 0               |
| endId       | query    | number  | No       | End ID; default 0                 |
| startTime   | query    | number  | No       | Start time, timestamp             |
| endTime     | query    | number  | No       | End time, timestamp               |
| orderType   | query    | integer | No       | 1: regular 2: conditional         |
| limit       | query    | integer | No       | Page size, default 20             |
| X-EC-APIKEY | header   | string  | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1734336800495,
      "orderId": 1842145031932136000,
      "aid": 1757195645905643800,
      "clientOrderId": "1734336799969",
      "symbolId": "BTC-SWAP-USDT",
      "basicTokenId": "BTC-SWAP-USDT",
      "pricingTokenId": "USDT",
      "orderPrice": "105118.8",
      "originQuantity": "100",
      "executedQuantity": "0",
      "executedAmount": null,
      "executedPrice": "0",
      "executedOrderId": 0,
      "averagePrice": null,
      "orderType": 2,
      "side": 2,
      "feeInfoList": null,
      "orderStatus": 1,
      "orderLever": "75",
      "orderDirection": null,
      "orderPriceType": 1,
      "touchOffPrice": "10500",
      "noExecutedQty": null,
      "marginLock": null,
      "intentionType": 1,
      "originalIntentionType": 1,
      "touchOffCondition": 2,
      "closeDirectionType": 0,
      "takeProfitStopLossType": 0,
      "forceCloseOrder": null,
      "forceCloseOrderType": null,
      "forceClosePrice": null,
      "pnl": null,
      "positionOrder": null
    }
  ]
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                      | Type     | Required | Description                                                                                                       |
| ------------------------- | -------- | -------- | ----------------------------------------------------------------------------------------------------------------- |
| » msg                     | string   | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason                          |
| » code                    | string   | true     | Response status code, 0-success, non-0-failure                                                                    |
| » data                    | [object] | true     | none                                                                                                              |
| »» time                   | number   | false    | time                                                                                                              |
| »» orderId                | string   | false    | order ID                                                                                                          |
| »» aid                    | number   | false    | account ID                                                                                                        |
| »» clientOrderId          | string   | false    | client order ID                                                                                                   |
| »» symbolId               | string   | false    | symbol ID                                                                                                         |
| »» basicTokenId           | string   | false    | base token ID                                                                                                     |
| »» pricingTokenId         | string   | false    | quote token ID                                                                                                    |
| »» orderPrice             | string   | false    | price                                                                                                             |
| »» originQuantity         | string   | false    | quantity                                                                                                          |
| »» executedQuantity       | string   | false    | executed quantity                                                                                                 |
| »» executedAmount         | string   | false    | executed amount                                                                                                   |
| »» executedPrice          | string   | false    | executed price                                                                                                    |
| »» executedOrderId        | string   | false    | executed order ID                                                                                                 |
| »» averagePrice           | string   | false    | average price                                                                                                     |
| »» orderType              | integer  | false    | 1: regular 2: conditional                                                                                         |
| »» side                   | integer  | false    | 1: buy open long 2: sell open short 3: buy close long 4: sell close short                                         |
| »» feeInfoList            | [string] | false    | fees                                                                                                              |
| »» orderStatus            | integer  | false    | regular 0:create 1:partial 2:filled 4:cancel 8:reject; conditional 11:create 12:entrusted 13:rejected 14:canceled |
| »» lever                  | string   | false    | leverage                                                                                                          |
| »» orderDirection         | integer  | false    | 1: close 0: open                                                                                                  |
| »» orderPriceType         | integer  | false    | 1: input price 5: market price                                                                                    |
| »» touchOffPrice          | string   | false    | trigger price                                                                                                     |
| »» noExecutedQty          | string   | false    | unfilled quantity                                                                                                 |
| »» marginLock             | string   | false    | margin                                                                                                            |
| »» intentionType          | integer  | false    | planned order type (see above)                                                                                    |
| »» originalIntentionType  | integer  | false    | planned order type (same)                                                                                         |
| »» touchOffCondition      | integer  | false    | 0: latest 1: index 2: mark                                                                                        |
| »» closeDirectionType     | integer  | false    | 0: close only closeable 1: close all                                                                              |
| »» takeProfitStopLossType | integer  | false    | 0: position TP/SL 1: quantity TP/SL                                                                               |
| »» forceCloseOrder        | integer  | false    | 1: forced close 2: non-forced                                                                                     |
| »» forceCloseOrderType    | integer  | false    | 0: non-liquidation 1: liquidation close 2: liquidation reduction                                                  |
| »» forceClosePrice        | string   | false    | forced close price                                                                                                |
| »» pnl                    | string   | false    | P&L                                                                                                               |
| »» positionOrder          | string   | Yes      | position order                                                                                                    |

## POST Set Leverage

POST /uapi/contract/v1/set/leverage/merge

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name           | Location | Type    | Required | Description                       |
| -------------- | -------- | ------- | -------- | --------------------------------- |
| symbolId       | query    | string  | Yes      | Symbol                            |
| lever          | query    | integer | Yes      | Leverage                          |
| positionDirect | query    | integer | No       | Default 0 (all); 1-long; 2-short  |
| X-EC-APIKEY    | header   | string  | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": true
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name   | Type    | Required | Description                                                                              |
| ------ | ------- | -------- | ---------------------------------------------------------------------------------------- |
| » code | string  | true     | Response status code, 0-success, non-0-failure                                           |
| » msg  | string  | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data | boolean | true     | payload                                                                                  |

## GET Query Leverage

GET /uapi/contract/v1/get/leverage/merge

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type   | Required | Description                       |
| ----------- | -------- | ------ | -------- | --------------------------------- |
| symbolId    | query    | string | Yes      | Symbol                            |
| X-EC-APIKEY | header   | string | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": {
    "cross": 0,
    "lever": 10,
    "longLever": 10,
    "shortLever": 5,
    "symbolId": "ETH-SWAP-USDT"
  }
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name          | Type    | Required | Description                                                                              |
| ------------- | ------- | -------- | ---------------------------------------------------------------------------------------- |
| » code        | string  | Yes      | Response status code, 0-success, non-0-failure                                           |
| » msg         | string  | Yes      | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data        | object  | Yes      | payload                                                                                  |
| »» longLever  | integer | Yes      | Long leverage                                                                            |
| »» shortLever | integer | Yes      | Short leverage                                                                           |
| »» symbolId   | string  | Yes      | Symbol                                                                                   |
| »» cross      | integer | Yes      | 1-cross, 0-isolated                                                                      |
| »» lever      | integer | Yes      | Leverage                                                                                 |

## GET Trade History

GET /uapi/contract/v1/history/trades

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type    | Required | Description                       |
| ----------- | -------- | ------- | -------- | --------------------------------- |
| symbolId    | query    | string  | No       | Symbol ID; default empty          |
| fromId      | query    | number  | No       | Start ID; default 0               |
| endId       | query    | number  | No       | End ID; default 0                 |
| startTime   | query    | number  | No       | Start time, timestamp             |
| endTime     | query    | number  | No       | End time, timestamp               |
| limit       | query    | integer | No       | Page size, default 20             |
| X-EC-APIKEY | header   | string  | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1734423281500,
      "tradeId": 1842870487400627500,
      "orderId": 1842867159950237700,
      "aid": 1757195645905643800,
      "symbolId": "BTC-SWAP-USDT",
      "basicTokenId": "BTC-SWAP-USDT",
      "pricingTokenId": "USDT",
      "tradePrice": "107022.6",
      "tradeQuantity": "100",
      "tradeAmount": "10702260",
      "costTokenId": "USDT",
      "cost": "0.214",
      "tradeType": 1,
      "side": 2,
      "executedAmount": null,
      "pnl": "0",
      "orderPriceType": 1,
      "forceCloseOrderType": 0
    }
  ]
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                   | Type     | Required | Description                                                                              |
| ---------------------- | -------- | -------- | ---------------------------------------------------------------------------------------- |
| » msg                  | string   | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » code                 | string   | true     | Response status code, 0-success, non-0-failure                                           |
| » data                 | [object] | true     | none                                                                                     |
| »» time                | number   | true     | time                                                                                     |
| »» tradeId             | string   | true     | trade ID                                                                                 |
| »» orderId             | string   | true     | order ID                                                                                 |
| »» aid                 | number   | true     | account ID                                                                               |
| »» symbolId            | string   | true     | symbol ID                                                                                |
| »» basicTokenId        | string   | true     | base token ID                                                                            |
| »» pricingTokenId      | string   | true     | quote token ID                                                                           |
| »» tradePrice          | string   | true     | price                                                                                    |
| »» tradeQuantity       | string   | true     | quantity                                                                                 |
| »» tradeAmount         | string   | true     | amount                                                                                   |
| »» costTokenId         | string   | true     | fee token ID                                                                             |
| »» cost                | string   | true     | fee                                                                                      |
| »» tradeType           | integer  | true     | 1: limit 2: market                                                                       |
| »» side                | integer  | true     | 1: buy open long 2: sell open short 3: buy close long 4: sell close short                |
| »» executedAmount      | string   | true     | executed amount                                                                          |
| »» pnl                 | string   | true     | trade P&L                                                                                |
| »» orderPriceType      | integer  | true     | 1: input price 5: market price                                                           |
| »» forceCloseOrderType | integer  | true     | 0: non-liquidation 1: liquidation close 2: liquidation reduction                         |
| »» truthCost           | string   | true     | real fee                                                                                 |
| »» trialFundCost       | string   | true     | trial fund fee                                                                           |
| »» offsetFundCost      | string   | true     | offset fund fee                                                                          |

## GET Order Trade Details

GET /uapi/contract/v1/trade/details

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type    | Required | Description                       |
| ----------- | -------- | ------- | -------- | --------------------------------- |
| symbolId    | query    | string  | No       | Symbol ID; default empty          |
| fromId      | query    | number  | No       | Start ID; default 0               |
| pageSize    | query    | integer | No       | Page size, default 20             |
| orderId     | query    | number  | Yes      | Order ID                          |
| X-EC-APIKEY | header   | string  | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1734423281500,
      "tradeId": 1842870487400627500,
      "orderId": 1842867159950237700,
      "aid": 1757195645905643800,
      "symbolId": "BTC-SWAP-USDT",
      "basicTokenId": "BTC-SWAP-USDT",
      "pricingTokenId": "USDT",
      "tradePrice": "107022.6",
      "tradeQuantity": "100",
      "tradeAmount": "10702260",
      "costTokenId": "USDT",
      "cost": "0.214",
      "tradeType": 1,
      "side": 2,
      "executedAmount": null,
      "pnl": "0",
      "orderPriceType": 1,
      "forceCloseOrderType": 0
    }
  ]
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                   | Type     | Required | Description                                                                              |
| ---------------------- | -------- | -------- | ---------------------------------------------------------------------------------------- |
| » msg                  | string   | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » code                 | string   | true     | Response status code, 0-success, non-0-failure                                           |
| » data                 | [object] | true     | none                                                                                     |
| »» time                | number   | true     | none                                                                                     |
| »» tradeId             | string   | true     | none                                                                                     |
| »» orderId             | string   | true     | none                                                                                     |
| »» aid                 | number   | true     | none                                                                                     |
| »» symbolId            | string   | true     | none                                                                                     |
| »» basicTokenId        | string   | true     | none                                                                                     |
| »» pricingTokenId      | string   | true     | none                                                                                     |
| »» tradePrice          | string   | true     | none                                                                                     |
| »» tradeQuantity       | string   | true     | none                                                                                     |
| »» tradeAmount         | string   | true     | none                                                                                     |
| »» costTokenId         | string   | true     | none                                                                                     |
| »» cost                | string   | true     | none                                                                                     |
| »» tradeType           | integer  | true     | none                                                                                     |
| »» side                | integer  | true     | none                                                                                     |
| »» executedAmount      | string   | true     | none                                                                                     |
| »» pnl                 | string   | true     | none                                                                                     |
| »» orderPriceType      | integer  | true     | none                                                                                     |
| »» forceCloseOrderType | integer  | true     | none                                                                                     |
| »» truthCost           | string   | true     | none                                                                                     |
| »» trialFundCost       | string   | true     | none                                                                                     |
| »» offsetFundCost      | string   | true     | none                                                                                     |

## GET Position Mode

GET /uapi/contract/v1/get/position/mode

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type   | Required | Description                       |
| ----------- | -------- | ------ | -------- | --------------------------------- |
| symbolId    | query    | string | Yes      | Symbol ID                         |
| X-EC-APIKEY | header   | string | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": {
    "cross": 0,
    "symbolId": "ETH-SWAP-USDT",
    "flag": true
  }
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name        | Type    | Required | Constraints | Description                                                                              |
| ----------- | ------- | -------- | ----------- | ---------------------------------------------------------------------------------------- |
| » msg       | string  | true     | none        | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » code      | string  | true     | none        | Response status code, 0-success, non-0-failure                                           |
| » data      | object  | true     | none        | payload                                                                                  |
| »» symbolId | string  | true     | none        | symbol ID                                                                                |
| »» flag     | boolean | true     | none        | modifiable                                                                               |
| »» cross    | integer | true     | none        | 1-cross, 0-isolated                                                                      |

## POST Set Position Mode

POST /uapi/contract/v1/set/position/mode

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name        | Location | Type    | Required | Description                       |
| ----------- | -------- | ------- | -------- | --------------------------------- |
| symbolId    | query    | string  | Yes      | Symbol                            |
| cross       | query    | integer | Yes      | 1 cross, 0 isolated               |
| X-EC-APIKEY | header   | string  | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": true
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name   | Type    | Required | Description                                                                              |
| ------ | ------- | -------- | ---------------------------------------------------------------------------------------- |
| » code | string  | true     | Response status code, 0-success, non-0-failure                                           |
| » msg  | string  | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data | boolean | true     | true                                                                                     |

## POST Modify Margin

POST /uapi/contract/v1/modify/margin

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name           | Location | Type    | Required | Description                       |
| -------------- | -------- | ------- | -------- | --------------------------------- |
| symbolId       | query    | string  | Yes      | Symbol                            |
| type           | query    | integer | Yes      | 1 increase; 2 decrease            |
| amount         | query    | string  | Yes      | Amount                            |
| positionIndex  | query    | number  | No       | Default 0                         |
| positionDirect | query    | integer | Yes      | 1 long; 0                         |
| X-EC-APIKEY    | header   | string  | Yes      | Apikey, contact support to obtain |

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": true
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name   | Type    | Required | Description                                                                              |
| ------ | ------- | -------- | ---------------------------------------------------------------------------------------- |
| » code | string  | true     | Response status code, 0-success, non-0-failure                                           |
| » msg  | string  | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » data | boolean | true     | true                                                                                     |

## GET Query Order Details

GET /uapi/contract/v1/order

<pre>
Trading APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

| Name          | Location | Type    | Required | Description                          |
| ------------- | -------- | ------- | -------- | ------------------------------------ |
| clientOrderId | query    | number  | No       | Client order ID, prefix `uapi_`      |
| orderId       | query    | number  | No       | Order ID                             |
| orderType     | query    | integer | No       | Order type 1: regular 2: conditional |
| X-EC-APIKEY   | header   | string  | Yes      | Apikey, contact support to obtain    |

#### Details

**clientOrderId**: Client order id, fixed prefix `uapi_`
Example: uapi_MnwkeCGHqGGdg6SfLtXrsltMex27vkh8

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": [
    {
      "time": 1734946163513,
      "orderId": 1847256737549172500,
      "aid": 1325347180177789400,
      "clientOrderId": "1734946162964",
      "symbolId": "BTC-SWAP-USDT",
      "basicTokenId": "BTC-SWAP-USDT",
      "pricingTokenId": "USDT",
      "orderPrice": "96879.7",
      "originQuantity": "100",
      "executedQuantity": "0",
      "executedAmount": "0",
      "executedPrice": "",
      "executedOrderId": 0,
      "averagePrice": "0",
      "orderType": 1,
      "side": 2,
      "feeInfoList": [],
      "orderStatus": 0,
      "lever": "100",
      "orderDirection": 0,
      "orderPriceType": 0,
      "touchOffPrice": "",
      "touchOffTime": 0,
      "noExecutedQty": "100",
      "marginLock": "9.6879",
      "intentionType": 0,
      "originalIntentionType": 0,
      "touchOffCondition": 0,
      "closeDirectionType": 0,
      "takeProfitStopLossType": 0,
      "forceCloseOrder": 0,
      "forceCloseOrderType": 0,
      "forceClosePrice": "",
      "pnl": "",
      "cross": 0,
      "inForTime": ""
    }
  ]
}
```

### Response

| Status Code | Meaning                                                 | Description | Data Model |
| ----------- | ------------------------------------------------------- | ----------- | ---------- |
| 200         | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | none        | Inline     |

### Response Schema

Status code **200**

| Name                      | Type     | Required | Description                                                                              |
| ------------------------- | -------- | -------- | ---------------------------------------------------------------------------------------- |
| » msg                     | string   | true     | Response message, when code = 0, message = "success"; when code != 0, shows error reason |
| » code                    | string   | true     | Response status code, 0-success, non-0-failure                                           |
| » data                    | object   | true     | none                                                                                     |
| »» time                   | number   | true     | time                                                                                     |
| »» tradeId                | string   | true     | trade ID                                                                                 |
| »» orderId                | string   | true     | order ID                                                                                 |
| »» aid                    | number   | true     | account ID                                                                               |
| »» symbolId               | string   | true     | symbol ID                                                                                |
| »» basicTokenId           | string   | true     | base token ID                                                                            |
| »» pricingTokenId         | string   | true     | quote token ID                                                                           |
| »» orderPrice             | string   | true     | price                                                                                    |
| »» originQuantity         | string   | true     | quantity                                                                                 |
| »» executedQuantity       | string   | true     | executed quantity                                                                        |
| »» executedAmount         | string   | true     | executed amount                                                                          |
| »» executedPrice          | string   | true     | executed price                                                                           |
| »» executedOrderId        | string   | true     | executed order ID                                                                        |
| »» averagePrice           | string   | true     | average price                                                                            |
| »» orderType              | integer  | true     | 1: regular 2: conditional                                                                |
| »» side                   | integer  | true     | 1: buy open long 2: sell open short 3: buy close long 4: sell close short                |
| »» feeInfoList            | [string] | true     | fees                                                                                     |
| »» orderStatus            | integer  | true     | 0: create 1: partial 2: filled 4: cancel 8: reject                                       |
| »» lever                  | string   | true     | leverage                                                                                 |
| »» orderDirection         | integer  | true     | 1: close 0: open                                                                         |
| »» orderPriceType         | integer  | true     | 1: input price 5: market price                                                           |
| »» touchOffPrice          | string   | true     | trigger price                                                                            |
| »» touchOffTime           | integer  | true     | trigger time                                                                             |
| »» noExecutedQty          | string   | true     | unfilled quantity                                                                        |
| »» marginLock             | string   | true     | margin                                                                                   |
| »» intentionType          | integer  | true     | planned order type (see above)                                                           |
| »» originalIntentionType  | integer  | true     | planned order type (see above)                                                           |
| »» touchOffCondition      | integer  | true     | 0: latest 1: index 2: mark                                                               |
| »» closeDirectionType     | integer  | true     | 0: close only closeable 1: close all                                                     |
| »» takeProfitStopLossType | integer  | true     | 0: position TP/SL 1: quantity TP/SL                                                      |
| »» forceCloseOrder        | integer  | true     | 1: forced close 2: non-forced                                                            |
| »» forceCloseOrderType    | integer  | true     | 0: non-liquidation 1: liquidation close 2: liquidation reduction                         |
| »» forceClosePrice        | string   | true     | forced close price                                                                       |
| »» pnl                    | string   | true     | P&L                                                                                      |
| »» cross                  | integer  | true     | 1: cross 0: isolated                                                                     |
