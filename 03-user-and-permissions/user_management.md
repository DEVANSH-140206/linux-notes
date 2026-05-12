## 🎬 User & Permission Management (Linux)

---

## 👤 1. Identify Current User

whoami

👉 Shows current logged-in user

Example:
whoami  
Output: devansh

---

## 👤 2. User Creation

### Interactive (Recommended)

sudo adduser <username>

👉 Creates user with full setup

Example:
sudo adduser thor

- asks password
- creates /home/thor
- sets shell

---

### Non-Interactive (Raw)

sudo useradd <username>

👉 Minimal user creation

Example:
sudo useradd ironman

⚠ No password, no home directory

---

### Create User WITH Home Directory

sudo useradd -m <username>

👉 Creates user + home folder

Example:
sudo useradd -m hulk

Now:
/home/hulk exists

---

### Set / Change Password

sudo passwd <username>

👉 Sets or changes password

Example:
sudo passwd ironman

Then:
Enter new password: jarvis

---

## 📂 3. User Information Files

### View All Users

cat /etc/passwd

Example:
cat /etc/passwd

👉 Shows all system users

---

### View Password Hashes

sudo cat /etc/shadow

Example:
sudo cat /etc/shadow

👉 Shows encrypted passwords

---

## 🏠 4. Home Directory

/home/<username>

Example:
cd /home/thor  
ls

👉 User’s personal files

---

## ✏️ 5. Modify Users

### Change Shell

sudo usermod --shell /bin/bash <username>

Example:
sudo usermod --shell /bin/bash ironman

👉 Changes default terminal

---

### Rename User

sudo usermod -l newname oldname

Example:
sudo usermod -l tonystark ironman

---

## 🔄 6. Switching Users

### Switch User

su - <username>

Example:
su - ironman  
(password required)

---

### Switch to Root

su -

---

### Switch Using sudo

sudo su - <username>

Example:
sudo su - ironman

👉 No password needed

---

### Become Root

sudo su

---

### Exit User

exit  
OR Ctrl + D

---

## ⚡ 7. SUDO

sudo <command>

👉 Run command as admin

Example:
sudo useradd spiderman

---

### Error Example

"user is not in the sudoers file"

👉 User has no sudo access

---

## 🔐 8. Sudoers File

### Open Safely

sudo visudo

---

### Give User Full Access

username ALL=(ALL) ALL

Example:
thanos ALL=(ALL) ALL

---

### Give Group Access

%groupname ALL=(ALL) ALL

Example:
%sudo ALL=(ALL) ALL

---

### Passwordless Sudo

%groupname ALL=(ALL) NOPASSWD: ALL

Example:
%infinity_gauntlet ALL=(ALL) NOPASSWD: ALL

---

## 👥 9. Group Management

### Create Group

sudo groupadd <groupname>

Example:
sudo groupadd infinity_gauntlet

---

### View Groups

cat /etc/group

---

### Check User Groups

groups

Example:
groups

Output:
devansh sudo

---

## ➕ 10. Add User to Group

sudo usermod -aG <group> <user>

Example:
sudo usermod -aG infinity_gauntlet ironman

👉 ironman now has group access

---

### Verify

cat /etc/group

Example:
cat /etc/group | grep infinity_gauntlet

---

## ➖ 11. Remove User from Group

sudo gpasswd -d <user> <group>

Example:
sudo gpasswd -d thanos infinity_gauntlet

👉 removes thanos from group

---

## ❌ 12. Deletion

### Delete User

sudo userdel <username>

Example:
sudo userdel thor

---

### Delete Group

sudo groupdel <groupname>

Example:
sudo groupdel infinity_gauntlet

👉 Only group deleted, users remain

---

## 🧠 13. Core Concepts

- root → full control
- sudo → temporary admin access
- sudoers → who gets power
- groups → manage permissions
- home directory → user workspace
- least privilege → give only required access


# User Information & Permissions

# `alias`

## Create command shortcuts

```bash
alias ll='ls -l'
```

Now typing:

```bash
ll
```

runs:

```bash
ls -l
```

---

# Why use aliases?

Used to:
- save time
- shorten long commands
- create custom shortcuts

Example:

```bash
alias update='sudo apt update && sudo apt upgrade'
```

---

# Temporary vs Permanent

Aliases created in terminal are temporary.

To make permanent:
- add them to `.bashrc`

---

# `ls -l` File Details

Example:

```bash
-rwxr-xr-- 1 user group 2048 May 10 file.txt
```

---

# Permission Breakdown

```text
-rwxr-xr--
```

## First Character

- `-` = file
- `d` = directory

---

## Permission Groups

```text
rwx r-x r--
```

Split into:
- owner/user
- group
- others

---

# Permission Letters

- `r` = read
- `w` = write
- `x` = execute

---

# Permission Meaning

Example:

```text
rwx
```

means:
- read
- write
- execute

Example:

```text
r-x
```

means:
- read
- execute
- no write

---

# `chmod`

## Change file permissions

Basic structure:

```bash
chmod who+/-permissions filename
```

Example:

```bash
chmod u+x script.sh
```

Adds execute permission to user.

---

# Who Values

- `u` = user/owner
- `g` = group
- `o` = others
- `a` = all

---

# Operators

- `+` = add permission
- `-` = remove permission
- `=` = set exact permission

---

# Permission Values

- `r` = read
- `w` = write
- `x` = execute

---

# Examples

## Add execute permission

```bash
chmod +x script.sh
```

## Remove write permission from others

```bash
chmod o-w file.txt
```

## Give read/write to user only

```bash
chmod u=rw file.txt
```

---

# `/etc/passwd`

## View user account information

```bash
cat /etc/passwd
```

Contains user account details.

---

# Example Entry

```text
root:x:0:0:root:/root:/bin/bash
```

---

# Field Breakdown

```text
username:password:UID:GID:comment:home:shell
```

## Important Fields

- `username` → account name
- `x` → password stored elsewhere
- `UID` → user ID
- `GID` → group ID
- `home` → home directory
- `shell` → default shell

---

# Important Notes

- `root` user has UID `0`
- Normal users usually start from UID `1000`
- `/bin/bash` means Bash shell is used