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
- `01-Documentation/Linux-User-Management.md`

Screenshots:
- `02-Screenshots/03-Linux-User-Management/`

### Next Steps

- Linux Group Management
- File Permissions
- Sudo Privileges
- User Switching (`su`)


# Repository Information

**Repository:** Enterprise IT Support Lab

**Author:** Ankit Gupta

**GitHub Repository:**
https://github.com/guptaankits937/Enterprise-IT-Support-Lab

**Last Updated:** 05 August 2026
