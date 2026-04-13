# Private SOC Lab

## Overview
This project is a private SOC lab built to simulate attacks and monitor security events using Kali Linux, Wazuh SIEM, Suricata IDS, and an Ubuntu victim server.

## Lab Topology
![Private SOC Lab Topology](screenshots/lab-topology.png)

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
- Ubuntu Server with Wazuh (SIEM): `192.168.106.130`
- Ubuntu Live Server with Suricata + Wazuh Agent (Victim): `192.168.106.131`
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
- SSH brute-force-like bursts
- Suspicious outbound connection to TCP port 4444

## Suricata Integration with Wazuh
Suricata is integrated with Wazuh by forwarding EVE JSON logs to the Wazuh manager. This allows Suricata network alerts to be collected, parsed, and monitored through the SIEM platform.

Suricata log source:
- `/var/log/suricata/eve.json`

Suricata custom rules:
- `/var/lib/suricata/rules/local.rules`

## Monitoring Workflow
1. The attacker machine generates simulated attack traffic toward the victim server.
2. Suricata running on the victim analyzes the traffic and generates alerts based on custom rules.
3. Suricata writes the events into `eve.json` on the victim machine.
4. Wazuh reads the Suricata JSON logs from the victim through the agent configuration.
5. The logs are forwarded to the Wazuh manager for centralized monitoring and analysis.
6. Alerts and events can then be reviewed in the Wazuh dashboard.

## Evidence and Screenshots
The following screenshots document the setup, configuration, and detection results of the lab environment:
- Lab topology diagram
- IP configuration of each virtual machine
- Wazuh manager service status
- Suricata service status
- Suricata custom rules
- Wazuh integration with Suricata in `ossec.conf`
- Suricata configuration test results
- Suricata alert logs in `fast.log` or `eve.json`
- Wazuh dashboard alerts

## Current Project Status
This lab environment has been set up and configured successfully. The current focus is on validating detections, collecting screenshots, and documenting attack simulations for portfolio purposes.

## Future Improvements
- Add more attack simulation scenarios
- Create more custom Suricata detection rules
- Improve alert correlation in Wazuh
- Expand the lab with additional endpoints
- Add incident investigation notes and response playbooks

## Author
**Matthew Benedict Ezekiel Saisab**  
Cybersecurity learner and Informatics undergraduate at Universitas Atma Jaya Yogyakarta, building hands-on SOC lab projects for learning and internship preparation.
