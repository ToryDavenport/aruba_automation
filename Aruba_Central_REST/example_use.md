
# Example Use of Aruba Central API

Note: Instructions for gathering a token are not covered here. Once you have your access token, you can follow the rest to run the sample rest api call.

## Example Token

```json
{
  "access_token": "111222333444",
  "appname": "nms",
  "authenticated_userid": "<REDACTED>",
  "created_at": 1650390007212,
  "credential_id": "60a2ca81-2f2e-4d30-9aec-2d25c0801b21",
  "expires_in": 7200,
  "id": "101a5ad9-d941-40e6-928c-fbe060f02199",
  "refresh_token": "<REDACTED>",
  "scope": "all",
  "token_type": "bearer"
}

```

## Get All networks

We can use the http GET method and the url defined below (yours will be different) to get the list of networks in Aruba Central.

https://apigw-uswest4.central.arubanetworks.com/monitoring/v2/networks

```bash
http GET https://apigw-uswest4.central.arubanetworks.com/monitoring/v2/networks?access_token=111222333444
```

*Example Output*
```bash
student@ubuntu:~/TORY$ http GET https://apigw-uswest4.central.arubanetworks.com/monitoring/v2/networks?access_token=111222333444
HTTP/1.1 200 OK
Access-Control-Allow-Origin: *
Cache-Control: no-cache, no-store, must-revalidate, private
Connection: keep-alive
Content-Length: 35
Content-Type: application/json
Date: Tue, 19 Apr 2022 18:01:00 GMT
Pragma: no-cache
Via: kong/0.14.1
X-Frame-Options: SAMEORIGIN
X-Kong-Proxy-Latency: 229
X-Kong-Upstream-Latency: 558
X-RateLimit-Limit-day: 1000
X-RateLimit-Remaining-day: 990
X-Request-Start: t=1650391260.699
X-XSS-Protection: 1; mode=block

{
    "count": 0,
    "networks": []
}
```
