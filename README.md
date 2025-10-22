# KHQR Transaction Checker by Sophada Proxy

A minimal PHP proxy for checking KHQR transaction responses. This repository is intended only for educational and testing purposes and not for production use.

Note: The proxy may not allow requests from other countries or networks. It is designed for learning and demonstration only.

## Quick Overview

* Forwards a JSON md5 payload to the KHQR endpoint and returns the upstream response.
* Lightweight, single-file example with safe-by-default recommendations.
* Use it to learn request and response flow and response parsing.
* Accepts dynamic md5 input instead of a hardcoded value.

## Example Responses

### Error Response

```json
{
  "responseCode": 1,
  "responseMessage": "Transaction could not be found. Please check and try again.",
  "errorCode": 1,
  "data": null
}
```

| Field | Meaning |
|-------|---------|
| responseCode | 1 means failure |
| responseMessage | Human-readable error description |
| errorCode | Internal error code |
| data | null, no transaction data |

### Success Response

```json
{
  "responseCode": 0,
  "responseMessage": "Success",
  "errorCode": null,
  "data": {
    "hash": "8608b339522xxxxxxxxxx6a014030a39f6026d69770924daxxxxxxxxxxx",
    "fromAccountId": "abaakhppxxx@abaa",
    "toAccountId": "sophada@vbl",
    "currency": "USD",
    "amount": 1,
    "description": null,
    "createdDateMs": 1761154142000,
    "acknowledgedDateMs": 1761154143000,
    "trackingStatus": null,
    "receiverBank": null,
    "receiverBankAccount": null,
    "instructionRef": null,
    "externalRef": "100FT35781491692"
  }
}
```

| Field | Meaning |
|-------|---------|
| responseCode | 0 means success |
| responseMessage | Success message |
| errorCode | null, no error |
| data.hash | Unique transaction ID |
| data.fromAccountId | Sender account |
| data.toAccountId | Receiver account |
| data.currency | Currency code, for example USD |
| data.amount | Numeric amount |
| data.createdDateMs | Created timestamp in milliseconds since epoch |
| data.acknowledgedDateMs | Acknowledged timestamp in milliseconds since epoch |
| data.externalRef | Merchant or reference ID |
| Other fields | Optional information such as bank, tracking, instruction, description |

## Usage Example

Place the proxy file in your web root, for example khqr-proxy.php, and POST JSON to it with the md5 value:

```bash
curl -X POST "https://yourdomain.com/khqr-proxy.php" \
  -H "Content-Type: application/json" \
  -d '{"md5":"your_transaction_md5_here"}'
```

The proxy will forward the md5 to the KHQR endpoint and return the correct JSON response.

## Important Educational and Testing Note

This project is published for learning and testing only. Do not use it in production without proper security and hardening.

* Do not commit or publish real API secrets or production tokens.
* Validate incoming input. The md5 must match 32 hexadecimal characters.
* Add authentication if used beyond local tests.
* Rate-limit and log safely. Avoid storing raw secrets in logs.
* Keep the file outside public access or restrict by firewall if it will be used for real checks.

If the rightful owner (KHQR dev team) objects to this public example or you want this project taken down, contact contact@sophada.com or +85587877774 and it will be addressed promptly.

## License

MIT, see LICENSE file. Include attribution if required.
