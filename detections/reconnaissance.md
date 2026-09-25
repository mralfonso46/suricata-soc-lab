# Detection: ICMP Reconnaissance / Test Traffic

**Signature:** `1000001` — `SOC LAB ICMP Test`

## Trigger

ICMP traffic crossing the Suricata sensor from the LAB-IN network toward the LAB-OUT target.

## Validation

From Kali:

```bash
ping -c 3 10.10.20.10
```

## Expected Alert

`fast.log` records an ICMP alert with source `10.10.10.10` and destination `10.10.20.10`.

`eve.json` records the same event as `event_type: alert` with `proto: ICMP` and signature ID `1000001`.

## SOC Investigation Fields

- Source IP: `10.10.10.10`
- Destination IP: `10.10.20.10`
- Interface: `ens38`
- Protocol: ICMP
- Signature ID: `1000001`
- Severity: 3
- Action: allowed

The action is `allowed` because this lab is operating in IDS alerting mode rather than inline IPS blocking mode.
