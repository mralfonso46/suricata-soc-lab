# Detection: TCP SYN Port Scan

**Signature:** `1000002` — `SOC LAB Possible TCP SYN Scan`

## Trigger

Ten or more TCP SYN packets from the same source within five seconds.

## Validation

From Kali:

```bash
nmap -sS -p 1-1000 10.10.20.10
```

The scan identified TCP/22 as open on the target while the remaining scanned ports were closed.

## Alert Evidence

Suricata generated repeated alerts such as:

```text
SOC LAB Possible TCP SYN Scan
10.10.10.10 -> 10.10.20.10
```

The EVE JSON evidence records source/destination IPs, source/destination ports, protocol TCP, interface `ens38`, and signature ID `1000002`.

## Tuning Notes

The rule is intentionally simple. In a production SOC, consider thresholds based on destination scope, service baselines, scanner allowlists, and correlation with flow/connection telemetry.
