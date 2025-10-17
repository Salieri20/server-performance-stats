# server-performance-stats
A Bash script (server-stats.sh) to analyze basic server performance metrics on any Linux system. It provides insights into CPU usage, memory usage, disk utilization, and the top resource-consuming processes. Optional stretch features include OS version, uptime, load averages, logged-in users, and failed login attempts.

## Features

- **Memory Usage**  
  - Shows total, used, and available memory in human-readable format.  
  - Displays memory usage percentages.  

- **CPU Usage**  
  - Measures total CPU usage, and breaks it down into user, system, and idle percentages.  
  - Uses `/proc/stat` to calculate CPU usage over a 1-second interval for accurate results.  

- **Disk Usage**  
  - Displays all non-temporary filesystems with total, used, available space, and usage percentages.  

- **Top Processes**  
  - Lists the top 5 processes by memory usage.  
  - Lists the top 5 processes by CPU usage.  

---

## Installation

1. **Clone the repository**:

```bash
git clone https://github.com/your-username/server-stats.git
cd server-stats
```
2. **Make the script executable**:

```bash
chmod +x server-stats.sh
```

## Usage
**Run the script**:
```bash
./server-stats.sh
```
**Sample Output**:
```bash
=============== SERVER PERFORMANCE STATS =================
--------------------
Total Memory Usage |
--------------------
Total           Used            Available
8G              3.2G            4.5G
100%            40.00%          60.00%

---------------------------------
Top 5 processes by memory usage |
---------------------------------
  PID COMMAND         %MEM
 1234 firefox         12.5
 2345 chrome          10.0
 ...

-----------------
Total CPU Usage |
-----------------
CPU Usage: Total=7% | User=4% | System=3% | Idle=93%

------------------------------
Top 5 processes by CPU usage |
------------------------------
  PID COMMAND         %CPU
 3456 python3         25.0
 4567 java            12.5
 ...

------------------
Total Disk Usage |
------------------
Filesystem                  Total     Used     Avail    Use%   Avail%
/dev/mapper/centos-root     50G       20G      28G      42%    58%
/dev/sda1                   500M      200M     300M     40%    60%
```

## How It Works

**CPU Usage**:

- Reads CPU counters from /proc/stat at two points, 1 second apart.

- Calculates the delta for user, system, idle, and iowait times.

- Computes the total CPU usage as (total - idle) / total * 100.

**Memory Usage**:

- Uses the free command to show total, used, and available memory.

- Calculates usage percentages.

**Disk Usage**:

- Uses df -h and filters out tmpfs and CD-ROM devices.

- Calculates used and available percentages per filesystem.

**Top Processes**:

- Uses ps to list top 5 processes by CPU and memory usage.

## Requirements

- Bash shell

- Standard Linux utilities: ps, df, free, awk, grep

## Compatibility

**Tested on**:

- CentOS / RHEL

- Ubuntu / Debian
