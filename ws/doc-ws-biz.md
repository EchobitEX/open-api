# Business WebSocket API

> WebSocket provides real-time business data push.
> Signed access required.

## WebSocket EndPoint

Name | base endpoint
------------ | ------------
websocket | wss://uapi.echobit.com/uapi/ws/information

## Parameters

|Name| Location            |Type|Required|Description|
|---|---------------------|---|---|---|
|timestamp| query               |string| Yes |Current UTC timestamp (ms)
|signature| query               |string| Yes |Signature: see examples
|X-EC-APIKEY| header or cookie or query |string| YES |Apikey, contact support to obtain; <br/> Priority: header > cookie > query

# Spot Orders / Spot Assets

## Filled Trades

### Subscription Params

```json
{
  "id": "coin_history_trade",
  "topic": "coin_history_trade",
  "event": "sub",
  "params": {

  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "coin_history_trade",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "coin_history_trade",
  "event": "sub",
  "data": [
    {
      "time": "time",
      "tradeId": "trade ID",
      "orderId": "order ID",
      "aid": "account ID",
      "symbolId": "symbol ID",
      "basicTokenId": "base token ID",
      "pricingTokenId": "quote token ID",
      "tradePrice": "price",
      "tradeQuantity": "quantity",
      "tradeAmount": "amount",
      "costTokenId": "fee token",
      "cost": "fee",
      "tradeType": "1: limit 2: market",
      "side": "1: buy 2: sell"
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|Yes|Response status code, 0-success, non-0-failure|
|topic|string|Yes|Topic|
|event|string|Yes|Event type|
|data|[object]|Yes|Data array|
|» time|string|Yes|time|
|» tradeId|string|Yes|trade ID|
|» orderId|string|Yes|order ID|
|» aid|string|Yes|account ID|
|» symbolId|string|Yes|symbol ID|
|» basicTokenId|string|Yes|base token ID|
|» pricingTokenId|string|Yes|quote token ID|
|» tradePrice|string|Yes|trade price|
|» tradeQuantity|string|Yes|trade quantity|
|» tradeAmount|string|Yes|trade amount|
|» costTokenId|string|Yes|fee token|
|» cost|string|Yes|fee|
|» tradeType|string|Yes|1: limit 2: market|
|» side|string|Yes|1: buy 2: sell|

## Current Orders

### Subscription Params

```json
{
  "id": "coin_current_order",
  "topic": "coin_current_order",
  "event": "sub",
  "params": {
  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "coin_current_order",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "coin_current_order",
  "event": "sub",
  "data": [
    {
      "time": 1764139752492,
      "orderId": "2092150313360414208",
      "userId": "",
      "aid": 1904423274357580000,
      "clientOrderId": "1764139752333",
      "symbolId": "ETHUSDT",
      "basicTokenId": "ETH",
      "pricingTokenId": "USDT",
      "orderPrice": "2940.4",
      "originQuantity": "1",
      "executedQuantity": "0",
      "executedAmount": "0",
      "averagePrice": "0",
      "orderType": 1,
      "side": 1,
      "feeInfoList": [],
      "orderStatus": 0
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|Yes|Response status code, 0-success, non-0-failure|
|topic|string|Yes|Topic|
|event|string|Yes|Event type|
|data|[object]|Yes|Data array|
|» time|string|Yes|time|
|» orderId|string|Yes|order ID|
|» aid|string|Yes|account ID|
|» clientOrderId|string|Yes|client order ID|
|» symbolId|string|Yes|symbol ID|
|» basicTokenId|string|Yes|base token ID|
|» pricingTokenId|string|Yes|quote token ID|
|» orderPrice|string|Yes|order price|
|» originQuantity|string|Yes|order quantity|
|» executedQuantity|string|Yes|executed quantity|
|» executedAmount|string|Yes|executed amount|
|» averagePrice|string|Yes|average buy price|
|» orderType|string|Yes|1: limit 2: market|
|» side|string|Yes|1: buy 2: sell|
|» feeInfoList|array|Yes|fee info list|
|» orderStatus|string|Yes|0: created 1: partial 2: filled 4: canceled|

## Completed Orders

### Subscription Params

```json
{
  "id": "coin_order_finish",
  "topic": "coin_order_finish",
  "event": "sub",
  "params": {

  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "coin_order_finish",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "coin_order_finish",
  "event": "sub",
  "data": [
    {
      "time": "time",
      "orderId": "order ID",
      "aid": "account ID",
      "clientOrderId": "client order ID",
      "symbolId": "symbol ID",
      "basicTokenId": "base token ID",
      "pricingTokenId": "quote token ID",
      "orderPrice": "order price",
      "originQuantity": "order quantity",
      "executedQuantity": "executed quantity",
      "executedAmount": "executed amount",
      "averagePrice": "average buy price",
      "orderType": "1: limit 2: market",
      "side": "1: buy 2: sell",
      "feeInfoList": [],
      "orderStatus": "0: created 1: partial 2: filled 4: canceled"
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|true|Response status code, 0-success, non-0-failure|
|topic|string|true|Topic|
|event|string|true|Event type|
|data|[object]|true|Data array|
|» time|string|true|time|
|» orderId|string|true|order ID|
|» aid|string|true|account ID|
|» clientOrderId|string|true|client order ID|
|» symbolId|string|true|symbol ID|
|» basicTokenId|string|true|base token ID|
|» pricingTokenId|string|true|quote token ID|
|» orderPrice|string|true|order price|
|» originQuantity|string|true|order quantity|
|» executedQuantity|string|true|executed quantity|
|» executedAmount|string|true|executed amount|
|» averagePrice|string|true|average buy price|
|» orderType|string|true|1: limit 2: market|
|» side|string|true|1: buy 2: sell|
|» feeInfoList|array|string|true|fee info list|
|» orderStatus|string|true|order status|

## Spot Assets

### Subscription Params

```json
{
  "id": "coin_property",
  "topic": "coin_property",
  "event": "sub",
  "params": {

  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "coin_property",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "coin_property",
  "event": "sub",
  "data": [
    {"tokenId":"tokenId","tokenName":"token name","positionLock":"lock","totalValue":"total","useable":"available","uTotalValue":"total in USDT"}
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|true|Response status code, 0-success, non-0-failure|
|topic|string|true|Topic|
|event|string|true|Event type|
|data|[object]|true|Data array|
|» tokenId|string|true|Token ID|
|» tokenName|string|true|Token name|
|» positionLock|string|true|Locked amount|
|» totalValue|string|true|Asset total|
|» useable|string|true|Available amount|
|» uTotalValue|string|true|Total (USDT)|

## Spot Plan Orders

### Subscription Params

```json
{
  "id": "coin_plan_order",
  "topic": "coin_plan_order",
  "event": "sub",
  "params": {

  }
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "coin_plan_order",
  "event": "sub",
  "data": [
    {
      "time": "1732786291601",
      "orderId": "1829138420527537920",
      "aid": "1325347180177789441",
      "clientOrderId": "1732786291223",
      "symbolId": "BTCUSDT",
      "basicTokenId": "BTC",
      "pricingTokenId": "USDT",
      "orderPrice": "93412.04",
      "originQuantity": "0.001",
      "orderType": 1,
      "side": 1,
      "orderStatus": 1,
      "touchOffPrice": "93400.04",
      "touchOffTime": "0",
      "pricingPrice": "93412.04",
      "executedOrderId": "0",
      "executedPrice": "0",
      "executedQuantity": "0",
      "updateTime": "1732786291601",
      "timeInForce": "GTC"
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|true|Response status code, 0-success, non-0-failure|
|topic|string|true|Topic|
|event|string|true|Event type|
|data|[object]|true|Data array|
|» time|string|true|time|
|» orderId|string|true|order ID|
|» aid|string|true|account ID|
|» clientOrderId|string|true|client order ID|
|» symbolId|string|true|symbol ID|
|» basicTokenId|string|true|base token ID|
|» pricingTokenId|string|true|quote token ID|
|» orderPrice|string|true|order price|
|» originQuantity|string|true|order quantity|
|» orderType|integer|true|order type|
|» side|integer|true|side|
|» orderStatus|integer|true|order status|
|» touchOffPrice|string|true|trigger price|
|» touchOffTime|string|true|trigger time|
|» pricingPrice|string|true|pricing price|
|» executedOrderId|string|true|executed order ID|
|» executedPrice|string|true|executed price|
|» executedQuantity|string|true|executed quantity|
|» updateTime|string|true|update time|
|» timeInForce|string|true|time in force|

# Futures Orders / Assets

## Futures Asset Balance

### Subscription Params

```json
{
  "id": "contract_property",
  "topic": "contract_property",
  "event": "sub",
  "params": {

  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "contract_property",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "contract_property",
  "event": "sub",
  "data": [
    {
      "tokenId": "USDT",
      "upnl": "-1",
      "walletBalanceValue": "90.45049604",
      "trialFund": "0",
      "offsetFund": "0",
      "giftVoucherValue": "0",
      "userableMarginValue": "71.03908388",
      "positionMarginValue": "18.41141216",
      "entrustMarginValue": "0",
      "transferableValue": "71.03908388",
      "totalValue": "90.45049604",
      "totalEquityValue": "89.45049604"
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|Yes|Response status code, 0-success, non-0-failure|
|topic|string|Yes|Topic|
|event|string|Yes|Event type|
|data|[object]|Yes|Data array|
|» tokenId|string|Yes|Token ID|
|» upnl|string|Yes|Unrealized PnL|
|» walletBalanceValue|string|Yes|Wallet balance|
|» trialFund|string|Yes|Trial fund|
|» offsetFund|string|Yes|Offset fund|
|» userableMarginValue|string|Yes|Available margin|
|» positionMarginValue|string|Yes|Position margin|
|» entrustMarginValue|string|Yes|Entrusted margin|
|» transferableValue|string|Yes|Transferable|
|» totalValue|string|Yes|Total assets|
|» totalEquityValue|string|Yes|Total equity|

## Futures Tradable Info

### Subscription Params

```json
{
  "id": "contract_can_trade",
  "topic": "contract_can_trade",
  "event": "sub",
  "params": {

  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "contract_can_trade",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "contract_can_trade",
  "event": "sub",
  "data": [
    {
      "tokenId": "FLOKI-SWAP-USDT",
      "longPositionValue": "0",
      "longAvailablePosition": "0",
      "shortPositionValue": "0",
      "shortAvailablePosition": "0",
      "profitLossConfig": {
        "availableMargin": "71.039083883537565726",
        "positionMargin": "0",
        "entrustMargin": "0",
        "realizedProfitLoss": "0",
        "upnl": "0"
      }
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|Yes|Response status code, 0-success, non-0-failure|
|topic|string|true|Topic|
|event|string|true|Event type|
|data|[object]|true|Data array|
|» tokenId|string|true|Symbol ID|
|» longPositionValue|string|true|Long position|
|» longAvailablePosition|string|true|Long closeable|
|» shortPositionValue|string|true|Short position|
|» shortAvailablePosition|string|true|Short closeable|
|» profitLossConfig|object|true|PnL config|
|»» availableMargin|string|true|Available margin|
|»» positionMargin|string|true|Position margin|
|»» entrustMargin|string|true|Entrusted margin|
|»» realizedProfitLoss|string|true|Realized PnL|
|»» upnl|string|true|Unrealized PnL|

## Futures Position

### Subscription Params

```json
{
  "id": "contract_position",
  "topic": "contract_position",
  "event": "sub",
  "params": {
  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "contract_position",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "contract_position",
  "event": "sub",
  "data": [
    {
      "positionId": 2087199914173983000,
      "positionWebId": "2087199914173982976",
      "symbolId": "TRX-SWAP-USDT",
      "symbolName": "TRX-SWAP-USDT",
      "lever": "9.24",
      "totalPosition": "10",
      "valueOfPosition": "161",
      "positionMargin": "18.41141",
      "minReductionMargin": "15.19141",
      "entrustMargin": "0",
      "averagePrice": "0.161",
      "estimateLiquidationPrice": "0.07214",
      "marginRatio": "0.1081",
      "indexPrice": "0.16",
      "contractPrice": "0.16",
      "availablePosition": "10",
      "availableMargin": "0",
      "positionDirect": 1,
      "realizedProfitLoss": "-0.1207",
      "upnl": "-1",
      "coin": "USDT",
      "pnlRatio": "-0.0543",
      "fixedLever": "20",
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
        "lossCloseType": 0,
        "profitOpenDelegationType": 0,
        "lossOpenDelegationType": 0,
        "profitDelegationInputPrice": "",
        "lossDelegationInputPrice": ""
      },
      "cross": 1,
      "finishedUpnl": "0",
      "valueOfPositionTotal": "161",
      "adlAlarmStatus": 1,
      "priceBenchmark": "0.16",
      "pnlRefPrice": "0.16"
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|Yes|Response status code, 0-success, non-0-failure|
|topic|string|true|Topic|
|event|string|true|Event type|
|data|[object]|true|Data array|
|» positionId|string|true|Position ID|
|» symbolId|string|true|Symbol ID|
|» lever|string|true|Leverage|
|» totalPosition|string|true|Position (lots)|
|» valueOfPosition|string|true|Position value|
|» positionMargin|string|true|Position margin|
|» minReductionMargin|string|true|Max reducible margin|
|» entrustMargin|string|true|Entrusted margin|
|» averagePrice|string|true|Avg open price|
|» estimateLiquidationPrice|string|true|Estimated liquidation price|
|» marginRatio|string|true|Margin ratio|
|» indexPrice|string|true|Index price|
|» contractPrice|string|true|Contract price|
|» availablePosition|string|true|Closeable quantity|
|» availableMargin|string|true|Available margin|
|» positionDirect|string|true|1=long, 0=short|
|» realizedProfitLoss|string|true|Realized PnL|
|» upnl|string|true|Unrealized PnL|
|» coin|string|true|Coin unit|
|» pnlRatio|string|true|Return ratio|
|» fixedLever|string|true|Fixed leverage|
|» profitLossConfig|object|true|TP/SL config|
|»» stopProfit|string|true|TP enabled|
|»» profitPrice|string|true|TP price|
|»» profitOrderId|string|true|TP order ID|
|»» profitTouchType|string|true|TP trigger: 0 latest, 1 index, 2 mark|
|»» profitCloseType|string|true|TP close: 0 partial, 1 all|
|»» stopLoss|string|true|SL enabled|
|»» lossPrice|string|true|SL price|
|»» lossOrderId|string|true|SL order ID|
|»» lossTouchType|string|true|SL trigger: 0 latest, 1 index, 2 mark|
|»» lossCloseType|string|true|SL close: 0 partial, 1 all|
|» cross|string|true|1 cross, 0 isolated|
|» finishedUpnl|string|true|Settled unrealized PnL|
|» valueOfPositionTotal|string|true|Cumulative open value|

## Futures Completed Orders

### Subscription Params

```json
{
  "id": "contract_order_finish",
  "topic": "contract_order_finish",
  "event": "sub",
  "params": {
  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "contract_order_finish",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "contract_order_finish",
  "event": "sub",
  "data": [
    {
      "time": "time",
      "orderId": "order ID",
      "aid": "account ID",
      "clientOrderId": "client order ID",
      "symbolId": "symbol ID",
      "basicTokenId": "base token ID",
      "pricingTokenId": "quote token ID",
      "orderPrice": "price",
      "originQuantity": "quantity",
      "executedQuantity": "executed quantity",
      "executedAmount": "executed amount",
      "averagePrice": "average price",
      "orderType": "1: regular 2: conditional",
      "side": "1: buy open long 2: sell open short 3: buy close long 4: sell close short",
      "orderStatus": "regular: 0 create 1 partial 2 filled 4 cancel 8 reject; conditional: 11 create 12 entrusted 13 rejected 14 canceled",
      "lever": "leverage",
      "orderDirection": "1 close, 0 open",
      "noExecutedQty": "unfilled",
      "amount": "amount",
      "marginLock": "margin"
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|Yes|Response status code, 0-success, non-0-failure|
|topic|string|true|Topic|
|event|string|true|Event type|
|data|[object]|true|Data array|
|» time|string|true|time|
|» orderId|string|true|order ID|
|» aid|string|true|account ID|
|» clientOrderId|string|true|client order ID|
|» symbolId|string|true|symbol ID|
|» basicTokenId|string|true|base token ID|
|» pricingTokenId|string|true|quote token ID|
|» orderPrice|string|true|price|
|» originQuantity|string|true|quantity|
|» executedQuantity|string|true|executed quantity|
|» executedAmount|string|true|executed amount|
|» averagePrice|string|true|average price|
|» orderType|string|true|1: regular 2: conditional|
|» side|string|true|1: buy open long 2: sell open short 3: buy close long 4: sell close short|
|» orderStatus|string|true|order status|
|» lever|string|true|leverage|
|» orderDirection|string|true|1 close, 0 open|
|» noExecutedQty|string|true|unfilled quantity|
|» amount|string|true|amount|
|» marginLock|string|true|margin|

## Futures Current Orders

### Subscription Params

```json
{
  "id": "contract_current_order",
  "topic": "contract_current_order",
  "event": "sub",
  "params": {
  }
}
```

### Response Example

```json
{
  "code": "200",
  "topic": "contract_current_order",
  "event": "subbed"
}
```

### Data Push Example

```json
{
  "code": "200",
  "topic": "contract_current_order",
  "event": "sub",
  "data": [
    {
      "time": 1764140005062,
      "orderId": "2092152431785924096",
      "aid": 1904423274357580000,
      "userId": "",
      "clientOrderId": "1764140004850",
      "symbolId": "ETH-SWAP-USDT",
      "basicTokenId": "",
      "pricingTokenId": "USDT",
      "orderPrice": "2946.2",
      "originQuantity": "1",
      "executedQuantity": "0",
      "executedAmount": "0",
      "executedPrice": "",
      "executedOrderId": "",
      "averagePrice": "0",
      "orderType": 1,
      "side": 1,
      "feeInfoList": [],
      "orderStatus": 0,
      "lever": "10",
      "orderDirection": 0,
      "orderPriceType": 1,
      "touchOffPrice": "",
      "touchOffTime": 0,
      "noExecutedQty": "1",
      "amount": "2946.2",
      "marginLock": "2.9462",
      "intentionType": 0,
      "originalIntentionType": 0,
      "touchOffCondition": 0,
      "closeDirectionType": 0,
      "takeProfitStopLossType": 0,
      "forceCloseOrder": 2,
      "forceCloseOrderType": 0,
      "forceClosePrice": "0",
      "pnl": "",
      "cross": 0,
      "openPositionAvgPrice": "",
      "avgLeverage": 0,
      "updateTime": 0,
      "remark": "",
      "quotePrice": "",
      "positionIndex": 0,
      "parentUid": "",
      "parentRemark": ""
    }
  ]
}
```

### Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|true|Return code|
|topic|string|true|Topic|
|event|string|true|Event type|
|data|[object]|true|Data array|
|» time|string|true|time|
|» orderId|string|true|order ID|
|» aid|string|true|account ID|
|» clientOrderId|string|true|client order ID|
|» symbolId|string|true|symbol ID|
|» basicTokenId|string|true|base token ID|
|» pricingTokenId|string|true|quote token ID|
|» orderPrice|string|true|order price|
|» originQuantity|string|true|order quantity|
|» executedQuantity|string|true|executed quantity|
|» executedPrice|string|true|executed price|
|» executedOrderId|string|true|executed order ID|
|» orderType|string|true|1: regular 2: conditional|
|» side|string|true|1: buy open long 2: sell open short 3: buy close long 4: sell close short|
|» orderStatus|string|true|regular 0:create 1:partial 2:filled 4:cancel 8:reject; conditional 11:create 12:entrusted 13:rejected 14:canceled|
|» lever|string|true|leverage|
|» orderPriceType|string|true|1: input price 5: market price|
|» touchOffPrice|string|true|trigger price|
|» touchOffTime|string|true|trigger time|
|» intentionType|string|true|planned order type|
|» touchOffCondition|string|true|0: latest 1: index 2: mark|
|» takeProfitStopLossType|string|true|0: position TP/SL 1: quantity TP/SL|
