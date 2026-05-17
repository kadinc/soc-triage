# soc-triage
My amorphous SOC triage project. Whatever that means

My plans for this are to develop some classical ML, as well as contemporary approaches to SOC triage and anomaly detection using synthesized logs. 



# Attack Log Generator

Generates synthetic security logs for SOC analyst training, anomaly detection engineering, and machine learning dataset construction. Uses Claude Haiku to produce realistic Linux, Windows, and network logs across a range of attack profiles and normal baseline activity.

## Why

Real attack logs are either proprietary, legally sensitive, or stripped of the contextual signals that make them useful for training. This generates correlated, realistic log data on demand — including matched network logs for every host-based attack scenario.

## Setup

```bash
pip install anthropic
export ANTHROPIC_API_KEY="your-key-here"
```

## Usage

```bash
# Generate everything full corpus with network companions
python attack-log-generator.py

# Full corpus at custom duration
python attack-log-generator.py all 20

# single profile + auto generated companion network log
python attack-log-generator.py linux successful-breach 20

# Network log only
python attack-log-generator.py network dns-exfiltration 15
```

## Attack Profiles

**Linux**
- `ssh-bruteforce` — distributed brute force across common usernames
- `slow-burn` — evasive, rate-limited brute force
- `successful-breach` — brute force → login → sudo enumeration → C2 callback
- `port-scan` — Nmap-style scan and service enumeration
- `normal` — baseline business hours activity

**Windows**
- `password-spray` — Active Directory password spray (Event IDs 4625, 4624, 4648)
- `successful-breach` — auth failure → success → lateral movement (4624, 4672, 4688, 4776)
- `privilege-escalation` — scheduled task and service manipulation (4698, 4702, 7045)
- `lateral-movement` — SMB and remote service execution (4624, 4648, 5140, 7036)
- `normal` — baseline AD environment activity

**Network**
- `ssh-bruteforce` — firewall/NetFlow correlated with SSH brute force
- `slow-burn` — sparse connection attempts across rotating source IPs
- `successful-breach` — port 22 traffic → outbound anomalies → C2 callback
- `port-scan` — sequential port hits, SYN probes, service enumeration
- `password-spray` — SMB/Kerberos volume spike to domain controller
- `lateral-movement` — internal SMB and RPC between hosts
- `privilege-escalation` — DCOM, WMI, scheduled task network activity
- `c2-callback` — beaconing traffic, regular intervals, DNS indicators
- `dns-exfiltration` — long query strings, TXT records, high query frequency
- `normal` — baseline network traffic