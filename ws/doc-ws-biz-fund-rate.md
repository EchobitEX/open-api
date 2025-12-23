# EndPoint

Name | base endpoint
------------ | ------------
websocket | wss://uapi.echobit.com/uapi/ws/inform

# Funding Rates

## Parameters

|Name| Location                  |Type|Required|Description|
|---|---------------------------|---|---|---|
|timestamp| query                     |string| Yes |Current UTC timestamp (ms)
|X-EC-APIKEY| header or cookie or query |string| YES |Apikey, contact support to obtain; <br/> Priority: header > cookie > query

## Subscription Params

```json
{
  "id": "fund_rates",
  "topic": "fund_rates",
  "event": "sub"
}
```

## Data Push Example

```json
{
  "code": "200",
  "topic": "fund_rates",
  "event": "sub",
  "data": [
    {
      "symbolId": "BTC-SWAP-USDT",
      "currentTime": "1736927447995",
      "settleTime": 1736913600000,
      "settleRate": "0.000005286201335189",
      "nextSettleTime": 1736942400000,
      "fundRate": "-0.000001065727100968"
    }
  ]
}
```

## Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|code|string|Yes|Response status code, 0-success, non-0-failure|
|topic|string|Yes|Topic|
|event|string|Yes|Event type|
|data|[object]|Yes|Data array|
|» symbolId|string|Yes|Symbol|
|» currentTime|string|Yes|Server time|
|» settleTime|integer|Yes|Current settlement time|
|» settleRate|string|Yes|Current funding rate|
|» nextSettleTime|integer|Yes|Next settlement time|
|» fundRate|string|Yes|Predicted funding rate|
