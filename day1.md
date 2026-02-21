🐧 Linux Core Components – Easy Notes
1️⃣ Core Components of Linux

Linux is mainly divided into three layers:

+---------------------------+
|        User Space         |
|  (Apps, Shell, Commands)  |
+------------↑--------------+
|          Kernel           |
| (CPU, Memory, Devices)    |
+------------↑--------------+
|        Hardware           |
| (CPU, RAM, Disk, NIC)     |
+---------------------------+
🔹 Kernel (Heart of Linux)

The kernel is the core of the operating system.

What it does:

Manages CPU scheduling

Manages memory (RAM)

Controls devices (disk, network, USB)

Handles system calls (bridge between apps & hardware)

📌 Example:
When you run ls, the kernel:

Reads the disk

Fetches file info

Sends results back to the shell

🔹 User Space

This is where users and applications live.

Includes:

Shell (bash, zsh)

Commands (ls, ps, top)

Applications (nginx, docker, java)

📌 User space cannot directly access hardware — it must ask the kernel.

🔹 Init / systemd

The first process started by the kernel.

Old systems: init

Modern systems: systemd

📌 systemd always has:

PID = 1
2️⃣ How Processes Are Created & Managed
🔹 Process Creation Flow
User runs command
     |
     v
Shell (bash)
     |
     v
fork()  ---> creates new process
     |
     v
exec()  ---> loads program into memory
     |
     v
Process running

📌 Important terms:

PID → Process ID

PPID → Parent Process ID

Example:

ps -ef
🔹 Process States
Running  → Ready → Sleeping → Zombie

Running – Using CPU

Sleeping – Waiting (I/O, network)

Zombie – Finished but not cleaned

Kernel controls all process states.

3️⃣ What systemd Does (and Why It Matters)
🔹 systemd Overview

systemd is the service & system manager.

Kernel
  |
  v
systemd (PID 1)
  |
  +-- nginx
  +-- sshd
  +-- docker
  +-- cron
🔹 What systemd Manages

✔ Starts services at boot
✔ Stops & restarts services
✔ Handles dependencies
✔ Logs system events
✔ Controls targets (runlevels)

🔹 Common systemd Commands
systemctl status nginx
systemctl start nginx
systemctl stop nginx
systemctl enable nginx
journalctl -xe
🔥 Why systemd is Important (DevOps View)

Faster boot (parallel service start)

Automatic service restart

Centralized logging

Essential for production servers

📌 Without systemd:
❌ Manual service handling
❌ Slower boot
❌ Hard troubleshooting

🧠 One-Line Summary (Interview Gold)

Linux consists of the kernel, user space, and systemd. The kernel manages hardware and processes, user space runs applications, and systemd controls system startup and services.