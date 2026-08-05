# Lesson 7 — File Permissions & Ownership

**Difficulty:** ⭐⭐⭐⭐⭐

**Importance for Cybersecurity/Pentesting:** ⭐⭐⭐⭐⭐

---

# Why This Lesson Matters

File permissions are one of the core security mechanisms in Linux.

Every penetration tester, Linux administrator, DevOps engineer, malware analyst, digital forensic investigator, and system administrator works with permissions every day.

Many privilege escalation vulnerabilities exist because of incorrectly configured file permissions.

If you understand Linux permissions, you'll understand why users can or cannot access files, why scripts sometimes refuse to run, and how attackers abuse permission misconfigurations.

---

# The Big Idea

Imagine you own a house.

There are three categories of people.

```
You (Owner)

↓

Your Family (Group)

↓

Everyone Else (Others)
```

Suppose your house contains an important cupboard.

Who should be allowed to:

- Open it?
- Put things inside it?
- Remove things from it?

Probably not everyone.

Linux uses exactly the same idea.

Every file and every directory asks three questions:

- What can the Owner do?
- What can the Group do?
- What can Others do?

This is the entire foundation of Linux permissions.

---

# Every File Has Three Audiences

Create a file

```bash
touch notes.txt
```

Linux automatically records an owner.

Example

```
notes.txt

Owner → kali
```

Linux now divides all users into three categories.

```
               notes.txt

        ┌──────────────────────┐
        │      Owner           │
        │       kali           │
        └──────────────────────┘

        ┌──────────────────────┐
        │      Group           │
        │     students         │
        └──────────────────────┘

        ┌──────────────────────┐
        │      Others          │
        │   Everyone else      │
        └──────────────────────┘
```

There is only **one file**.

Linux simply applies different permissions depending on who is trying to access it.

---

# The Three Permissions

Every audience receives three possible permissions.

```
Read

Write

Execute
```

These are represented by

```
r

w

x
```

---

# Read Permission (r)

Read means:

"I am allowed to view the contents."

Examples

```bash
cat notes.txt

less notes.txt

more notes.txt

head notes.txt

tail notes.txt

nano notes.txt
```

Without Read permission

```
Permission denied
```

---

# Write Permission (w)

Write means

"I am allowed to modify the file."

Examples

```bash
nano notes.txt

vim notes.txt

echo "hello" >> notes.txt
```

Without Write permission

```
Permission denied
```

Although deleting a file actually depends on the permissions of its parent directory, it is useful to think of Write permission as allowing changes to the file itself.

---

# Execute Permission (x)

This permission confuses many beginners.

Execute means

"The operating system is allowed to run this file as a program or script."

Example

Suppose

```bash
attack.sh
```

contains

```bash
echo Hello
```

Run

```bash
./attack.sh
```

Without Execute permission

```
Permission denied
```

Even if the script itself is correct.

---

# Viewing Permissions

Command

```bash
ls -l
```

Example output

```
-rwxr-xr-- 1 kali kali 2456 Aug 5 attack.sh
```

Most beginners only notice

```
attack.sh
```

Professionals first examine

```
-rwxr-xr--
```

because it tells them the security settings.

---

# Understanding the Permission String

Example

```
-rwxr-xr--
```

Split it into parts.

```
-

rwx

r-x

r--
```

The first character is the file type.

The remaining nine characters are divided into three groups.

```
Owner

↓

rwx

Group

↓

r-x

Others

↓

r--
```

---

# File Type

The first character tells Linux what kind of object it is.

| Symbol | Meaning |
|---------|----------|
| - | Regular file |
| d | Directory |
| l | Symbolic link |
| c | Character device |
| b | Block device |
| s | Socket |
| p | Named pipe |

Example

```
drwxr-xr-x Documents
```

The leading

```
d
```

means

Directory.

---

# Reading rwx

Owner

```
rwx
```

Meaning

✅ Read

✅ Write

✅ Execute

---

Group

```
r-x
```

Meaning

✅ Read

❌ Write

✅ Execute

---

Others

```
r--
```

Meaning

✅ Read

❌ Write

❌ Execute

---

# Common Permission Combinations

| Permission | Meaning |
|------------|----------|
| rwx | Full control |
| rw- | Read + Write |
| r-x | Read + Execute |
| r-- | Read only |
| -wx | Write + Execute |
| -w- | Write only |
| --x | Execute only |
| --- | No permissions |

---

# chmod

Command

```bash
chmod
```

Meaning

```
CHange MODe

↓

Change file permissions
```

This command changes who is allowed to Read, Write, or Execute a file.

---

# Symbolic Permission Method

Suppose

```
-rw-r--r--
```

The file cannot be executed.

Add Execute permission

```bash
chmod +x attack.sh
```

Remove Execute permission

```bash
chmod -x attack.sh
```

Add Write permission

```bash
chmod +w attack.sh
```

Remove Write permission

```bash
chmod -w attack.sh
```

---

# What Does + Mean?

Think mathematically.

Current permissions

```
Read

Write
```

Command

```bash
chmod +x file
```

Means

```
Current permissions

+

Execute

=

Read

Write

Execute
```

Similarly

```
+x

Add Execute

-x

Remove Execute

+w

Add Write

-w

Remove Write

+r

Add Read

-r

Remove Read
```

---

# Who Gets the Permission?

If you simply write

```bash
chmod +x file
```

Linux treats it like

```bash
chmod a+x file
```

where

```
a

↓

All users
```

You can be more specific.

| Symbol | Meaning |
|---------|----------|
| u | User (Owner) |
| g | Group |
| o | Others |
| a | All |

---

Examples

Owner receives Execute

```bash
chmod u+x attack.sh
```

Group receives Write

```bash
chmod g+w report.txt
```

Others lose Read permission

```bash
chmod o-r notes.txt
```

Everyone receives Execute

```bash
chmod a+x attack.sh
```

---

# Reading Symbolic Commands Like English

Example

```bash
chmod u+x attack.sh
```

Translate it

```
chmod

↓

Change permissions

u

↓

Owner

+

↓

Add

x

↓

Execute

attack.sh

↓

On this file
```

English sentence

```
Give the owner Execute permission on attack.sh.
```

---

Another example

```bash
chmod g-w report.txt
```

Meaning

```
Remove Write permission from the Group.
```

---

Another example

```bash
chmod o+r notes.txt
```

Meaning

```
Allow Others to Read this file.
```

---

# Numeric Permission Method (Very Important)

Linux also represents permissions using numbers.

Permission values

```
Read

=

4

Write

=

2

Execute

=

1
```

Add them together.

---

```
rwx

4 + 2 + 1

=

7
```

---

```
rw-

4 + 2

=

6
```

---

```
r-x

4 + 1

=

5
```

---

```
r--

4

=

4
```

---

```
---

0
```

---

# Numeric Permission Table

| Number | Permission |
|---------|------------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 3 | -wx |
| 2 | -w- |
| 1 | --x |
| 0 | --- |

---

# chmod 755

One of the most common permissions.

Command

```bash
chmod 755 attack.sh
```

Breakdown

Owner

```
7

↓

rwx
```

Group

```
5

↓

r-x
```

Others

```
5

↓

r-x
```

Final permissions

```
rwxr-xr-x
```

Meaning

Owner has full control.

Everyone else can read and execute but cannot modify.

Commonly used for executable programs and shell scripts.

---

# chmod 644

Another very common permission.

Command

```bash
chmod 644 notes.txt
```

Breakdown

Owner

```
6

↓

rw-
```

Group

```
4

↓

r--
```

Others

```
4

↓

r--
```

Final permissions

```
rw-r--r--
```

Meaning

Owner can read and edit.

Everyone else can only read.

This is commonly used for text files, configuration files, and documents.

---

# chmod 777

Command

```bash
chmod 777 file
```

Permissions

```
Owner

rwx

Group

rwx

Others

rwx
```

Everyone can

- Read
- Write
- Execute

This is almost always considered insecure.

If everyone can modify a file, an attacker may be able to replace or alter it.

Pentesters actively search for files and directories with overly permissive settings because they may provide opportunities for privilege escalation or unauthorized modification.

---

# Practice Commands

Create a file

```bash
touch test.txt
```

View its permissions

```bash
ls -l test.txt
```

Add Execute permission

```bash
chmod +x test.txt
```

Check again

```bash
ls -l test.txt
```

Remove Execute

```bash
chmod -x test.txt
```

Owner only gets Execute

```bash
chmod u+x test.txt
```

Group gets Write

```bash
chmod g+w test.txt
```

Others lose Read

```bash
chmod o-r test.txt
```

Assign numeric permissions

```bash
chmod 755 test.txt

chmod 644 test.txt

chmod 777 test.txt
```

Observe how the permission string changes after every command.

---

# Why Pentesters Care About Permissions

Incorrect permissions can create serious security vulnerabilities.

Examples include

- World-writable files
- Writable configuration files
- Writable scripts executed by privileged users
- Misconfigured SUID binaries
- Files that attackers can replace or modify

Many Linux privilege escalation techniques begin by checking permissions on important files and directories.

Understanding permissions is therefore one of the most important Linux skills for cybersecurity professionals.

---

# Key Takeaways

- Every file has one Owner, one Group, and permissions for Others.
- Every permission group can receive Read (r), Write (w), and Execute (x).
- `ls -l` displays the permission string.
- `chmod` changes permissions.
- Symbolic mode uses `u`, `g`, `o`, `a` together with `+` or `-`.
- Numeric mode uses `r=4`, `w=2`, and `x=1`.
- `755` is commonly used for executable files and scripts.
- `644` is commonly used for text files.
- `777` grants full access to everyone and should generally be avoided.
- Misconfigured permissions are a common source of privilege escalation vulnerabilities in Linux.