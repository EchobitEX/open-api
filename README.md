# Open API Documentation

This directory contains the EchoBit platform's open API documentation, divided into two main parts: WebSocket API and HTTP API.

## Documentation Structure

### WebSocket API (`/ws` Directory)

WebSocket API provides real-time data push services, supporting market data, business data, and funding rate pushes.

#### Core Documents
- [`doc-ws.md`](./ws/doc-ws.md) - WebSocket API basic connection and signature methods
- [`doc-ws-quote.md`](./ws/doc-ws-quote.md) - Market data WebSocket API
- [`doc-ws-biz.md`](./ws/doc-ws-biz.md) - Business data WebSocket API
- [`doc-ws-biz-fund-rate.md`](./ws/doc-ws-biz-fund-rate.md) - Funding rate WebSocket API

#### WebSocket Endpoints
| Type | Endpoint | Signature Required |
|------|----------|-------------------|
| Market | wss://uapi.echobit.com/uapi/exchange/ws | No |
| Funding Rate | wss://uapi.echobit.com/uapi/ws/inform | No |
| Business | wss://uapi.echobit.com/uapi/ws/information | Yes |

### HTTP API (`/http` Directory)

HTTP API provides account management, spot trading, futures trading, and market data functions.

#### Core Documents
- [`doc-http.md`](./http/doc-http.md) - HTTP API basic information and signature methods
- [`doc-http-common.md`](./http/doc-http-common.md) - Common APIs (server time, trading pairs, etc.)
- [`doc-http-account.md`](./http/doc-http-account.md) - Account-related APIs
- [`doc-http-exchange-spot.md`](./http/doc-http-exchange-spot.md) - Spot trading APIs
- [`doc-http-exchange-future.md`](./http/doc-http-exchange-future.md) - Futures trading APIs
- [`doc-http-market-data.md`](./http/doc-http-market-data.md) - Market data APIs

#### HTTP Endpoint
- Base endpoint: `https://uapi.echobit.com`

### FAQ and Examples (`/faq` Directory)

- [`common-error-code.md`](./faq/common-error-code.md) - Common error codes and solutions
- [`ws_demo.html`](./faq/ws_demo.html) - WebSocket debugging tool and examples

## API Rate Limits

| Category | Rate Limit | Signature Required |
|----------|------------|-------------------|
| Common APIs - GET | 1200/60s | No |
| Market Data - GET | 1200/60s | No |
| Account - GET | 300/60s | Yes |
| Spot Trading - POST | 300/60s | Yes |
| Spot Trading - GET | 300/60s | Yes |
| Futures Trading - POST | 300/60s | Yes |
| Futures Trading - GET | 300/60s | Yes |

## API Signature

All requests except public APIs require signature. For signature methods, please refer to:
- [HTTP API Signature Method](./http/doc-http.md#api-signature)
- [WebSocket API Signature Method](./ws/doc-ws.md#signature)

## Quick Start

1. Obtain API Key and Secret Key (contact support team)
2. Select the appropriate API type based on your needs (WebSocket or HTTP)
3. Refer to the example code in the corresponding documentation to start development
4. Use the [WebSocket Debugging Tool](./faq/ws_demo.html) to test WebSocket connections

## Supported Languages

The documentation provides example code in multiple languages:
- Java
- Shell/curl
- JavaScript (WebSocket)

## Contact Support

For any questions or to obtain an API Key, please contact the EchoBit support team.