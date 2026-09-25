# Lessons Learned

## 1. Detection is not the same as prevention

The lab produced alerts successfully, but `alert.action` remained `allowed`. This demonstrates IDS visibility without claiming IPS blocking.

## 2. Rules need validation and restart awareness

`suricata -T` validates configuration and rules, but a running Suricata process must be restarted after rule changes when rules are loaded at process startup.

## 3. EVE JSON is the primary investigation source

`eve.json` provides structured fields that are easier to correlate than plain-text alerts, including source/destination, protocol, signature ID, flow information, and HTTP metadata.

## 4. Simple rules require tuning

The SYN threshold and `/admin` URI match are intentionally basic. Production detections should consider false positives, baselines, allowlists, context, and correlation.

## 5. Timestamps should be normalized

The Suricata sensor used UTC while Kali displayed `+03:00`. The same event therefore appeared three hours apart in wall-clock display while representing the same instant. SOC pipelines should normalize timestamps, preferably to UTC.

## 6. Evidence should be captured after verification

Screenshots were taken only after the relevant detection or evidence was confirmed. This makes the portfolio artifacts easier to audit.

## 7. Controlled lab testing matters

All scanning and HTTP requests were performed against lab-owned systems on isolated VMware networks.
