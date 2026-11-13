# Rogue Device Authenticator (RDA)

**A Python-based LAN security system for detecting, classifying and controlling unauthorised devices on a network.**

## Overview

The Rogue Device Authenticator (RDA) is a network security project designed to identify devices connected to a Local Area Network (LAN), determine whether they are authorised and take action against devices that do not meet the network's access requirements.

The system combines network scanning, device identification, database-backed device management and firewall enforcement to provide a practical approach to controlling network access.

RDA follows the principles of **Zero Trust Security**, where devices are not automatically trusted simply because they are connected to the network.

## Problem Statement

Unauthorised devices connecting to an organisation's internal network can introduce security risks, including unauthorised access to resources, information exposure and potential network compromise.

Traditional networks may allow devices to communicate once they gain network connectivity, without continuously verifying whether those devices are authorised.

RDA addresses this problem by providing a mechanism to discover network devices, compare them against registered devices and restrict access to devices identified as unauthorised.

## Key Features

- **Network Discovery:** Identifies active devices on the local network using ARP scanning and Nmap.
- **Device Classification:** Categorises discovered devices according to their authorisation status.
- **Device Enrolment:** Allows legitimate devices to be registered and recognised by the system.
- **Device Management:** Maintains records of trusted devices and scanning activity using SQLite.
- **Rogue Device Detection:** Identifies devices that are not registered as trusted.
- **Access Control:** Uses iptables firewall rules to block identified unauthorised devices.
- **Web Dashboard:** Provides a Flask-based interface for managing devices and viewing network security information.
- **Scan Logging:** Records scanning activity to support monitoring and investigation.

## System Architecture

RDA follows a modular architecture consisting of the following components:

1. **Network Scanning Layer:** Discovers active devices using ARP and Nmap.
2. **Detection and Classification Layer:** Processes discovered device information and determines its authorisation status.
3. **Database Layer:** Stores trusted device records and network scanning logs using SQLite.
4. **Management Layer:** Provides device enrolment and management functionality.
5. **Enforcement Layer:** Applies iptables firewall rules to restrict unauthorised devices.
6. **Dashboard Layer:** Uses Flask to provide a web-based interface for interacting with the system.

### Device Classification

The system uses the following device states:

| Status | Description |
|---|---|
| Trusted | Device is registered and authorised. |
| Enrolled-Pending | Device has been submitted for enrolment but is awaiting approval. |
| Rogue | Device has been detected but is not authorised. |
| Blocked | Device has had its network access restricted. |

## Technologies Used

| Technology | Purpose |
|---|---|
| Python 3 | Core application development |
| Scapy | ARP-based network discovery |
| Nmap | Network scanning and device identification |
| Flask | Web dashboard and application interface |
| SQLite | Device records and scan logs |
| iptables | Network access enforcement |
| Linux | Execution environment |
| GNS3 | Network simulation and testing |
| VMware | Virtualised lab environment |

## Project Structure

```text
rogue-device-authenticator/
│
├── app.py              # Flask web dashboard
├── run_rda.py          # Main application entry point
├── scan_engine.py      # Network scanning coordination
├── arp_scan.py         # ARP-based device discovery
├── nmap_scan.py        # Nmap-based network scanning
├── db_setup.py         # Database initialisation
├── seed.py             # Database initial data
├── enrol_agent.py      # Device enrolment functionality
│
├── rda.db              # SQLite database (generated locally)
│
└── README.md
```

## How It Works

The general workflow is:

1. The system scans the local network to discover active devices.
2. Discovered devices are identified and their network information is collected.
3. The system compares the discovered devices against its database of trusted devices.
4. Devices are assigned an appropriate authorisation status.
5. Unauthorised devices can be restricted through iptables firewall rules.
6. Scanning activity and device information are maintained for monitoring and management.

## Testing Environment

The project was developed and tested in a virtualised network environment using GNS3, VMware and Kali Linux.

The test network used the private subnet:

```text
192.168.27.0/24
```

The isolated lab environment provided a controlled setting for testing device discovery, classification and network access enforcement.

## Security Considerations

- Device discovery and enforcement require appropriate network privileges.
- ARP-based identification relies on network-layer information and should not be treated as cryptographically verified device identity.
- Firewall enforcement depends on the network topology and the system's position within the traffic path.
- Testing should be performed in an isolated or explicitly authorised network environment.

## Project Objectives

- Demonstrate practical network security implementation.
- Explore Zero Trust principles in LAN environments.
- Develop an automated approach to identifying unauthorised network devices.
- Integrate network discovery with database-backed device management.
- Demonstrate network access enforcement using Linux firewall mechanisms.

## Future Improvements

Potential areas for further development include:

- Stronger device identity verification.
- Real-time network monitoring.
- Alerting and notification integration.
- Improved audit logs and reporting.
- Support for additional network enforcement mechanisms.

## Disclaimer

Rogue Device Authenticator is an academic cybersecurity project developed for educational and controlled laboratory testing.

Do not deploy network scanning or access-control functionality on networks without proper authorisation.

## Author

**Benedict Kirui**

Cybersecurity and Computer Networks Student

- GitHub: [Artof-cod3](https://github.com/Artof-cod3)
- LinkedIn: [Benedict Kirui](https://www.linkedin.com/in/benedict-kirui-413540357/)
