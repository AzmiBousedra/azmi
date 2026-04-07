# Linux Command Line Cheat Sheet: Developer Edition
**Author:** Azmi-Salah Bousedra

This cheat sheet is organized by common developer workflows, from basic file navigation to managing remote servers. Mastering these commands will keep you fast and efficient in the terminal, whether you're working locally, on a virtual machine, or SSHing into a remote server.

---

## 1. Navigation & Browsing
*Getting around the filesystem and finding what you need.*

| Command | Description |
| :--- | :--- |
| `pwd` | Print Working Directory. Shows your current exact folder path. |
| `ls` | List files and folders in the current directory. |
| `ls -la` | List *all* files (including hidden `.files`), with detailed info (permissions, size, owner). |
| `cd <path>` | Change directory. (e.g., `cd /var/www/` or `cd Documents`). |
| `cd ..` | Go up one directory level. (`cd ../..` goes up two levels). |
| `cd ~` | Go straight to your home directory. |
| `find . -name "*.py"` | Search for all Python files in the current directory and all subdirectories. |
| `grep -r "TODO" .` | Search for the exact text "TODO" inside *all files* within the current directory. |

---

## 2. File & Directory Operations
*Creating, moving, and destroying things.*

| Command | Description |
| :--- | :--- |
| `touch <file.txt>` | Create a new, empty file. |
| `mkdir <folder>` | Make a new directory. |
| `mkdir -p a/b/c` | Create a nested directory structure all at once (creates parents if missing). |
| `cp <file> <dest>` | Copy a file to a new destination. |
| `cp -r <folder> <dest>` | Copy an entire directory and everything inside it recursively. |
| `mv <file> <dest>` | Move a file (also used to rename a file: `mv old.txt new.txt`). |
| `rm <file>` | Delete a file permanently. |
| `rm -r <folder>` | Delete a folder and all its contents safely. |
| `rm -rf <folder>` | **DANGER:** Force delete a folder and all contents without asking for confirmation. Use with extreme caution. |

---

## 3. Viewing & Editing Files
*Reading code or logs without opening a heavy graphical editor.*

| Command | Description |
| :--- | :--- |
| `cat <file>` | Print the entire contents of a file directly to the terminal. |
| `less <file>` | Open a file in a scrollable viewer. (Use `Space` to page down, `q` to quit). |
| `tail <file>` | Print the last 10 lines of a file. |
| `tail -f <file.log>` | Live-stream the end of a file. Essential for watching live error logs. (Press `Ctrl+C` to exit). |
| `nano <file>` | Open a simple, beginner-friendly text editor in the terminal. (`Ctrl+O` saves, `Ctrl+X` exits). |

---

## 4. SSH & File Transfers (Machine-to-Machine)
*Connecting to remote servers and moving data across the network.*

| Command | Description |
| :--- | :--- |
| `ssh user@192.168.x.x` | Secure Shell. Log in to a remote machine. You will be prompted for the password. |
| `ssh -i key.pem user@ip`| Log in to a remote machine using a specific SSH key instead of a password (common for AWS/Cloud). |
| `scp file.txt user@ip:/path`| Secure Copy. Send `file.txt` from your local machine to a remote server. |
| `scp user@ip:/path/file .`| Download a file from a remote server to your current local directory (the `.`). |
| `scp -r folder/ user@ip:/` | Send an entire folder to a remote machine recursively. |
| `rsync -avz folder/ user@ip:/`| Better than SCP for large transfers. It compresses data (`z`), shows progress (`v`), and only sends files that changed. |

---

## 5. Permissions & Ownership (The `rwx` System)
*Fixing "Permission Denied" errors. Linux uses a number system for permissions:*
* **Read (r) = 4**
* **Write (w) = 2**
* **Execute (x) = 1**

*(Add them up: 7 = Read + Write + Execute. The three numbers stand for Owner, Group, and Everyone else).*

| Command | Description |
| :--- | :--- |
| `sudo <command>` | Run a command as the "superuser" (Admin). Will ask for your password. |
| `chmod +x script.sh` | Make a script executable so you can run it with `./script.sh` (adds `x` to the owner). |
| `chmod 777 <file>` | **DANGER:** Gives everyone (7) Read (4) + Write (2) + Execute (1). Bad for security. |
| `chmod 644 <file>` | Standard secure file permission: Owner can read/write (6), everyone else can only read (4). |
| `chmod 755 <folder>` | Standard folder permission: Owner has full control (7), others can read and open it (5). |
| `chown user:group <file>` | Change the owner and group of a file or directory. |

---

## 6. Installing Software (Package Management)
*How to download and install tools on Debian/Ubuntu-based systems.*

| Command | Description |
| :--- | :--- |
| `sudo apt update` | Refreshes the list of available software packages. **Always run this first.** |
| `sudo apt upgrade` | Installs the latest versions of all packages currently on your system. |
| `sudo apt install <pkg>` | Downloads and installs a new piece of software (e.g., `sudo apt install git`). |
| `sudo apt remove <pkg>` | Uninstalls a package but keeps its configuration files. |
| `sudo apt purge <pkg>` | Completely removes a package and deletes all its configuration files. |

---

## 7. System & Process Management
*Figuring out what's eating your RAM or killing a frozen script.*

| Command | Description |
| :--- | :--- |
| `top` | Open a live task manager showing CPU and RAM usage by process. (Press `q` to quit). |
| `htop` | A prettier, colorized, and easier-to-read version of `top` (install with `sudo apt install htop`). |
| `ps aux` | List every single process currently running on the machine. |
| `kill <PID>` | Politely ask a process (using its Process ID) to terminate. |
| `kill -9 <PID>` | Forcefully assassinate a frozen process that won't close. |
| `df -h` | Show available disk space on all mounted drives in human-readable format (GB/MB). |
| `du -sh <folder>` | Calculate the total size of a specific folder. |