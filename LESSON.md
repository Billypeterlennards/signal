# From Zero to Running a Python Tool from GitHub

A step-by-step lesson for adults. It ends with a real task: unlocking a Signal
Android backup with
[signal_for_android_decryption](https://github.com/mossblaser/signal_for_android_decryption).

**How to use this lesson:** work through the parts in order. Each one ends with
a short **Try it** exercise, so do them, because typing the commands yourself is
how this sticks.

| Part | Topic |
|---|---|
| 1 | What is a programming language? |
| 2 | What is Python? |
| 3 | How Python code actually gets executed |
| 4 | How Python differs from other languages |
| 5 | The terminal: talking to your computer in text |
| 6 | Why you must install Python on Windows |
| 7 | Why you add Python to PATH |
| 8 | Writing and running a Python file |
| 9 | Packages, pip and requirements.txt |
| 10 | Git: what it is and how to use it |
| 11 | GitHub: what it is and how it relates to Git |
| 12 | Cloning a project and using it afterwards |
| 13 | Final task: unlocking the Signal backup |

---

## Part 1: What is a programming language?

A computer's processor only understands **machine code**: long sequences of
numbers that mean things like "add these two values" or "jump to this
instruction." Writing that by hand is slow and error-prone.

A **programming language** is a human-friendly way to write instructions,
plus a tool that translates those instructions into something the machine can
run.

There are two main translation strategies:

| Strategy | How it works | Analogy |
|---|---|---|
| **Compiled** | A *compiler* translates the whole program into machine code **ahead of time**, producing an `.exe`. You run the `.exe`. | Translating a whole book before handing it to a reader |
| **Interpreted** | An *interpreter* program reads your code and carries it out **while it runs**. | A live interpreter translating a speech sentence by sentence |

Many modern languages use a mix of the two, and Python is one of them, as you'll see.

**Try it:** Think of an app you use and guess whether it was distributed as a
compiled `.exe` or needs another program to run it.

---

## Part 2: What is Python?

Python is a **high-level, general-purpose programming language**, created by
Guido van Rossum and first released in 1991.

- **High-level** means it hides the machine's details. You don't manage memory
  or think about the processor. You write things like
  `for photo in photos: save(photo)`.
- **General-purpose** means it's used for almost everything: automation scripts,
  websites, data analysis, AI, and small utilities like the Signal tool.

Why people like it:
- **Readable:** it looks close to plain English.
- **Batteries included:** it comes with a large standard library (files,
  networking, JSON, maths and more).
- **Huge ecosystem:** hundreds of thousands of free add-on packages.

A taste of Python:

```python
name = input("What's your name? ")
if name:
    print("Hello, " + name + "!")
else:
    print("Hello, stranger!")
```

Notice that there are no semicolons or curly braces. **Indentation (spaces at
the start of a line) defines the blocks.** The lines indented under `if` belong
to the `if`.

---

## Part 3: How Python code actually gets executed

When you type `python hello.py`, this happens:

```
 hello.py           (1) compile          bytecode           (2) execute
 your source code  ───────────────────►  .pyc instructions ──────────────────► results
 (text you wrote)   done automatically   (simple, compact)   by the Python
                    by python.exe                            Virtual Machine
```

1. **You write source code**: a plain text file ending in `.py`.
2. **`python.exe` starts.** This program is the **interpreter**. The standard
   one is called **CPython** because it's written in the C language.
3. **It compiles your code into bytecode.** Bytecode is a simplified,
   lower-level set of instructions. It is *not* machine code: your processor
   can't run it directly. Python sometimes caches it in a `__pycache__` folder
   as `.pyc` files so it can start faster next time.
4. **The Python Virtual Machine (PVM) runs the bytecode.** The PVM is a loop
   inside `python.exe` that reads each bytecode instruction and performs it,
   one after another.

**Key takeaway:** a Python program can't run by itself. **It always needs
`python.exe` present to run it.** That's why Python has to be installed, which
is the subject of Part 6.

**Try it (after installing Python in Part 6):** run this in the Python prompt
to see the bytecode for a tiny function:

```python
import dis
def add(a, b):
    return a + b
dis.dis(add)
```

---

## Part 4: How Python differs from other languages

| | **Python** | **C / C++ / Rust** | **Java / Kotlin / C#** | **JavaScript** |
|---|---|---|---|---|
| How it runs | Interpreter (bytecode + PVM) | Compiled straight to machine code (`.exe`) | Compiled to bytecode, run by a virtual machine (JVM / .NET) | Run by a JavaScript engine, usually in a browser |
| Speed | Slower | Fastest | Fast | Fast |
| Ease of learning | Very easy | Hard | Medium | Easy-medium |
| Types | **Dynamic**: a variable can hold anything, checked while running | **Static**: types are declared and checked before running | Static | Dynamic |
| Blocks | Indentation | `{ }` braces | `{ }` braces | `{ }` braces |
| Typical uses | Scripts, automation, data, AI, tools | Operating systems, games, drivers | Android apps, business software | Websites, web apps |

The same program, "print Hello", in four languages:

```python
# Python
print("Hello")
```
```c
// C
#include <stdio.h>
int main() { printf("Hello\n"); return 0; }
```
```java
// Java
public class Main { public static void main(String[] a) { System.out.println("Hello"); } }
```
```javascript
// JavaScript
console.log("Hello");
```

**Where Python fits:** it trades raw speed for fast writing and easy reading.
For a tool like the Signal decryptor, which runs once, reads a file and writes
some files, that trade-off is ideal. Heavy lifting such as the actual
encryption maths is done inside packages written in C, so you get speed where
it matters.

Fun connection: the **Signal Android app** is written in **Java and Kotlin**,
but the backup tool is written in **Python**. Different jobs suit different
languages.

---

## Part 5: The terminal

Before installing anything, you need the place where you'll type commands.

- A **terminal** is a text window for giving your computer commands.
- A **shell** is the program inside it that understands those commands. On
  Windows you have:
  - **CMD (Command Prompt):** the older shell
  - **PowerShell:** the newer, more capable one. **Use this one.**

**Opening PowerShell in a specific folder:** open the folder in File Explorer,
click the address bar, type `powershell`, and press Enter.

**Essential commands:**

| Command | Meaning |
|---|---|
| `pwd` | Show which folder I'm in |
| `ls` | List what's in this folder |
| `cd foldername` | Go into a folder |
| `cd ..` | Go up one folder |
| `mkdir name` | Make a new folder |
| `cls` | Clear the screen |

**Paths** are file addresses:
- **Absolute:** `C:\Users\HP\Downloads\signal` (the full address)
- **Relative:** `signal\README.md` (counted from where you are now)
- `.` = this folder, `..` = the folder above

**Tips:** press `Tab` to auto-complete names, `↑` to repeat earlier commands,
and `Ctrl + C` to stop a running command.

**Try it:**
```powershell
cd ~\Downloads
ls
cd signal
pwd
```

---

## Part 6: Why you must install Python on Windows

From Part 3: **Python code needs the interpreter, `python.exe`, to run.**

- macOS and Linux often come with Python already installed, because many system
  tools are written in it.
- **Windows does not.** Windows has a fake `python` shortcut that just opens
  the Microsoft Store. It isn't a real Python.

Installing Python gives you:
- `python.exe`, the interpreter
- the **standard library** (built-in modules like `os`, `json`, `sys`)
- **pip**, the package installer (Part 9)
- `py.exe`, the **Python Launcher** for Windows, which helps pick between
  installed versions

**How to install:**
1. Go to https://www.python.org/downloads/ and download the latest Python 3.
2. Run the installer.
3. **On the first screen, tick "Add python.exe to PATH".** (Part 7 explains why.)
4. Click **Install Now**.
5. **Close and reopen** any PowerShell windows.

**Check that it worked:**
```powershell
python --version
pip --version
```
You should see something like `Python 3.13.0`.

**If `python` opens the Microsoft Store:** go to Settings → Apps → Advanced app
settings → **App execution aliases** and turn off the two "python" entries.

---

## Part 7: Why you add Python to PATH

When you type `python` in a terminal, Windows has to find `python.exe`
somewhere on your disk. It doesn't search the whole disk, which would be far too
slow. Instead it checks a **short list of folders** stored in an
**environment variable** called **PATH**.

- An **environment variable** is a named setting that the system and programs
  can read, like a sticky note on the computer: `PATH = C:\Windows;C:\Windows\System32;...`
- **PATH** is the list of folders Windows searches, in order, whenever you type
  a command name.

```
You type:  python

Windows checks:   C:\Windows\System32\python.exe     ✗ not here
                  C:\Windows\python.exe              ✗ not here
                  C:\Users\HP\AppData\Local\Programs\Python\Python313\python.exe  ✓ found, run it
```

Python installs into a folder that is **not** on PATH by default. Ticking
**"Add python.exe to PATH"** adds that folder to the list. If you skip it:

```
python : The term 'python' is not recognized as the name of a cmdlet, function, script file, or operable program.
```

That error means Windows searched every PATH folder and didn't find
`python.exe`. Python may be installed, but Windows doesn't know where.

**See it for yourself:**
```powershell
$env:Path -split ";"    # shows your PATH, one folder per line
where.exe python        # shows which python.exe Windows finds
```

**Fixing PATH later:** rerun the Python installer and choose **Modify** (or
reinstall with the box ticked). Or use Start → "Edit environment variables for
your account" → **Path** → **Edit** → **New**, and add the Python folder.
**Always reopen the terminal afterwards**, because a terminal only reads PATH
when it starts.

**Workaround:** `py` (the Python Launcher) is usually installed somewhere Windows
can find, so `py script.py` often works even when `python` doesn't.

---

## Part 8: Writing and running a Python file

### 8.1 The interactive prompt (good for experiments)
```powershell
python
```
```
>>> 2 + 3
5
>>> print("hi")
hi
>>> exit()
```

### 8.2 A script file (good for real programs)
1. Make a practice folder:
   ```powershell
   mkdir ~\Downloads\signal\practice
   cd ~\Downloads\signal\practice
   notepad hello.py
   ```
2. Put this into Notepad and save:
   ```python
   name = input("What's your name? ")
   print(f"Hello, {name}! Python is working.")
   ```
3. Run it:
   ```powershell
   python hello.py
   ```

In `python hello.py`, `python` is the program (the interpreter) and `hello.py`
is the argument (the file to run).

### 8.3 Passing arguments to a script
Real tools get their inputs from the command line. Create `greet.py`:
```python
import sys
print("All arguments:", sys.argv)
print("First argument:", sys.argv[1])
```
Run it:
```powershell
python greet.py Alice
```
Output:
```
All arguments: ['greet.py', 'Alice']
First argument: Alice
```
`sys.argv` is the list of words typed after `python`. **This is exactly how
the Signal tool works:**
```powershell
python decrypt_backup.py  my.backup  outputfolder
#      └ script           └ input    └ output
```

### 8.4 Importing modules
`import sys` loads a **module**, a file of ready-made code. `sys` is built into
Python. Some modules aren't built in and must be installed, which leads to
Part 9.

**Try it:** write `add.py`, which takes two numbers as arguments and prints their
sum. (Hint: `int(sys.argv[1])` turns text into a number.)

---

## Part 9: Packages, pip and requirements.txt

**Package or library:** code someone else wrote and published so you can reuse
it. The Signal tool needs packages for things like cryptography, because writing
encryption code yourself is hard and risky.

**Dependency:** a package a project needs in order to run. If it's missing, you
get:
```
ModuleNotFoundError: No module named 'something'
```

**PyPI** (https://pypi.org) is the public online store of Python packages.

**pip** is the program that downloads and installs packages from PyPI.

| Command | Meaning |
|---|---|
| `pip install requests` | Install one package |
| `pip list` | Show installed packages |
| `pip uninstall requests` | Remove a package |
| `python -m pip install ...` | Same as above, but guaranteed to use the same Python you run. **This is the safest form.** |

**requirements.txt** is a shopping list of every package a project depends on,
one per line, often with versions:
```
cryptography>=3.0
protobuf==3.20.0
```
`==` means exactly this version, and `>=` means this version or newer.

```powershell
pip install -r requirements.txt
```
The `-r` flag means "read the package list from this file." One command
installs everything.

### Virtual environments (recommended)
If every project installs packages into one shared Python, versions eventually
clash. A **virtual environment** gives each project its own private set of
packages:

```powershell
python -m venv .venv            # create it (a folder called .venv)
.venv\Scripts\Activate.ps1      # turn it on; your prompt shows (.venv)
pip install -r requirements.txt # installs go into .venv only
deactivate                      # turn it off
```

If PowerShell says *"running scripts is disabled on this system"*, run this once:
```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```
This allows local scripts to run for your user account only.

**Try it:**
```powershell
cd ~\Downloads\signal\practice
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install requests
python -c "import requests; print(requests.get('https://example.com').status_code)"
```
Seeing `200` means a package was installed and used successfully.

---

## Part 10: Git, the time machine for code

**Git** is a **version control system**: a program that records snapshots of
a project folder over time. With it you can:
- see exactly what changed, when, and why
- go back to any earlier version
- work with others without overwriting each other's work

**Key words:**

| Term | Meaning |
|---|---|
| **Repository (repo)** | A folder Git is tracking. Git stores its history in a hidden `.git` folder inside it. |
| **Commit** | A saved snapshot with a message, like "Fixed passphrase check" |
| **Staging** | Choosing which changes go into the next commit |
| **Branch** | A separate line of development |
| **Clone** | A full copy of an existing repo, including all its history |
| **Remote** | The copy of the repo stored online (usually named `origin`) |

### Install Git
1. Download it from https://git-scm.com/download/win
2. Run the installer. The default options are fine, and it **adds Git to PATH
   for you** (same idea as Part 7).
3. Reopen PowerShell and check:
   ```powershell
   git --version
   ```

### One-time setup
Git labels every commit with an author:
```powershell
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### The basic workflow
```
edit files  ──►  git add  ──►  git commit  ──►  (git push to GitHub)
  working        staging        history
```

**Try it:**
```powershell
cd ~\Downloads\signal\practice
git init                         # start tracking this folder
git status                       # see untracked files
git add hello.py                 # stage the file
git commit -m "Add hello script" # save a snapshot
```
Now edit `hello.py` (change the message) and run:
```powershell
git diff                         # see what you changed (+ added, - removed)
git add hello.py
git commit -m "Change greeting"
git log --oneline                # see your history
```
To view the old version without changing anything:
```powershell
git show HEAD~1:hello.py         # HEAD~1 = "one commit before the latest"
```

---

## Part 11: GitHub, Git's home on the internet

**Git** is the tool on your computer. **GitHub** (github.com) is a website that
stores Git repositories online so people can share and collaborate.

Analogy: Git is like your camera's photo history, and GitHub is like a photo
site where you upload and share albums.

**Reading a GitHub repo page** (open the Signal tool's page and find these):
- **Owner / name** at the top: `mossblaser / signal_for_android_decryption`
- **File list:** the project's files (`decrypt_backup.py`, `requirements.txt`, ...)
- **README:** shown below the files. It's the project's instructions. **Always
  read it first.**
- **Green "Code" button:** how you download the project
- **Commits:** the project's history
- **Issues:** bug reports and questions from users. If the tool breaks, check
  here first, because someone may have the same problem.
- **Stars / forks:** rough signs of popularity

**Open source:** the code is public, so anyone can read it, check it's safe, and
suggest improvements. The README thanks two people who contributed this way.

You **don't need a GitHub account** to download public projects.

---

## Part 12: Cloning a project and using it afterwards

### Two ways to get the code
| Method | How | When to use it |
|---|---|---|
| **Download ZIP** | Green **Code** button → **Download ZIP**, then extract | Quick and needs no Git, but there's no history and no easy updates |
| **git clone** | `git clone <url>` | Gives the full history, and you can update later with `git pull` |

### Cloning
```powershell
cd ~\Downloads\signal
git clone https://github.com/mossblaser/signal_for_android_decryption.git
```
- `git clone` copies the whole repo, including all its history.
- The URL comes from the green **Code** button (HTTPS tab).
- Git creates a new folder named after the repo:
  `signal_for_android_decryption`.

### What to do after cloning: the standard routine
This routine works for almost any Python project on GitHub:

1. **Go into the folder:**
   ```powershell
   cd signal_for_android_decryption
   ```
2. **Look around:**
   ```powershell
   ls
   ```
3. **Read the README.** It tells you the requirements and how to run the tool:
   ```powershell
   notepad README.md
   ```
4. **Check the Python version required.** This one needs Python 3.7 or newer.
5. **Create and activate a virtual environment:**
   ```powershell
   python -m venv .venv
   .venv\Scripts\Activate.ps1
   ```
6. **Install the dependencies:**
   ```powershell
   pip install -r requirements.txt
   ```
7. **Run the main script** the way the README says.

### Keeping it updated
```powershell
git pull     # download any new commits from GitHub
```

---

## Part 13: Final task: unlocking the Signal backup

Now you'll use everything from Parts 1–12.

### Background: what you're doing
- **Signal** is a private messaging app.
- On Android, it can save all your messages and media into a single
  **backup file** (`.backup`).
- The backup is **encrypted**: scrambled with a key derived from a **30-digit
  passphrase** that Signal shows you once.
- This **Python** tool (Parts 2–3) uses **cryptography packages** (Part 9) to
  unscramble the file with your passphrase and write the contents to a folder.

**Limits:**
- It only works on **your own** backup, and only if you have the passphrase.
- It was written around **2021**. Newer Signal versions may produce backups it
  can't read. If it fails, see the troubleshooting table at the end.
- The output is **not encrypted**, so keep it private and delete it when you're done.

### Step 1: Create the backup on your phone
1. In Signal: **profile picture → Settings → Chats → Chat backups → Turn on**.
2. **Write the 30-digit passphrase down on paper.** Without it, the backup
   can't be unlocked by anyone, including you.
3. Tap **Create backup** and wait. It can take a long time if you have lots of media.

### Step 2: Copy the backup to the PC
1. Connect the phone with USB and choose **File transfer** on the phone.
2. In File Explorer, open the folder that Signal's Chat backups screen shows.
3. Copy the `signal-YYYY-MM-DD-HH-MM-SS.backup` file to
   `C:\Users\HP\Downloads\signal`.

### Step 3: Check your tools *(Parts 6, 7, 10)*
```powershell
python --version    # must be 3.7 or newer
git --version
```
If either shows "not recognized," go back to Part 7 (PATH).

### Step 4: Clone the tool *(Parts 11–12)*
```powershell
cd ~\Downloads\signal
git clone https://github.com/mossblaser/signal_for_android_decryption.git
cd signal_for_android_decryption
```

### Step 5: Set up its environment and dependencies *(Part 9)*
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### Step 6: Run it *(Part 8: script plus arguments)*
```powershell
python decrypt_backup.py ..\signal-YYYY-MM-DD-HH-MM-SS.backup ..\unlocked
```
- `decrypt_backup.py` is the script to run.
- `..\signal-....backup` is the input. `..` means "go up one folder" to where
  you saved the backup. **Tip:** type `..\sig` and press `Tab` to auto-complete
  the long name.
- `..\unlocked` is the output folder the tool will create.

When asked, type your **30-digit passphrase** (spaces are optional) and press Enter.

### Step 7: Explore the results
```powershell
cd ..\unlocked
ls
explorer .
```

| What you'll find | What it is |
|---|---|
| `database.sqlite` | All messages and metadata in an SQLite database. Open it with **DB Browser for SQLite** (sqlitebrowser.org) and look at the tables. |
| `attachments\*.bin` | Photos, videos and files. Rename them with the right extension (`.jpg`, `.mp4`) to open them. |
| `stickers\*.bin`, `avatars\*.bin` | Stickers and profile pictures |
| `preferences.json`, `key_value.json` | App settings (open them in Notepad) |

### Step 8: Clean up
```powershell
deactivate                                # turn off the virtual environment
```
When you've finished with the unlocked data, delete the `unlocked` folder and
empty the Recycle Bin. The data inside is unprotected.

### Troubleshooting
| Problem | Cause | Fix | Lesson |
|---|---|---|---|
| `python` / `git` not recognized | Not on PATH | Reinstall with PATH ticked, then reopen the terminal | Part 7 |
| `python` opens the Microsoft Store | Windows alias | Turn off App execution aliases | Part 6 |
| `running scripts is disabled` | PowerShell policy | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` | Part 9 |
| `ModuleNotFoundError` | Dependencies missing or venv not active | Activate `.venv`, rerun `pip install -r requirements.txt` | Part 9 |
| `No such file or directory` | Wrong path | Check with `pwd` and `ls`, and use `Tab` to complete names | Part 5 |
| Error about the passphrase / MAC / HMAC | Wrong passphrase | Re-check every digit | — |
| Other crashes partway through | Backup format newer than the 2021 tool | Check the repo's **Issues** page, or try the actively maintained [signalbackup-tools](https://github.com/bepaald/signalbackup-tools) | Part 11 |

---

## Recap: what you now understand

- **Python** is a high-level, interpreted language. Your `.py` text is compiled
  to bytecode and run by the Python Virtual Machine inside `python.exe`.
- **It differs from C or Java** in being dynamically typed, indentation-based,
  slower but much quicker to write, and it needs the interpreter installed to run.
- **Windows needs Python installed** because it doesn't ship with an
  interpreter.
- **PATH** is the list of folders Windows searches for commands. Adding Python
  to it lets you just type `python`.
- **Running a file** is `python file.py arg1 arg2`, and the script reads the
  arguments through `sys.argv`.
- **pip** installs packages from PyPI. **requirements.txt** lists a project's
  dependencies, and a **venv** keeps them separate per project.
- **Git** tracks versions locally. **GitHub** hosts repos online. **Clone**
  copies a repo, and **pull** updates it.
- **After cloning:** `cd` in, read the README, create a venv, install the
  requirements, and run the script.

You've gone from "what is Python?" to running a real open-source tool from GitHub.
