# WebSocket API

> WebSocket provides real-time data push services.

## EndPoint

Channel | Endpoint | Signature
------------ |--------------------------------------------| -----------
Market | wss://uapi.echobit.com/uapi/exchange/ws    | No
Funding Rate | wss://uapi.echobit.com/uapi/ws/inform     | No
Business | wss://uapi.echobit.com/uapi/ws/information | Yes

## Connection

- Connection rate limit: 60/minute (per API key)
- Max connections: 5

### Heartbeat

> After a successful WebSocket connection, the client needs to send a heartbeat message (ping), and the server will reply with a heartbeat message (pong). <br/>
> If no heartbeat message is received within 60 seconds, the server will close the connection.

Ping message:

```json
{
  "ping": 1764579210000
}
```

Pong message:

```json
{
  "pong": 1764579210000
}
```

## sub

###  Subscription Reqeust Example
```json
{
    "topic": "contract_position",
    "event": "sub",
    "params": {
    }
}

```

### Subscription Response Example

```json
{
  "code": "200",
  "topic": "contract_position",
  "event": "subbed"
}
```
> **Note:**
>
> * Subscribing to `/uapi/exchange/ws` returns **no `subbed` event** upon successful subscription;
> * Subscribing to `/uapi/ws/inform` returns a **`subbed` event** upon successful subscription;
> * Subscribing to `/uapi/ws/information` returns a **`subbed` event** upon successful subscription.


## unsub

### Unsubscription Reqeust Example
```json
{
    "topic": "contract_position",
    "event": "cancel",
    "params": {
    }
}
```

### Unsubscription Response Example
```json
{
  "code": "200",
  "topic": "contract_position",
  "event": "canceled"
}
```

## Signature

### Java

```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import javax.xml.bind.DatatypeConverter;
import java.io.IOException;

public class SignatureHelper {
    public static String sign(String message, String secret) {
        try {
            Mac sha256_HMAC = Mac.getInstance("HmacSHA256");
            SecretKeySpec secretKeySpec = new SecretKeySpec(secret.getBytes(), "HmacSHA256");
            sha256_HMAC.init(secretKeySpec);
            byte[] hash = sha256_HMAC.doFinal(message.getBytes());
            return DatatypeConverter.printHexBinary(hash).toLowerCase();
        } catch (Exception e) {
            throw new RuntimeException("Unable to sign message.", e);
        }
    }

    public static void main(String[] args) throws IOException {
        String apiKey = "Replace your apiKey";
        String apiSecret = "Replace your secretKey";
        long timestamp = System.currentTimeMillis();

        String originStr = "timestamp=" + timestamp;
        String signature = sign(originStr, apiSecret);
        System.out.println(timestamp);
        System.out.println(signature);
    }
}
```

### Shell

```bash
apiSecret="Replace your secretKey"
timestamp="Replace your millisecond timestamp"
originStr="timestamp=${timestamp}"
signature=$(printf "%s" "$originStr" | openssl dgst -sha256 -hmac "$apiSecret" | awk '{print $NF}')
echo "$timestamp"
echo "$signature"
```
