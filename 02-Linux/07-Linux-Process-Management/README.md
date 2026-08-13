# Linux Process Management

## Overview

This lab demonstrates a practical Linux process investigation and recovery workflow in a controlled Ubuntu Server environment.

The scenario simulates an unresponsive application process. The objective was to identify the process, investigate its state and parent process, monitor system activity, terminate the process safely, verify the result, and understand when forced termination may be required.

The focus of this lab is not only Linux commands, but also a structured troubleshooting approach that can be applied in IT Support, Application Support, Technical Operations, and incident investigation environments.

---

## Ticket Information

- **Ticket ID:** INC-0005
- **Category:** Linux Process Management
- **Priority:** Medium
- **Environment:** Ubuntu Server
- **Status:** Resolved
- **Project:** Enterprise IT Support Lab

---

## Scenario

A Linux-hosted application is reported as unresponsive.

As the support engineer, the objective is to:

1. Review currently running processes.
2. Monitor system and process activity.
3. Identify the affected application process.
4. Investigate its PID, PPID, user, state, and runtime.
5. Attempt graceful process termination.
6. Verify that the process has stopped.
7. Understand forced termination using SIGKILL.
8. Confirm that no test processes remain after troubleshooting.

A harmless `sleep` process was used to safely simulate the affected application.

---

## Investigation and Troubleshooting Workflow

### 1. Reviewed Running Processes

Running processes were reviewed to understand the current state of the server.

```bash
ps aux
```

This provided information including process ownership, PID, CPU usage, memory usage, process state, and command.

---

### 2. Reviewed PID and PPID Relationships

```bash
ps -ef
```

This helped examine process relationships and understand how running processes are associated with their parent processes.

---

### 3. Monitored Processes in Real Time

```bash
top
```

`top` was used to observe live process activity and overall CPU and memory utilization.

In a production incident, this can help identify processes consuming excessive system resources.

---

### 4. Created a Controlled Test Process

```bash
sleep 1000 &
```

A harmless background process was created to represent the simulated unresponsive application.

Running the command in the background allowed troubleshooting to continue while the process remained active.

---

### 5. Identified the Target Process

```bash
ps aux | grep '[s]leep 1000'
```

The target process was located and its PID was identified.

Observed during the lab:

- **User:** `ankit`
- **PID:** `1058`
- **Process:** `sleep 1000`

---

### 6. Investigated Process Details

```bash
ps -o pid,ppid,user,stat,etime,cmd -p 1058
```

The process was examined before taking corrective action.

The investigation identified:

- PID
- Parent Process ID (PPID)
- Process owner
- Process state
- Elapsed runtime
- Executed command

Observed values included:

- **PID:** `1058`
- **PPID:** `961`
- **User:** `ankit`
- **State:** `S` (sleeping)
- **Command:** `sleep 1000`

This step ensured that the correct process was identified before termination.

---

### 7. Performed Graceful Termination

```bash
kill 1058
```

A normal `kill` command was used first.

By default, this sends the **SIGTERM** signal, allowing the process an opportunity to terminate gracefully.

Graceful termination should normally be preferred before using forced termination.

---

### 8. Verified Process Termination

```bash
ps -p 1058 -o pid,ppid,user,stat,cmd
```

The process entry was no longer present, confirming that PID `1058` had successfully terminated.

This demonstrated an important troubleshooting principle:

**Corrective action should always be followed by verification.**

---

## SIGKILL Demonstration

A second controlled process was created to demonstrate forced process termination.

```bash
sleep 2000 &
```

The new process was assigned PID `1218`.

It was then terminated using:

```bash
kill -9 1218
```

`kill -9` sends **SIGKILL**, which forces the operating system to terminate the process immediately.

SIGKILL should generally be treated as a last-resort action when a process does not respond to normal termination.

---

## SIGKILL Verification

```bash
ps -p 1218 -o pid,ppid,user,stat,cmd
```

No process entry was returned and the shell reported the process as killed, confirming successful forced termination.

---

## Final Cleanup Verification

```bash
pgrep -a sleep
```

No output was returned.

This confirmed that no controlled `sleep` processes remained after the investigation.

---

## Key Commands

| Command | Purpose |
|---|---|
| `ps aux` | Display running processes and resource information |
| `ps -ef` | Display processes including PID and PPID relationships |
| `top` | Monitor processes and system resources in real time |
| `sleep 1000 &` | Create a controlled background process |
| `ps aux \| grep '[s]leep 1000'` | Locate the simulated application process |
| `ps -o pid,ppid,user,stat,etime,cmd -p PID` | Investigate detailed process information |
| `kill PID` | Send SIGTERM for graceful termination |
| `kill -9 PID` | Send SIGKILL for forced termination |
| `pgrep -a sleep` | Search for remaining sleep processes |

---

## Troubleshooting Approach

The lab followed a structured incident workflow:

**Observe → Identify → Investigate → Act → Verify → Clean Up**

Rather than immediately terminating a process, process information was collected first to ensure that the correct process was being investigated.

Graceful termination was attempted before demonstrating forced termination.

The outcome of each corrective action was independently verified before the incident was considered resolved.

---

## Evidence

The following screenshots document the investigation:

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

See the `Screenshots/` directory for supporting evidence.

---

## Skills Demonstrated

- Linux process management
- Process monitoring
- PID and PPID investigation
- Process-state analysis
- CPU and memory monitoring
- Background process management
- SIGTERM and SIGKILL handling
- Troubleshooting methodology
- Incident verification
- Operational cleanup
- Technical documentation

---

## Interview Relevance

This lab demonstrates how an unresponsive Linux application process can be approached systematically.

Instead of immediately forcing termination, the process was first identified and investigated. A graceful termination was attempted and verified before forced termination was demonstrated in a separate controlled test.

This workflow reflects a practical support mindset:

**Identify the affected process → investigate its state → take the least disruptive corrective action → verify recovery.**

---

## Outcome

The simulated application processes were successfully identified, investigated, terminated, and verified.

The lab demonstrated both graceful and forced process termination while emphasizing investigation and verification before incident closure.

**Ticket Status: Resolved**

---

## Repository Information

This lab is part of the **Enterprise IT Support Lab**, a hands-on portfolio project focused on practical IT support, Linux administration, troubleshooting, incident investigation, service recovery, and operational documentation.

All activities were performed in a controlled lab environment for learning and portfolio demonstration purposes.
