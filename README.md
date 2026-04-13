# Private SOC Lab

## Overview
This project is a private SOC lab built to simulate attacks and monitor security events using Kali Linux, Wazuh SIEM, Suricata IDS, and an Ubuntu victim server.

## Lab Topology
![Private SOC Lab Topology](Screenshots/lab-topology.jpeg)

## Objectives
- Simulate basic cyber attacks in a controlled lab
- Monitor logs and alerts through Wazuh
- Detect suspicious traffic with Suricata
- Build a portfolio-ready SOC project

## Lab Components
- Kali Linux — Attacker
- Ubuntu Server with Wazuh + Suricata — SIEM / Monitoring
- Ubuntu Live Server — Victim

## Network Information
- Kali Linux (Attacker): `192.168.106.128`
- Ubuntu Live Server (Victim): `192.168.106.131`
- Ubuntu Server with Wazuh + Suricata (SIEM): `192.168.106.130`
- Internal network: `192.168.106.0/24`

## Tools Used
- Kali Linux
- Wazuh SIEM
- Suricata IDS
- Ubuntu Live Server
- SSH
- Nmap

## Attack Scenarios
The lab is used to simulate several basic attack scenarios in a controlled environment, including:
- ICMP ping activity
- TCP SYN scan activity using Nmap
- SSH access attempts
- SSH brute-force-like bursts
- Suspicious outbound connection activity on port 4444

## Detection Rules
Custom detection rules were created in Suricata to identify suspicious or malicious traffic generated during the lab simulations. These rules were designed to detect several common attack patterns and network events.

The implemented custom rules include:
- ICMP ping detection
- ICMP flood-like activity
- TCP SYN scan activity
- TCP SYN flood-like activity
- SSH access to server

## Suricata Integration with Wazuh
Suricata is integrated with Wazuh by forwarding EVE JSON logs to the Wazuh manager. This allows Suricata network alerts to be collected, parsed, and monitored through the SIEM platform.

Suricata log source:
- `/var/log/suricata/eve.json`

Suricata custom rules:
- `/var/lib/suricata/rules/local.rules`
- SSH brute-force-like bursts
- Suspicious outbound connection to TCP port 4444
## Monitoring Workflow
1. The attacker machine generates simulated attack traffic toward the victim server.
2. Suricata analyzes the traffic and generates alerts based on custom rules.
3. Suricata writes the events into `eve.json`.
4. Wazuh reads the Suricata JSON logs through `ossec.conf`.
5. Alerts and events can then be reviewed in the Wazuh dashboard.
