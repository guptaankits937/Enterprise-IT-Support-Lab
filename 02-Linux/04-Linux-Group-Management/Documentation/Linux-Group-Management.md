# Linux Group Management

## Lab Information

**Lab Name:** Linux Group Management  
**Project:** Enterprise IT Support Lab  
**Date:** 08 August 2026  
**Operating System:** Ubuntu Server  

### Objective

Learn how to create, verify, assign, remove, and delete Linux groups using standard system administration commands.

The lab also demonstrates the difference between primary and supplementary groups and shows how group membership can be used to manage user access.

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
- Terminal
- Sudo Privileges
- Local User and Group Management
- Existing user account: `john`

---

## Lab Duration

**Estimated Time:** 20–30 Minutes

---

## Commands Used

### 1. Check Current Logged-in User

```bash
whoami
```

**Purpose:**  
Verify the currently logged-in user before performing administrative tasks.

The command confirmed that the administrative session was being performed using the expected account.

---

### 2. Display Current User and Group Information

```bash
id
```

**Purpose:**  
Display information about the currently logged-in user, including:

- User ID (UID)
- Primary Group ID (GID)
- Supplementary group memberships

This provided a baseline for understanding Linux user and group membership.

---

### 3. Check Whether the Group Already Exists

```bash
getent group it-support
```

**Purpose:**  
Verify whether a group named `it-support` already existed before attempting to create it.

No output was returned, confirming that the group did not exist.

---

### 4. Create the IT Support Group

```bash
sudo groupadd it-support
```

**Purpose:**  
Create a new Linux group named `it-support`.

The command completed successfully without returning an error.

---

### 5. Verify the New Group

```bash
getent group it-support
```

**Result:**

```text
it-support:x:1002:
```

**Purpose:**  
Confirm that the `it-support` group was created successfully.

The result showed:

- Group name: `it-support`
- Group ID (GID): `1002`
- No supplementary members assigned yet

---

### 6. Verify the Existing User

```bash
id john
```

**Result before group assignment:**

```text
uid=1001(john) gid=1001(john) groups=1001(john)
```

**Purpose:**  
Confirm that the existing user `john` was available before modifying group membership.

The output showed that `john` initially belonged only to the user's primary group.

---

### 7. Add User to the IT Support Group

```bash
sudo usermod -aG it-support john
```

**Purpose:**  
Add the existing user `john` to the `it-support` supplementary group.

#### Understanding `-aG`

- `-a` means **append**.
- `-G` specifies the supplementary group or groups.

Using `-aG` is important because it adds the new group membership without replacing the user's existing supplementary group memberships.

---

### 8. Verify Updated User Membership

```bash
id john
```

**Result after group assignment:**

```text
uid=1001(john) gid=1001(john) groups=1001(john),1002(it-support)
```

**Purpose:**  
Verify that `john` had successfully been added to the `it-support` group.

The output confirmed that:

- `john` remained the user's primary group.
- `it-support` was added as a supplementary group.

---

### 9. Verify Group Membership Directly

```bash
getent group it-support
```

**Result:**

```text
it-support:x:1002:john
```

**Purpose:**  
Verify the group membership directly from the Linux group database.

The result confirmed that `john` was a member of the `it-support` group.

---

### Primary vs Supplementary Groups

Linux users have a **primary group** and may also belong to one or more **supplementary groups**.

For the user `john`:

```text
gid=1001(john)
```

shows that `john` is the primary group.

After adding the user to `it-support`:

```text
groups=1001(john),1002(it-support)
```

shows that `it-support` is an additional supplementary group.

Supplementary groups are commonly used to grant users access to shared resources without changing their primary group.

---

### 10. Remove User from the IT Support Group

```bash
sudo gpasswd -d john it-support
```

**Result:**

```text
Removing user john from group it-support
```

**Purpose:**  
Remove `john` from the `it-support` supplementary group when the temporary access was no longer required.

This demonstrates access revocation as part of the user access lifecycle.

---

### 11. Verify User Access Removal

```bash
id john
```

**Result:**

```text
uid=1001(john) gid=1001(john) groups=1001(john)
```

**Purpose:**  
Confirm that `john` was no longer a member of the `it-support` group.

The output showed that the user had returned to only the original primary group membership.

---

### 12. Verify the Group After User Removal

```bash
getent group it-support
```

**Result:**

```text
it-support:x:1002:
```

**Purpose:**  
Confirm that the `it-support` group still existed but no longer contained `john` as a supplementary member.

---

### 13. Delete the Temporary Group

```bash
sudo groupdel it-support
```

**Purpose:**  
Delete the `it-support` group after the access-management test was completed.

This demonstrates proper cleanup of temporary administrative resources.

---

### 14. Verify Group Deletion

```bash
getent group it-support
```

**Purpose:**  
Confirm that the group had been successfully deleted.

No output was returned, confirming that `it-support` no longer existed.

---

## Verification Results

The following checks confirmed successful completion of the ticket:

- Current user and group memberships were verified.
- The `it-support` group was created successfully.
- The new group received GID `1002`.
- Existing user `john` was verified.
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

The following screenshots were captured during the lab:

1. `01-current-user-and-groups.png` — Verified the current user and group information.
2. `02-create-and-verify-group.png` — Confirmed creation and verification of the `it-support` group.
3. `03-id-john-before-group.png` — Verified `john` before supplementary group assignment.
4. `04-add-john-to-it-support.png` — Confirmed successful supplementary group assignment.
5. `05-remove-john-from-group.png` — Confirmed removal of `john` from the group.
6. `06-delete-and-verify-group.png` — Confirmed deletion and final verification of the temporary group.

---

## Lessons Learned

During this lab, I learned how to:

- Verify Linux user and group information.
- Understand how Linux Group IDs (GIDs) identify groups.
- Create and verify a new Linux group.
- Add an existing user to a supplementary group.
- Understand the purpose of the `usermod -aG` command.
- Understand the difference between primary and supplementary groups.
- Verify group membership using multiple commands.
- Remove a user's supplementary group access.
- Verify successful access revocation.
- Delete a temporary Linux group.
- Perform verification after administrative changes.
- Understand the importance of cleanup after temporary access changes.

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
- Technical Documentation

---

## Outcome

Successfully completed the Linux Group Management lab by creating and verifying a Linux group, assigning an existing user to the group, validating supplementary group membership, revoking the user's access, and removing the temporary group using standard Linux administration practices.

---

## Repository Information

**Repository:** Enterprise-IT-Support-Lab  
**Lab:** `02-Linux/04-Linux-Group-Management/`  
**Documentation:** `02-Linux/04-Linux-Group-Management/Documentation/Linux-Group-Management.md`  
**Screenshots:** `02-Linux/04-Linux-Group-Management/Screenshots/`  
**Status:** Completed  
**Version:** 1.0
