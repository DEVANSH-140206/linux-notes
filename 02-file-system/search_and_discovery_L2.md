# Lesson 6 — Finding Files & Inspecting Them Like a Pentester

---

# Why This Lesson Matters

As a Linux user, system administrator, or penetration tester, you'll constantly need to answer questions like:

- Where is a specific file?
- Which files contain a certain password or keyword?
- Where is a program installed?
- Is this file actually what it claims to be?
- Who owns this file?
- When was this file modified?
- Which files have dangerous permissions?

Linux provides specialized commands for each of these jobs. They may all seem like "search" commands at first, but each solves a different problem.

---

# The Big Picture

Think of the Linux filesystem as a huge library.

```
Linux Filesystem
│
├── Search for files by name        → find
├── Search inside file contents     → grep
├── Search quickly using database   → locate
├── Find executable location        → which
├── Find executable + manuals       → whereis
├── Identify real file type         → file
└── View file metadata              → stat
```

Each command answers a different question.

---

# Command Comparison

| Question | Command |
|----------|----------|
| Where is a file named notes.txt? | find |
| Where is it quickly? | locate |
| Which files contain the word password? | grep |
| Where is the nmap executable? | which |
| Where are the executable and manual pages? | whereis |
| What type of file is this really? | file |
| Who owns this file and when was it modified? | stat |

---

# COMMAND 1 — find

## Purpose

Searches for files and directories based on different properties.

Unlike grep, it does NOT read file contents.

It searches:

- File names
- Directories
- Permissions
- Size
- Owner
- Time
- Type
- And many more properties

Think of it as searching addresses, not the contents inside them.

---

# Grammar

```bash
find START_DIRECTORY OPTIONS
```

Example

```bash
find . -name "notes.txt"
```

Breakdown

```
find
│
├── .
│     Current directory
│
├── -name
│     Search by filename
│
└── "notes.txt"
      Exact filename
```

---

# Starting Locations

Current directory

```bash
find .
```

Home directory

```bash
find ~
```

Desktop

```bash
find ~/Desktop
```

Entire filesystem

```bash
sudo find /
```

Remember

```
.

Current Directory

~

Home Directory

/

Root of Linux
```

---

# Searching by Filename

Find an exact file

```bash
find . -name "passwords.txt"
```

---

Ignore uppercase/lowercase

```bash
find . -iname "passwords.txt"
```

Matches

```
passwords.txt
Passwords.txt
PASSWORDS.TXT
```

---

# Wildcards

The * wildcard means

"Anything"

It can match zero or more characters.

Examples

```
*.txt
```

Matches

```
notes.txt
linux.txt
report.txt
```

---

```
n*
```

Matches

```
notes
network
nikto
nmap
```

---

```
*map*
```

Matches

```
nmap
sqlmap
mapping
```

---

# Search Only Files

```bash
find . -type f
```

Output

```
notes.txt
script.py
report.pdf
```

---

# Search Only Directories

```bash
find . -type d
```

Output

```
Desktop
Downloads
CyberLab
```

---

# Find Empty Files

```bash
find . -empty
```

Useful for

- Empty logs
- Empty configuration files
- Unused files

---

# Search by Size

Larger than 100 MB

```bash
find . -size +100M
```

Smaller than 1 MB

```bash
find . -size -1M
```

Exactly 10 MB

```bash
find . -size 10M
```

---

# Search by Time

Modified within the last day

```bash
find . -mtime -1
```

Modified more than 30 days ago

```bash
find . -mtime +30
```

Useful for

- Recent logs
- Recent malware
- Old backups

---

# Search by Owner

Files owned by kali

```bash
find /home -user kali
```

Files owned by root

```bash
find / -user root
```

---

# Search by Permissions

World writable files

```bash
find / -perm -002
```

These are interesting because anyone can modify them.

---

Find SUID binaries

```bash
find / -perm -4000
```

Very important for privilege escalation.

---

# Delete While Searching

Delete every txt file

```bash
find . -name "*.txt" -delete
```

Very dangerous.

Always verify your search results before using `-delete`.

---

# Execute Commands on Search Results

One of find's most powerful features.

Display every txt file

```bash
find . -name "*.txt" -exec cat {} \;
```

Breakdown

```
-exec

Execute another command

{}

Current file that find found

\;

End of command
```

---

Delete every log

```bash
find . -name "*.log" -exec rm {} \;
```

---

Make every shell script executable

```bash
find . -name "*.sh" -exec chmod +x {} \;
```

---

# COMMAND 2 — locate

## Purpose

Find files extremely quickly.

Unlike find, locate does NOT search the disk live.

Instead, it searches a pre-built database.

Think of it like a phonebook.

```
find

Walks through every folder

↓

Slower

--------------------

locate

Looks inside a database

↓

Very Fast
```

---

Example

```bash
locate rockyou.txt
```

Output

```
/usr/share/wordlists/rockyou.txt
```

---

# Why locate Sometimes Fails

If you created a file recently, locate may not know it exists.

Update the database

```bash
sudo updatedb
```

Then search again.

---

# find vs locate

find

✔ Searches live filesystem

✔ Always current

❌ Slower

locate

✔ Very fast

✔ Great for known files

❌ Database may be outdated

---

# COMMAND 3 — which

## Purpose

Shows which executable Linux will run when you type a command.

Example

```bash
which python
```

Output

```
/usr/bin/python
```

Another example

```bash
which nmap
```

Output

```
/usr/bin/nmap
```

Useful when multiple versions of a program exist.

---

# COMMAND 4 — whereis

Purpose

Shows

- Executable
- Manual pages
- Source files (if available)

Example

```bash
whereis nmap
```

Output

```
nmap:
/usr/bin/nmap
/usr/share/man/man1/nmap.1.gz
```

Difference

which

Executable only

whereis

Executable

+

Manual pages

+

Source locations

---

# COMMAND 5 — file

Purpose

Determines the real type of a file.

Linux does NOT trust filename extensions.

Example

```bash
file attack.py
```

Output

```
Python script
```

Example

```bash
file photo.jpg
```

Output

```
JPEG image
```

Suppose someone renames

```
virus.exe

↓

cat.jpg
```

Run

```bash
file cat.jpg
```

Linux examines the file's internal structure rather than its name.

This helps identify disguised executables or suspicious files.

---

# COMMAND 6 — stat

Purpose

Displays detailed metadata about a file.

Example

```bash
stat notes.txt
```

Shows

- File size
- Permissions
- Owner
- Group
- Access time
- Modification time
- Change time
- Inode number
- Number of hard links

Useful for

- Digital forensics
- Incident response
- Permission auditing
- File investigation

---

# grep vs find (Very Important)

Many beginners confuse these commands.

Remember this rule forever.

find asks

"What files match these properties?"

Examples

```
Find every PHP file

Find every log

Find every file larger than 1 GB

Find every file owned by root
```

grep asks

"What files contain this text?"

Examples

```
Find the word password

Find admin

Find API keys

Find SQL queries
```

Think

```
find

↓

Search filenames and properties

----------------------

grep

↓

Open files

↓

Read contents

↓

Search text
```

---

# Practical Pentester Commands

Find every shell script

```bash
find / -name "*.sh"
```

Find backup files

```bash
find / -name "*.bak"
```

Find SSH private keys

```bash
find / -name "id_rsa"
```

Find password-related files

```bash
find / -iname "*pass*"
```

Find log files

```bash
find /var/log -name "*.log"
```

Find PHP files

```bash
find /var/www -name "*.php"
```

Find world-writable files

```bash
find / -perm -002
```

Find SUID binaries

```bash
find / -perm -4000
```

Find huge files

```bash
find / -size +500M
```

Find files modified today

```bash
find . -mtime -1
```

Locate the rockyou wordlist

```bash
locate rockyou.txt
```

Locate the nmap executable

```bash
which nmap
```

Locate executable and manual

```bash
whereis hydra
```

Determine a file's real type

```bash
file suspicious_file
```

Inspect detailed metadata

```bash
stat suspicious_file
```

Search every file for the word "password"

```bash
grep -R "password" .
```

---

# Real Pentesting Workflow

Imagine you've gained access to a Linux server.

You need to investigate it.

Questions you might ask:

Where are all PHP files?

```bash
find /var/www -name "*.php"
```

Do any of those files contain passwords?

```bash
grep -R "password" /var/www
```

Where is the rockyou wordlist?

```bash
locate rockyou.txt
```

Which nmap executable will run?

```bash
which nmap
```

Where are nmap's executable and manual?

```bash
whereis nmap
```

Is this downloaded file really a PDF?

```bash
file suspicious.pdf
```

Who owns this file, what are its permissions, and when was it modified?

```bash
stat suspicious.pdf
```

---

# Key Takeaways

- **find** → Search files/directories by properties (name, size, owner, permissions, time, etc.).
- **locate** → Search files quickly using an indexed database.
- **grep** → Search inside file contents for text or patterns.
- **which** → Show the executable that will run from your PATH.
- **whereis** → Show executable, manual pages, and related resources.
- **file** → Identify a file's true type, regardless of its extension.
- **stat** → Display detailed metadata about a file.

Never confuse **find** with **grep**:

- **find** answers: *"Which file is it?"*
- **grep** answers: *"Which file contains this text?"*

Understanding this distinction is fundamental for Linux administration, cybersecurity, and penetration testing.