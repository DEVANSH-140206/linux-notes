# Linux Fundamentals: Working with Paths & Shell Expansion

> **Goal:** Learn how Linux finds files, why `/` is important, when to use absolute vs relative paths, and how shell expansion (`{}`, `*`, `~`) works.

---

# 1. The General Structure of a Linux Command

Almost every Linux command follows this pattern:

```bash
COMMAND [OPTIONS] PATH
```

Example:

```bash
cp -r /home/kali/Notes /home/kali/Backup
```

Breakdown:

| Part | Meaning |
|------|---------|
| `cp` | Command (Copy) |
| `-r` | Option (Copy recursively) |
| `/home/kali/Notes` | Source path |
| `/home/kali/Backup` | Destination path |

Think of it like an English sentence:

```
Verb     Option      Object

Copy   Recursively   This Folder
```

---

# 2. What is a Path?

A **path** is simply the **address** of a file or folder.

Just like your home address.

Example:

```
India
 ↓
State
 ↓
City
 ↓
Street
 ↓
House
```

Linux works exactly the same way.

```
/
└── home
     └── kali
          └── Desktop
               └── CyberLab
                    └── notes.txt
```

The complete address

```
/home/kali/Desktop/CyberLab/notes.txt
```

is called the **path**.

---

# 3. Why Does Every Path Start With "/"?

Linux has one single filesystem.

Everything begins from one place:

```
/
```

called the **Root Directory**.

```
/
├── home
├── etc
├── var
├── usr
└── tmp
```

When Linux sees

```bash
/home/kali/Desktop
```

it thinks:

```
Start at /

↓

Go into home

↓

Go into kali

↓

Go into Desktop
```

This is called an **Absolute Path**.

---

# 4. Absolute Path vs Relative Path

## Absolute Path

Starts from **Root (`/`)**

Works no matter where you currently are.

Example

```bash
cat /etc/passwd
```

Linux always starts from

```
/
```

then finds

```
etc

↓

passwd
```

---

## Relative Path

Starts from your **Current Directory**.

Suppose:

```bash
pwd
```

Output

```text
/home/kali
```

Now type

```bash
ls Desktop
```

Linux silently understands

```text
/home/kali/Desktop
```

because you're already inside

```
/home/kali
```

---

Another example

Current directory

```
/home/kali/Desktop
```

Command

```bash
cat CyberLab/tools.txt
```

Linux understands

```text
/home/kali/Desktop/CyberLab/tools.txt
```

---

# 5. When Should I Use "/"?

Use `/` whenever you want to give Linux the **complete address**.

Example

```bash
cat /etc/passwd
```

```bash
nano /etc/hosts
```

```bash
mkdir /home/kali/Hacking
```

These work from **any directory**.

---

# 6. When Should I NOT Use "/"?

When the file is inside your current directory.

Example

Current directory:

```
/home/kali/Desktop
```

Command

```bash
cat notes.txt
```

Linux automatically looks for

```
/home/kali/Desktop/notes.txt
```

No leading slash needed.

---

# 7. Why is "/" Sometimes at the END?

Example

```bash
cp notes.txt Backup/
```

instead of

```bash
cp notes.txt Backup
```

Both usually work.

The final `/` simply tells humans

> "This is definitely a directory."

It makes commands easier to read.

---

# 8. The Power of Absolute Paths

One of Linux's biggest advantages:

**You never have to enter a directory to work with files inside it.**

Current directory:

```text
/home
```

Create a file somewhere else

```bash
touch /home/kali/Desktop/tools.txt
```

Read it

```bash
cat /home/kali/Desktop/tools.txt
```

Delete it

```bash
rm /home/kali/Desktop/tools.txt
```

Copy it

```bash
cp report.txt /home/kali/Desktop/
```

Move it

```bash
mv report.txt /home/kali/Desktop/
```

Everything works without using `cd`.

---

# 9. The Golden Rule

Almost every Linux command follows

```bash
COMMAND PATH
```

Examples

```bash
cat /etc/passwd
```

Read a file.

---

```bash
nano /etc/hosts
```

Edit a file.

---

```bash
touch /home/kali/test.txt
```

Create a file.

---

```bash
mkdir /home/kali/Hacking
```

Create a folder.

---

```bash
rm /tmp/file.txt
```

Delete a file.

---

```bash
find /home -name "*.txt"
```

Search for files.

---

# 10. Shell Expansion (The Magic Before Commands Run)

This is where many beginners get confused.

Example

```bash
mkdir Project/{Nmap,Hydra}
```

Does `mkdir` understand `{}`?

**No.**

Bash expands it **before** running `mkdir`.

Internally Bash changes

```bash
mkdir Project/{Nmap,Hydra}
```

into

```bash
mkdir Project/Nmap Project/Hydra
```

Then `mkdir` runs.

---

Another example

```bash
touch {one,two,three}.txt
```

becomes

```bash
touch one.txt two.txt three.txt
```

---

Another example

```bash
echo {1..5}
```

becomes

```text
1 2 3 4 5
```

---

# 11. When Should I Use Brace Expansion `{}`?

Whenever you want to create or generate multiple names quickly.

Instead of

```bash
mkdir Nmap
mkdir Hydra
mkdir Reports
mkdir Loot
```

Use

```bash
mkdir CyberLab/{Nmap,Hydra,Reports,Loot}
```

Much faster.

---

Create multiple files

```bash
touch report{1,2,3}.txt
```

Creates

```
report1.txt
report2.txt
report3.txt
```

---

Create folders

```bash
mkdir Week{1..5}
```

Creates

```
Week1
Week2
Week3
Week4
Week5
```

---

# 12. Can I Mix Paths and Brace Expansion?

Yes.

Example

```bash
mkdir -p ~/CyberLab/{Nmap,Hydra,Reports,Loot}
```

Bash expands it into

```bash
mkdir -p \
~/CyberLab/Nmap \
~/CyberLab/Hydra \
~/CyberLab/Reports \
~/CyberLab/Loot
```

---

# 13. Special Symbols You Must Know

| Symbol | Meaning | Example |
|---------|----------|---------|
| `/` | Root directory / Path separator | `/home/kali/Desktop` |
| `.` | Current directory | `./script.sh` |
| `..` | Parent directory | `cd ..` |
| `~` | Your Home directory | `~/Desktop` |
| `{}` | Generate multiple names before command runs | `mkdir {Nmap,Hydra}` |
| `*` | Wildcard (matches existing files) | `rm *.txt` |

---

# 14. `{}` vs `*` (Very Important)

## `{}`

Creates or expands names.

Doesn't care whether files exist.

Example

```bash
touch {a,b,c}.txt
```

Creates

```
a.txt
b.txt
c.txt
```

---

## `*`

Matches files that already exist.

Example

```bash
rm *.txt
```

Deletes every `.txt` file in the current directory.

It **cannot create files**.

---

# 15. Writing to Files (`>` vs `>>`)

Without redirection:

```bash
echo "Hello"
```

Output

```text
Hello
```

appears on the terminal.

---

Use `>`

```bash
echo "nmap, hydra" > Folder/Attack/tools.txt
```

Meaning:

- `echo` → print text
- `>` → send output into a file
- `Folder/Attack/tools.txt` → destination

If the file doesn't exist → Linux creates it.

If it exists → everything inside is replaced.

---

Use `>>`

```bash
echo "sqlmap" >> Folder/Attack/tools.txt
```

Adds the text to the end of the file instead of replacing it.

Result

```text
nmap, hydra
sqlmap
```

---

# 16. Think Like a Pentester

Imagine you get access to a Linux server.

Current directory

```text
/tmp
```

Need to inspect SSH keys.

❌ Slow method

```bash
cd /home
cd alice
cd .ssh
cat id_rsa
```

✅ Professional method

```bash
cat /home/alice/.ssh/id_rsa
```

Edit a config

```bash
nano /etc/ssh/sshd_config
```

Read web logs

```bash
tail /var/log/apache2/access.log
```

Experienced Linux users think in **paths**, not in **where they are standing**.

---

# Quick Revision

✅ A **Path** is the address of a file or folder.

✅ **Absolute Path** starts with `/` and always begins from the root.

✅ **Relative Path** starts from your current directory.

✅ The trailing `/` usually means "this is a directory."

✅ Most Linux commands follow:

```bash
COMMAND [OPTIONS] PATH
```

✅ `{}` generates multiple names **before** the command runs.

✅ `*` matches **existing** files.

✅ `>` overwrites a file.

✅ `>>` appends to a file.

✅ You can work with any file using its path—no need to `cd` into its directory.