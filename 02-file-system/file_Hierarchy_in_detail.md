# Linux Filesystem Hierarchy (FHS) - Complete Pentester Notes

# ==========================================================
# LINUX FILESYSTEM OVERVIEW
# ==========================================================

Unlike Windows, Linux does NOT use drives like

C:
D:
E:

Everything starts from ONE root directory.

```
                    /
                    │
 ┌──────────────────┼─────────────────────┐
 │                  │                     │
bin               boot                 dev
 │                  │                     │
etc               home                 lib
 │                  │                     │
media             mnt                  opt
 │                  │                     │
proc              root                 run
 │                  │                     │
sbin              srv                  sys
 │                  │                     │
tmp               usr                  var
```

Think of "/" as the root of a giant upside-down tree.

Every file, every folder, every program, every device,
every user exists somewhere under "/".

There are NO separate drives.

Everything belongs to this tree.

---

# COMPLETE DIRECTORY TABLE

| Directory | Purpose | What is Stored Here | Pentester's View | Common Commands |
|-----------|----------|--------------------|------------------|-----------------|
| / | Root Directory | Parent of everything | Starting point of the entire filesystem | cd / |
| /home | Home directories of normal users | Desktop, Downloads, Documents, SSH keys, hidden configs | FIRST place to search for user data, credentials, notes, SSH keys | cd /home |
| /root | Home directory of root user | Root user's personal files | Check after privilege escalation | sudo ls /root |
| /etc | System configuration | passwd, shadow, ssh config, DNS config, cron jobs | GOLD MINE for enumeration and privilege escalation | cd /etc |
| /bin | Essential user commands | ls, cp, mv, rm, cat, pwd | Core Linux commands | ls /bin |
| /sbin | System administration commands | reboot, shutdown, fsck | Mostly administrator tools | ls /sbin |
| /usr | Installed software | Programs, libraries, documentation | Where most applications live | ls /usr/bin |
| /var | Variable data | Logs, databases, web files, package cache | Extremely valuable for forensics and log analysis | cd /var/log |
| /tmp | Temporary files | Temporary downloads, payloads | Common place attackers store tools | ls /tmp |
| /opt | Optional software | Burp Suite, Nessus, Google Chrome | Third-party software often installed here | ls /opt |
| /dev | Device files | Hard disks, terminals, USB devices | Hardware is represented as files | ls /dev |
| /proc | Virtual filesystem | Running processes, CPU info, Memory info | Excellent for system enumeration | cat /proc/cpuinfo |
| /sys | Virtual kernel information | Hardware and kernel information | Useful for advanced enumeration | ls /sys |
| /boot | Boot files | Linux kernel, GRUB, initramfs | Rarely touched during normal pentests | ls /boot |
| /media | Auto-mounted USB devices | USB drives, DVDs | Look for removable storage | ls /media |
| /mnt | Manual mount point | Mounted drives | Used by admins for manual mounting | ls /mnt |
| /run | Runtime information | PID files, sockets | Useful for investigating running services | ls /run |
| /srv | Service data | FTP, Web servers | May contain website data | ls /srv |
| /lib | Shared libraries | DLL equivalent in Linux | Required by programs | ls /lib |

---

# DIRECTORY HIERARCHY

```
/

├── bin
│     Essential commands
│
├── boot
│     Linux kernel
│     GRUB Bootloader
│
├── dev
│     Hard Disk
│     USB
│     Keyboard
│     Mouse
│     Terminal
│
├── etc
│     passwd
│     shadow
│     hosts
│     resolv.conf
│     ssh/
│     apache2/
│     nginx/
│     crontab
│
├── home
│     ├── kali
│     │      Desktop
│     │      Downloads
│     │      Documents
│     │      Pictures
│     │      .ssh
│     │      .bashrc
│     │      .gitconfig
│     │
│     ├── alice
│     └── bob
│
├── lib
│     Shared Libraries
│
├── media
│     USB Drives
│
├── mnt
│     Manual Mounts
│
├── opt
│     Burp Suite
│     Nessus
│     Chrome
│
├── proc
│     cpuinfo
│     meminfo
│     version
│     process IDs
│
├── root
│     Root User's Home
│
├── run
│     Runtime Data
│
├── sbin
│     System Commands
│
├── srv
│     Service Data
│
├── sys
│     Hardware Information
│
├── tmp
│     Temporary Files
│
├── usr
│     ├── bin
│     ├── sbin
│     ├── lib
│     └── share
│
└── var
      ├── log
      ├── www
      ├── cache
      ├── mail
      └── lib
```

---

# MOST IMPORTANT DIRECTORIES FOR PENTESTERS

★★★★★

/etc

Why?

Contains almost every important configuration.

Interesting Files

/etc/passwd

Users

-------------------

/etc/shadow

Password Hashes

-------------------

/etc/hosts

Hostname mappings

-------------------

/etc/resolv.conf

DNS Server

-------------------

/etc/ssh/

SSH Configuration

-------------------

/etc/crontab

Scheduled Jobs

-------------------

/etc/apache2/

Apache Configuration

-------------------

Attackers often search here for:

• Weak configurations
• Passwords
• Misconfigured services
• Cron jobs
• SSH settings

---

★★★★★

/home

Contains

Desktop

Downloads

SSH Keys

Documents

Hidden Files

Browser Data

Projects

Most Important Hidden Files

.bash_history

.bashrc

.profile

.ssh

.gitconfig

Attackers search here for

• Passwords

• API Keys

• SSH Keys

• Notes

• Scripts

• Database Credentials

---

★★★★★

/root

Only accessible after gaining root privileges.

Contains

Administrator's files

SSH Keys

Backups

Scripts

Configuration Files

Private Documents

---

★★★★★

/var

Contains constantly changing information.

Most Important

/var/log

Logs

Examples

auth.log

syslog

apache2 logs

nginx logs

kern.log

Attackers

Read logs

Blue Team

Investigates logs

---

★★★★★

/var/www

Default Website Directory

Contains

HTML

PHP

CSS

JavaScript

Uploads

Configuration Files

Web Pentesters spend lots of time here.

---

★★★★★

/tmp

Temporary Files

Properties

✔ Everyone can write here

✔ Usually emptied after reboot

✔ Used for testing

Attackers often

Download payloads

Extract exploits

Run temporary scripts

---

★★★★★

/proc

Virtual Filesystem

NOT stored on disk.

Generated by the Linux Kernel.

Useful Files

/proc/cpuinfo

CPU Details

----------------

/proc/meminfo

RAM Details

----------------

/proc/version

Kernel Version

----------------

/proc/PID/

Information about running process

Excellent for

System Enumeration

Kernel Enumeration

Process Enumeration

---

★★★★★

/dev

Device Files

Examples

/dev/sda

Entire Hard Disk

----------------

/dev/sda1

First Partition

----------------

/dev/null

Black Hole

Everything written here disappears.

Example

echo hello > /dev/null

Output

Nothing

Useful in scripting.

---

★★★★★

/usr

Contains most installed software.

Important

/usr/bin

Applications

----------------

/usr/sbin

Admin Programs

----------------

/usr/lib

Libraries

----------------

/usr/share

Documentation

Icons

Manual Pages

---

# DIRECTORY IMPORTANCE FOR HACKERS

★★★★★  Extremely Important

/etc

/home

/var

/proc

/tmp

/root

★★★★☆

/usr

/dev

/opt

★★★☆☆

/boot

/media

/mnt

/run

/sys

★★☆☆☆

/srv

/lib

---

# TYPICAL PENTEST ENUMERATION FLOW

Gain Shell

↓

pwd

↓

whoami

↓

id

↓

ls -la

↓

cd /home

↓

Look for users

↓

Read user files

↓

Check hidden files

↓

Go to /etc

↓

Read configuration files

↓

Check cron jobs

↓

Check SSH configuration

↓

Go to /var/log

↓

Read logs

↓

Go to /var/www

↓

Read website source

↓

Go to /tmp

↓

Look for temporary files

↓

Read /proc

↓

Identify kernel version

↓

Privilege Escalation

---

# EASY MEMORY TRICK

```
/
│
├── home     → Users
├── root     → Administrator
├── etc      → Settings
├── var      → Logs & Databases
├── usr      → Installed Programs
├── tmp      → Temporary Files
├── proc     → Running System Info
├── dev      → Hardware Devices
├── boot     → Boot Files
├── opt      → Third-party Software
├── media    → USB Drives
├── mnt      → Manual Mounts
├── bin      → Essential Commands
├── sbin     → System Commands
└── sys      → Kernel & Hardware
```

---

# IF YOU REMEMBER ONLY 7 DIRECTORIES

1. /home → User Files
2. /etc → Configuration Files
3. /var → Logs & Websites
4. /tmp → Temporary Files
5. /proc → Running System Information
6. /usr → Installed Software
7. /root → Root User's Home

Master these seven, and you'll know where to look during most Linux administration tasks and many penetration testing engagements.