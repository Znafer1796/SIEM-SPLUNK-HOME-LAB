# Splunk Queries – SIEM Home Lab

These SPL queries were used to verify log ingestion, inspect OPNsense firewall events, and investigate network traffic generated during authorized lab testing.

## 1. Verify Log Ingestion

```spl
index="main" sourcetype="syslog"
| stats count by sourcetype
```

**Purpose:** Verify that Splunk has collected syslog events.

## 2. View Recent Firewall Logs

```spl
index="main" sourcetype="syslog"
| sort - _time
| table _time host sourcetype _raw
```

**Purpose:** Inspect recent events and review the raw firewall log data.

## 3. Search for Block-Related Events

```spl
index="main" sourcetype="syslog" "block"
| sort - _time
| table _time host _raw
```

**Purpose:** Find events containing the keyword `block` for further investigation.

**Note:** Keyword matching alone does not confirm that every result represents a blocked connection.

## 4. Investigate Traffic from the Test Machine

```spl
index="main" sourcetype="syslog" "KALI_IP"
| sort - _time
| table _time host _raw
```

**Purpose:** Search for events containing the Kali machine's IP address.

**Note:** Replace `KALI_IP` with the actual IP address. Verify the event timestamps and packet details before attributing events to the Nmap scan.

## 5. Review Firewall Events Over Time

```spl
index="main" sourcetype="syslog"
| timechart span=5m count
```

**Purpose:** Visualize firewall log volume in five-minute intervals and identify periods worth investigating.

**Note:** Event spikes indicate increased log volume, not necessarily malicious activity.

## Investigation Workflow

1. Verify that Splunk is receiving logs.
2. Inspect the raw firewall events.
3. Search for block-related records.
4. Correlate timestamps and IP addresses with the lab test.
5. Document the evidence and any limitations.
