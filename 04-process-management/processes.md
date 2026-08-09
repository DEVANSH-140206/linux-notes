# Process Management

## 📌 Overview

Processes are programs running in the system.

## 🧠 Commands

- ps → list running processes

## ⚙️ Examples

ps
ps aux (havent studied yet)

## 💡 Explanation

Every command or application runs as a process.

## 🔥 Use Case

Used to detect suspicious or running services.

## 📝 Summary

Process monitoring helps in system analysis.

LESSON 8 — PROCESSES & PROCESS MANAGEMENT
Difficulty: ⭐⭐⭐⭐☆
Importance for Cybersecurity: ⭐⭐⭐⭐⭐

==================================================
1. WHAT IS A PROCESS?
==================================================

First understand the difference between a PROGRAM and a PROCESS.

PROGRAM
-------

A program is a file stored on disk.

Examples:

/usr/bin/nmap
firefox
python

A program is NOT currently running.

Think:

Recipe book sitting on a shelf
        ↓
     PROGRAM


PROCESS
-------

A process is a program that is currently running.

Example:

Firefox opened
      ↓
Running in RAM
      ↓
Uses CPU
      ↓
Has an ID
      ↓
PROCESS

Think:

Recipe book
    ↓
Program

Actually cooking
    ↓
Process


Example:

You open Firefox.

Linux creates:

Firefox
   ↓
Firefox Process


If you open:

Firefox
VS Code
Terminal
Spotify

Linux may have many processes running at the same time.


==================================================
2. PROGRAM VS PROCESS
==================================================

PROGRAM:

- Stored on disk
- Not necessarily running
- Contains instructions/code

PROCESS:

- Running instance of a program
- Loaded into memory/RAM
- Uses CPU and other resources
- Has a PID


Easy memory trick:

PROGRAM = Recipe

PROCESS = Cooking


==================================================
3. PROCESS LIFECYCLE
==================================================

Program on Disk
      ↓
User opens it
      ↓
Loaded into RAM
      ↓
CPU executes instructions
      ↓
Running Process
      ↓
Finished / Closed
      ↓
Removed from RAM


==================================================
4. PID — PROCESS ID
==================================================

PID means:

Process ID

Linux gives every process a unique number.

Example:

Firefox
   ↓
PID 2845

Chrome
   ↓
PID 3150

Nmap
   ↓
PID 4721


Think of PID like a student's roll number.

Student
   ↓
Roll Number

Process
   ↓
PID


==================================================
5. WHY DOES LINUX NEED PIDs?
==================================================

Imagine you have many Firefox-related processes.

If you simply say:

"Close Firefox"

Linux needs to know exactly which process you mean.

Instead:

Kill PID 2845

The PID identifies the exact process.


Important idea:

PID = Unique identifier for a running process


==================================================
6. PARENT AND CHILD PROCESSES
==================================================

Processes can create other processes.

Example:

You open a Terminal.

Linux creates:

Terminal
PID 5000

Then inside the Terminal you run:

nano notes.txt

Linux creates another process:

Terminal
   ↓
  nano

Terminal = Parent Process

nano = Child Process


Visual:

Terminal (Parent)
       ↓
     nano
     (Child)


This relationship is important because many Linux services,
shells, and applications create child processes.


==================================================
7. COMMAND — ps
==================================================

Command:

ps

Purpose:

Show currently running processes.


Example:

ps


You may see:

PID     TTY      TIME     CMD
2534    pts/0    00:00:00 bash
2754    pts/0    00:00:00 ps


==================================================
8. UNDERSTANDING ps OUTPUT
==================================================

PID

Process ID.

A unique number assigned to the process.


TTY

The terminal associated with the process.

For now remember:

TTY
 ↓
Which terminal is running this process?


TIME

CPU time used by the process.

IMPORTANT:

TIME does NOT simply mean how long the program has been open.

It means approximately how much CPU time the process has consumed.


CMD

The command/program that started the process.


Example:

PID     TTY      TIME        CMD
2534    pts/0    00:00:00    bash

Meaning:

PID:
2534

Terminal:
pts/0

CPU time:
00:00:00

Command:
bash


==================================================
9. WHY DOES ps SHOW SO FEW PROCESSES?
==================================================

If you run:

ps

you may only see a few processes.

Why?

Because basic:

ps

normally shows processes associated with your current terminal/session,
rather than every process running on the entire system.

Later you will learn commands/options that show much more of the system.


==================================================
10. IMPORTANT MENTAL MODEL
==================================================

PROGRAM

↓
File stored on disk


PROCESS

↓
Running instance of a program


PID

↓
Number identifying the process


PARENT

↓
Process that creates another process


CHILD

↓
Process created by another process


ps

↓
View processes


==================================================
11. CYBERSECURITY IMPORTANCE
==================================================

Processes are extremely important in cybersecurity.

When analyzing a Linux system, you may need to know:

- What programs are running?
- Which user is running them?
- What PID does a process have?
- Which process started another process?
- Which process is consuming CPU?
- Which process should be stopped?
- Is a suspicious process running?
- Is a vulnerable service running?

This is why process management is a core Linux skill for:

- Penetration testing
- CTFs
- SOC analysis
- Malware analysis
- Incident response
- System administration
- Linux security


==================================================
12. COMMANDS COMING NEXT
==================================================

The rest of Process Management will cover commands such as:

ps
ps aux
top
htop
kill
killall

and concepts such as:

PID
PPID
Foreground processes
Background processes
&
bg
fg
Process termination
Process monitoring


==================================================
13. QUICK REVISION
==================================================

PROGRAM
→ File containing instructions stored on disk.

PROCESS
→ A running instance of a program.

PID
→ Process ID; identifies a running process.

PARENT PROCESS
→ A process that creates another process.

CHILD PROCESS
→ A process created by another process.

ps
→ Displays processes.


==================================================
14. EASY MEMORY TRICK
==================================================

Think about a recipe:

RECIPE BOOK
    ↓
PROGRAM

COOKING THE RECIPE
    ↓
PROCESS

ORDER NUMBER
    ↓
PID

COOK CREATES ASSISTANT
    ↓
PARENT → CHILD

CHECK WHO IS COOKING
    ↓
ps


==================================================
15. COMMANDS LEARNED TODAY
==================================================

ps

Purpose:
Show currently running processes associated with the current
terminal/session.

Important output fields:

PID
TTY
TIME
CMD


==================================================
16. PRACTICE
==================================================

Run:

ps

Then identify:

1. What is the PID of bash?
2. What is the TTY?
3. What is the CPU TIME?
4. What command appears under CMD?
5. What is the PID of the ps command itself?

Then open another program from the terminal and run:

ps

Observe how the process list changes.


==================================================
LESSON 8 — CORE TAKEAWAY
==================================================

A PROGRAM is a file.

A PROCESS is a running program.

Every process has a PID.

Processes can have parent-child relationships.

The command:

ps

lets you view processes.

The next step is learning how to see ALL processes,
monitor them, identify suspicious processes,
and control/terminate them.
