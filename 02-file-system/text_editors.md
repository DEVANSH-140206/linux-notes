# Linux Text Editors (Nano & Vim)

## Why Do We Need Text Editors?

Linux systems store almost everything as **text files**:

- Configuration files (`/etc/hosts`)
- User lists (`/etc/passwd`)
- Logs (`/var/log/`)
- Bash scripts (`script.sh`)
- Python programs (`exploit.py`)
- HTML/CSS/JavaScript files
- Notes and reports

Unlike Windows, Linux administrators and penetration testers often edit these files directly from the terminal.

Two editors you'll use the most as a beginner are:

- **Nano** → Easy, beginner-friendly
- **Vim** → Powerful, fast, used by professionals

Think of them like this:

| Editor | Analogy | Best For |
|---------|----------|----------|
| Nano | Notepad | Beginners, quick edits |
| Vim | Keyboard-only IDE | Professional Linux users |

---

# Nano

## What is Nano?

Nano is a simple terminal text editor.

Think of it as **Notepad inside the terminal.**

Unlike Vim, Nano starts in **editing mode immediately.**

The moment you open a file, you can start typing.

No special modes.

No complicated commands.

---

## Opening Nano

```bash
nano notes.txt
```

If the file exists:

- Nano opens it.

If it doesn't exist:

- Nano creates a new empty file.

---

## Screen Layout

```
---------------------------------
|                               |
|        File Contents          |
|                               |
|                               |
---------------------------------
^G Help
^O Write Out
^X Exit
```

The shortcuts at the bottom tell you what each key does.

Notice the **^**

It means:

**Ctrl**

Example:

```
^X
```

means

```
Ctrl + X
```

---

# Writing Text

Simply type.

Example:

```
Nmap

Hydra

Metasploit
```

Everything you type immediately appears.

No Insert Mode.

No Command Mode.

---

# Saving a File

Shortcut:

```
Ctrl + O
```

Think:

**O = Output**

Nano asks:

```
File Name to Write:
```

Usually it already shows the current filename.

Press:

```
Enter
```

The file is saved.

---

# Exiting Nano

Shortcut:

```
Ctrl + X
```

Think:

```
X = Exit
```

---

# Unsaved Changes

If you've changed the file and try to exit:

```
Save modified buffer?

Y
N
Cancel
```

Options:

```
Y
```

Save changes.

```
N
```

Discard changes.

```
Ctrl + C
```

Cancel exiting.

---

# Searching

Shortcut

```
Ctrl + W
```

Think:

```
Where?
```

Type:

```
Hydra
```

Press Enter.

Nano jumps to the word.

---

# Cut & Paste

Nano doesn't use Ctrl+C and Ctrl+V like most editors.

Instead:

```
Ctrl + K
```

Cuts the current line.

```
Ctrl + U
```

Pastes it.

Think:

```
K = Kill
U = Unkill (Paste)
```

---

# Nano Cheat Sheet

| Shortcut | Purpose |
|----------|---------|
| Ctrl + O | Save file |
| Ctrl + X | Exit |
| Ctrl + W | Search |
| Ctrl + K | Cut current line |
| Ctrl + U | Paste |
| Ctrl + G | Help |

---

# Vim

## What is Vim?

Vim is one of the most powerful text editors in Linux.

Unlike Nano, Vim has **modes**.

Imagine driving a car.

You don't start driving immediately.

You first:

```
Unlock

↓

Start Engine

↓

Drive

↓

Stop

↓

Turn Engine Off
```

Vim works the same way.

```
Open File

↓

Command Mode

↓

Insert Mode

↓

Type

↓

Command Mode

↓

Save

↓

Quit
```

---

# Opening Vim

```bash
vim notes.txt
```

If the file exists:

It opens.

If it doesn't:

A new editing session starts.

---

# Command Mode

This is the default mode.

When Vim opens:

You are NOT typing.

Every key is interpreted as a command.

For example:

```
i
```

does NOT type the letter i.

Instead it means:

```
Enter Insert Mode
```

---

# Insert Mode

Press:

```
i
```

Bottom of screen shows:

```
-- INSERT --
```

Now Vim behaves like a normal editor.

Type:

```
Nmap
Hydra
Metasploit
```

Press Enter to create new lines.

---

# Returning to Command Mode

Press:

```
Esc
```

The `-- INSERT --` message disappears.

Now you're back in Command Mode.

---

# The Colon (:)

The colon opens Vim's command line.

Think:

```
:
```

means

> "Hey Vim, execute this command."

---

# Saving

Type:

```
:w
```

Press Enter.

Think:

```
w = Write
```

The file is written (saved) to disk.

---

# Quitting

```
:q
```

Think:

```
q = Quit
```

If there are no unsaved changes:

Vim exits.

---

# Save and Quit

```
:wq
```

Meaning:

```
Write

+

Quit
```

Most commonly used.

---

# Quit Without Saving

```
:q!
```

The `!` means:

**Force**

Discard every unsaved change.

---

# Deleting a Line

Move the cursor onto a line.

Press:

```
dd
```

Think:

```
Delete

Delete Line
```

The current line disappears.

---

# Copying a Line

Move the cursor onto a line.

Press:

```
yy
```

Think:

```
Yank

Copy
```

Nothing appears to happen.

The line is copied internally.

---

# Pasting

Press:

```
p
```

The copied line is pasted **below** the current line.

---

# Searching

Press:

```
/
```

Type:

```
Hydra
```

Press Enter.

Vim jumps to the first match.

Next result:

```
n
```

Previous result:

```
N
```

---

# Undo

Press:

```
u
```

Undo the previous action.

---

# Vim Workflow

```
vim file.txt

↓

Command Mode

↓

i

↓

Insert Mode

↓

Type

↓

Esc

↓

:w

↓

:q
```

Or simply:

```
:wq
```

---

# Nano vs Vim

| Feature | Nano | Vim |
|----------|------|-----|
| Beginner Friendly | ✅ Very Easy | ❌ Hard at first |
| Starts Typing Immediately | ✅ Yes | ❌ No |
| Uses Modes | ❌ No | ✅ Yes |
| Powerful Editing | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| Used by Professionals | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |

---

# Which Should I Use?

Use **Nano** when:

- Editing configuration files quickly
- Writing notes
- Making small changes
- You're still learning Linux

Use **Vim** when:

- Working on remote Linux servers
- Editing large files
- Learning professional Linux administration
- Doing penetration testing where Vim is often pre-installed

---

# Commands to Remember

## Nano

```text
nano file.txt      Open or create file
Ctrl + O           Save
Ctrl + X           Exit
Ctrl + W           Search
Ctrl + K           Cut line
Ctrl + U           Paste line
```

## Vim

```text
vim file.txt       Open file
i                  Enter Insert Mode
Esc                Return to Command Mode
:w                 Save
:q                 Quit
:wq                Save & Quit
:q!                Quit without saving
dd                 Delete current line
yy                 Copy current line
p                  Paste below current line
/word              Search
n                  Next match
N                  Previous match
u                  Undo
```

---

# Real Pentester Examples

Edit the hosts file:

```bash
sudo nano /etc/hosts
```

Edit SSH configuration:

```bash
sudo vim /etc/ssh/sshd_config
```

Create a Bash script:

```bash
nano script.sh
```

Write a Python exploit:

```bash
vim exploit.py
```

Take notes during an engagement:

```bash
nano findings.md
```

---

# Quick Revision

- **Nano** is a simple, beginner-friendly editor that lets you type immediately.
- **Vim** is a powerful editor that uses **Command Mode** and **Insert Mode**.
- Press **`i`** to start typing in Vim.
- Press **`Esc`** to return to Command Mode.
- Use **`:w`** to save, **`:q`** to quit, and **`:wq`** to save and quit.
- **`dd`** deletes a line, **`yy`** copies a line, **`p`** pastes it, and **`/`** searches for text.
- Nano is great for beginners, while Vim is widely used by Linux administrators and penetration testers.