# Linux Group Management

## Overview

This lab demonstrates Linux group administration in an Ubuntu Server environment.

The objective was to create and verify a Linux group, add an existing user to the group, verify group membership, remove the user from the group, and finally remove the group after completing the task.

This lab is part of the **Enterprise IT Support Lab** project.

---

## Ticket Information

**Ticket ID:** INC-0002  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed

---

## Scenario

The IT Operations team received a request to provide an existing Linux user with access to resources assigned to the IT Support team.

A new Linux group named `it-support` was created and the existing user `john` was added to the group.

After verifying the group membership, the user's access was removed and the temporary group was deleted as part of the cleanup process.

---

## Tasks Completed

- Verified the current Linux user and group memberships.
- Created the `it-support` group.
- Verified the new group and its Group ID (GID).
- Verified the existing `john` user.
- Added `john` to the `it-support` supplementary group.
- Verified the updated group membership.
- Removed `john` from the `it-support` group.
- Verified successful access removal.
- Deleted the `it-support` group.
- Verified that the group no longer existed.

---

## Commands Used

```bash
whoami
id
getent group it-support
sudo groupadd it-support
id john
sudo usermod -aG it-support john
getent group it-support
sudo gpasswd -d john it-support
sudo groupdel it-support

---

## Repository Information

**Repository:** Enterprise-IT-Support-Lab  
**Section:** 02-Linux  
**Lab:** 04-Linux-Group-Management  
**Documentation:** Documentation/Linux-Group-Management.md  
**Screenshots:** Screenshots/  
**Status:** Completed  
**Version:** 1.0

