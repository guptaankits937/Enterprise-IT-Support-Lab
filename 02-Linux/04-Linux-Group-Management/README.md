# Linux Group Management

## Overview

This lab demonstrates practical Linux group administration in an Ubuntu Server environment.

The scenario simulates an IT Operations request to create a Linux group, provide an existing user with group-based access, verify the membership, revoke the access, and remove the temporary group after completing the task.

This lab is part of the **Enterprise IT Support Lab** portfolio.

---

## Ticket Information

**Ticket ID:** INC-0002  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed  

---

## Scenario

The IT Operations team received a request to provide an existing Linux user with access to resources assigned to the IT Support team.

A new Linux group named `it-support` needed to be created.

The existing user `john` needed to be added to the group and the membership verified before access could be considered successfully assigned.

After testing the group membership, the user's access was removed and the temporary group was deleted as part of the cleanup process.

---

## Environment

- Ubuntu Server
- Linux Terminal
- Sudo Privileges
- Local User and Group Management
- Existing User Account: `john`

---

## Tasks Completed

During this lab, I performed the following tasks:

1. Verified the current Linux user and group memberships.
2. Checked whether the `it-support` group already existed.
3. Created the `it-support` group.
4. Verified the new group and its Group ID (GID).
5. Verified the existing `john` user.
6. Added `john` to the `it-support` supplementary group.
7. Verified the updated group membership using `id` and `getent`.
8. Confirmed that the user's primary group remained unchanged.
9. Removed `john` from the `it-support` group.
10. Verified successful access removal.
11. Deleted the temporary `it-support` group.
12. Verified that the group no longer existed.
13. Documented the implementation and captured supporting evidence.

---

## Key Commands

```bash
whoami
```

```bash
id
```

```bash
getent group it-support
```

```bash
sudo groupadd it-support
```

```bash
id john
```

```bash
sudo usermod -aG it-support john
```

```bash
sudo gpasswd -d john it-support
```

```bash
sudo groupdel it-support
```

---

## Verification

The following checks confirmed that the task was completed successfully:

- The `it-support` group was created successfully.
- The new group received GID `1002`.
- The existing `john` user was verified.
- `john` was successfully added to the supplementary group.
- Membership was verified using both `id` and `getent`.
- The user's primary group remained unchanged.
- `john` was successfully removed from the supplementary group.
- Access removal was verified.
- The temporary `it-support` group was deleted.
- Final verification confirmed that the group no longer existed.

---

## Troubleshooting

No command errors occurred during this lab.

An important administrative consideration was the use of:

```bash
sudo usermod -aG it-support john
```

The `-a` option was used together with `-G` to append the new supplementary group membership.

Using `usermod -G` without `-a` can replace existing supplementary group memberships, so the command should be used carefully in production environments.

Verification commands were performed after each major change to confirm that the intended configuration had been applied successfully.

---

## Evidence

Screenshots captured during the practical lab include:

- `01-current-user-and-groups.png`
- `02-create-and-verify-group.png`
- `03-id-john-before-group.png`
- `04-add-john-to-it-support.png`
- `05-remove-john-from-group.png`
- `06-delete-and-verify-group.png`

Supporting screenshots are available in the [`Screenshots`](./Screenshots/) directory.

---

## Detailed Documentation

Complete technical documentation, including command explanations, verification results, administrative notes, and lessons learned, is available here:

[`Linux-Group-Management.md`](./Documentation/Linux-Group-Management.md)

---

## Skills Demonstrated

- Linux Group Administration
- Linux User Administration
- User and Group Management
- Access Management
- Group Membership Verification
- Primary and Supplementary Groups
- Linux Verification Commands
- Access Revocation
- Basic Troubleshooting
- System Administration
- Incident/Ticket Documentation
- Technical Documentation

---

## Interview Relevance

This lab provides practical examples that can be discussed during IT Support, Application Support, System Administration, and junior cybersecurity interviews.

Examples include:

- How to create and verify a Linux group.
- How Linux Group IDs (GIDs) are used.
- How to add a user to a supplementary group.
- Why `usermod -aG` is important when modifying group membership.
- How to distinguish between primary and supplementary groups.
- How to verify group membership using `id` and `getent`.
- How to revoke group-based access.
- How to verify and clean up temporary administrative changes.

---

## Outcome

The Linux group was successfully created and verified, and the existing user was successfully assigned to the supplementary group.

The user's access was later revoked, the change was verified, and the temporary group was successfully removed.

The practical task demonstrated a structured approach to Linux group administration, access management, verification, cleanup, and technical documentation.

---

## Repository Information

**Project:** Enterprise IT Support Lab  
**Section:** Linux Administration  
**Lab:** 04 - Linux Group Management  
**Status:** Completed
