# Linux Process Management

## Lab Information

**Lab Name:** Linux Process Management  
**Project:** Enterprise IT Support Lab  
**Date:** 13 August 2026  
**Operating System:** Ubuntu Server

### Objective

Learn how to identify, investigate, monitor, terminate, and verify Linux processes using standard process-management commands and a structured troubleshooting approach.

---

## Ticket Information

**Ticket ID:** INC-0005  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed

---

## Scenario

The IT Operations team received a report that a Linux-hosted application process had become unresponsive.

A controlled `sleep` process was used to safely simulate the affected application.

The process needed to be identified and investigated before corrective action was taken. Graceful termination was performed first and verified.

A second controlled process was then used to demonstrate forced termination using SIGKILL.

Final verification was performed to confirm that no test processes remained running.

---

## Environment

- Ubuntu Server
- Linux Terminal
- Bash Shell
- Standard Linux Process Management Utilities
- Controlled Lab Environment

---

## Lab Duration

**Estimated Time:** 30–40 Minutes

---

## Commands Used

### 1. Review Running Processes

```bash
ps aux
```

**Purpose:**  
Display currently running processes and review information including process owner, PID, CPU usage, memory usage, process state, and command.

---

### 2. Review PID and PPID Information

```bash
ps -ef
```

**Purpose:**  
Review running processes with PID and Parent Process ID (PPID) information to understand process relationships.

---

### 3. Monitor Processes in Real Time

```bash
top
```

**Purpose:**  
Monitor running processes, CPU utilization, memory utilization, and system activity in real time.

---

### 4. Create a Controlled Background Process

```bash
sleep 1000 &
```

**Purpose:**  
Create a harmless background process to simulate the application process being investigated.

**Observed Result:**

```text
PID: 1058
```

---

### 5. Identify the Target Process

```bash
ps aux | grep '[s]leep 1000'
```

**Purpose:**  
Locate the controlled process and confirm its PID and process owner.

**Observed Result:**

```text
User: ankit
PID: 1058
Command: sleep 1000
```

---

### 6. Investigate Process Details

```bash
ps -o pid,ppid,user,stat,etime,cmd -p 1058
```

**Purpose:**  
Inspect the target process before taking corrective action.

**Observed Result:**

```text
PID: 1058
PPID: 961
USER: ankit
STAT: S
CMD: sleep 1000
```

The `S` process state indicated that the process was sleeping.

---

### 7. Perform Graceful Termination

```bash
kill 1058
```

**Purpose:**  
Send SIGTERM to the target process and allow it to terminate gracefully.

Graceful termination was attempted before using forced termination.

---

### 8. Verify Graceful Termination

```bash
ps -p 1058 -o pid,ppid,user,stat,cmd
```

**Observed Result:**

No process entry was returned for PID `1058`.

The shell also reported:

```text
[1]+ Terminated sleep 1000
```

**Purpose:**  
Confirm that the corrective action successfully terminated the target process.

---

### 9. Create a Process for SIGKILL Testing

```bash
sleep 2000 &
```

**Purpose:**  
Create a second controlled process for demonstrating forced process termination.

**Observed Result:**

```text
PID: 1218
```

---

### 10. Perform Forced Termination

```bash
kill -9 1218
```

**Purpose:**  
Send SIGKILL to the controlled process and demonstrate forced process termination.

SIGKILL should generally be used when graceful termination is unsuccessful or when immediate forced termination is specifically required.

---

### 11. Verify Forced Termination

```bash
ps -p 1218 -o pid,ppid,user,stat,cmd
```

**Observed Result:**

No process entry was returned for PID `1218`.

The shell reported:

```text
[1]+ Killed sleep 2000
```

**Purpose:**  
Verify that the SIGKILL action successfully terminated the process.

---

### 12. Perform Final Cleanup Verification

```bash
pgrep -a sleep
```

**Observed Result:**

No output was returned.

**Purpose:**  
Confirm that no controlled `sleep` processes remained running after the troubleshooting exercise.

---

## Verification Results

The following checks confirmed successful completion of the ticket:

- Running Linux processes were reviewed.
- PID and PPID information was examined.
- Live process activity was monitored.
- A controlled application process was created and identified.
- PID `1058` was investigated before corrective action.
- Graceful termination using SIGTERM completed successfully.
- The termination of PID `1058` was independently verified.
- A second controlled process was created for SIGKILL testing.
- PID `1218` was successfully terminated using SIGKILL.
- Forced termination was independently verified.
- Final cleanup verification confirmed that no controlled `sleep` processes remained running.

---

## Troubleshooting

The simulated application process was investigated before termination.

The process PID, PPID, owner, state, runtime, and command were reviewed to ensure that the correct process had been identified.

Graceful termination was attempted first using:

```bash
kill 1058
```

The result was verified before the incident workflow continued.

A separate controlled process was used to demonstrate:

```bash
kill -9 1218
```

This demonstrated the difference between graceful termination using SIGTERM and forced termination using SIGKILL.

The troubleshooting approach followed during the lab was:

**Observe → Identify → Investigate → Act → Verify → Clean Up**

---

## Evidence

The following screenshots were captured during the lab:

1. `01-list-running-processes-ps-aux.png`
2. `02-view-pid-ppid-ps-ef.png`
3. `03-live-process-monitoring-top.png`
4. `04-create-background-process.png`
5. `05-identify-background-process.png`
6. `06-investigate-process-details.png`
7. `07-graceful-process-termination.png`
8. `08-verify-process-termination.png`
9. `09-create-process-for-sigkill-test.png`
10. `10-force-terminate-process-sigkill.png`
11. `11-verify-sigkill-termination.png`
12. `12-final-process-cleanup-verification.png`

---

## Lessons Learned

During this lab, I learned how to:

- Review running Linux processes.
- Understand PID and PPID information.
- Monitor processes using `top`.
- Create and identify background processes.
- Investigate process ownership and state.
- Use SIGTERM for graceful process termination.
- Use SIGKILL for forced process termination.
- Understand why SIGKILL should not normally be the first corrective action.
- Verify whether a process has actually terminated.
- Perform final cleanup verification.
- Follow a structured process troubleshooting workflow.

---

## Skills Demonstrated

- Linux Process Management
- Process Monitoring
- PID and PPID Investigation
- Process State Analysis
- Background Process Management
- SIGTERM
- SIGKILL
- Process Termination
- Process Verification
- Linux Troubleshooting
- Incident Investigation
- System Administration
- Technical Documentation

---

## Outcome

Successfully completed the Linux Process Management lab by identifying and investigating controlled Linux processes, performing graceful and forced process termination, and verifying the result of each corrective action.

The lab demonstrated a structured troubleshooting approach in which processes were investigated before action was taken and recovery was verified before the incident was considered resolved.

---

## Repository Information

**Repository:** Enterprise-IT-Support-Lab  
**Section:** 02-Linux  
**Lab:** 07-Linux-Process-Management  
**Documentation:** Documentation/Linux-Process-Management.md  
**Screenshots:** Screenshots/  
**Status:** Completed  
**Version:** 1.0
