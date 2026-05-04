## What is computer:
* It is a machine that can perform calculations,process data,ans store information,

## server
* it only host applications

## Client Server architecutrue:
* It is a design pattern used in network computing. It contain 2 main components to intarct
* 1.client
* 2.server

## If there is any issue after hitting any thing in browser 
* beacause of
* 1.Network application
* 2.Application issues

## How to connect to the server:
* required things:
* protocols:http/https
* port:80/443
* Ip:DNS IP
* username:
* password:

## ssh-----> secure shell
* port----> 22
* linux server work on SSH

## They are 2 types of traffic
* Inbound trafficd
* Outbound Traffic

## They are 2 types of keys
* private key
* public key


# LINUX ADMINISTARTION

## user mangement:

Here we want add user or groups. so we need to add admin. 

```bash
sudo su -         # To login as a admin
useradd <username>         # To crate user
id <username>              # To check whether the user is created or not. It will display the user information
```

In linux we have 2 types of groups  
1..Primary group (gid)  
2.secordary gruop (groups)  
when you create any user by deafault group also created.  
one primary group atleast one secondary group  

```bash
cat /etc/passwd       # It will show users list  
cat /etc/group        # It will show group list
```

```bash
groupadd <groupname>                # It will create groupname
usermod -g <groupname> <username>   # It will add user to particular group
usermod -aG <groupname> <username>  # It will add user to particular group 
```

- `-g` means primary group  
- `-aG` means secorndary group

```bash
userdel <username>     # It will delete the user
groupdel <groupname>   # It will delete the group
```

## set the password to user:

```bash
useradd <username>
passwd <username>
```

Try to login in another window with the latest user

first it will denied the permisssion beacuse we need to modigy the configuration file

```bash
vim /etc/ssh/sshd_config
```

Change the below line:

```
PasswordAuthentication yes
```

```bash
systemctl restart sshd
```

Now you can able to login

---

## Permissions:

```
r ----> READ    ----> 4  
w ----> Write   ----> 2  
x ----> Execute ----> 1
```

Example file permissions:

```
drwx r-x r-x-
```

- `d` ---> Directory/files  
- `rwx` ---> This is for user/admin/root ---> `u`  
- `r-x` ---> This is for groups             ---> `g`  
- `r-x` ---> This is for others             ---> `o`

```bash
chmod ugo+w         # It will write acess to all gruops users,and others
chmod ugo+rwx       # It will all acess to all users,gruops and other
```

By deafalut root can conatin write acess

```bash
chmod 700 <filename>       # It will all acess to user and remaing don't have any acess
chown <username> <filename>
```
# 🖥️ Virtual Machine

There are a lot of servers we have created, but we haven't used 100% of CPU and RAM.  
Here, a lot of data is wasted, so this is called **inefficiency**.

With the concept of **virtualization**, we install a **hypervisor**.

- **Hypervisor** is a software that can be installed on a physical machine.
- Here we can do **logical isolation**.
- We add **efficiency** using the hypervisor by logically separating resources.
- There is **no dependency** between all VMs — every VM has its own CPU, RAM, and all other components.

---

# 🐧 LINUX OS

**Operating System** means it is the **bridge between software and hardware components**.

### Example:

When we use a program (browser or any app), it doesn't talk to hardware components like CPU, memory, or disk directly.  
Instead, it uses the **Operating System (OS)**.


---

## 🔧 Key components between software and hardware:

### ✅ System Software
- Software that runs the system and helps work with hardware (e.g., **libraries**, **drivers**)

### ✅ User Process
- A program started by the user (e.g., **Chrome**, **a Python script**, etc.)

### ✅ System Libraries

- Ready-made code that both apps and the OS can use (e.g., **math functions**, **file handling**)
- System libraries are responsible for performing tasks like calculations, file handling, etc., so that applications don't have to write those from scratch.


### ✅ Kernel
- This is the **main part of the OS** that talks to hardware and controls everything.
- Kernel is responsible for communication between software and hardware.

#### Kernel Responsibilities:
- Device Management  
- Memory Management  
- Process Management  
- Handling Management  

### ✅ OS
- Software that **manages hardware** and lets applications run.

---

## 🔄 System Architecture

[User Process / App]
↓
[System Libraries]
↓
[Operating System]
↳ Shell / UI (what you see)
↳ Kernel (core manager)
↳ Drivers (to talk to devices)
↓
[Hardware]

## What is Linux?
- Linux is an open-source operating system like Windows and macOS, but it is free.

## Why Linux is Important?
- Most of the cloud providers like Azure, GCP, AWS run Linux VMs.
- Automation tools like Ansible, Kubernetes, Docker mostly work on Linux.
- CI/CD servers like Jenkins mostly run on Linux.
- Bash scripting is easy in Linux.

## What is Networking?
- Networking means connecting one or more devices like containers, servers, computers so they can share information.
- There are 2 types:
  - **Private Networking:** Used for internal purposes.
  - **Public Networking:** Used for internet-facing applications.

## Core Network Concepts:
- **IP Address:** Unique address of a machine on a network.
- **Port:** Doorway to communicate with a machine.
- **Protocol:** Rules for communication like HTTPS, HTTP, UDP, TCP.
- **Subnet:** A small network within a big network.
- **Gateway:** Device that connects two different networks.

## Viewing Network Interface:
- `ip config` or `ip link show`

## Configuring Network Interface:

### Static IP Address:
- You need to add the network configuration:
  - `sudo nano /etc/network/interfaces`
- To restart and save:
  - `sudo systemctl restart networking`

### Dynamic IP Configuration:
- It can be done using DHCP.
- Configuration example under `/etc/network/interfaces`:
  auto eth0 iface eth0 inet dhcp
- To restart and save:
- `sudo systemctl restart networking`

## Network Configuration Files:
- `/etc/network/interfaces` location.
- This file is mostly used on Debian-based systems to configure the network interface.

## What is CIDR Block?
- CIDR means Classless Inter-Domain Routing blocks.

## IPv4 Address:
- It contains 32-bit numeric values written in 4 decimals.
- Example: `192.168.1.1`

### IPv4 Address Classes:
- **Class A:**  
`1.0.0.0` to `127.255.255.255` (Default subnet mask: `255.0.0.0` /8)
- **Class B:**  
`128.0.0.0` to `191.255.255.255` (Default subnet mask: `255.255.0.0` /16)
- **Class C:**  
`192.0.0.0` to `223.255.255.255` (Default subnet mask: `255.255.255.0` /24)

## Calculating CIDR Blocks:

- Common prefix lengths:
- `/8`: 8 bits for network and 24 bits for host.
- `/16`: 16 bits for network and 16 bits for host.
- `/24`: 24 bits for network and 8 bits for host.

- Example:
- IP: `192.168.1.0`
- 32 bits total, each number (octet) has 8 bits (192, 168, 1, 0).
- `/24` means:
  - First 24 bits = Network part (fixed) → `192.168.1`
  - Last 8 bits = Host part → `0` can be changed.

## How Many Hosts You Get for a Given CIDR Block:
- Formula:  
`Number of hosts = 2^(number of host bits) - 2`
- We subtract 2 because:
- 1 for broadcast address (all bits 1).
- 1 for network address (all bits 0).

### Examples:
- `/24`:  
- 32-24 = 8 host bits  
- Total IP addresses = 2^8 = 256  
- Usable IPs = 256 - 2 = 254 hosts
- `/16`:  
- 32-16 = 16 host bits  
- Total IP addresses = 2^16 = 65536  
- Usable IPs = 65536 - 2 = 65534 hosts
- `/8`:  
- 32-8 = 24 host bits  
- Total IP addresses = 2^24 = 16,777,216  
- Usable IPs = 16,777,216 - 2 = 16,777,214 hosts

