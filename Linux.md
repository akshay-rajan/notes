# Linux

Linux is a family of UNIX - like Operating Systems based on the linux kernel, an Operating System Kernel released by Linus Torwalds in 1991.
Linux is open source, meaning it is _free to use_, _free to distribute_ and its _source code can be modified_.
Linux distributions (**distros**) package the linux kernel with various software applications and tools to create complete operating systems tailored for specific purposes. 
Popular linux distributions include **Ubundu, Debian, Fedora, OpenSUSE, elementary, Manjaro, Gentoo Linux, RedHat and Linux Mint**.
A *kernel* is a crucial component of an OS which acts as a bridge between the hardware of a system and the software applications running on it.

<hr>

| Contents | Contents | Contents |
| --- | --- | --- |
| 1. [5 Core Principles of linux](#5-core-principles) | 2. [Components](#components) | 3. [Linux Architecture](#linux-architecture) |
| 4. [File System Hierarchy](#file-system-hierarchy) | 5. [Shell](#shell) | 6. [System Information](#system-information) |
| 7. [Navigation](#navigation) | 8. [Working with Files](#working-with-files) | 9. [Find Files and Directories](#find-files-and-directories) |
| 10. [File Descriptors](#file-descriptors) | 11. [Read Files](#read-files) | 12. [Permissions and Ownership](#permissions) |
| 13. [User Management](#user-management) | 14. [Package Management](#package-management) | 15. [Service and Process Management](#service-and-process-management) |
| 16. [Task Scheduling](#task-scheduling) | 17. [Network Services](#network-services) | 18. [Web Services](#web-services) |
| 19. [Backup and Restore Files and Folders](#backup-and-restore-files-and-folders) | 20. [File System Management](#file-system-management) | 21. [Network Configuration](#network-configuration) |
| 22. [Linux Hardening](#linux-hardening) | 23. [Wireshark](#wireshark) | 24. [tcpdump](#tcpdump) |
| 25. [Hacks](#hacks) ||

<hr>

## 5 Core Principles
Linux follows [5 core principles](https://dustybugger.com/core-linux-principles/):    
|Principle|Description|
|---------|-----------|
|Everything is a file|Not only regular files and directories, but also devices, processes and even certain communication channels are represented as files
|Small, single purpose programs|Creation of small, well performing specialised programs|
|Ability to chain programs together to perform complex tasks|Integration and combination of different tools enable us to carry out many large and complex tasks, like using the o/p of one program as the i/p of another|
|Avoid captive user interfaces|Linux is designed to work mainly with the command-line interfaces, and not with restrictive user interfaces|
|Configuration data stored in a text file|Configuration settings for softwares and system components are stored in plain text file, like in /etc/passwd which stores all users in the system|


## Components
Component|Description|
---|---
Bootloader|Code that guides the booting process to start the OS.
OS Kernel|Main component of an OS. Manages the resources for system's I/O devices at the hardware level.
Daemons|Background Services that run continuously on a computer. Performs tasks such as managing system services, handling requests or monitoring activities. They start up when the system boots up and continue until shut down.
OS Shell|Operating System Shell or Command Language Interpreter (CLI) is the interface between the OS and the user. This interface lets the user tell the OS what to do. [Types of shells](https://phoenixnap.com/kb/linux-shells) include **Bourne Shell (sh), C Shell (csh), TENEX C Shell (tcsh), KornShell(ksh), Debian Almquist Shell (dash), Bourne Again Shell (bash)**
Graphics Server|Linux Provides a graphical sub-system called "X-server" that allows graphical programs to run locally
Window Manager|Graphical User Interface (GUI). e.g. GNOME, KDE, MATE, Unity and Cinnamon
System Library | Special programs using which application programs access the kernel's features
Utilities|Programs that performs particular functions

## Linux Architecture

Layer|Description
---|---
Hardware|Peripheral devices such as the system's RAM, hard drive, CPU etc.
Kernel|The core of the linux operating system whose function is to virtualise and control common computer hardware resources like CPU, allocated memory, accessed data etc. The kernel gives each process its own virtual resources and prevents/mitigates conflicts between different processes.
Shell|An interface that a user can enter commands into to execute the kernel's functions
System Utility|Makes available to the user all of the operating system's functionality

![architecture](Others/linux_architecture.jpg)

## File System Hierarchy

Linux operating system is structured in a tree-like hierarchy (*FSH* - File System Hierarchy):

![linux_file_system](Others/filesystem.png)

Path|Description
---|---
/|root of the filesystem
/bin|binaries
/boot|bootloader and other files required to boot
/dev|device files that provide access to hardware devices (/dev/sda, sda1 - our hard drives)
/etc|configuration files (/etc/network/interfaces - newtork settings)
/home|each user has a subdirectory here for storage
/lib|shared library files required for system boot
/media|external media devices such as USB drives are mounted here
/mnt|temporary mount point for regular filesystems (drives mounted manually, using commands)
/opt|optional files such as third party tools
/root|home directory of the root user
/sbin|system binary files, used for system administration
/tmp|stores temporary files
/usr|executables, libraries, manuals etc.
/var|variable data files such as logs, web application files

## Shell

A Terminal Emulator is used to communicate with the shell.
A linux terminal / shell / command line provides a text based I/O interface between the user and the computer. Shell is a text-based GUI in which we enter commands to perform actions.

Shell scripting is a powerful tool used to automate tasks, test solutions and increase efficiency.
Shell script is a text file with a list of commands that instruct the OS to perform certain tasks.

The most commonly used linux shell is the **Bourne Again Shell (BASH)** which is part of the GNU project.

## Prompt

The bash prompt is a string of characters displayed on the terminal indicating that the system is ready for our input.

    <username>@<hostname><current-working-directory>$

The `$` sign represents the user. If we log in as root, the sign changes to `#`. 
The information present in the prompt can be customised to show IP address, exit status of last command, date etc. 

## Manuals

    man <tool>

Man pages contain the detailed manuals with explanations about each tool/command. To know about the usage of a command, do

    <tool> --help
    <tool> -h

To search the documentation for a particular keyword, do

    apropos <keyword>


## System Information

Command|Description
---|---
whoami|Current Username
id | User identity
hostname | Current host system
uname | OS and system Hardware (uname -o)
pwd | Print Working Directory
netstat | Network Status
ss | Sockets
ps | Process status
env | Environment
lsblk | Lists the Hard Drives


### SSH
**Secure Shell** refers to a protocol that allows clients to access and execute commands on remote computers. It is a permanently installed tool in linux-based hosts and servers.

    ssh [username]@[IP address]


## Navigation

To find which directory we are currently on, do

    pwd

To list all the contents of a directory,

    ls
    ls -l

Which would output

        total 32
        drwxr-xr-x 2 username nothing 4096 Nov 13 17:37 Desktop
        drwxr-xr-x 2 username something 4096 Nov 13 17:34 Documents

which mentions the *Total number of blocks used* (Memory used: 512 byte * 32). The column content includes in order,

* Type and Permission
* Number of hard links / references to the file/directory
* Owner
* Memory used
* Date and Time
* Name

To also view the hidden file, do

    ls -la

To move to a directory, run

    cd path/to/the/directory
    
    # To move to the recent location
    cd -

    # To move to the previous folder
    cd ..

To clear the terminal after going to a folder, do

    cd Desktop && clear

* Keyboard Shortcuts
    * Ctrl + L : Clear terminal
    * Ctrl + R : Search in the Command History
    
## Working with Files

Create an empty file,

    touch <name>

Create a new folder

    mkdir <folder_name>

To add directories inside a directory (p for parent),

    mkdir -p folder1/folder2/folder3

To view the structure of a folder, do

    tree .

To move or rename a file, 

    mv filename folder/filename
    mv old_name new_name
    mv <file1> <file2> <folder>/

To copy a file,

    cp <file> path/to/copy/into

### Nano
Nano is a text editor.

To Create a new file in nano, run

        nano filename.txt

Now the `pager` is open. Below, we can see two lines with short descriptions. Some commands include
* Search - Ctrl + W
* Save - Ctrl + O -> Enter
* Leave the editor - Ctrl + X

[<u>Cheat Sheet</u>](https://www.nano-editor.org/dist/latest/cheatsheet.html)

## Find Files and Directories

### 1. which:
This tool returns the path to the file or link that should be executed.

    which python

### 2. find:
This can find the location of a file and also filter the results.

    find <location> <options>

    find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

In the last command, the options used are

Option | Description
---|---
-type f| Type of the searched object - file
-name *.conf | Name of the file - Any file with extension .conf
-user root | Owner of the file - Root
-size +20k | Only display files greater than 20 KiB in size
-newermt 2023-03-04| Display files newer than a given date
-exec `<command>` \ ; | Execute a specified command.
2>/dev/null | STDERR redirection to the null device

### 3. locate:
`locate` works with a local database to find the files and folders, which offers a quicker way to search through the system.

    sudo updatedb
    locate *.conf

## File Descriptors

A File Descriptor (FD) is a connection maintained by the kernel to a file to perform I/O operations (called FileHandle in Windows). The first 3 FDs are
1. `STDIN` - 0 - Input
2. `STDOUT` - 1 - Output
3. `STDERR` - 2 - Error

* We can `redirect` the standard output of any command to a file by

        echo hello world > <filename>

* To redirect the standard error to a file and the standard output to anothe file, 

        <command> <options> 2> error.txt 1> output.txt

* Normal redirection causes overwriting if the file does not exist. to append to a file instead,

        <command> <options> >> <filename>

* To redirect STDIN Data Stream to a file,

        cat << EOF > stream.txt

* We can use pipes `|` to process the output of one program to be processed by another program

        find /etc/ -name *.conf 2>/dev/null | grep systemd

## Read Files

There are two tools `more` and `less` to read files.
These are fundamental `pagers` used to scroll through the file in an interactive view.

    more <filename>
    less <filename>

The output from less will not remain in the terminal. Also, we need to press Q to exit less.

To get the first few lines (10 lines by default), use `head`

    head <filename>

To get the last few lines (last 10 lines), use `tail`

    tail <filename>

We can sort the output of a program by using '|' with `sort` tool

    <command> | sort

#### `grep` is used for Pattern-Searching. 
grep stands for *Global Regular Expression Print*.

    grep <options> pattern <files>

Some options in `grep` include 
* **-c** for displaying only the count of the lines
* **-h** for displaying the matched lines and not their filenames
* **-i** for case insensitive search
* **-v** for all lines that donot match the pattern
* **-E** treat as extended regex

We can do

    cat /etc/passwd | grep "/bin/bash"

to search for all users with bash as their default terminal.

Other similar tools used for filtering results are
* cut
* tr
* column
* awk
* sed
* wc

### Regular Expressions

Regular expressions are used to search for patterns in text and files. They are a filter criterion used to manipulate strings. Regular expressions can be created with patterns called *metacharacters*. We can use it in tools like *grep* or *sed*.

#### Grouping Operators
Operators | Description
---|---
(a)|Group parts of a regex
[a-z]|Define Character classes
{1-10}|Quantifiers - how often a previous pattern repeats
\| | OR
.* | AND


    # For all occurences of "my" or "i"
    grep -E -i "(my|i)" test.txt


## Permissions

Permissions are assigned to users and groups. Each file / directory belongs to a specific user and a specific group. The permission system in linux is based on the octal number system, and the three types of permissions that can be assigned include
* (r) - Read
* (w) - Write
* (x) - Execute

For a user to navigate to a directory, they need *execute* permission in that directory. Otherwise they will be presented with "Permission Denied". Also, *execute* permission within a directory does not allow a user to modify or execute files in there. For that, they need the corresponding permission in that file.

    - rwx rw- r--   1 root root 1641 May  4 23:42 /etc/passwd
    - --- --- ---   |  |    |    |   |__________|
    |  |   |   |    |  |    |    |        |_ Date
    |  |   |   |    |  |    |    |__________ File Size
    |  |   |   |    |  |    |_______________ Group
    |  |   |   |    |  |____________________ User
    |  |   |   |    |_______________________ Number of hard links
    |  |   |   |_ Permission of others (read)
    |  |   |_____ Permissions of the group (read, write)
    |  |_________ Permissions of the owner (read, write, execute)
    |____________ File type (- = File, d = Directory, l = Link, ... )

We can change permissions using the **chmod** command, permission group references (u - user, g - group, o - others, a - all users) and a `+` or `-` to add or remove permissions.

    # Setting read permission to all users for a file
    chmod a+r <file/directory>

    # Changing permission of the user to read only
    chmod u=r <file/directory>

We can use octal values to change permissions

    Binary Notation:                 111   |   101   |   100 
    ----------------------------------------------------------
    Octal Value:                      7    |    5    |    4
    ----------------------------------------------------------
    Permission Representation:      r w x  |  r - x  |  r - -
    
To set permission of others to read and write, 
    
    chmod 756 <filename>

### Ownership

    chown <user>:<group> <file/directory>

is used to change the owner or the group of a file or directory.

    chown root:root myfile.txt

* Set User ID (SUID) and Set Group ID (SGID) are used to configure special permissions for files.
* Sticky bits add an extra bit of security, often used on shared folders, to let only the owner of the directory to delete files. It is represented by the letter 't'. (`rwxrwxrwt`).

## User Management

To add a new user, run

    adduser <username>

The users in the system are stored in the file `/etc/passwd`. To view the created user, run
    
    cat /etc/passwd

The passwords (hashed) are stored in `/etc/shadow`

    sudo cat /etc/shadow

Some Commands used for user management are
Command | Description
---|---
sudo | execute command as a different user
su | switch user
adduser, useradd | create a new user
userdel | delete a user account
usermod | modifiy a user account
groupadd, addgroup | adds a group
groupdel, delgroup | deletes a group
gpasswd | remove a user from a group
passwd | change user password

To change the password of a user, run

    sudo passwd <username>

To change the shell of a user to bash,

    sudo usermod <username> --shell /bin/bash

To create a new group,

    sudo groupadd <groupname>
    sudo /etc/group

### sudo
sudo or **SuperUser DO** is the command used to impersonate the *root user*. We can switch user using `su` to become the root user by doing

    sudo su - 

and entering the password.

The **sudoers file** is the file that defines who can use the `sudo` command. We can edit this file (caution!) by 

    sudo visudo

## Package Management

*Packages* are archives that contain binaries of software, configuration files, information about dependencies etc. 
Package Management Systems provide features such as Package Downloading, Dependency Resolution, a standard package format, common configuration and installation locations etc.
The two main package managers are
* dpkg - Depackager - Used to install, build, remove and manage Debian Packages. We need to manually download a package and the dependencies will not be resolved automatically.

        dpkg -i <packagename.deb>

* apt - Advanced Package Tool - High-level command-line interface for package management system. apt fetches the package from a repository (`apt-cache`) and installs it, along with the dependencies.

        sudo apt update                  # Update the list of packages
        sudo apt install <packagename>
        sudo apt show <packagename>      # Show the details of any package
        apt list --installed             # Show the list of all installed packages
        sudo apt search <something>
        sudo apt remove <packagename>    # Does not remove user-data
        sudo apt purge <packagename>     # Removes a package
        sudo apt upgrade                 # Updates the installed packages
        sudo apt full-upgrade            # Also removes previously installed redundant packages

* aptitude - Alternative to apt
* snap - Install, configure or remove snap packages. We can distribute our apps in the Snap Store. To install VS Code, just do

        sudo snap install --classic code

* gem - Package manager for Ruby
* pip - Package manager for python

        pip3 install -r requirements.txt
        # requirements.txt file contains package names of the format `package_name==version`

* git - A distributed version-control system

        git clone <url>

## Service and Process Management

There are two types of services, those that are required at the startup, and those installed by the user.

### Processes

**Process** is an instance of a running program. To list all the processes in the system, run

    ps -aux

Where, `a` - all users, `x` - processes not executed by the terminal, `u` - lists the user that the process belongs to.

To find all active processes running on the system, do

    ps -u <username>


A process can have 4 states:
* Running
* Waiting (for an event or resource)
* Stopped
* Zombie (stopped, but still in the process table)

To get a real-time view of active processes in the system, run

    top

We can control processes using commands like `kill`, `pkill`, `killall` etc.
To interact with a process, we must send a signal to it. 
Signal | Description
---|---
1 | Terminal controlling the process is closed
2 | Interrupt - Ctrl + C
3 | Quit - Ctrl + D
9 | SIGKILL - Kill a process
15 | Program termination
19 | Stop the program
20 | Suspend - Ctrl + Z

To get the process ID of a process by name, we can use the tool which combines `ps` and `grep` to do

    pgrep <process_name>

To kill a process, do 

    kill -9 <pid>
        or
    pkill -9 <process_name>

To view all the signals, run `kill -l`.

`Ctrl + D` pauses a process and moves it to the background. 
To display backgroud processes, run 
    
    jobs 

To resume background processes, or to bring a process to the foreground, run respectively 

    bg <job_id>
    fg <job_id>


### Services

**Daemons** are processes / services that run in the background, without any user interaction. These are identified by the letter `d` at the end of the program name, e.g. sshd or systemd.


The system manager, `systemd` is a daemon that monitors all other services in the system. It is an Init Process that starts first and then starts the other processes using a *forking*. To see the forking, run

    pstree

The daemons controlled by systemd are called `units`. Daemons can be started, stopped and restarted using the command `systemctl`.

    systemctl status <process>

    sudo systemctl start <process>
    sudo systemctl stop <process>
    sudo systemctl restart <process>
    sudo systemctl reload-or-restart <process>

To enable or disable startup services, run

    sudo systemctl disable <process>
    sudo systemctl enable <process>

To see the status of daemons, do

    sudo systemctl is-active <process>
    sudo systemctl is-enabled <process>

To see all daemons that are active, run

    sudo systemctl list-units

To see all processes,

    sudo systemctl list-units --all
    sudo systemctl list-unit-files

Journalctl contains the logs of SYSTEMD

    sudo journalctl -xe

## Task Scheduling

Task scheduling allows users to schedule and automate tasks like automatically updating software, running scripts, cleaning databases, automating backups etc. 
In addition, alerts can be set up when certain events occur. 

### CRON

To automate running a script on every boot, you can use the `cron` utility in Linux.

1. Open the terminal.
2. Type `crontab -e` to edit the cron table.
3. Add the following line to the end of the file:

```bash
@reboot /path/to/your/script.sh
```
This will run your script every time the system boots up.

`systemd` is a daemon / tool used to start services at a specific time. We can set up processes or scripts to run at a specific time, and also specify events that will trigger certain tasks.
To do this, we need to 

### 1. Create a timer

Create a directory where timer script will be stored
    
    sudo mkdir /etc/systemd/system/mytimer.timer.d
    
    sudo vim /etc/systemd/system/mytimer.timer

Configure the timer with a script file, including when to start after the system boot (`OnBootSec`) and at what interval it should repeat, after the activation (`OnUnitActiveSec`). 

    [Unit]
    Description=My Timer

    [Timer]
    OnBootSec=3min
    OnUnitActiveSec=1hour

    [Install]
    WantedBy=timers.target

### 2. Create a service

    sudo vim /etc/systemd/system/mytimer.service

Write the service file, mentioning the script to run in it (`ExecStart`) and when the service should be started (`WantedBy`).

    [Unit]
    Description=My Service

    [Service]
    ExecStart=/full/path/to/my/script.sh

    [Install]
    WantedBy=multi-user.target

Now we need to reload `systemd`

    sudo systemctl daemon-reload

### 3. Activate the timer

    sudo systemctl start mytimer.service
    sudo systemctl enable mytimer.service

## Network Services

Network Services are used to communicate with other computers over the network, connect, transfer files, analyze traffic etc. 

### SSH (Secure Shell)

SSH is a network protocol that allows the secure transmission of data and commands over a network. 
It is widely used to securely manage and access remote systems.
In order to connect to a remote system via SSH, an SSH server must be available and running. 

    sudo apt install openssh-server -y

The most commonly used SSH Server is `OpenSSH Server`. 

    systemctl status ssh

Log in to the remote server via

    ssh username@hostname

We can configure ssh by editing the file `/etc/ssh/sshd_config`.

### NFS (Network File System)

NFS allows us to store and manage files on remote systems. 

    sudo apt install nfs-kernel-server -y
    systemctl status nfs-kernel-server

We can configure NFS by editing ` /etc/exports`.

### Web Server

A web server is a type of application that provides data / documents / applications / functions over the internet. 
They use HTTP (HyperText Transfer Protocol) to send data to clients such as Web Browsers and to receive requests from them.
These are then rendered into HTML in the client's browser.
Some popular web servers of linux include `apache` and `nginx`.

    sudo systemctl enable apache2

We can serve a page using python, using `http.server`

    python -m http.server [port]

or php, via

    php -S 127.0.0.1 [port]

### VPN 

`Virtual Private Network` is a technology that allows us to connect securely to another network as if we were directly in it.
This is done by creating an encrypted tunnel connection between the client and the server. 
VPNs are commonly used by companies to provide their employees with secure access to the internal network without having to be physically located in the network.
It can also be used to anonymize traffic. 
Some VPN Servers for linux include OpenVPN, SoftEther, PPTP, etc. 
OpenVPN provides us with a variety of features including encryption, tunnelling etc.
To install OpenVPN and connect to it, run 
    
    sudo apt install openvpn -y
    sudo openvpn --config internal.ovpn

## Web Services

### cURL

`curl` is a very powerful tool that allows us to transfer files from the shell over protocols like HTTP, HTTPS, FTP etc.

    curl <https://url>
    curl <localhost:[port]>

This will get us the soruce code of the website on the terminal.


We can see the **response header** (`<`) of a website using curl

    curl -I <url>

For the **request header** (`>`), do
        
    curl -v <url>


### wget

With `wget`, we can download files from FTP or HTTP servers directly from the terminal. The content is downloaded and stored locally.

    wget <url>

We can also do this with curl:

    curl -o filename <url>

### Backup and Restore Files and Folders

`rsync` allows us to back up files and folders to a remote location. `deja dup` is a graphical backup tool for Ubuntu. 

    rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory

    rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory

## File System Management

Orgainzing and maintaining the data stored. Linux supports many file systems including `ext2, ext3, ext4, NTFS` etc.

Linux file system is based on Unix File System. 
At the base of this file system is the `inode table`, containing a table of information associated with each file and directory.

### Disk Management

* `fdisk`: Create, delete and manage partitions on a drive.
* `mount`, `unmount`: Mount / Unmount file system.

### Swap

When the system runs out of physical memory, the kernel transfers inactive pages of memory to the `swap` space, freeing up physical memory for use by active processes.

Swap space can be created either during installation or using commands `mkswap` and `swapon`.


## Network Configuration

### Configuring Network Interfaces

Network interfaces can be configured using the `ifconfig` or `ip` commands.
    
    ip addr

### Network Access Control (NAC)

NAC is a security system that ensures that only authorized systems have access to the network.
The common NAC technologies include `DAC (Discretionary)`, `MAC (Mandatory)`, `RBAC (Role-based)` etc.

### Troubleshooting

1. `ping`: To test the connectivity between two devices.

        ping <remote_host>
2. `traceroute`: Traces the root packets taken to reach a remote host

        traceroute <url>

3. `netstat`: Display active network connections and their ports

        netstat -a

## Linux Hardening

* Keep the installed applications and the operating system up-to-date by running

        sudo apt update && sudo apt dist-upgrade

* `fail2ban` counts the number of failed login attempts and if the predetermined limit is exceeded, the host is handled as configured.

* User's access to commands can be restricted by alloting only specific commands mentioned in the `sudoers file`.

* We can restrict traffic in and out of a system by using `Linux Firewall` and `iptables`

* We can lock down the system by using a kernel security module such as Security-Enhanced Linux (`SELinux`) or  `AppArmor`, which labels every process, file and directory.

* `TCP Wrapper` allows the system administrator to control which services are allowed to access the system.
This can be set in the configuration files `/etc/hosts.allow` and `/etc/hosts.deny`.

* `Firewalls` provide a security mechanism for controlling and monitoring network traffic.

* `iptables` utility provides a flexible set of rules for filtering network traffic based on criterias such as source and destination ip addresses, port numbers protocols etc.

* The main components of **iptables** are
    * Tables: To organize firewall rules. eg. filter, nat, mangle
    * Chains: Group a set of firewall rules applied to a specific type of network traffic
    * Rules: Defines the criteria for filtering the network traffic and the actions to take for packets that match the criteria
    * Matches: Match specific criteria for filtering network traffic, such as ip, ports, protocols etc.
    * Targets: Specify the actions for packets that match a specific rule

* `System Logs` are a set of files that contain information about the system and activities taking place in it.

Logs | Location | Information it Contains
--- | --- | ---
Kernel logs | /var/log/kern.log | system calls, hardware drivers, kernel events
System logs | /var/log/syslog | System level events such as service starts and stops, login attempts, system reboots
Authentication logs | /var/log/auth.log | Successful and failed user authentication attempts
Application logs | /var/log/< applicaton_name >/error.log | Activities of specific applications
Security logs | /var/log/fail2ban.log , ufw.log etc.  | Logs of a particular security application.

## Wireshark

Wireshark is a popular network protocol analyzer tool that allows you to inspect network traffic in real-time or from a saved file.

1. **Install Wireshark**: In Ubuntu, you can install Wireshark using the command `sudo apt install wireshark`. In Windows, you can download it from the official Wireshark website and follow the installation wizard.

    https://www.wireshark.org/download.html

2. **Start Wireshark**: Open Wireshark. You'll see a list of available network interfaces.

3. **Choose a network interface**: Select the network interface that you want to capture traffic from. This is typically the interface that's connected to the network you're interested in.

4. **Start capturing packets**: Click the "Start" button to begin capturing packets on that interface.

5. **Stop the capture**: Click the "Stop" button when you want to stop the capture.

6. **Analyze the packets**: You can now see a list of packets that have been captured. Click on a packet to see more details about it. You can also use the "Filter" bar at the top to filter packets based on various criteria.

For example, to filter HTTP traffic, you can enter "http" in the filter bar and press Enter. Only packets that match the filter will be displayed.

| Filter | Description |
| --- | --- |
| `ip.addr == 10.0.0.1` | Filter IP address |
| `tcp.port == 80` | Filter TCP port |
| `udp` | Filter all UDP packets |
| `tcp` | Filter all TCP packets |
| `http` | Filter all HTTP traffic |
| `dns` | Filter all DNS traffic |
| `ftp` | Filter all FTP traffic |
| `icmp` | Filter all ICMP traffic |
| `ip.src == 10.0.0.1` | Filter source IP address |
| `ip.dst == 10.0.0.1` | Filter destination IP address |
| `tcp.srcport == 80` | Filter source TCP port |
| `tcp.dstport == 80` | Filter destination TCP port |
| `frame.len == 64` | Filter by frame length |
| `eth.dst == 00:11:22:33:44:55` | Filter by destination MAC address |
| `eth.src == 00:11:22:33:44:55` | Filter by source MAC address |

You can combine filters using logical operators:

- `&&` (logical AND): `ip.src == 10.0.0.1 && tcp.port == 80`
- `||` (logical OR): `ip.src == 10.0.0.1 || ip.src == 10.0.0.2`
- `!` (logical NOT): `!arp`

## tcpdump

`tcpdump` is a command-line utility that captures and displays network traffic. It's available on most Unix-like operating systems and is used for network troubleshooting, analysis, software and communications protocol development, and education.

    sudo apt install tcpdump

* **Capture packets**: To capture packets and display them on the screen, you can use the command `sudo tcpdump -i <interface>`. Replace `<interface>` with the name of your network interface, such as `eth0` or `wlan0`.

* **Filter packets**: `tcpdump` supports a wide range of filters that allow you to limit which packets are captured or displayed. For example, `sudo tcpdump -i eth0 tcp port 80` will only capture TCP packets on port 80.

* **Write to a file**: To write the captured packets to a file instead of displaying them on the screen, you can use the `-w` option, like this: `sudo tcpdump -i eth0 -w output.pcap`.

* **Read from a file**: You can read packets from a file using the `-r` option, like this: `tcpdump -r output.pcap`.


# Hacks

| Action                          | Command                    |
|---------------------------------|----------------------------|
| Go to home directory            | `cd`                       |
| Jump back two directories       | `cd ../..`                 |
| Clear the terminal              | `Ctrl + L`                 |
| Get previous commands           | Arrow keys                 |
| Go back to the previous directory | `cd -`                     |
| List contents of current directory (long format) | `ls -l` or `ll`   |
| List all contents (including hidden files) | `ls -al` or `la`  |
| Zoom In / Out                   | `Ctrl + +` / `Ctrl + -`    |
| Autocomplete                    | `tab`                      |
| Copy                            | `Ctrl+Shift+C`             |
| Paste                           | `Ctrl+Shift+V`             |
| Move to beginning of line       | `Ctrl+A`                   |
| Move to end of line             | `Ctrl+E`                   |
| Delete text before cursor       | `Ctrl+U`                   |
| Delete text after cursor        | `Ctrl+K`                   |
Delete the last word | `Alt+Backspace`
Open current command in default text editor | `Ctrl+X+E`
To put a `sudo` before last command | `sudo !!`
Display all the current available options | `tab tab`
Monitor a file in real time | tail `-f` filename
Search in command history | `Ctrl+R`





