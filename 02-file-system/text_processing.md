# Linux Fundamentals: Text Processing & File Analysis

## Why These Commands Matter

These commands help you **read, search, analyze, and process text files**. They are used constantly by Linux administrators, cybersecurity professionals, and penetration testers when examining logs, configuration files, scan results, and source code.

---

# grep — Search for Text

**Purpose:** Search for a word or pattern **inside file contents**.

> Think of it as **Ctrl + F** for Linux.

## Syntax

```bash
grep "text" file
```

### Example

```bash
grep "Hydra" notes.txt
```

Searches for **Hydra** inside `notes.txt`.

---

## Common Options

### Ignore Uppercase/Lowercase

```bash
grep -i hydra notes.txt
```

Matches:

```
Hydra
HYDRA
hydra
HyDrA
```

---

### Show Line Numbers

```bash
grep -n Hydra notes.txt
```

Output

```
2:Hydra
7:Hydra
```

---

### Count Matches

```bash
grep -c Hydra notes.txt
```

Shows only the number of matching lines.

---

### Show Everything Except the Match

```bash
grep -v Hydra notes.txt
```

---

### Match Whole Words Only

```bash
grep -w cat file.txt
```

Matches:

```
cat
```

Not:

```
caterpillar
category
```

---

### Search an Entire Directory

```bash
grep -r "password" .
```

- `-r` → Search recursively
- `.` → Current directory

Searches every file inside the current folder and its subfolders.

---

## Real Pentesting Examples

Find passwords

```bash
grep -ri password .
```

Find API keys

```bash
grep -ri api .
```

Search web source code

```bash
grep -ri secret /var/www/html
```

Find failed SSH logins

```bash
grep "Failed password" /var/log/auth.log
```

Find POST requests

```bash
grep "POST" /var/log/apache2/access.log
```

Search Nmap results

```bash
grep "open" scan.txt
```

---

# grep + Pipe

Combine commands together.

```bash
cat notes.txt | grep Hydra
```

Flow

```
cat
 ↓
Outputs file

grep
 ↓
Filters matching lines
```

---

# wc — Count File Statistics

**Purpose:** Count lines, words, characters, or bytes.

## Syntax

```bash
wc file
```

Output

```
Lines   Words   Characters
```

---

### Count Lines

```bash
wc -l access.log
```

Very common for counting log entries.

---

### Count Words

```bash
wc -w notes.txt
```

---

### Count Characters

```bash
wc -m notes.txt
```

---

### Count Bytes

```bash
wc -c notes.txt
```

---

## Pentesting Examples

Count users

```bash
wc -l /etc/passwd
```

Count log entries

```bash
wc -l access.log
```

Count open ports from an Nmap scan

```bash
grep "open" scan.txt | wc -l
```

---

# nl — Number Lines

**Purpose:** Display line numbers.

```bash
nl notes.txt
```

Output

```
1  Nmap
2  Hydra
3  Metasploit
```

Useful for locating exact lines while editing configuration files.

---

# Bonus Commands

## sort

Sort lines alphabetically.

```bash
sort tools.txt
```

---

## uniq

Remove duplicate **consecutive** lines.

```bash
sort passwords.txt | uniq
```

Usually used after `sort`.

---

## cut

Extract specific fields from structured text.

```bash
cut -d ":" -f1 /etc/passwd
```

- `-d` → Delimiter
- `-f` → Field number

Output

```
john
mary
kali
```

Very useful for parsing `/etc/passwd`.

---

# Common Command Combinations

Count failed SSH logins

```bash
grep "Failed password" /var/log/auth.log | wc -l
```

Count HTTP services in an Nmap scan

```bash
grep "http" scan.txt | wc -l
```

List usernames

```bash
cut -d ":" -f1 /etc/passwd
```

Unique usernames

```bash
cut -d ":" -f1 /etc/passwd | sort | uniq
```

Search current project for passwords

```bash
grep -ri password .
```

Count password occurrences

```bash
grep -ri password . | wc -l
```

---

# Quick Revision Cheat Sheet

| Command | Purpose |
|----------|---------|
| `grep` | Search text inside files |
| `grep -r` | Search recursively in directories |
| `grep -i` | Ignore case |
| `grep -n` | Show line numbers |
| `grep -c` | Count matching lines |
| `grep -v` | Show non-matching lines |
| `grep -w` | Match whole words only |
| `wc` | Count lines, words, characters |
| `wc -l` | Count lines |
| `nl` | Number lines |
| `sort` | Sort lines alphabetically |
| `uniq` | Remove duplicate consecutive lines |
| `cut` | Extract specific fields |

---

# Commands Every Pentester Uses Regularly

```bash
grep -ri password .
grep -ri secret .
grep "Failed password" /var/log/auth.log
grep "open" scan.txt
grep "http" scan.txt
grep "POST" /var/log/apache2/access.log
wc -l access.log
grep "open" scan.txt | wc -l
cut -d ":" -f1 /etc/passwd
sort passwords.txt | uniq
```