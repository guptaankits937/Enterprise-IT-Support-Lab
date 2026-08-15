# Linux File Permissions

## Lab Information

**Lab Name:** Linux File Permissions  
**Project:** Enterprise IT Support Lab  
**Date:** 10 August 2026  
**Operating System:** Ubuntu Server

### Objective:

Learn how to manage Linux file permissions and ownership using standard system administration commands.

The lab demonstrates how to inspect file permissions, modify access using `chmod`, change file ownership using `chown`, test access from different user accounts, verify read/write permissions, troubleshoot command errors, and perform cleanup after completing administrative tasks.

---

## Ticket Information

**Ticket ID:** INC-0003  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed

---

## Scenario

The IT Operations team needed to secure a support report containing internal incident information.

A test file named `support-report.txt` was created and its default permissions were reviewed.

The file permissions needed to be restricted so that:

- The file owner could read and modify the file.
- Members of the assigned group could read the file.
- Other users had no access.

The file ownership was then transferred to the existing user `john`.

Access was tested from both the `john` and `ankit` user contexts to confirm that the configured Linux permissions were working as expected.

After successful testing, the temporary lab resources were removed.

---

## Environment

- Ubuntu Server
- Terminal
- Sudo Privileges
- Local User Management
- Existing administrative user: `ankit`
- Existing test user: `john`
- Test file: `support-report.txt`
- Test directory: `permissions-lab`

---

## Lab Duration

**Estimated Time:** 30–40 Minutes

---

## Commands Used

### 1. Verify Current Logged-in User

```bash
whoami
```

**Result:**

```text
ankit
```

**Purpose:**

Verify which user account was currently being used before performing file permission and ownership administration.

---

### 2. Verify Current Working Directory

```bash
pwd
```

**Result:**

```text
/home/ankit
```

**Purpose:**

Confirm the current working directory before creating the temporary lab environment.

---

### 3. Display Current User Information

```bash
id
```

**Purpose:**

Display information about the current user, including:

- User ID (UID)
- Primary Group ID (GID)
- Supplementary group memberships

This established the user and group context before modifying file permissions.

---

### 4. Create the Lab Directory

```bash
mkdir permissions-lab
```

**Purpose:**

Create a dedicated temporary directory for the file-permissions lab.

---

### 5. Enter the Lab Directory

```bash
cd permissions-lab
```

**Purpose:**

Move into the newly created lab directory before creating the test file.

---

### 6. Create the Test File

```bash
touch support-report.txt
```

**Purpose:**

Create an empty test file named `support-report.txt`.

The file represents an internal IT support report requiring controlled access.

---

### 7. Inspect Default File Permissions

```bash
ls -l
```

**Observed Result:**

```text
-rw-rw-r-- 1 ankit ankit 0 Aug 10 16:41 support-report.txt
```

**Purpose:**

Inspect the default permissions, owner, and group assigned to the newly created file.

The output showed:

- Owner: `ankit`
- Group: `ankit`
- Owner permissions: `rw-`
- Group permissions: `rw-`
- Others permissions: `r--`

---

# Understanding Linux Permission Structure

The permission string:

```text
-rw-rw-r--
```

can be divided into four sections:

```text
- | rw- | rw- | r--
```

The first character identifies the file type.

```text
-
```

indicates a regular file.

The remaining permissions are divided into:

- **Owner**
- **Group**
- **Others**

For this file:

```text
rw-
```

means the owner can read and write.

```text
rw-
```

means the group can read and write.

```text
r--
```

means other users can only read the file.

---

## 8. Restrict File Permissions

```bash
chmod 640 support-report.txt
```

**Purpose:**

Change the permissions of `support-report.txt` using numeric permission notation.

---

## 9. Verify Updated Permissions

```bash
ls -l support-report.txt
```

**Result:**

```text
-rw-r----- 1 ankit ankit 0 Aug 10 16:41 support-report.txt
```

The permission configuration was successfully changed to:

```text
640
```

---

# Understanding Permission 640

Linux numeric permissions use the following values:

- `4` = Read
- `2` = Write
- `1` = Execute

Permissions can be combined by adding these values.

### Owner — 6

```text
4 + 2 = 6
```

Therefore:

```text
6 = read + write = rw-
```

### Group — 4

```text
4 = read = r--
```

### Others — 0

```text
0 = no permissions = ---
```

Therefore:

```text
640
```

produces:

```text
-rw-r-----
```

This means:

- **Owner:** Read + Write
- **Group:** Read only
- **Others:** No access

This configuration follows the principle of restricting access to only users who require it.

---

## 10. Verify the Existing Test User

```bash
id john
```

**Observed Result:**

The command confirmed that the existing user `john` was available for ownership and access testing.

The user had UID `1001` and the primary group `john`.

---

## 11. Change File Ownership

The first attempt contained a filename typo:

```bash
sudo chown john suport-report.txt
```

Linux returned:

```text
chown: cannot access 'suport-report.txt': No such file or directory
```

The filename was reviewed and corrected:

```bash
sudo chown john support-report.txt
```

**Purpose:**

Change the owner of `support-report.txt` from `ankit` to `john`.

---

## 12. Verify File Ownership

```bash
ls -l support-report.txt
```

**Result:**

```text
-rw-r----- 1 john ankit 0 Aug 10 16:41 support-report.txt
```

The output confirmed:

- Owner: `john`
- Group: `ankit`
- Permissions: `640`

Only the file owner was changed.

The file's group remained `ankit`.

---

## 13. Change Both Owner and Group

```bash
sudo chown john:john support-report.txt
```

**Purpose:**

Change both the file owner and assigned group.

In the syntax:

```text
john:john
```

the value before the colon represents the **owner**, while the value after the colon represents the **group**.

---

## 14. Verify Owner and Group

```bash
ls -l support-report.txt
```

**Result:**

```text
-rw-r----- 1 john john 0 Aug 10 16:41 support-report.txt
```

The output confirmed:

- Owner: `john`
- Group: `john`
- Permissions: `640`

---

# Access Control Testing

After assigning ownership to `john:john`, access was tested from different user contexts.

Because the permissions were:

```text
-rw-r-----
```

the expected access was:

| User Context | Access |
| --- | --- |
| Owner `john` | Read + Write |
| Group `john` | Read |
| Other users | No access |

---

## 15. Test Access as Ankit

```bash
cat support-report.txt
```

**Result:**

```text
cat: support-report.txt: Permission denied
```

**Purpose:**

Verify whether the `ankit` account could read the file after ownership had been assigned to `john:john`.

The `Permission denied` result confirmed that the configured permissions prevented unauthorized access.

---

## 16. Test Access as John

```bash
sudo -u john cat support-report.txt
```

**Purpose:**

Execute the `cat` command using the `john` user context.

No permission error occurred.

At this stage the file was empty, so there was no content to display.

This confirmed that the file owner could access the file.

---

## 17. Test Owner Write Permission

```bash
sudo -u john sh -c 'echo "IT Support Incident Report" > support-report.txt'
```

**Purpose:**

Verify that `john`, as the file owner, could write data to the file.

The command successfully wrote:

```text
IT Support Incident Report
```

to `support-report.txt`.

---

## 18. Verify Owner Read Permission

```bash
sudo -u john cat support-report.txt
```

**Result:**

```text
IT Support Incident Report
```

**Purpose:**

Confirm that the file owner could successfully read the content after writing it.

This verified both **read** and **write** permissions for the owner.

---

## 19. Verify Unauthorized Access Again

```bash
cat support-report.txt
```

**Result:**

```text
cat: support-report.txt: Permission denied
```

**Purpose:**

Confirm that the `ankit` user still could not access the protected file.

This demonstrated that the access restrictions remained effective after content was added.

---

## Troubleshooting

## Issue

During the ownership change, an incorrect filename was entered:

```bash
sudo chown john suport-report.txt
```

The filename contained a typo:

```text
suport-report.txt
```

instead of:

```text
support-report.txt
```

### Error

Linux returned:

```text
No such file or directory
```

### Resolution

The filename was reviewed and the command was corrected:

```bash
sudo chown john support-report.txt
```

The ownership change then completed successfully.

### Troubleshooting Process

1. Reviewed the Linux error message.
2. Checked the target filename.
3. Identified the spelling error.
4. Corrected the command.
5. Re-ran the command.
6. Verified the ownership using `ls -l`.

This demonstrates the importance of carefully reviewing command syntax and Linux error messages during system administration.

---

## Cleanup

Before removing the temporary lab resources, ownership was restored using:

```bash
sudo chown ankit:ankit support-report.txt
```

The session then returned to the parent directory:

```bash
cd ..
```

The temporary lab directory was removed:

```bash
rm -r permissions-lab
```

A subsequent lookup for a file returned:

```text
No such file or directory
```

because the temporary lab directory had already been removed.

### Verification Note

A separate:

```bash
ls -l support-report.txt
```

verification of the restored `ankit:ankit` ownership was not captured before deleting the lab directory.

Therefore, this documentation records that the ownership restoration command was executed but does **not** claim a separately captured post-restoration ownership verification.

---

## Verification Results

The lab successfully demonstrated that:

- The current user and environment could be verified.
- A dedicated test directory and file could be created.
- Default Linux file permissions could be inspected.
- File permissions could be changed using `chmod`.
- Numeric permission `640` could be interpreted correctly.
- File ownership could be changed using `chown`.
- Both owner and group could be changed using `owner:group` syntax.
- Unauthorized file access could be blocked.
- Owner read access could be verified.
- Owner write access could be verified.
- Linux permission enforcement could be tested from different user contexts.
- Command errors could be identified and corrected.
- Temporary lab resources could be removed after testing.

---

## Evidence

Screenshots:

1. `01-current-user-environment.png`
2. `02-create-file-default-permissions.png`
3. `03-change-file-permissions-chmod.png`
4. `04-change-file-ownership-chown.png`
5. `05-change-owner-and-group.png`
6. `06-test-file-access-permissions.png`
7. `07-verify-owner-read-write-access.png`
8. `08-restore-ownership-and-cleanup.png`

---

## Lessons Learned

- Learned how Linux represents file permissions.
- Understood owner, group, and others permission categories.
- Learned the meaning of read (`r`), write (`w`), and execute (`x`) permissions.
- Used numeric permission notation with `chmod`.
- Understood how permission value `640` is calculated.
- Changed file ownership using `chown`.
- Changed both file owner and group.
- Tested file access using different user contexts.
- Verified owner read and write permissions.
- Verified that unauthorized access was denied.
- Used Linux error messages to identify a filename typo.
- Corrected an administrative command after troubleshooting.
- Learned the importance of verifying configuration changes before cleanup.
- Removed temporary lab resources after completing the task.

---

## Skills Demonstrated

- Linux File Permission Management
- Linux Access Control
- `chmod`
- Numeric Linux Permissions
- `chown`
- File Ownership Management
- User and Group Permissions
- Access Verification
- User Context Testing
- Principle of Least Privilege
- Linux Troubleshooting
- System Administration
- Technical Documentation

---

## Outcome

Successfully completed the Linux File Permissions lab by creating and securing a test file, modifying its permissions using `chmod`, changing ownership using `chown`, and testing access from different user contexts.

The lab demonstrated that the designated owner could read and modify the protected file while an unauthorized user was denied access.

The exercise also demonstrated basic Linux troubleshooting and the importance of verification and cleanup during system administration tasks.

---

## Repository Information

**Repository:** Enterprise-IT-Support-Lab  
**Lab:** `02-Linux/05-Linux-File-Permissions/`  
**Documentation:** `02-Linux/05-Linux-File-Permissions/Documentation/Linux-File-Permissions.md`  
**Screenshots:** `02-Linux/05-Linux-File-Permissions/Screenshots/`  
**Status:** Completed  
**Version:** 1.0
