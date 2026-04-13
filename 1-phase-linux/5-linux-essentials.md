# Essential Linux Commands: Systems, Services, & Software

As a DevOps engineer, you will often log into a random server in the cloud that you have never seen before. You need to quickly figure out who you are, what the server is, how to install software on it, and how to keep it running.

---

## 1. System Identity (Who & Where am I?)

* **`whoami`**: Prints your current username. (Extremely helpful to ensure you aren't accidentally logged in as the dangerous `root` user!).
* **`hostname`**: Tells you the name of the computer/server.
* **`hostname -i`**: Tells you the local IP Address of your server.
* **`ifconfig`** (or modern **`ip a`**): Shows detailed network interfaces, revealing all your IP addresses and MAC addresses.
* **`cat /etc/os-release` (🚀 DevOps Essential):** If you log into a brand-new server, run this! It reads the server's "nametag" and tells you exactly what Operating System it is running (e.g., Ubuntu 20.04, CentOS 8, Amazon Linux).

---

## 2. Installing Software (Package Managers)
In Windows, you go to a website and download a `.exe` installer. In Linux, you use a **Package Manager**—it's basically an App Store built right into the terminal!

### The Great Divide: `apt` vs `yum`
```text
          [ The Linux Family Tree ]
                 /         \
          [ Debian ]     [ Red Hat ]
          (Ubuntu)      (CentOS, AWS)
             |               |
         Uses 'apt'       Uses 'yum'
```
*How do you know which to use? Run `cat /etc/os-release` to find out what OS you are on!*

### Installing Apps (Using `apt` on Ubuntu as an example):
* **`apt update`**: Downloads the latest catalog of available apps. (Always run this before installing anything!).
* **`apt install apache2`**: Installs the Apache Web Server. *(Note: On Ubuntu the web server is called `apache2`, but on RedHat it's called `httpd`!)*
* **`apt install -y apache2`**: The `-y` stands for "Yes". It installs the software instantly without pausing to ask you "Are you sure? [Y/n]". **DevOps engineers use this in automation scripts!**
* **`apt remove apache2`**: Uninstalls/deletes the software.
* **`apt list --installed`**: Shows you a massive list of every single program currently installed on the server.

---

## 3. Managing Background Apps (Services)
When you run a web server, it doesn't open a window—it runs invisibly in the background. We call these background apps **Services**.

### The Old Way
Historically, Linux used these commands to manage background applications:
* `service httpd status` -> Shows if the app is happily running or if it crashed.
* `service httpd start` -> Starts the app.
* `service httpd stop` -> Stops the app.
* `chkconfig httpd on` -> Tells the server: *"Whenever you reboot and turn on, start this app automatically."*
* `chkconfig httpd off` -> Stops the app from automatically starting on boot.

### 🚀 DevOps Essential: The Modern Way (`systemctl`)
As a modern DevOps engineer, you will almost never use `chkconfig` or `service`. The Linux world upgraded to a powerful new engine called **Systemd**. You MUST know these replacements:
* **`systemctl status nginx`** -> Check if it's running (also shows you the latest error logs!).
* **`systemctl start nginx`** -> Start it.
* **`systemctl stop nginx`** -> Stop it.
* **`systemctl enable nginx`** -> *The modern version of chkconfig*. This permanently enables the app to automatically start whenever the server reboots!

---

## 4. Other Handy Tools
* **`echo`**: Just repeats text back to you. However, you can use it to instantly write text into files without opening an editor! (e.g. `echo "hello" > test.txt`).
* **`which`**: Tells you exactly *where* a program is installed.
  * **Example:** `which python` -> Outputs `/usr/bin/python`. 
  * **🚀 DevOps Trick:** This is crucial when you have 3 different versions of Python or Node installed, and you need to figure out which one the server is actually using!