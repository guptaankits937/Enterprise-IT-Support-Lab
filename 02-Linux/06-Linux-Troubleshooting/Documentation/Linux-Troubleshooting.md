# Linux Service Management & Troubleshooting

## Lab Information

**Lab Name:** Linux Service Management & Troubleshooting
**Project:** Enterprise IT Support Lab
**Date:** 11 August 2026
**Operating System:** Ubuntu Server

**Objective:**

Learn how to investigate and troubleshoot SSH service availability on a Linux server using standard Linux service-management, networking, and logging tools.

The lab demonstrates how to inspect SSH service and socket states, understand systemd socket activation, simulate an SSH availability incident, verify TCP port availability, restore SSH access, inspect the incident timeline, troubleshoot a separate host-to-VM connectivity issue, configure a dedicated management interface, and perform end-to-end remote SSH verification.

---

## Ticket Information

**Ticket ID:** INC-0004
**Department:** IT Operations
**Priority:** Medium
**Status:** Completed

---

# Scenario

The IT Operations team needed to investigate and validate SSH availability on an Ubuntu Server.

Initial inspection showed that `ssh.service` was loaded but inactive. Further investigation identified that the server was using systemd socket activation through `ssh.socket`.

The SSH socket was confirmed to be active and listening on TCP port 22.

A controlled SSH outage was then simulated by stopping `ssh.socket`. The incident was verified at both the systemd level and network-listener level.

The SSH socket was subsequently restored and recovery was verified. System journal logs were reviewed to reconstruct the socket deactivation and recovery timeline.

During final end-to-end remote-access testing, a separate host-to-VM networking issue was discovered. The Ubuntu interface using `192.168.56.20/24` belonged to the isolated VirtualBox `SOC-LAB` Internal Network and was therefore not directly reachable from the Windows host.

The existing SOC-LAB network was preserved. A third VirtualBox adapter was added as a dedicated Host-Only management interface. A separate `192.168.57.0/24` management subnet was configured, after which Windows-to-Ubuntu connectivity and remote SSH access were successfully verified.

---

# Environment

* Ubuntu Server
* Windows 10 Host
* VirtualBox
* OpenSSH
* systemd
* Netplan
* Sudo Privileges
* Administrative User: `ankit`
* Server Hostname: `ubuntuserver`
* Adapter 1: NAT
* Adapter 2: Internal Network (`SOC-LAB`)
* Adapter 3: Host-Only Adapter
* SOC-LAB Interface: `enp0s8`
* Management Interface: `enp0s9`

---

## Lab Duration

**Estimated Time:** 45–60 Minutes

---

# Commands Used

## 1. Verify SSH Service Status

```bash
systemctl status ssh --no-pager
systemctl is-enabled ssh
systemctl is-active ssh
```

**Observed Result:**

The SSH service was loaded but inactive.

The service information also showed that it was associated with:

```text
ssh.socket
```

through systemd socket activation.

**Purpose:**

Determine the current SSH service state before making any changes.

The inactive state of `ssh.service` was not immediately treated as an outage because the service status indicated that it could be triggered through `ssh.socket`.

---

## 2. Verify SSH Socket Status

```bash
systemctl status ssh.socket --no-pager
systemctl is-active ssh.socket
systemctl is-enabled ssh.socket
```

**Observed Result:**

The SSH socket was:

```text
active (listening)
```

The socket was also enabled and listening on TCP port 22.

The listener included:

```text
0.0.0.0:22
[::]:22
```

**Purpose:**

Determine whether SSH availability was being provided through systemd socket activation.

`0.0.0.0:22` represents the IPv4 listener on TCP port 22.

`[::]:22` represents the IPv6 listener.

This confirmed that an inactive `ssh.service` did not automatically mean that SSH was unavailable.

---

# Understanding SSH Socket Activation

Systemd can use socket activation to listen for incoming connections and start the associated service when required.

For SSH, the socket unit:

```text
ssh.socket
```

can listen for incoming connections on TCP port 22.

Therefore, checking only:

```bash
systemctl is-active ssh
```

can provide an incomplete picture of SSH availability.

A more complete investigation includes:

```bash
systemctl status ssh.socket --no-pager
```

and verification of the actual TCP port 22 listener.

---

## 3. Simulate an SSH Availability Incident

The SSH socket was intentionally stopped to create a controlled troubleshooting scenario.

```bash
systemctl stop ssh.socket
```

Authentication was requested and completed.

**Observed Result:**

The socket changed to:

```text
inactive (dead)
```

The system reported events including:

```text
ssh.socket: Deactivated successfully
Closed ssh.socket
```

**Purpose:**

Create a controlled SSH availability incident in the lab environment.

Stopping the socket removed the listener responsible for accepting new SSH connections.

---

## 4. Verify SSH Port Unavailability

```bash
sudo ss -tlnp | grep ':22'
```

The socket state was also checked:

```bash
systemctl is-active ssh.socket
```

**Observed Result:**

No TCP port 22 listener was returned.

The socket state remained:

```text
inactive
```

**Purpose:**

Verify the simulated outage using two independent checks:

* systemd socket state
* TCP network-listener state

The absence of a port 22 listener confirmed that SSH was unavailable for new incoming connections.

---

## 5. Restore SSH Availability

The SSH socket was started again.

```bash
sudo systemctl start ssh.socket
```

The status was then reviewed:

```bash
systemctl status ssh.socket --no-pager
```

**Observed Result:**

The socket returned to:

```text
active (listening)
```

The listener was restored on TCP port 22.

**Purpose:**

Restore SSH availability after the controlled outage.

---

## 6. Verify SSH Service Recovery

```bash
systemctl is-active ssh.socket
sudo ss -tlnp | grep ':22'
systemctl is-enabled ssh.socket
```

**Observed Result:**

The socket returned:

```text
active
```

TCP port 22 was again shown in the:

```text
LISTEN
```

state.

The socket was also confirmed as enabled.

**Purpose:**

Verify that recovery was successful at both the systemd and network-listener levels.

The important recovery indicators were:

* `ssh.socket` active
* TCP port 22 listening
* socket enabled

---

# Understanding the `ss` Output

The TCP listener output contained values similar to:

```text
LISTEN 0 4096
```

The value `0` does not indicate a failure.

It represents the current receive queue.

The important troubleshooting evidence was:

```text
LISTEN
```

and:

```text
:22
```

which confirmed that the SSH port was accepting connections again.

---

## 7. Inspect SSH Socket Incident Timeline

```bash
sudo journalctl -u ssh.socket --since "today" --no-pager
```

**Observed Result:**

The journal showed the SSH socket being closed/deactivated during the controlled incident and later returning to the listening state after recovery.

**Purpose:**

Review system logs and reconstruct the incident timeline.

This demonstrated how `journalctl` can be used during Linux incident investigation to correlate service events with troubleshooting and recovery actions.

---

# Additional SSH Log Investigation

The SSH service journal was also inspected:

```bash
sudo journalctl -u ssh.service --since "today" --no-pager
```

**Observed Result:**

```text
-- No entries --
```

**Purpose:**

Determine whether the `ssh.service` unit contained additional incident information.

No useful service-unit entries were available.

Because the incident involved the socket unit directly, `ssh.socket` provided the relevant timeline information.

This check was part of the troubleshooting process but was not retained as one of the final evidence screenshots.

---

# End-to-End Remote Access Verification

After restoring `ssh.socket`, remote access was tested from the Windows host.

The initial SSH connection did not succeed.

Ubuntu had already confirmed that:

* `ssh.socket` was active.
* TCP port 22 was listening.
* The SSH socket had been successfully restored.

This indicated that the remaining problem was likely related to network connectivity rather than SSH service recovery.

---

# Network Connectivity Troubleshooting

## Issue

The Windows host initially could not reach the Ubuntu Server using:

```text
192.168.56.20
```

A ping test resulted in:

```text
Request timed out
```

Because SSH was confirmed as locally available on Ubuntu, the network path between Windows and Ubuntu was investigated.

---

## Verify Ubuntu Network Interfaces

Ubuntu network interfaces were inspected:

```bash
ip addr
```

The server showed multiple interfaces.

The relevant interfaces included:

```text
enp0s3
enp0s8
```

The interface:

```text
enp0s8
```

was configured with:

```text
192.168.56.20/24
```

---

## Verify Windows Network Configuration

Windows network configuration was inspected using:

```text
ipconfig
```

The VirtualBox Host-Only Ethernet Adapter was initially configured as:

```text
IPv4 Address: 192.168.56.1
Subnet Mask: 255.255.255.0
```

At first, Windows and Ubuntu appeared to be using addresses from the same subnet.

However, further VirtualBox investigation showed that they were attached to different virtual network types.

---

# VirtualBox Network Investigation

The Ubuntu VM network configuration was inspected.

The existing configuration was:

```text
Adapter 1 → NAT
Adapter 2 → Internal Network (SOC-LAB)
```

Adapter 1 provided internet connectivity.

Adapter 2 provided the isolated network used for the SOC lab environment.

The Ubuntu interface:

```text
enp0s8
```

with address:

```text
192.168.56.20/24
```

belonged to the VirtualBox Internal Network:

```text
SOC-LAB
```

The Windows Host-Only adapter was not part of this Internal Network.

Therefore, the Windows host could not directly reach `enp0s8`, even though both addresses appeared to use the `192.168.56.0/24` subnet.

---

# Network Design Decision

The `SOC-LAB` Internal Network was intentionally preserved because it would be required for the isolated cybersecurity lab environment.

Changing Adapter 2 to Host-Only networking would have modified the existing lab architecture.

Instead, a separate management interface was added.

The new design became:

```text
Adapter 1 → NAT
Adapter 2 → Internal Network (SOC-LAB)
Adapter 3 → Host-Only Adapter
```

This separated:

* Internet access
* Isolated SOC-LAB communication
* Windows-to-Ubuntu management access

---

# Configure Adapter 3

The Ubuntu VM was cleanly powered off before modifying VirtualBox network hardware.

Adapter 3 was enabled and configured as:

```text
Attached to: Host-only Adapter
Name: VirtualBox Host-Only Ethernet Adapter
Virtual Cable Connected: Enabled
```

After Ubuntu started again, the new interface was detected as:

```text
enp0s9
```

Initially, the interface was down and had no configured IPv4 address.

---

# Inspect Existing Netplan Configuration

The available Netplan file was identified:

```bash
ls /etc/netplan/
```

**Observed Result:**

```text
50-cloud-init.yaml
```

The existing configuration was inspected:

```bash
sudo cat /etc/netplan/50-cloud-init.yaml
```

The configuration contained:

```text
enp0s3
enp0s8
```

The new `enp0s9` interface had not yet been configured.

---

# Separate SOC-LAB and Management Subnets

The existing SOC-LAB interface already used:

```text
192.168.56.20/24
```

Configuring `enp0s9` on the same IPv4 subnet could create an overlapping subnet and ambiguous routing configuration.

A separate management subnet was therefore selected:

```text
192.168.57.0/24
```

The Windows Host-Only adapter was changed to:

```text
192.168.57.1
```

with:

```text
255.255.255.0
```

as the network mask.

---

# Configure VirtualBox Host-Only DHCP

The VirtualBox Host-Only DHCP configuration was also moved to the new subnet.

The configuration became:

```text
Server Address:       192.168.57.100
Server Mask:          255.255.255.0
Lower Address Bound:  192.168.57.101
Upper Address Bound:  192.168.57.254
```

The configuration was applied.

Windows network configuration was then checked again:

```text
ipconfig
```

**Observed Result:**

The VirtualBox Host-Only Ethernet Adapter now showed:

```text
IPv4 Address: 192.168.57.1
Subnet Mask: 255.255.255.0
```

---

# Backup Netplan Configuration

Before modifying Ubuntu network configuration, the existing Netplan file was backed up:

```bash
sudo cp /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.backup
```

**Purpose:**

Preserve the existing working configuration before making network changes.

This provides a recovery option if a configuration error causes connectivity problems.

---

# Configure the Host-Only Interface

The Netplan file was opened:

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

The new interface configuration was added:

```yaml
enp0s9:
  dhcp4: false
  addresses:
    - 192.168.57.20/24
```

The resulting interface design became:

```text
enp0s3 → NAT
enp0s8 → SOC-LAB → 192.168.56.20/24
enp0s9 → Host-Only → 192.168.57.20/24
```

---

# Netplan Configuration Troubleshooting

## Issue

During configuration of `enp0s9`, the `addresses` field was initially entered with incorrect spelling.

Before applying the network changes, the configuration was validated:

```bash
sudo netplan generate
```

Netplan returned an error.

### Resolution

The recently added YAML configuration was reviewed.

The incorrect field was identified and corrected to:

```text
addresses
```

The validation command was then run again.

```bash
sudo netplan generate
```

The corrected configuration passed validation.

### Troubleshooting Process

1. Edited the Netplan configuration.
2. Used `netplan generate` before applying the change.
3. Reviewed the validation error.
4. Checked the newly added interface configuration.
5. Identified the spelling mistake.
6. Corrected the `addresses` field.
7. Re-ran `netplan generate`.
8. Confirmed that validation completed successfully.
9. Applied the corrected configuration.

This demonstrated the importance of validating network configuration before applying changes.

---

# Apply the Network Configuration

After successful validation:

```bash
sudo netplan apply
```

The new interface was verified:

```bash
ip addr show enp0s9
```

**Observed Result:**

The interface successfully showed:

```text
192.168.57.20/24
```

**Purpose:**

Confirm that the dedicated Host-Only management interface was configured successfully.

---

# Verify Host-to-VM Connectivity

From Windows:

```text
ping 192.168.57.20
```

**Observed Result:**

The ping test succeeded.

**Purpose:**

Verify basic IP connectivity between the Windows host and Ubuntu Server before testing the SSH application layer.

This confirmed that the dedicated Host-Only management network was working.

---

## 8. Verify SSH Remote Access After Recovery

Remote SSH access was tested from Windows:

```text
ssh ankit@192.168.57.20
```

Authentication completed successfully.

A remote Ubuntu shell was opened.

The connected user was verified:

```bash
whoami
```

**Result:**

```text
ankit
```

The remote hostname was verified:

```bash
hostname
```

**Result:**

```text
ubuntuserver
```

**Purpose:**

Perform final end-to-end validation of SSH availability after service recovery and network troubleshooting.

The successful remote session confirmed:

* Windows-to-Ubuntu connectivity.
* TCP port 22 accessibility.
* SSH connection acceptance.
* Successful authentication.
* Functional remote shell access.
* Connection to the expected Ubuntu Server.

---

# Troubleshooting Summary

Two separate troubleshooting situations occurred during this lab.

## Issue 1 — Controlled SSH Availability Incident

The SSH outage was intentionally created by stopping:

```text
ssh.socket
```

The outage was verified using:

* `systemctl`
* Socket state
* `ss`
* TCP port 22 listener state

The socket was restored and recovery was confirmed using:

* Socket status
* Port 22 verification
* Socket enabled state
* System journal logs

## Issue 2 — Host-to-VM Network Connectivity

During final remote SSH verification, the Windows host could not initially reach Ubuntu.

Investigation identified that:

```text
192.168.56.20/24
```

belonged to the isolated VirtualBox `SOC-LAB` Internal Network.

A dedicated Host-Only management adapter was introduced without changing the SOC-LAB network.

The new management configuration became:

```text
Windows Host-Only: 192.168.57.1/24
Ubuntu enp0s9:      192.168.57.20/24
```

After applying the configuration, ping and SSH testing succeeded.

The network-connectivity issue was separate from the intentionally simulated SSH socket outage and was not treated as its root cause.

---

# Final Network Architecture

```text
Adapter 1 / enp0s3
Type: NAT
Purpose: Internet Connectivity

Adapter 2 / enp0s8
Type: Internal Network
Network: SOC-LAB
IP: 192.168.56.20/24
Purpose: Isolated Lab Communication

Adapter 3 / enp0s9
Type: Host-Only Adapter
IP: 192.168.57.20/24
Purpose: Windows-to-Ubuntu Management and SSH
```

Windows Host-Only interface:

```text
192.168.57.1/24
```

The final design separates internet access, isolated SOC-LAB communication, and host-management traffic.

---

# Verification Results

The lab successfully demonstrated that:

* SSH service status could be inspected using `systemctl`.
* SSH socket activation could be identified and understood.
* An inactive `ssh.service` did not automatically indicate an SSH outage.
* SSH socket state could be inspected independently.
* TCP port 22 availability could be verified using `ss`.
* A controlled SSH availability incident could be simulated.
* The outage could be confirmed at both the service-management and network-listener levels.
* SSH availability could be restored.
* Recovery could be verified using multiple diagnostic methods.
* `journalctl` could be used to reconstruct the incident timeline.
* Service-level and network-level problems could be distinguished.
* VirtualBox NAT, Internal Network, and Host-Only networking could be differentiated.
* The existing SOC-LAB architecture could be preserved.
* A dedicated Host-Only management network could be configured.
* Overlapping network configuration could be avoided by using separate subnets.
* Existing Netplan configuration could be backed up before modification.
* Netplan configuration could be validated before application.
* A Netplan configuration error could be identified and corrected.
* Host-to-VM connectivity could be verified using ping.
* End-to-end remote SSH access could be verified.
* The connected user and remote hostname could be validated.

---

# Evidence

Screenshots:

1. `01-verify-ssh-service-status.png`
2. `02-verify-ssh-socket-status.png`
3. `03-simulate-ssh-service-outage.png`
4. `04-verify-ssh-port-unavailable.png`
5. `05-restore-ssh-service.png`
6. `06-verify-ssh-service-recovery.png`
7. `07-inspect-ssh-socket-incident-timeline.png`
8. `08-verify-ssh-remote-access-after-recovery.png`

---

# Lessons Learned

* Learned how systemd socket activation affects SSH service behavior.
* Understood the difference between `ssh.service` and `ssh.socket`.
* Learned not to diagnose SSH availability from service state alone.
* Used `systemctl` to inspect and manage SSH components.
* Used `ss` to verify TCP port 22 availability.
* Used `journalctl` to reconstruct an incident timeline.
* Practiced a controlled SSH outage and recovery workflow.
* Learned to verify recovery using evidence from multiple system layers.
* Distinguished an SSH service issue from a network-connectivity issue.
* Reviewed VirtualBox NAT, Internal Network, and Host-Only networking.
* Learned that matching IP subnets do not provide connectivity when interfaces belong to separate VirtualBox network types.
* Preserved the isolated SOC-LAB architecture while adding a separate management interface.
* Configured separate subnets for isolated lab and management traffic.
* Backed up Netplan before making network changes.
* Used `netplan generate` to validate configuration before applying it.
* Identified and corrected a Netplan configuration error.
* Used ping to verify network-layer connectivity.
* Performed successful end-to-end SSH remote-access testing.
* Reinforced the importance of client-side verification after server-side recovery.

---

## Skills Demonstrated

* Linux Service Management
* Linux Troubleshooting
* systemd
* systemd Socket Activation
* SSH Administration
* OpenSSH
* `systemctl`
* `journalctl`
* `ss`
* Network Listener Verification
* TCP Port Troubleshooting
* Incident Investigation
* Incident Recovery
* Log Analysis
* TCP/IP Troubleshooting
* VirtualBox Networking
* NAT
* Internal Network
* Host-Only Networking
* Linux Network Interfaces
* Netplan
* YAML Configuration
* Network Configuration Validation
* Remote Access Troubleshooting
* End-to-End Service Verification
* Root Cause Isolation
* Technical Documentation

---

# Outcome

Successfully completed the Linux Service Management & Troubleshooting lab by investigating SSH service behavior, identifying systemd socket activation, simulating a controlled SSH availability incident, verifying the outage, restoring SSH availability, reviewing system logs, and validating recovery.

During final end-to-end testing, a separate VirtualBox host-to-VM connectivity issue was identified.

The existing SOC-LAB Internal Network was preserved and a dedicated Host-Only management network was introduced.

The Ubuntu management interface was successfully configured as:

```text
192.168.57.20/24
```

and the Windows Host-Only interface as:

```text
192.168.57.1/24
```

Windows-to-Ubuntu connectivity was successfully verified using ping.

A remote SSH connection was then established using:

```text
ssh ankit@192.168.57.20
```

Final verification confirmed:

```text
User: ankit
Hostname: ubuntuserver
```

The lab demonstrated a structured troubleshooting process using service state, socket state, TCP listeners, system logs, network architecture, configuration validation, and end-to-end client testing.

---

## Repository Information

**Repository:** Enterprise-IT-Support-Lab
**Section:** 02-Linux
**Lab:** 06-Linux-Troubleshooting
**Documentation:** Documentation/Linux-Troubleshooting.md
**Screenshots:** Screenshots/
**Status:** Completed
**Version:** 1.0

