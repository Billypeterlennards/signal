# Signal Backup Unlocker — A Beginner's Guide

This guide explains the tool at
https://github.com/mossblaser/signal_for_android_decryption
in simple words, step by step.

---

## Part 1: What is all this?

### What is Signal?
Signal is a messaging app, kind of like WhatsApp. People use it to send texts,
photos and videos to friends and family. It's famous for keeping messages
**very private**.

### What is a backup?
On Android phones, Signal can save a copy of everything (your messages, photos,
stickers and profile pictures) into **one single file**. That file is called a
**backup**. If you lose your phone or get a new one, you can use the backup to
get your old messages back.

### Why is the backup locked?
Signal locks the backup with a **secret code** called a **passphrase**. It's a
30-digit number, like this (not a real one):

```
12345 67890 12345 67890 12345 67890
```

Without the code, the backup file just looks like scrambled nonsense. That way,
nobody else can read your messages if they find the file.

### What does this tool do?
The tool is like a **key**. If you have:
1. the backup file, **and**
2. the secret 30-digit code,

then the tool unlocks the backup on your computer and takes everything out of it.

### What do you get out?

| What comes out       | What it is                                                          |
|----------------------|---------------------------------------------------------------------|
| `database.sqlite`    | All your messages, stored in a database file (needs special tools to read) |
| `attachments/` folder | Photos and videos you sent or received                             |
| `stickers/` folder   | Stickers used in chats                                              |
| `avatars/` folder    | Profile pictures of contacts and groups                             |
| `preferences.json`   | Some app settings                                                   |
| `key_value.json`     | More app settings and info                                          |

**Note:** The photos and videos come out ending in `.bin` instead of `.jpg` or
`.mp4`. You may need to rename them (for example `photo.bin` → `photo.jpg`) to
open them.

### Who made it?
A programmer called **mossblaser** made it as a free side project. It is **not**
made by the Signal company. It was made in **2021**, so it might not work with
backups from newer versions of Signal.

---

## Part 2: Important rules ⚠️

1. **Only use it on YOUR OWN backup.** It cannot break into anyone else's
   messages, and reading other people's private messages isn't OK anyway.
2. **The unlocked files are NOT protected anymore.** Anyone who uses your
   computer could read them. Delete them when you're done, or keep them
   somewhere safe.
3. **Ask a grown-up for help** if you're not sure about a step, especially
   installing programs.

---

## Part 3: How to run it (step by step, on Windows)

### Step 1: Make a backup on your phone
1. Open **Signal** on your Android phone.
2. Tap your **profile picture** → **Settings** → **Chats** → **Chat backups**.
3. Tap **Turn on**.
4. Signal shows you a **30-digit code**. **Write it down carefully on paper!**
   If you lose it, the backup can never be unlocked.
5. Tap **Create backup** and wait. If you have lots of photos and videos, this
   can take a long time (even hours).

### Step 2: Copy the backup to your computer
1. Plug your phone into the computer with a USB cable.
2. On the phone, allow **File transfer** when it asks.
3. On the computer, open **File Explorer**, click your phone, and find the
   **Signal** → **Backups** folder (the exact place is shown in Signal's
   Chat backups screen).
4. Copy the file (it's named something like `signal-2026-10-06-12-00-00.backup`)
   into this folder: `C:\Users\HP\Downloads\signal`

### Step 3: Install Python
The tool is written in a programming language called **Python**, so your
computer needs it.
1. Go to https://www.python.org/downloads/
2. Download and run the installer.
3. **Important:** on the first screen, tick the box that says
   **"Add python.exe to PATH"**, then click **Install Now**.

### Step 4: Download the tool
1. Go to https://github.com/mossblaser/signal_for_android_decryption
2. Click the green **Code** button → **Download ZIP**.
3. Open the ZIP file and drag the folder inside into
   `C:\Users\HP\Downloads\signal`
4. Rename that folder to `tool` to keep things simple.

Your `signal` folder should now look like this:
```
signal\
├── README.md                (this file)
├── signal-XXXX.backup       (your backup)
└── tool\
    ├── decrypt_backup.py
    ├── requirements.txt
    └── ...
```

### Step 5: Open PowerShell in the tool folder
1. Open the `C:\Users\HP\Downloads\signal\tool` folder in File Explorer.
2. Click the address bar at the top, type `powershell`, and press **Enter**.
   A blue or black window with text appears. This is where you type commands.

### Step 6: Install what the tool needs
Type this and press **Enter**:
```
pip install -r requirements.txt
```
Wait until it finishes.

### Step 7: Unlock the backup!
Type this (change the backup file name to match yours) and press **Enter**:
```
python decrypt_backup.py ..\signal-XXXX.backup ..\unlocked
```
- `..\signal-XXXX.backup` is your backup file (`..` means "the folder above").
- `..\unlocked` is the new folder where everything will be put.

The tool will ask for your **passphrase**. Type your 30-digit code (spaces are
optional) and press **Enter**.

### Step 8: Look at your stuff
Open `C:\Users\HP\Downloads\signal\unlocked` and look inside! 🎉

---

## Part 4: If something goes wrong

| Problem | What to try |
|---------|-------------|
| `python is not recognized` | Python isn't installed right. Reinstall it and tick **"Add python.exe to PATH"**. |
| `pip is not recognized` | Use `python -m pip install -r requirements.txt` instead. |
| It says the passphrase is wrong | Check every digit of your code carefully. |
| Some other error | Your backup may be from a newer Signal version that this 2021 tool doesn't understand. Try a newer tool such as **signalbackup-tools**: https://github.com/bepaald/signalbackup-tools |

---

## Part 5: When you're done
The unlocked files aren't protected, so **delete the `unlocked` folder** when
you don't need it anymore, or move it somewhere safe. Keep your 30-digit code
secret!
