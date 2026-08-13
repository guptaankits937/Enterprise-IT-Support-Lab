# Linux Process Management

## Overview

This lab demonstrates practical Linux process management and troubleshooting in an Ubuntu Server environment.

The scenario simulates an IT Operations incident involving an unresponsive application process. The lab covers process discovery, PID and PPID investigation, real-time process monitoring, controlled background process creation, graceful termination using SIGTERM, forced termination using SIGKILL, and final process cleanup verification.

A harmless `sleep` process was used to safely represent the affected application during the controlled lab scenario.

This lab is part of the **Enterprise IT Support Lab** portfolio.

---

## Ticket Information

**Ticket ID:** INC-0005  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed

---

## Scenario

The IT Operations team received a report that a Linux-hosted application process had become unresponsive.

The objective was to investigate the running processes, identify the affected process, review its process information and state, and safely terminate it.

A controlled background process was created to simulate the affected application.

The process was first terminated gracefully using SIGTERM and the result was verified.

A second controlled process was then used to demonstrate forced termination using SIGKILL and to understand why `kill -9` should be treated as a last-resort action.

Final verification was performed to confirm that no controlled test processes remained running.

---

## Environment

- Ubuntu Server
- Linux Terminal
- Bash Shell
- Linux Process Management Utilities
- Controlled Lab Environment

---

## Tasks Completed

During this lab, I performed the following tasks:

1. Reviewed currently running Linux processes.
2. Examined PID and PPID process relationships.
3. Monitored live process and system activity using `top`.
4. Created a controlled background process using `sleep`.
5. Located the simulated application process.
6. Identified the process PID.
7. Investigated the PID, PPID, user, process state, elapsed runtime, and command.
8. Performed graceful process termination using SIGTERM.
9. Verified that the process had successfully terminated.
10. Created a second controlled process for SIGKILL testing.
11. Performed forced process termination using SIGKILL.
12. Verified successful forced termination.
13. Confirmed that no controlled `sleep` processes remained running.
14. Documented the investigation and captured supporting evidence.

---

## Key Commands

```bash
ps aux
```

```bash
ps -ef
```

```bash
top
```

```bash
sleep 1000 &
```

```bash
ps aux | grep '[s]leep 1000'
```

```bash
ps -o pid,ppid,user,stat,etime,cmd -p 1058
```

```bash
kill 1058
```

```bash
ps -p 1058 -o pid,ppid,user,stat,cmd
```

```bash
sleep 2000 &
```

```bash
kill -9 1218
```

```bash
ps -p 1218 -o pid,ppid,user,stat,cmd
```

```bash
pgrep -a sleep
```

---

## Verification

The following checks confirmed that the process investigation and recovery were completed successfully:

- The controlled `sleep 1000` process was successfully identified.
- PID `1058` was confirmed as the target process during the lab.
- Process details including PID, PPID, user, state, elapsed runtime, and command were reviewed before corrective action.
- Graceful termination was performed using the default SIGTERM signal.
- PID `1058` was no longer present after termination.
- A second controlled `sleep 2000` process was created for SIGKILL testing.
- PID `1218` was forcefully terminated using SIGKILL.
- PID `1218` was no longer present after forced termination.
- `pgrep -a sleep` returned no output during final cleanup verification.
- No controlled test processes remained running after the lab.

---

## Troubleshooting

The lab followed a structured process investigation and recovery workflow.

The simulated application process was not terminated immediately after creation. Running processes were first reviewed and the target process was identified before corrective action was taken.

Detailed process information was then examined to confirm the PID, PPID, process owner, state, runtime, and executed command.

The first controlled process was terminated using:

```bash
kill 1058
```

This sends SIGTERM by default and allows the process an opportunity to terminate gracefully.

The result was independently verified using:

```bash
ps -p 1058 -o pid,ppid,user,stat,cmd
```

A second controlled process was then used to demonstrate forced termination:

```bash
kill -9 1218
```

SIGKILL forces immediate process termination and should generally be used only when normal termination is unsuccessful or inappropriate for the incident.

The forced termination was also independently verified.

Finally:

```bash
pgrep -a sleep
```

was used to confirm that no controlled test processes remained running.

The troubleshooting workflow demonstrated during the lab was:

**Observe → Identify → Investigate → Act → Verify → Clean Up**

---

## Evidence

Screenshots captured during the practical lab include:

- `01-list-running-processes-ps-aux.png`
- `02-view-pid-ppid-ps-ef.png`
- `03-live-process-monitoring-top.png`
- `04-create-background-process.png`
- `05-identify-background-process.png`
- `06-investigate-process-details.png`
- `07-graceful-process-termination.png`
- `08-verify-process-termination.png`
- `09-create-process-for-sigkill-test.png`
- `10-force-terminate-process-sigkill.png`
- `11-verify-sigkill-termination.png`
- `12-final-process-cleanup-verification.png`

Supporting screenshots are available in the [`Screenshots`](./Screenshots/) directory.

---

## Detailed Documentation

Complete technical documentation, including command explanations, process investigation, PID and PPID analysis, process-state interpretation, SIGTERM and SIGKILL handling, verification results, and lessons learned, is available here:

[`Linux-Process-Management.md`](./Documentation/Linux-Process-Management.md)

---

## Skills Demonstrated

- Linux Process Management
- Linux Command-Line Administration
- Process Discovery
- PID and PPID Investigation
- Process State Analysis
- Real-Time Process Monitoring
- Background Process Management
- SIGTERM Handling
- SIGKILL Handling
- Process Termination Verification
- Incident Investigation
- Troubleshooting Methodology
- Operational Cleanup
- Technical Documentation

---

## Interview Relevance

This lab provides practical examples that can be discussed during IT Support, Application Support, System Administration, Technical Operations, and junior cybersecurity interviews.

Examples include:

- How to investigate an unresponsive Linux application process.
- How to identify a process and its PID.
- How PID and PPID are used during process investigation.
- How to review process state and runtime information.
- How to monitor running processes using `top`.
- Why a process should be investigated before termination.
- The difference between SIGTERM and SIGKILL.
- Why graceful termination should normally be attempted before forced termination.
- How to verify that corrective action was successful.
- How to confirm that no test processes remain after troubleshooting.
- How to document a structured incident investigation and resolution.

---

## Outcome

The simulated application processes were successfully identified, investigated, terminated, and verified.

The first controlled process was terminated gracefully using SIGTERM, while a separate controlled process was used to demonstrate forced termination using SIGKILL.

Final verification confirmed that no controlled test processes remained running.

The practical task demonstrated a structured approach to Linux process investigation, process management, corrective action, recovery verification, and technical documentation.

---

## Repository Information

**Repository:** Enterprise-IT-Support-Lab  
**Section:** 02-Linux  
**Lab:** 07-Linux-Process-Management  
**Documentation:** Documentation/Linux-Process-Management.md  
**Screenshots:** Screenshots/  
**Status:** Completed  
**Version:** 1.0
