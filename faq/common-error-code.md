# error code 

code = "0", request success.
code != "0", request failed.


## -1002
### possible reason :

- The X-EC-APIKEY field in the header is not filled in.

### eg
```json
{
    "msg": "You are not authorized to execute this request",
    "code": "-1002",
    "data": ""
}
```

## -2015 

possible reason :

- Incorrect apiKey entered.
- ApiKey not enabled.
- The requested IP is not in your configured IP whitelist.

### eg
```json
{
    "msg": "Invalid API-key, IP, or permissions for action.",
    "code": "-2015",
    "data": ""
}
```

## 30003
possible reason :

- Request parameters are not within the valid range
  - eg: The `/exapi/spot/v1/order` interface side only supports values 1 and 2; however, the input value is 3.

### eg
```json
{
    "msg": "Request parameter verification error",
    "code": "30003",
    "data": ""
}
```