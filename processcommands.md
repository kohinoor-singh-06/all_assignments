## 🐧 Linux Process Management 

It covers essential Linux commands for monitoring and managing processes.
Each section explains what the command does, why it’s useful, and includes examples.

### Table of Contents

- Show All Processes (ps aux)
- Process Tree (pstree -p)
- Real-Time Monitoring (top)
- Adjust Process Priority (nice, renice)
- CPU Affinity (taskset)
- I/O Scheduling Priority (ionice)
- File Descriptors (lsof)
- Trace System Calls (strace)
- Find Process Using a Port (fuser)
- Per-Process Statistics (pidstat)
- Control Groups (cgroups)

#### 1. 🔍 Show All Processes

```bash
ps aux
```

- Options:
   - a → show processes for all users
   - u → show the user/owner of the process
   - x → show processes not attached to a terminal

- "ps aux" It list all the running commands on system includinng system daemons

#### Output: <img width="1347" height="1064" alt="Screenshot from 2025-09-27 00-54-15" src="https://github.com/user-attachments/assets/59c6ec8b-0157-458c-a67c-3e3f1b18e016" />

<img width="1696" height="1028" alt="Screenshot from 2025-09-27 00-54-45" src="https://github.com/user-attachments/assets/b4a25297-1c53-4e66-8e60-6c1dab6ec8e9" />

<img width="1984" height="1041" alt="Screenshot from 2025-09-27 00-55-28" src="https://github.com/user-attachments/assets/224f3021-37ce-465b-a7a5-1848affb386d" />

<img width="1984" height="1041" alt="Screenshot from 2025-09-27 00-55-49" src="https://github.com/user-attachments/assets/146b0f0a-c5ae-48e5-8b2e-b1edab96663c" />




- Useful for system monitoring, troubleshooting high CPU/memory usage, or finding PIDs.

#### 2. 🌲 Process Tree

```bash
pstree -p
```

- It Shows processes in a hierarchical tree structure.
- It Helps understand parent-child relationships.

#### Output:
<img width="1990" height="892" alt="Screenshot from 2025-09-27 00-57-01" src="https://github.com/user-attachments/assets/67dcf5f6-7d5b-48a7-a397-f9ca86da08a9" />


- Great for debugging orphan processes (An orphan process is a process whose parent has terminated (exited) while the child is still running.), or seeing how daemons and shells are linked.

#### 3. 📊 Real-Time Monitoring

```bash
top
```

- Interactive command to monitor CPU, memory, and tasks in real time.
- Navigation:
    - Press q → quit
    - Press k → kill a process
    - Press h → help

#### Output:
<img width="391" height="83" alt="Screenshot from 2025-09-27 00-58-24" src="https://github.com/user-attachments/assets/57a39032-2a13-4a33-b82f-e150b5d644bd" />

<img width="1336" height="1071" alt="Screenshot from 2025-09-27 00-58-38" src="https://github.com/user-attachments/assets/4e2380f8-af26-4aca-b389-aa36de61741d" />





#### 4.(1) ⚡ Adjust Process Priority

- Start a process with priority

```bash
nice -n 10 sleep 300 &
```

- -n 10 → sets nice value = 10 (lower priority).
- Background job [1] 30085 created.
  - Alternatives to nice - chrt (Real-time Scheduling),systemd-run and schedtool 


#### Output:
<img width="554" height="87" alt="Screenshot from 2025-09-27 00-59-58" src="https://github.com/user-attachments/assets/fcbbdb08-6eac-404e-bb4d-dff5ae0dca38" />


####  (2) Change priority of running process

```bash
renice -n -5 -p 30085
```

- Used when you want critical tasks to run faster or background jobs to run slower.

#### Output:
<img width="623" height="99" alt="Screenshot from 2025-09-27 01-01-31" src="https://github.com/user-attachments/assets/e41e8334-9395-4088-a9a4-9bb5c3a8de7c" />


#### 5. 🧩 CPU Affinity (Bind Process to CPU Core)

```bash
taskset -cp 30085
```

- It Shows CPU cores a process can use.

#### Output:
<img width="623" height="99" alt="Screenshot from 2025-09-27 01-02-25" src="https://github.com/user-attachments/assets/d59d31c9-8fe7-4577-91e4-dafcf3673728" />


- Restrict to core 1:

```bash
taskset -cp 1 30085
```

##### Output:
<img width="623" height="99" alt="Screenshot from 2025-09-27 01-02-46" src="https://github.com/user-attachments/assets/ec488f43-e7db-4272-a8b7-a2630dfd5dac" />


- Useful in performance tuning, ensuring tasks run on specific cores.

6. 📂 I/O Scheduling Priority

```bash
ionice -c 3 -p 30085
ionice -p 30085 (To Verify)
```

-  Controls disk I/O priority of a process.
- set pid 3050's IO scheduling class to idle

#### Output:
<img width="623" height="99" alt="Screenshot from 2025-09-27 01-03-55" src="https://github.com/user-attachments/assets/a95afd9e-de87-488d-bb83-9cbea017276e" />


- Prevents background jobs (like backups) from slowing down disk access.

#### 7. 📑 File Descriptors Used by a Process

```bash
lsof -p 30085 | head -5
```

- It lists files opened by a process ie checks which files, sockets, or devices a process is using.

#### Output:
<img width="1199" height="293" alt="Screenshot from 2025-09-27 01-04-38" src="https://github.com/user-attachments/assets/0f59819d-dc5d-4d0e-a0df-24290f723053" />


#### 8. 🐛 Trace System Calls of a Process

```bash
strace -p 30085
```

- Attaches to a process and shows system calls.

#### Output:
<img width="719" height="101" alt="Screenshot from 2025-09-27 01-05-13" src="https://github.com/user-attachments/assets/79da2dae-ee9b-4e84-8118-ab0eab119b98" />


- used in debugging programs by checking file, network, and system interactions.

#### 9. 📡 Find Process Using a Port

```bash
sudo fuser -n tcp 8080
```

- system prompts to enter password
- It finds which process is bound to a TCP/UDP port.
- used in debugging web servers, databases, or services.

-  PID 9467 is using port 8080.

#### 10. 📊 Per-Process Statistics

```bash
pidstat -p 30085 2 3
```

- It displays detailed CPU usage for a process over time.
    - 2 = interval (seconds)
    - 3 = number of reports

#### Output:
<img width="898" height="146" alt="Screenshot from 2025-09-27 01-06-17" src="https://github.com/user-attachments/assets/6b09b2f1-30a4-417d-971c-0fc5a008c23d" />


- It is usually considered better than top when monitoring one specified process

#### 11. 🔐 Control Groups (cgroups) for Resource Limits

1. Create a cgroup:

- Before proceeding to create control groups (cgroups), it is necessary to first install the relevant cgroup tools on your Linux system. These tools, such as cgcreate, cgset, and cgexec, are essential utilities that allow for the easy definition, configuration, and management of resource limits—like CPU time, memory, and disk I/O—for processes within the kernel's cgroup framework.  This prerequisite installation ensures that the commands you will use to set up and manage cgroups are available and functional.

```bash
sudo cgcreate -g cpu,memory:/testgroup
```

#### Output:
<img width="1989" height="820" alt="Screenshot from 2025-09-27 01-08-05" src="https://github.com/user-attachments/assets/60192445-f4a0-4fce-aae1-462e5a3155a6" />


2. Limit CPU and Memory:

- First indentify if your system is running on cgroup v1 or cgroup v2
  - If running on cgroup v1,files like cpu.cfs_quota_us and memory.limit_in_bytes exist but if on v2 cpu.max,memory.max exist
- cgroup v1 or cgroup v2 can be identifed using 

```bash
mount | grep cgroup
```

<img width="1064" height="85" alt="Screenshot from 2025-09-27 01-09-17" src="https://github.com/user-attachments/assets/e2551372-e0ca-480e-8af4-473635147bfc" />

#### Example:

- My system is running on cgroup v2

```bash
echo "50000 100000" | sudo tee /sys/fs/cgroup/testgroup/cpu.max
```

#### Output:

<img width="1064" height="97" alt="Screenshot from 2025-09-27 01-11-03" src="https://github.com/user-attachments/assets/8b636743-8f83-43bd-85ce-36ae723e2484" />



- Add process (PID 3050) to cgroup:

```bash
echo 3050 | sudo tee /sys/fs/cgroup/cpu/testgroup/cgroup.procs
```

#### Output:

<img width="1064" height="97" alt="Screenshot from 2025-09-27 01-11-52" src="https://github.com/user-attachments/assets/8b98195e-520d-40ac-94ed-db62782005fe" />


- These commands enforce resource limits on a specific process by utilizing Linux Control Groups (cgroups).  The result is that the process identified by <PID> is placed into the testgroup cgroup, where it is immediately constrained to use a maximum of 50% of a single CPU core (by setting the cpu.max value to 50000 out of 100000) and is limited to 100 Megabytes (MB) of total memory (by setting the memory.max value). This practice is crucial for resource isolation, preventing a potentially runaway or resource-intensive process from consuming all available system resources and ensuring fair sharing among all running applications.
#### Summary Table:

| Tool        | Focus                             | Alternative to        |
|------------|-----------------------------------|------------------------|
| chrt        | Real-time scheduling policies     | nice                   |
| ionice      | I/O priority control              | (complementary)        |
| taskset     | CPU affinity control              | (complementary)        |
| cgroups     | Fine-grained resource management  | nice (more powerful)   |
| systemd-run | systemd + cgroups resource mgmt   | nice                   |
| schedtool   | Custom scheduling policies        | nice                   |
