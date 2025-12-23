# Documentation

> APIs are divided into unauthenticated and signed APIs. See [API Signature](#api-signature) for signing details.

## EndPoint

Name | base endpoint
------------ | ------------
rest-api | https://uapi.echobit.com

## API Response

Format:
```json
{
    "msg": "success",
    "code": "0",
    "data": ""
}
```

Description

Name  | Location       | Type   | Required | Description
------------ |--------------|--------|------------| ------------ | 
`code` | ResponseBody | string | `YES`      | Response status code, 0-success, non-0-failure
`msg`  | ResponseBody | string | `YES`      | Response message, when code = 0, message = "success"; when code != 0, shows error reason
`data`| ResponseBody  | any    | `YES`      | Response payload


## Authentication & Rate Limits

Category       | Rate           | Signature   
--------------|--------------|-------| 
Common APIs - GET   | 1200 per 60s     | NO
Market Data - GET   | 1200 per 60s     | NO 
Account - GET      | 300 per 60s      | YES
Spot Trading - POST  | 300 per 60s      | YES
Spot Trading - GET   | 300 per 60s      | YES
Futures Trading - POST  | 300 per 60s      | YES
Futures Trading - GET   | 300 per 60s      | YES



# API Signature

## Credentials
> Except for unauthenticated APIs, all requests must include: <br/>
> `query` must contain `timestamp` and `signature`; <br/>
> `header` must contain `X-EC-APIKEY`;

Name| Location | Type        | Required | Description
------------ |--------|-----------|------------| ------------ | 
`timestamp`  | query  | string    | `YES`      | Current UTC timestamp
`signature`  | query  | string    | `YES`      | Signature, see request example
`X-EC-APIKEY`| header | string    | `YES`      | Apikey, contact support to obtain

## Request Examples

### Java

Here we use `GET account balance` as an example to demonstrate signature generation and usage

```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import javax.xml.bind.DatatypeConverter;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class SignatureHelper {
  /**
   * Generate signature
   *
   * @param message plain text
   * @param secret  secret key
   * @return cipher text
   */
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
    String apiKey = "Replace with your apiKey";
    String secretKey = "Replace with your secretKey";

    String urlPrefix = "https://uapi.echobit.com/uapi/account/v1/available";
    StringBuilder queryParams = new StringBuilder();
    queryParams.append("tokenId=USDT");
    queryParams.append("&timestamp=").append(System.currentTimeMillis());

    String signature = sign(queryParams.toString(), secretKey);
    queryParams.append("&signature=").append(signature);

    URL url = new URL(urlPrefix + "?" + queryParams.toString());
    HttpURLConnection connection = (HttpURLConnection) url.openConnection();
    connection.setRequestMethod("GET");
    connection.setRequestProperty("X-EC-APIKEY", apiKey);
    
    int responseCode = connection.getResponseCode();
    System.out.println("Response Code: " + responseCode);

    try (BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));) {
      String inputLine;
      StringBuilder response = new StringBuilder();

      while ((inputLine = in.readLine()) != null) {
        response.append(inputLine);
      }
      System.out.println("Response Body: " + response.toString());
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}

```

### curl Example

```shell
curl --location --request GET 'https://uapi.echobit.com/uapi/account/v1/available?tokenId=USDT&timestamp=1754382518876&signature=bc55d18586293e926dd1ff4ffb5f33dce17b653924504fb43a76e4e0cec19b2e' \
--header 'X-EC-APIKEY: tKlfW7wURwNYgrqo9moajllpQcfRqFWe4f2KPpPNw1Vqqk64oL2wfbCfgGdAo99s'
```
