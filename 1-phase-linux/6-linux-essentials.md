# Essential Linux Commands: Users, Links, & Archives

Here is the straightforward guide to managing people on your server, creating shortcuts, and zipping files!

---

## 1. User Management (Who gets access?)
Every person or background app that uses Linux gets a "User" account.

* **`useradd`**: Creates a brand new user.
  * **Example:** `useradd shubham`
* **`passwd`**: Gives the user a password so they can log in.
  * **Example:** `passwd shubham` (The terminal will ask you to type the new password twice. Once complete, this is how you **update a password** too!).
* **`userdel`**: Deletes a user from the system.
  * **Example:** `userdel shubham` (or use `userdel -r shubham` to perfectly delete their home folder as well).

### How do you verify Users?
Linux stores all user information in special text files inside the `/etc/` folder!
* **Verify a user was created:** Run `cat /etc/passwd`. Look at the very bottom of the file to see the new user.
* **Verify a password was set:** Run `sudo cat /etc/shadow`. This file is highly restricted and holds the encrypted code for all passwords. If there is a huge string of random characters next to the user's name, they have a password!

---

## 2. Group Management (Teams in Linux)
If you have 100 developers, you don't want to give them permissions one-by-one. Instead, you create a "Group" and put all 100 people inside it.

* **`groupadd`**: Creates a new team/group.
  * **Example:** `groupadd developers`
* **Verify a group is created:** Run `cat /etc/group`. Just like users, groups are stored in a text file!

### Adding Users to a Group (`gpasswd`)
* **`gpasswd -a` (Add one):** Adds a single user to a group.
  * **Example:** `gpasswd -a shubham developers`
* **`gpasswd -M` (Multi-Add):** Sets the exact list of users in a group all at once, separating them by commas.
  * **Example:** `gpasswd -M shubham,john,jane developers`

---

## 3. File Links (Shortcuts vs Clones)
In Linux, you can make a connection to a file without copying it.

### The Soft Link (The Regular Shortcut) 
A soft link (`ln -s`) is exactly like a desktop shortcut in Windows. It is just a signpost pointing to the original file. **If you delete the original file, the soft link breaks and becomes useless!**
* **Command:** `ln -s [target_file] [shortcut_name]`
* **Example:** `ln -s /var/www/html/index.html website_shortcut`
* **🚀 DevOps Use Case:** Having a shortcut called `live_app/` that points to a folder `version_1.0/`. When you deploy a new update, you just delete the shortcut and make a new one pointing to `version_2.0/`. The web server never has to stop!

### The Hard Link (The Identical Twin)
A hard link (`ln`) does NOT point to a file name. It points to the physical hard drive hardware where the data lives. It creates an identical clone! **If you delete the original file, the hard link STILL WORKS perfectly** because it holds a direct physical connection to the data.
* **Command:** `ln [target_file] [twin_name]`
* **Example:** `ln core_backup.sql twin_backup.sql`

---

## 4. Packing Up Files (Archives & Zipping)
In Windows, you right-click a folder and click "Zip". In Linux, it is historically a two step process: First we **Tape** the files together into one big box using `tar`, then we **Crush/Zip** the box to make it small using `gzip`.

### The `tar` Command (The File Taper)
* **To Pack/Create a box (`tar -cvf`):** 
  * **Example:** `tar -cvf my_archive.tar /var/log/`
  * **`-c`** = **C**reate (Make a new archive box).
  * **`-v`** = **V**erbose (Talkative - show me the name of every file on the screen as you pack it).
  * **`-f`** = **F**ilename (The very next word I type will be the name of the new archive).

* **To Unpack/Extract a box (`tar -xvf`):** 
  * **Example:** `tar -xvf my_archive.tar`
  * **`-x`** = e**X**tract (Open the box and take everything out).

### The `gzip` Command (The File Crusher)
Now that `tar` made one big file, we use `gzip` to shrink its file size so we can email it or upload it.
* **Example:** `gzip my_archive.tar` -> This crushes it and automatically renames it to `my_archive.tar.gz`!

*(🚀 **DevOps Trick:** You can Tape AND Crush at the exact same time by adding a `z` to the tar command! Example: `tar -czvf my_archive.tar.gz /var/log/`)*

---

## 5. Downloading from the Web
* **`wget`**: The command-line web downloader. If you have a direct link to a file, zip, or setup script on the internet, `wget` downloads it instantly to your current folder.
* **Example:** `wget https://example.com/software-installer.tar.gz`
