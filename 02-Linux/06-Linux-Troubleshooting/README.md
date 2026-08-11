# Linux Service Management & Troubleshooting

## Overview

This lab demonstrates practical Linux service management and troubleshooting in an Ubuntu Server environment.

The scenario simulates an IT Operations incident involving SSH availability. The lab covers SSH service and socket investigation, systemd socket activation, controlled service outage and recovery, TCP port verification, log analysis, network troubleshooting, and final remote-access validation.

During final verification, a separate VirtualBox host-to-VM connectivity issue was identified and resolved by configuring a dedicated Host-Only management network while preserving the existing isolated SOC-LAB network.

This lab is part of the **Enterprise IT Support Lab** portfolio.

---

## Ticket Information

**Ticket ID:** INC-0004  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed

---

## Scenario

The IT Operations team needed to investigate and validate SSH availability on an Ubuntu Server.

Initial investigation showed that `ssh.service` was inactive. Further troubleshooting identified that SSH was using systemd socket activation through `ssh.socket`, which was active and listening on TCP port 22.

A controlled SSH availability incident was simulated by stopping the SSH socket. The outage was verified, the socket was restored, and the incident timeline was reviewed using system logs.

During final remote-access verification, the Windows host could not initially reach the Ubuntu Server because the existing server interface belonged to the isolated `SOC-LAB` Internal Network.

A dedicated VirtualBox Host-Only management interface was configured on a separate subnet. Network connectivity was restored and remote SSH access was successfully verified.

---

## Environment

- Ubuntu Server
- Windows 10 Host
- VirtualBox
- OpenSSH
- systemd
- Netplan
- Sudo Privileges
- NAT Network
- Internal Network (`SOC-LAB`)
- Host-Only Management Network

---

## Tasks Completed

During this lab, I performed the following tasks:

1. Verified the initial SSH service status.
2. Identified that SSH was using systemd socket activation.
3. Verified the status of `ssh.socket`.
4. Confirmed that TCP port 22 was listening.
5. Simulated a controlled SSH outage by stopping `ssh.socket`.
6. Verified that TCP port 22 became unavailable.
7. Restored SSH availability by starting the socket.
8. Verified SSH recovery and TCP port 22 availability.
9. Reviewed the SSH socket incident timeline using `journalctl`.
10. Investigated failed Windows-to-Ubuntu connectivity during final remote-access testing.
11. Identified the difference between the SOC-LAB Internal Network and Host-Only network.
12. Added a dedicated VirtualBox Host-Only network adapter.
13. Configured a separate `192.168.57.0/24` management subnet.
14. Backed up the existing Netplan configuration.
15. Configured the new Ubuntu `enp0s9` management interface.
16. Identified and corrected a Netplan configuration error.
17. Validated and applied the corrected Netplan configuration.
18. Verified Windows-to-Ubuntu connectivity using ping.
19. Successfully established remote SSH access from Windows.
20. Verified the remote user and Ubuntu Server hostname.
21. Documented the troubleshooting process and captured supporting evidence.

---

## Key Commands

```bash
systemctl status ssh --no-pager
```

```bash
systemctl status ssh.socket --no-pager
```

```bash
systemctl is-active ssh.socket
```

```bash
systemctl stop ssh.socket
```

```bash
sudo ss -tlnp | grep ':22'
```

```bash
sudo systemctl start ssh.socket
```

```bash
sudo journalctl -u ssh.socket --since "today" --no-pager
```

```bash
ip addr
```

```bash
sudo cp /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.backup
```

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

```bash
sudo netplan generate
```

```bash
sudo netplan apply
```

```bash
ip addr show enp0s9
```

```bash
ping 192.168.57.20
```

```bash
ssh ankit@192.168.57.20
```

```bash
whoami
hostname
```

---

## Verification

The following checks confirmed that the troubleshooting and recovery were completed successfully:

- `ssh.socket` returned to the active listening state.
- TCP port 22 returned to the `LISTEN` state.
- The SSH socket incident timeline was confirmed using `journalctl`.
- The dedicated Host-Only management interface `enp0s9` was configured successfully.
- Ubuntu received the management address `192.168.57.20/24`.
- The Windows Host-Only interface used `192.168.57.1/24`.
- Windows successfully reached the Ubuntu Server using ping.
- Remote SSH authentication completed successfully.
- `whoami` returned `ankit`.
- `hostname` returned `ubuntuserver`.
- End-to-end remote SSH access was successfully validated.

---

## Troubleshooting

Two separate troubleshooting scenarios were handled during this lab.

### SSH Availability Incident

A controlled SSH outage was created by stopping:

```bash
systemctl stop ssh.socket
```

The socket became inactive and TCP port 22 was no longer listening.

The issue was resolved by restarting the socket:

```bash
sudo systemctl start ssh.socket
```

Recovery was confirmed using `systemctl`, `ss`, and `journalctl`.

### Host-to-VM Network Connectivity

During final remote-access testing, the Windows host could not initially reach the Ubuntu Server.

Investigation showed that the Ubuntu `192.168.56.20/24` interface belonged to the isolated VirtualBox `SOC-LAB` Internal Network rather than the Host-Only management network.

The existing SOC-LAB network was preserved and a third VirtualBox adapter was added for Host-Only management access.

A separate management network was configured:

```text
Windows Host: 192.168.57.1/24
Ubuntu enp0s9: 192.168.57.20/24
```

During Netplan configuration, an incorrect spelling of the `addresses` field caused a validation error.

The configuration was reviewed, corrected, successfully validated using `netplan generate`, and then applied.

Windows-to-Ubuntu connectivity and remote SSH access were successfully restored.

---

## Evidence

Screenshots captured during the practical lab include:

- `01-verify-ssh-service-status.png`
- `02-verify-ssh-socket-status.png`
- `03-simulate-ssh-service-outage.png`
- `04-verify-ssh-port-unavailable.png`
- `05-restore-ssh-service.png`
- `06-verify-ssh-service-recovery.png`
- `07-inspect-ssh-socket-incident-timeline.png`
- `08-verify-ssh-remote-access-after-recovery.png`

Supporting screenshots are available in the [`Screenshots`](./Screenshots/) directory.

---

## Detailed Documentation

Complete technical documentation, including command explanations, observed results, SSH socket activation, incident investigation, network troubleshooting, Netplan configuration, verification results, and lessons learned, is available here:

[`Linux-Troubleshooting.md`](./Documentation/Linux-Troubleshooting.md)

---

## Skills Demonstrated

- Linux Service Management
- Linux Troubleshooting
- SSH Administration
- OpenSSH
- systemd
- systemd Socket Activation
- Linux Command-Line Administration
- TCP Port Verification
- Incident Investigation
- Incident Recovery
- Log Analysis
- TCP/IP Troubleshooting
- VirtualBox Networking
- NAT Networking
- Internal Networking
- Host-Only Networking
- Netplan Configuration
- Network Configuration Validation
- Remote Access Troubleshooting
- End-to-End Service Verification
- Technical Documentation

---

## Interview Relevance

This lab provides practical examples that can be discussed during IT Support, Application Support, System Administration, and junior cybersecurity interviews.

Examples include:

- How to investigate an inactive Linux service.
- How systemd socket activation works with SSH.
- How to verify whether TCP port 22 is listening.
- How to simulate and recover from a controlled service outage.
- How to use `journalctl` during incident investigation.
- How to distinguish a service issue from a network-connectivity issue.
- How VirtualBox NAT, Internal Network, and Host-Only networking differ.
- How to configure a dedicated Linux management interface.
- How to validate and troubleshoot Netplan configuration.
- How to verify service recovery from the client side.
- How to document an incident investigation and resolution.

---

## Outcome

The SSH availability incident was successfully investigated, simulated, recovered, and verified.

The lab demonstrated that an inactive `ssh.service` does not automatically indicate SSH unavailability when systemd socket activation is being used.

A separate host-to-VM network connectivity issue discovered during final verification was also successfully diagnosed and resolved while preserving the existing SOC-LAB Internal Network.

Windows-to-Ubuntu connectivity was restored through a dedicated Host-Only management network, and final testing confirmed successful remote SSH access.

The practical task demonstrated a structured approach to Linux service management, incident investigation, network troubleshooting, recovery verification, and technical documentation.

---

## Repository

**Project:** Enterprise IT Support Lab  
**Section:** Linux Administration  
**Lab:** 06 - Linux Service Management & Troubleshooting  
**Status:** Completed
