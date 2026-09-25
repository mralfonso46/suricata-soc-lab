# Custom Suricata Rules

## Rule 1000001 — ICMP Test / Reconnaissance

```text
alert icmp any any -> any any (msg:"SOC LAB ICMP Test"; sid:1000001; rev:1;)
```

**Purpose:** generate a deterministic alert for ICMP traffic in the isolated lab.

## Rule 1000002 — TCP SYN Scan

```text
alert tcp any any -> any any (flags:S; msg:"SOC LAB Possible TCP SYN Scan"; threshold:type threshold, track by_src, count 10, seconds 5; sid:1000002; rev:1;)
```

**Purpose:** detect a burst of TCP SYN packets from one source. This is a lab-oriented detection and can produce false positives in environments with legitimate connection bursts.

## Rule 1000003 — Suspicious HTTP URI

```text
alert http any any -> any any (http.uri; content:"/admin"; msg:"SOC LAB Suspicious HTTP URI"; sid:1000003; rev:1;)
```

**Purpose:** alert when an HTTP request contains `/admin` in the URI. This is intentionally simple for a training lab and should be tuned before production use.

## Rule Validation

```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

The lab configuration validated successfully after each rule update.
