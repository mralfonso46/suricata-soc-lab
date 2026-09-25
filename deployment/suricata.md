# Suricata Deployment

## Platform

- Suricata: **7.0.3 RELEASE**
- OS: Ubuntu Server
- Capture: AF_PACKET
- Detection engine: enabled
- Logs: `/var/log/suricata/`
- Rules: `/var/lib/suricata/rules/suricata.rules`
- Configuration: `/etc/suricata/suricata.yaml`

## Interface Mapping

| Interface | Role | Address |
|---|---|---|
| `ens33` | Management/NAT | `192.168.232.145/24` during the documented lab run |
| `ens38` | LAB-IN | `10.10.10.1/24` |
| `ens37` | LAB-OUT | `10.10.20.1/24` |

## Routing

The sensor was configured as an IPv4 router between the two isolated lab networks:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

The test client routed `10.10.20.0/24` through `10.10.10.1`.

## Validation

```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

Successful validation produced:

```text
Configuration provided was successfully loaded. Exiting.
```

## Running Suricata for the Lab

```bash
sudo suricata -i ens38 -c /etc/suricata/suricata.yaml
```

The documented lab run showed `Engine started.`

## Logs

- Fast alerts: `/var/log/suricata/fast.log`
- Structured events: `/var/log/suricata/eve.json`

The EVE JSON records include interface, source/destination IPs, protocol, signature ID, signature, and HTTP metadata where applicable.
