# Package Management

# Update package list

```bash
sudo apt update
```

Downloads latest package information from repositories.

Does NOT install updates.

---

# Upgrade installed packages

```bash
sudo apt upgrade
```

Installs available package updates.

---

# Search package

```bash
apt search package_name
```

Example:

```bash
apt search nmap
```

---

# Install package

```bash
sudo apt install package_name
```

Example:

```bash
sudo apt install htop
```

---

# Important Notes

- `sudo` = run command as administrator/root
- `apt` = package manager used in Debian/Ubuntu
- Always run `sudo apt update` before upgrading/installing