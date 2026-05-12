# File Viewing Commands

## 📌 Overview

Used to view file contents in terminal. (open the contents of a file as everything is a file in linux even commands are files)

## 🧠 Commands

- cat → display file content
- lsof → list open files

## ⚙️ Examples

cat file.txt
lsof

## 💡 Explanation

Linux treats everything as a file, so viewing files is important.

## 🔥 Use Case

Used to read logs, configs, or sensitive files.

## 📝 Summary

File viewing is important for inspecting system data.


# File Viewing Commands

# `head`

## Show first lines of file

```bash
head file.txt
```

Default:
- shows first 10 lines

---

# `tail`

## Show last lines of file

```bash
tail file.txt
```

Default:
- shows last 10 lines

---

# `tail -f`

## Follow live file changes

```bash
tail -f logfile.log
```

Used for:
- monitoring logs in real time
- debugging
- watching server activity

`-f` = follow

Press `Ctrl + C` to stop.

---

# `journalctl`

## View system logs

```bash
journalctl
```

Used to read logs collected by `systemd`.

Useful for:
- debugging errors
- checking crashes
- viewing boot logs

---

# Important Idea

Linux stores almost everything as files:
- logs
- configs
- devices
- user information