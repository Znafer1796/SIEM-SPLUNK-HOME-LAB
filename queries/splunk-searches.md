## 1. Verify Log Ingestion

### Objective
Verify that Splunk is receiving events and inspect the available data sources.

```spl
index=* earliest=-24h
| stats count by index sourcetype
| sort - count
```

**What it does:**
- Counts events by index and sourcetype.
- Helps identify where the incoming firewall logs are stored.
- Provides a starting point for building more specific searches.

**Investigation note:** Replace `index=*` with the confirmed index once the data source has been identified.

## 2. Inspect Recent Firewall Events

### Objective
Review recent events and identify the fields available in the collected logs.

```spl
index=* earliest=-60m
| head 100
```

**What it does:**
- Displays up to 100 matching events from the last hour.
- Helps verify event timestamps and inspect raw log content.

**Next step:** Identify the relevant index and sourcetype before narrowing the search to OPNsense events.

## 3. Search for OPNsense-Related Events

### Objective
Find events that contain OPNsense or firewall-related information.

```spl
index=* earliest=-24h
("filterlog" OR "OPNsense" OR "firewall")
| table _time host source sourcetype _raw
| sort - _time
```

**What it does:**
- Searches raw event content for the specified terms.
- Displays timestamps, source metadata, and raw events for inspection.

**Limitation:** This is a broad discovery query. It may miss events that do not contain these exact terms. Once the source is confirmed, filter by the actual index, sourcetype, or host.

## 4. Summarize Events Over Time

### Objective
Observe changes in event volume over time.

```spl
index=* earliest=-24h
| timechart span=1h count
```

**What it does:**
- Counts matching events in hourly intervals.
- Helps identify periods with unusually high or low event volume.

**Investigation note:** Use the confirmed firewall index to avoid mixing unrelated events.

## 5. Identify Frequently Seen Source IP Addresses

### Objective
Find source IP addresses that appear frequently in the collected events.

```spl
index=* earliest=-24h
| rex field=_raw "(?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| where isnotnull(src_ip)
| stats count by src_ip
| sort - count
| head 20
```

**What it does:**
- Extracts IPv4-shaped strings from raw event text.
- Counts how frequently each extracted value appears.

**Limitation:** This regular expression does not establish whether an address is a source IP, destination IP, or another address contained in the event. Validate the log format and field mapping before drawing conclusions.

## 6. Inspect Potentially Blocked Traffic

### Objective
Search for firewall events that may indicate blocked or rejected traffic.

```spl
index=* earliest=-24h
("block" OR "blocked" OR "deny" OR "drop" OR "reject")
| table _time host sourcetype _raw
| sort - _time
```

**What it does:**
- Searches event content for common blocking-related terms.
- Provides raw evidence for manual review.

**Limitation:** Matching a keyword does not prove that the firewall blocked the connection. Confirm the actual action field or the documented log format.

## 7. Investigate Activity from a Known Test IP

### Objective
Review events associated with a known IP address used during an authorized lab test.

```spl
index=* earliest=-60m
"192.168.1.100"
| table _time host source sourcetype _raw
| sort - _time
```

**How to use it:**
1. Replace `192.168.1.100` with the actual test IP address.
2. Set the time picker to the period when the test occurred.
3. Inspect matching events and compare their timestamps with the test activity.

**Important:** This example uses a placeholder IP. It is not an assertion about the lab's actual addressing.

## 8. Find Repeated Events

### Objective
Identify repeated raw event messages that may warrant further investigation.

```spl
index=* earliest=-24h
| stats count by sourcetype _raw
| where count > 10
| sort - count
| head 20
```

**What it does:**
- Groups identical raw messages by sourcetype.
- Highlights messages that occur more than ten times.

**Limitation:** Repeated events are not necessarily malicious. Routine firewall activity can generate many identical messages.

## 9. Compare Event Volume by Source

### Objective
Compare the number of events associated with different log sources.

```spl
index=* earliest=-24h
| stats count by host source sourcetype
| sort - count
```

**What it does:**
- Summarizes event counts by host, source, and sourcetype.
- Helps assess which data sources are contributing events.

**Investigation note:** The `host` and `source` metadata values depend on how Splunk receives and parses the data.

## 10. Basic Investigation Workflow

When investigating a test event:

1. Set an appropriate time range.
2. Locate the relevant event source.
3. Inspect the raw event and extracted fields.
4. Identify the timestamp, IP addresses, protocol, and action where available.
5. Compare the event with the known test activity.
6. Record the query, evidence, interpretation, and limitations.

A useful investigation record should distinguish observed facts from hypotheses.
