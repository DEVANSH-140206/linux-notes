# Linux Fundamentals: File & Directory Management

> **Goal:** Learn how to create, copy, move, rename, and delete files/directories efficiently from the terminal.

---

# `mkdir` — Create Directories

**Purpose:** Create new folders.

### Syntax

```bash
mkdir <folder_name>
```

### Example

```bash
mkdir CyberLab
```

Creates:

```
CyberLab/
```

### Create Multiple Directories

```bash
mkdir Notes Scripts Scans
```

### Create Nested Directories (`-p`)

```bash
mkdir -p CyberLab/Reports/July
```

**`-p` (Parents):**

- Creates all missing parent directories automatically.
- No need to create each folder one by one.

### Pentesting Example

```bash
mkdir -p Project/{Nmap,Hydra,Wordlists,Loot,Screenshots}
```

Creates an organized project structure for an engagement.

> **Remember:** `mkdir` = **Make Directory**

---

# `rmdir` — Remove Empty Directories

**Purpose:** Delete **only empty** folders.

### Syntax

```bash
rmdir <folder_name>
```

### Example

```bash
rmdir Test
```

### Limitation

If the folder contains files:

```text
Directory not empty
```

Linux refuses to delete it.

> **Remember:** `rmdir` works **only on empty directories**.

---

# `touch` — Create Empty Files

Originally used to update timestamps, but now mainly used to create empty files.

### Syntax

```bash
touch filename
```

### Examples

```bash
touch notes.txt
touch exploit.py
touch report.md
touch passwords.txt
```

### Multiple Files

```bash
touch one.txt two.txt three.txt
```

Creates all files at once.

### Cybersecurity Uses

Create report:

```bash
touch findings.md
```

Create Python exploit:

```bash
touch exploit.py
```

> **Remember:** Creates **0-byte empty files** if they don't already exist.

---

# `cp` — Copy Files & Directories

**Purpose:** Duplicate files or folders.

### Syntax

```bash
cp <source> <destination>
```

### Copy a File

```bash
cp notes.txt backup.txt
```

Now both files exist.

### Copy to Another Folder

```bash
cp notes.txt Reports/
```

### Copy Multiple Files

```bash
cp one.txt two.txt Backup/
```

### Copy Directories (`-r`)

```bash
cp -r Folder Backup/
```

**`-r` = Recursive**

Copies:

- All subfolders
- All files
- Entire directory tree

### Cybersecurity Example

Always back up logs before modifying them.

```bash
cp access.log access.log.bak
```

> **Remember:** Directories require **`-r`**.

---

# `mv` — Move or Rename

One command, **two jobs**.

## 1. Move Files

```bash
mv notes.txt Reports/
```

Moves the file.

---

## 2. Rename Files

```bash
mv notes.txt linux_notes.txt
```

Renames the file.

The original name disappears.

---

## Move & Rename Together

```bash
mv notes.txt Reports/linux_notes.txt
```

Moves and renames in one command.

### Cybersecurity Example

Rename downloaded exploit:

```bash
mv exploit.py ms08_067.py
```

> **Remember:** `mv` **does not copy**—it moves or renames.

---

# `rm` — Delete Files

Deletes files permanently.

### Syntax

```bash
rm filename
```

### Example

```bash
rm notes.txt
```

File is removed.

---

## Delete Multiple Files

```bash
rm one.txt two.txt
```

---

## Interactive Mode (`-i`)

```bash
rm -i notes.txt
```

Linux asks before deleting.

---

## Force Delete (`-f`)

```bash
rm -f notes.txt
```

Deletes immediately without confirmation.

Use carefully.

> **Remember:** Linux usually has **no Recycle Bin**.

---

# `rm -r` — Delete Directories Recursively

Deletes folders **and everything inside them**.

### Example

```bash
rm -r Project
```

Deletes:

- All files
- All subfolders
- Entire directory

---

## Force Recursive Delete

```bash
rm -rf Project
```

Options:

- `-r` → Recursive
- `-f` → Force

Deletes immediately without asking.

### ⚠️ Dangerous Command

Never run commands like:

```bash
rm -rf /
```

It attempts to delete the entire filesystem.

Modern Linux has protections, but similar commands can still destroy important data.

### Cybersecurity Note

During professional pentests:

- Avoid deleting client files.
- Preserve evidence whenever possible.

---

# `clear` — Clear Terminal

Clears the visible terminal screen.

```bash
clear
```

Shortcut:

```text
Ctrl + L
```

Does **not** erase command history.

---

# `history` — View Command History

Shows previously executed commands.

```bash
history
```

Example:

```text
1 pwd
2 ls
3 cd Desktop
4 mkdir Test
5 rm Test
```

### Run a Previous Command

Execute command number 4:

```bash
!4
```

Repeat the last command:

```bash
!!
```

Useful for repeating long commands quickly.

---

# `echo` — Print Text or Write to Files

Displays text or variable values.

### Print Text

```bash
echo Hello
```

Output:

```text
Hello
```

---

## Print Environment Variables

```bash
echo $HOME
```

Example:

```text
/home/kali
```

---

## Create a File with Text

```bash
echo "Nmap Scan" > report.txt
```

Creates:

```
report.txt
```

Contents:

```text
Nmap Scan
```

---

## Append Text

```bash
echo "Port 80 Open" >> report.txt
```

Contents become:

```text
Nmap Scan
Port 80 Open
```

### Difference

| Operator | Purpose |
|----------|---------|
| `>` | Overwrite/Create file |
| `>>` | Append to existing file |

---

# Cybersecurity Examples

### Create Lab Structure

```bash
mkdir -p Lab/{Scans,Loot,Scripts,Reports}
```

### Create Empty Files

```bash
touch exploit.py findings.md targets.txt
```

### Backup Evidence

```bash
cp access.log access.log.bak
```

### Rename Exploit

```bash
mv exploit.py eternalblue.py
```

### Remove Temporary File

```bash
rm temp.txt
```

### Save Scan Result

```bash
echo "Nmap Scan Started" > scan.txt
```

### Add Open Port

```bash
echo "22/tcp Open" >> scan.txt
```

---

# Quick Revision

| Command | Purpose |
|----------|---------|
| `mkdir` | Create directory |
| `mkdir -p` | Create nested directories |
| `rmdir` | Delete empty directory |
| `touch` | Create empty file |
| `cp` | Copy files |
| `cp -r` | Copy directories |
| `mv` | Move or rename |
| `rm` | Delete files |
| `rm -r` | Delete directories recursively |
| `rm -rf` | Force delete recursively ⚠️ |
| `clear` | Clear terminal screen |
| `history` | Show previous commands |
| `echo` | Print text / write to files |

---

# Things to Remember

- **`mkdir -p`** → Create nested folders.
- **`touch`** → Create empty files.
- **`cp -r`** → Required for copying directories.
- **`mv`** → Moves **or** renames.
- **`rm`** → Permanent deletion (usually no recycle bin).
- **`rm -rf`** → Extremely dangerous.
- **`history`** → View previous commands.
- **`!!`** → Repeat last command.
- **`!<number>`** → Run a specific command from history.
- **`echo >`** → Overwrite/create file.
- **`echo >>`** → Append to file.