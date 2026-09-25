# Lab Machines

| Machine | Role | Network | IP |
|---|---|---|---|
| Suricata Sensor | IDS/router | LAB-IN | `10.10.10.1/24` |
| Suricata Sensor | IDS/router | LAB-OUT | `10.10.20.1/24` |
| Suricata Sensor | Management | NAT | `192.168.232.145/24` during documented run |
| Kali Linux | Test client | LAB-IN | `10.10.10.10/24` |
| Ubuntu GUI | Target/Web service | LAB-OUT | `10.10.20.10/24` |

## VMware Networks

- LAB-IN: `VMnet10` / `10.10.10.0/24`
- LAB-OUT: `VMnet11` / `10.10.20.0/24`
- Management: VMware NAT

## Connectivity Validation

A successful test was performed from Kali to the Ubuntu target:

```bash
ping -c 3 10.10.20.10
```

The replies traversed the Suricata routing path, confirming end-to-end connectivity through the sensor.
