# WebSocket Market API

> Provides real-time market data push.
> No signature required.

## EndPoint

Name | base endpoint
------------ | ------------
websocket | wss://uapi.echobit.com/uapi/exchange/ws

## Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|timestamp|query|string| Yes |Current UTC timestamp (ms)
|X-EC-APIKEY| header or cookie or query |string| YES |Apikey, contact support to obtain; <br/> Priority: header > cookie > query

# Market WS

## Subscription Params

```json
{
  "id": "quotesData",
  "topic": "quotesData",
  "event": "sub",
  "params": {
  }
}
```

## Response Example

```json
{
    "topic": "quotesData",
    "params": {
        "realtimeInterval": "24h"
    },
    "data": [
        {
            "t": 0,
            "s": "SHIBUSDT",
            "sn": "SHIBUSDT",
            "c": "0.000080001",
            "h": "0.000080001",
            "l": "0.000080001",
            "o": "0.000080001",
            "v": "0",
            "qv": "0",
            "m": "0",
            "f": false
        }
    ],
    "f": false,
    "sendTime": 1733727904000,
    "id": "quotesData"
}
```

## Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|topic|string|Yes|Topic|
|params|object|Yes|Param object|
|» realtimeInterval|string|Yes|Realtime interval|
|data|[object]|Yes|Data array|
|»» t|integer|Yes|timestamp|
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
|f|boolean|Yes|flag|
|sendTime|integer|Yes|send time|
|id|string|Yes|request id|

# Depth

## Subscription Params

```json
{
    "id": "depth.BTCUSDT",
    "topic": "depth",
    "event": "sub",
    "symbol": "BTCUSDT",
    "params": {
    }
}
```

## Response Example

```json
{
    "symbol": "BTCUSDT",
    "symbolName": "BTCUSDT",
    "topic": "depth",
    "params": {
        "realtimeInterval": "24h"
    },
    "data": [
        {
            "s": "BTCUSDT",
            "t": 1733727899915,
            "v": "413781_18",
            "b": [
                [
                    "69550",
                    "34.570518"
                ]
            ],
            "a": [
                [
                    "94000",
                    "0.084125"
                ]
            ],
            "o": 0
        }
    ],
    "f": true,
    "sendTime": 1733728120685,
    "id": "depth.BTCUSDT"
}
```

## Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|symbol|string|Yes|symbol|
|symbolName|string|Yes|symbol name|
|topic|string|Yes|topic|
|params|object|Yes|param object|
|» realtimeInterval|string|Yes|realtime interval|
|data|[object]|Yes|data array|
|»» s|string|Yes|symbol|
|»» t|integer|Yes|timestamp|
|»» v|string|Yes|version|
|»» b|array|Yes|bids depth|
|»» a|array|Yes|asks depth|
|»» o|integer|Yes|operation type|
|f|boolean|Yes|flag|
|sendTime|integer|Yes|send time|
|id|string|Yes|request id|

# Klines

## Subscription Params

```json
{
    "id": "kline_BTCUSDT15m",
    "topic": "kline_15m",
    "event": "sub",
    "symbol": "BTCUSDT",
    "params": {
        "klineType": "15m",
        "realtimeInterval": "24h",
        "limit": 100
    }
}
```

> **Supported Time:** 1m, 3m, 5m, 15m, 30m, 1h, 2h, 4h, 6h, 12h, 1d, 1w, 1M
>
> * Fill in `id`, `topic`, and `params.klineType` according to the selected Time type.


## Response Example

```json
{
    "symbol": "BTCUSDT",
    "symbolName": "BTCUSDT",
    "topic": "kline",
    "params": {
        "realtimeInterval": "24h",
        "klineType": "15m"
    },
    "data": [
        {
            "t": 1733726700000,
            "s": "BTCUSDT",
            "sn": "BTCUSDT",
            "c": "94000",
            "h": "94000",
            "l": "94000",
            "o": "94000",
            "v": "0"
        }
    ],
    "f": true,
    "sendTime": 1733728189559,
    "id": "kline_BTCUSDT15m"
}
```

## Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|symbol|string|Yes|symbol|
|symbolName|string|Yes|symbol name|
|topic|string|Yes|topic|
|params|object|Yes|param object|
|» realtimeInterval|string|Yes|realtime interval|
|» klineType|string|Yes|kline type|
|data|[object]|Yes|data array|
|»» t|integer|Yes|timestamp|
|»» s|string|Yes|symbol|
|»» sn|string|Yes|symbol name|
|»» c|string|Yes|close|
|»» h|string|Yes|high|
|»» l|string|Yes|low|
|»» o|string|Yes|open|
|»» v|string|Yes|volume|
|f|boolean|Yes|flag|
|sendTime|integer|Yes|send time|
|id|string|Yes|request id|

# Mark Klines

## Subscription Params

```json
{
    "id": "markKline_TRXUSDT_1m",
    "topic": "markKline_1m",
    "event": "sub",
    "limit": 1,
    "symbol": "TRXUSDT",
    "params": {
    }
}
```

## Response Example

```json
{
    "symbol": "BTCUSDT",
    "symbolName": "BTCUSDT",
    "topic": "markKline",
    "params": {
        "limit": "2",
        "realtimeInterval": "24h",
        "klineType": "15m"
    },
    "data": [
        {
            "t": 1733726700000,
            "s": "BTCUSDT",
            "sn": "BTCUSDT",
            "c": "94000",
            "h": "94000",
            "l": "94000",
            "o": "94000",
            "v": "0"
        }
    ],
    "f": true,
    "sendTime": 1733728189559,
    "id": "markKline_BTCUSDT15m"
}
```


> **Supported Time:** 1m, 3m, 5m, 15m, 30m, 1h, 2h, 4h, 6h, 12h, 1d, 1w, 1M
>
> * Fill in `id`, `topic`, and `params.klineType` according to the selected Time type.


## Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|symbol|string|Yes|symbol|
|symbolName|string|Yes|symbol name|
|topic|string|Yes|topic|
|params|object|Yes|param object|
|» realtimeInterval|string|Yes|realtime interval|
|» klineType|string|Yes|kline type|
|data|[object]|Yes|data array|
|»» t|integer|Yes|timestamp|
|»» s|string|Yes|symbol|
|»» sn|string|Yes|symbol name|
|»» c|string|Yes|close|
|»» h|string|Yes|high|
|»» l|string|Yes|low|
|»» o|string|Yes|open|
|»» v|string|Yes|volume|
|f|boolean|Yes|flag|
|sendTime|integer|Yes|send time|
|id|string|Yes|request id|

# Index Klines

## Subscription Params

```json
{
    "id": "indexKline_BTCUSDT15m",
    "topic": "indexKline_15m",
    "event": "sub",
    "symbol": "BTCUSDT",
    "params": {
        "klineType": "15m",
        "realtimeInterval": "24h",
        "limit": 2
    }
}
```

> **Supported Time:** 1m, 3m, 5m, 15m, 30m, 1h, 2h, 4h, 6h, 12h, 1d, 1w, 1M
>
> * Fill in `id`, `topic`, and `params.klineType` according to the selected Time type.



## Response Example

```json
{
    "symbol": "BTCUSDT",
    "symbolName": "BTCUSDT",
    "topic": "indexKline_15m",
    "params": {
        "limit": "2",
        "realtimeInterval": "24h",
        "klineType": "15m"
    },
    "data": [
        {
            "t": 1733726700000,
            "s": "BTCUSDT",
            "sn": "BTCUSDT",
            "c": "94000",
            "h": "94000",
            "l": "94000",
            "o": "94000",
            "v": "0"
        }
    ],
    "f": true,
    "sendTime": 1733728189559,
    "id": "indexKline_BTCUSDT15m"
}
```

## Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|symbol|string|true|symbol|
|symbolName|string|true|symbol name|
|topic|string|true|topic|
|params|object|true|param object|
|» limit|string|true|limit|
|» realtimeInterval|string|true|realtime interval|
|» klineType|string|true|kline type|
|data|[object]|true|data array|
|»» t|integer|true|timestamp|
|»» s|string|true|symbol|
|»» sn|string|true|symbol name|
|»» c|string|true|close|
|»» h|string|true|high|
|»» l|string|true|low|
|»» o|string|true|open|
|»» v|string|true|volume|
|f|boolean|true|flag|
|sendTime|integer|true|send time|
|id|string|true|request id|

# Recent Trades

## Subscription Params

```json
{
  "id": "trade.BTCUSDT",
  "topic": "trade",
  "event": "sub",
  "symbol": "BTCUSDT",
  "params": {
  }
}
```

## Response Example

```json
{
    "symbol": "BTCUSDT",
    "symbolName": "BTCUSDT",
    "topic": "trade",
    "params": {
        "realtimeInterval": "24h"
    },
    "data": [
        {
            "v": "1828423721862578177",
            "t": 1732701092881,
            "p": "93421.82",
            "q": "0.00095",
            "f": false,
            "m": false
        }
    ],
    "f": true,
    "sendTime": 1733728274833,
    "id": "trade.BTCUSDT"
}
```

## Response Schema

|Name|Type|Required|Description|
|---|---|---|---|
|symbol|string|Yes|symbol|
|symbolName|string|Yes|symbol name|
|topic|string|Yes|topic|
|params|object|Yes|param object|
|» realtimeInterval|string|Yes|realtime interval|
|data|[object]|Yes|data array|
|»» v|string|Yes|version|
|»» t|integer|Yes|timestamp|
|»» p|string|Yes|price|
|»» q|string|Yes|quantity|
|»» f|boolean|Yes|isVirtual|
|»» m|boolean|Yes|isMaker|
|f|boolean|Yes|flag|
|sendTime|integer|Yes|send time|
|id|string|Yes|request id|
