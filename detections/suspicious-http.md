# Detection: Suspicious HTTP URI

**Signature:** `1000003` — `SOC LAB Suspicious HTTP URI`

## Trigger

An HTTP request containing `/admin` in the URI.

## Lab Web Service

The Ubuntu target ran a temporary Python HTTP server:

```bash
sudo python3 -m http.server 80
```

## Validation

From Kali:

```bash
curl http://10.10.20.10/admin
```

The server returned HTTP `404`, but the request itself generated the Suricata alert.

## EVE Evidence

The documented event included:

- Source: `10.10.10.10:45266`
- Destination: `10.10.20.10:80`
- Method: `GET`
- URI: `/admin`
- User-Agent: `curl/8.18.0`
- Status: `404`
- Signature ID: `1000003`

The HTTP status does not negate the detection: the rule is detecting the request URI, not successful resource access.
