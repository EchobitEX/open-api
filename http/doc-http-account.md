# Account

## GET Team Membership

GET /uapi/account/v1/in/team

<pre>
Account APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|userId|query|string| Yes |User ID|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": {
    "status": 1
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
|»» status|integer|Yes|1: in team, 0: not in team|

## GET Account Balance

GET /uapi/account/v1/available

<pre>
Account APIs require signature;
Signature: query must include parameters `timestamp` and `signature`.
</pre>

### Request Parameters

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|tokenId|query|string| No |Token ID|
|X-EC-APIKEY|header|string| Yes |Apikey, contact support to obtain|

> Response Example

> 200 Response

```json
{
  "msg": "success",
  "code": "0",
  "data": {
    "walletBalanceValue": "1999.634244125",
    "trialFund": "0.000000000000000000"
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
|»» walletBalanceValue|string|Yes|Transferable balance|
|»» trialFund|string|Yes|Trial fund balance|

## GET User

GET /uapi/account/v1/user

<pre>
Account APIs require signature;
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
  "data": {
    "userId": 1611498967203393000
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
|»» userId|integer|Yes|User ID|
