### Firewall and IPS Testing

The lab was used to perform controlled network security tests against the OPNsense firewall and IPS.

**Test scenarios:**

- **Nmap scanning:** Generate network scanning traffic from Kali Linux and inspect the corresponding firewall or IPS events.
- **hping3 traffic testing:** Generate controlled test traffic and observe whether OPNsense blocks or detects it.

**Evidence:** [Nmap and hping3 blocking demonstration](https://drive.google.com/file/d/1Sxk2leolpvccfGR80S3T9WBvTqrvkn3p/view?usp=sharing)

**Validation:** Review OPNsense firewall/IPS logs and the corresponding events received by Splunk to determine which traffic was detected or blocked.
