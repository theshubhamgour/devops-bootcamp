# Essential Linux Commands: Navigation & Operations

Think of your Linux terminal as a virtual car. You need commands to tell it where to drive, what to look at, and how to transport objects (files).

---

## 1. Directory (Folder) Navigation

If you want to move around, you need to understand where you are.
```text
           [The Highway of Linux]
/ (Root) =====> /home/ =====> /home/shubham/ =====> /home/shubham/project
```

* **`pwd` (Print Working Directory):** The "Where am I GPS". It tells you your exact current location. **Always run this before deleting anything!**
* **`mkdir` (Make Directory):** Creates a brand new folder.
  * **Example:** `mkdir frontend_code`
  * **🚀 DevOps Trick:** `mkdir -p app/src/logs` (The `-p` lets you create a folder inside a folder inside a folder, all at once without errors!).
* **`cd` (Change Directory):** The "Drive me there" command.
  * **Example (`cd folder_name`):** `cd project` -> Drives forward into that folder.
  * **Example (`cd ..`):** Drives backwards/upwards exactly one level.
  * **Example (`cd ../../..`):** Drives backwards three levels rapidly.
  * **Example (`cd` or `cd ~`):** Instantly teleports you back to your personal home base directory (`/home/yourname/`).

---

## 2. Looking at Files
* **`ls` (List):** The basic "What is inside here?" command.
* **`ls -l` (Long List):** Provides a detailed list. Instead of just names, you see file sizes, who owns the file, and when it was created. *(Note: `ll` works on many systems as a shortcut for this).*
* **`ls -la` (List All):** The `-a` stands for "All". This reveals **Hidden Files**. 

### How to Create a Hidden File / Folder
In Linux, there is no "right-click -> hide" button. To hide a file or folder, you simply start the name with a dot `.`!
* **Example:** `touch .secret_key.txt` -> The file is now hidden.
* **Example:** `mkdir .private_data` -> The folder is now hidden.

---

## 3. Copying, Moving, and Renaming

* **`cp` (Copy):** Duplicates an object.
  * **Example:** `cp server.yaml server-backup.yaml` (Makes a copy of the file).
  * **🚀 DevOps Trick:** `cp -r old_folder new_folder` (To copy an entire folder, you MUST use `-r` which means "recursive").
* **`mv` (Move / Rename):** This is the Swiss Army Knife. It does two things depending on how you use it:
  * **1. Moving (Cut & Paste):** `mv index.html /var/www/html/` (Moves the file into a completely different folder).
  * **2. Renaming:** `mv bad_name.txt good_name.txt` (If you keep it in the same folder, it simply renames the file!).

---

## 4. Deleting Things ⚠️ (Danger Zone)
Linux does **NOT** have a recycle bin. When you delete something here, it is gone forever.
* **`rm` (Remove):** Deletes a file.
  * **Example:** `rm old_config.txt`
* **`rmdir` (Remove Directory):** Deletes a folder, but *only if it is 100% empty*.
* **`rm -r` (Remove Recursive):** The sledgehammer. It deletes a folder and everything inside of it completely. **Use with extreme caution.**
  * **Example:** `rm -r broken_project/`

---

## 🚀 Crucial Commands for DevOps Engineers

### 1. Server Exhaustion (Checking Hard Drive Space)
One of the most common tickets a DevOps engineer gets is: *"The server crashed because the hard drive is full!"*
* **`df -h` (Disk Free - Human Readable):** Shows you exactly how much total hard drive space you have left on the server in GBs and MBs.
* **`du -sh *` (Disk Usage):** Shows the exact size of all the folders around you. This helps you track down which specific folder (usually logs) is eating up all the space!

### 2. Hunting Down Lost Files
You know a file exists, but you have no idea what folder it's in.
* **`find` (The Ultimate Locator):** Scans the entire file system.
  * **Example:** `find / -name "nginx.conf"` -> This tells Linux: "Start at the Root `/`, and search every single folder until you find a file exactly named nginx.conf."

### 3. Quick Re-cap of DevOps Reading Tools
*(These were covered heavily in the previous chapter, but are essential here too!)*
* **`head app.log`**: Quickly peeks at the first 10 lines of a huge file.
* **`tail app.log`**: Quickly peeks at the last 10 lines of a huge file.
