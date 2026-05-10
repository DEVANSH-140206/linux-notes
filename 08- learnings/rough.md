# File Operations & Basic Terminal Commands

## Clear Terminal Screen

```bash
Ctrl + L
```

Clears the terminal screen without deleting files or command history.

---

# `ls`

## List files and folders

```bash
ls
```

## Detailed list

```bash
ls -l
```

Shows:
- permissions
- owner
- file size
- date and time
- filename

---

# `touch`

## Create empty file

```bash
touch file.txt
```

Used to quickly create files.

---

# `mkdir`

## Create folder

```bash
mkdir foldername
```

Example:

```bash
mkdir notes
```

---

# `cp`

## Copy file

```bash
cp file.txt copy.txt
```

## Copy folder

```bash
cp -r folder1 folder2
```

`-r` = recursive (required for folders)

---

# `mv`

## Move file or folder

```bash
mv file.txt /path/
```

## Rename file

```bash
mv old.txt new.txt
```

Used for both moving and renaming.

---

# `rm`

## Delete file

```bash
rm file.txt
```

## Delete folder

```bash
rm -r foldername
```

> Warning: Deleted files are usually not recoverable.

---

# `nano`

## Open or create file

```bash
nano file.txt
```

Beginner-friendly text editor.

### Important Shortcuts

- `Ctrl + O` → Save
- `Ctrl + X` → Exit

---

# `vim`

## Open file

```bash
vim file.txt
```

### Basic Commands

- `i` → Insert mode
- `Esc` → Normal mode
- `:wq` → Save and quit
- `:q!` → Quit without saving