# System Monitoring Commands

# `free`

## Show RAM usage

```bash
free
```

Shows:
- total memory
- used memory
- free memory

## Human-readable format

```bash
free -m
```

`-m` = show memory in MB

---

# `df`

## Show disk usage

```bash
df
```

Shows filesystem storage usage.

## Human-readable format

```bash
df -h
```

`-h` = human-readable sizes (MB, GB)

---

# `htop`

## Interactive system monitor

```bash
htop
```

Shows:
- CPU usage
- RAM usage
- running processes
- system load

Better version of `top`.

---

# `uptime`

## Show system uptime

```bash
uptime
```

Shows:
- how long system has been running
- current time
- system load