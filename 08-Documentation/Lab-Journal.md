# Enterprise IT Support Lab Journal

## Project Overview

This repository documents my hands-on Enterprise IT Support Lab, created to strengthen practical skills in Linux Administration, Application Support, SQL Administration, Networking, Incident Management, and Technical Troubleshooting.

The objective of this project is to simulate real-world enterprise IT support tasks and document every activity professionally.

---

# Lab Environment

**Host OS**
- Windows 10

**Virtualization**
- Oracle VirtualBox

**Virtual Machines**
- Ubuntu Server 24.04 LTS
- Kali Linux (Planned)
- Windows 10 (Planned)

**Current Status**
- Ubuntu Server Installed
- SSH Enabled
- Network Connectivity Working

---

# Lab Journal

## Day 1

**Date:** 04 August 2026

### Objective

Deploy Ubuntu Server for the Enterprise IT Support Lab.

### Tasks Completed

- Installed Ubuntu Server 24.04 LTS
- Completed initial server configuration
- Verified package mirror
- Installed OpenSSH Server
- Logged into the system successfully
- Verified IP configuration
- Tested network connectivity
- Completed first system boot

### Challenges Faced

- Installation configuration review
- Network configuration verification
- SSH setup validation

### Outcome

Ubuntu Server was successfully deployed and is ready for Linux administration activities.

## Skills Demonstrated

- Ubuntu Server Installation
- Linux Administration
- OpenSSH Configuration
- Basic Networking
- Technical Documentation

## Lessons Learned

- Understood the Ubuntu Server installation process.
- Learned the importance of package mirror verification.
- Successfully configured and verified SSH access.
- Gained practical experience with basic Linux networking.
- Improved troubleshooting and documentation skills.

---

## Next Steps

- Linux User Management
- File Permissions
- SSH Administration
- Networking
- Bash Scripting

---

## Day 2

**Date:** 05 August 2026

### Ticket Information

- **Ticket ID:** INC-0001
- **Department:** IT Operations
- **Priority:** Medium
- **Status:** Completed

### Objective

Perform Linux user administration by creating and verifying a new employee account using enterprise administration practices.

### Tasks Completed

- Verified the current logged-in user (`whoami`)
- Checked user identity and group membership (`id`)
- Verified the server hostname (`hostname`)
- Created a new Linux user (`john`)
- Assigned a password to the new user
- Verified the user account using `id john`
- Verified the home directory using `ls /home`

### Commands Used

- `whoami`
- `id`
- `hostname`
- `sudo useradd -m john`
- `sudo passwd john`
- `id john`
- `ls /home`

### Challenges Faced

- Mistyped the username as `joh` while setting the password.
- Corrected the username to `john` and completed the task successfully.

### Outcome

Successfully completed the first Linux User Management ticket. The new employee account was created, secured with a password, and verified.

### Skills Demonstrated

- Linux User Administration
- Password Management
- User Verification
- Basic Linux Troubleshooting
- Command Line Administration

### Lessons Learned

- Verified user identity before performing administrative tasks.
- Understood the purpose of UID and GID.
- Learned how to create and verify Linux user accounts.
- Understood why the `-m` option creates a home directory.
- Practiced troubleshooting by correcting an invalid username.

### Evidence

Documentation:
- `02-Linux/03-Linux-User-Management/Documentation/Linux-User-Management.md`

Screenshots:
- `02-Linux/03-Linux-User-Management/Screenshots/`

### Next Steps

- Linux Group Management
- File Permissions
- Sudo Privileges
- User Switching (`su`)

---

## Day 3

**Date:** 06 August 2026

### Ticket Information

- **Ticket ID:** INC-0002
- **Department:** IT Operations
- **Priority:** Medium
- **Status:** Completed

### Objective

Perform Linux group administration by creating a group, managing user membership, verifying access configuration, and completing cleanup.

### Tasks Completed

- Verified the existing user account.
- Created a new Linux group.
- Added the user to the group.
- Verified group membership.
- Tested group administration commands.
- Removed the user from the group.
- Verified the membership change.
- Removed the test group after completing the lab.
- Documented the implementation and captured supporting evidence.

### Commands Used

- `id john`
- `sudo groupadd`
- `sudo usermod -aG`
- `getent group`
- `groups`
- `sudo gpasswd -d`
- `sudo groupdel`

### Challenges Faced

- Verified group membership at multiple stages to ensure the intended changes were applied correctly.
- Performed cleanup carefully after completing the access-management tests.

### Outcome

Successfully completed the Linux Group Management ticket by creating and managing a Linux group, modifying user membership, verifying the configuration, and completing cleanup.

### Skills Demonstrated

- Linux Group Administration
- Group Membership Management
- Access Management
- Linux Command-Line Administration
- Verification and Validation
- Technical Documentation

### Lessons Learned

- Learned how Linux groups are created and managed.
- Understood how supplementary group membership is assigned.
- Practiced verifying group configuration after administrative changes.
- Learned how users can be removed safely from groups.
- Reinforced the importance of cleanup after lab testing.

### Evidence

Documentation:
- `02-Linux/04-Linux-Group-Management/Documentation/`

Screenshots:
- `02-Linux/04-Linux-Group-Management/Screenshots/`

### Next Steps

- Linux File Permissions
- File Ownership
- Access Control
- Permission Troubleshooting

---

## Day 4

**Date:** 07 August 2026

### Ticket Information

- **Ticket ID:** INC-0003
- **Department:** IT Operations
- **Priority:** Medium
- **Status:** Completed

### Objective

Investigate and configure Linux file permissions and ownership, validate access from different user contexts, troubleshoot permission-denied scenarios, and verify the final configuration.

### Tasks Completed

- Created a controlled test directory and file.
- Inspected initial file permissions and ownership.
- Modified permissions using symbolic `chmod`.
- Verified permission changes.
- Modified permissions using numeric mode `640`.
- Changed file ownership using `chown`.
- Verified the new ownership configuration.
- Switched to another user account for access testing.
- Confirmed successful read access.
- Removed read permission for the group.
- Verified the expected `Permission denied` result.
- Restored group read permission.
- Verified that access worked again.
- Tested the effect of directory permissions.
- Investigated an unexpected access result.
- Verified parent directory permissions.
- Identified the effect of supplementary group membership.
- Corrected the test conditions and confirmed expected denial.
- Restored the directory configuration.
- Performed cleanup and verified removal of the test directory.
- Documented the lab and captured evidence.

### Commands Used

- `mkdir`
- `touch`
- `ls -l`
- `chmod`
- `chown`
- `su`
- `cat`
- `id`
- `namei -l`
- `rm -rf`

### Challenges Faced

- An expected permission denial initially did not occur during access testing.
- Investigated the complete directory path and user group membership.
- Identified that supplementary group membership affected the test result.
- Corrected the test conditions and successfully reproduced the expected permission-denied behavior.

### Outcome

Successfully completed the Linux File Permissions ticket by configuring permissions and ownership, validating access under different user contexts, troubleshooting an unexpected authorization result, restoring access, and completing cleanup.

### Skills Demonstrated

- Linux File Permissions
- `chmod`
- `chown`
- File Ownership
- Linux Access Control
- User Context Testing
- Permission Troubleshooting
- Root Cause Analysis
- Verification and Validation
- Technical Documentation

### Lessons Learned

- Learned how Linux owner, group, and other permission bits control file access.
- Practiced both symbolic and numeric permission modes.
- Understood how file ownership and group ownership affect authorization.
- Learned why directory traversal permissions matter.
- Understood how supplementary group membership can affect troubleshooting results.
- Reinforced the importance of testing permissions from the actual user context.
- Practiced restoring configuration and cleaning up after testing.

### Evidence

Documentation:
- `02-Linux/05-Linux-File-Permissions/Documentation/Linux-File-Permissions.md`

Screenshots:
- `02-Linux/05-Linux-File-Permissions/Screenshots/`

### Next Steps

- Linux Service Management
- SSH Troubleshooting
- Log Investigation
- Network Troubleshooting

---

## Day 5

**Date:** 11 August 2026

### Ticket Information

- **Ticket ID:** INC-0004
- **Department:** IT Operations
- **Priority:** Medium
- **Status:** Completed

### Objective

Investigate Linux SSH availability, understand systemd socket activation, simulate and recover from a controlled SSH outage, review system logs, troubleshoot host-to-VM connectivity, and verify remote SSH access.

### Tasks Completed

- Verified the initial SSH service status.
- Identified that SSH was using systemd socket activation.
- Verified `ssh.socket` status.
- Confirmed TCP port 22 availability.
- Simulated a controlled SSH outage by stopping `ssh.socket`.
- Verified that the SSH socket became inactive.
- Confirmed that TCP port 22 was no longer listening.
- Restored SSH availability by starting `ssh.socket`.
- Verified socket recovery and TCP port 22 availability.
- Reviewed the SSH socket incident timeline using `journalctl`.
- Investigated failed Windows-to-Ubuntu connectivity.
- Identified that the existing Ubuntu interface belonged to the isolated `SOC-LAB` Internal Network.
- Preserved the existing SOC-LAB network architecture.
- Added a dedicated VirtualBox Host-Only management adapter.
- Configured a separate `192.168.57.0/24` management network.
- Backed up the existing Netplan configuration.
- Configured the new Ubuntu `enp0s9` interface.
- Detected and corrected a Netplan configuration error.
- Validated the corrected configuration using `netplan generate`.
- Applied the configuration using `netplan apply`.
- Verified the new management interface.
- Tested Windows-to-Ubuntu connectivity using ping.
- Successfully connected to the Ubuntu Server using SSH.
- Verified the remote user and server hostname.
- Documented the incident investigation and captured supporting evidence.

### Commands Used

- `systemctl status ssh --no-pager`
- `systemctl status ssh.socket --no-pager`
- `systemctl is-active ssh.socket`
- `systemctl stop ssh.socket`
- `sudo ss -tlnp | grep ':22'`
- `sudo systemctl start ssh.socket`
- `sudo journalctl -u ssh.socket --since "today" --no-pager`
- `ip addr`
- `sudo cp /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.backup`
- `sudo nano /etc/netplan/50-cloud-init.yaml`
- `sudo netplan generate`
- `sudo netplan apply`
- `ip addr show enp0s9`
- `ping 192.168.57.20`
- `ssh ankit@192.168.57.20`
- `whoami`
- `hostname`

### Challenges Faced

- `ssh.service` initially appeared inactive, requiring investigation of systemd socket activation.
- Remote SSH testing initially failed even after the SSH socket was restored.
- Windows could not initially reach the Ubuntu `192.168.56.20` address.
- Investigation showed that the interface belonged to the isolated VirtualBox `SOC-LAB` Internal Network.
- A separate Host-Only management network was required without changing the existing SOC-LAB architecture.
- A spelling error in the Netplan `addresses` field caused configuration validation to fail.
- The Netplan configuration was corrected and successfully validated before being applied.

### Outcome

Successfully completed the Linux Service Management & Troubleshooting ticket.

The controlled SSH outage was investigated, verified, and recovered successfully. A separate VirtualBox network-connectivity issue discovered during final validation was also diagnosed and resolved.

The existing SOC-LAB network was preserved while a dedicated Host-Only management interface was configured. Windows-to-Ubuntu connectivity was restored and final SSH access was successfully verified.

### Skills Demonstrated

- Linux Service Management
- Linux Troubleshooting
- SSH Administration
- systemd Socket Activation
- `systemctl`
- `journalctl`
- TCP Port Verification
- Incident Investigation
- Incident Recovery
- Log Analysis
- TCP/IP Troubleshooting
- VirtualBox Networking
- Host-Only Networking
- Netplan Configuration
- Network Configuration Validation
- Remote Access Troubleshooting
- Root Cause Isolation
- Technical Documentation

### Lessons Learned

- Learned that an inactive `ssh.service` does not automatically mean SSH is unavailable.
- Understood how systemd socket activation works with SSH.
- Learned to verify TCP port availability independently of service status.
- Practiced controlled service outage and recovery.
- Used system logs to reconstruct an incident timeline.
- Learned to separate service-level troubleshooting from network-level troubleshooting.
- Understood the difference between VirtualBox Internal Network and Host-Only networking.
- Learned why separate subnets should be used for isolated lab and management interfaces.
- Practiced backing up and validating Netplan configuration before applying changes.
- Corrected a network configuration error using validation output.
- Verified service recovery from the client side using ping and SSH.

### Evidence

Documentation:
- `02-Linux/06-Linux-Troubleshooting/Documentation/Linux-Troubleshooting.md`

Screenshots:
- `02-Linux/06-Linux-Troubleshooting/Screenshots/`

### Next Steps

- Continue Linux Administration Labs
- Linux Process Management
- Linux Log Analysis
- Bash Scripting
- Application Support Labs
- SQL Administration Labs

---

# Repository Information

**Repository:** Enterprise IT Support Lab

**Author:** Ankit Gupta

**GitHub Repository:**  
https://github.com/guptaankits937/Enterprise-IT-Support-Lab

**Last Updated:** 11 August 2026
