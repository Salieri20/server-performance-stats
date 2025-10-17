#!/bin/bash

echo "=============== SERVER PERFORMANCE STATS ================="
echo "--------------------"
echo -e "Total Memory Usage |"
echo "--------------------"
echo -e "Total\t\tUsed\t\tAvailable"
free -h | awk 'NR==2 {print $2 "\t\t" $3 "\t\t"  $7}'
free | awk 'NR==2 {printf "100%%\t\t%0.2f%%\t\t%0.2f%%\n", ($3/$2)*100, ($7/$2)*100}'

echo "---------------------------------"
echo -e "Top 5 processes by memory usage |"
echo "---------------------------------"
ps -eo pid,comm,pmem --sort=-pmem | head -n 6

echo "-----------------"
echo -e "Total CPU Usage |"
echo "-----------------"

read -r cpu user1 nice1 system1 idle1 iowait1 irq1 softirq1 steal1 guest1 guest_nice1 <<< "$(grep '^cpu ' /proc/stat)"

sleep 1

read -r cpu user2 nice2 system2 idle2 iowait2 irq2 softirq2 steal2 guest2 guest_nice2 <<< "$(grep '^cpu ' /proc/stat)"

idle=$(( (idle2 + iowait2) - (idle1 + iowait1) ))
total=$(( (user2+nice2+system2+irq2+softirq2+steal2+idle) - (user1+nice1+system1+irq1+softirq1+steal1) ))

cpu_total=$((100 * (total-idle) / total))
cpu_idle=$((100 * idle / total))
cpu_user=$((100 * ((user2+nice2) - (user1+nice1)) / total))
cpu_system=$((100 * ((system2+irq2+softirq2) - (system1+irq1+softirq1)) / total))

echo "CPU Usage: Total=$cpu_total% | User=$cpu_user% | System=$cpu_system% | Idle=$cpu_idle%"

echo "------------------------------"
echo -e "Top 5 processes by CPU usage |"
echo "------------------------------"
ps -eo pid,comm,pcpu --sort=-pcpu | head -n 6

echo "------------------"
echo -e "Total Disk Usage |"
echo "------------------"
echo -e "Filesystem\t\t  Total    Used     Avail    Use%   Avail%"
df -h | grep -Ev '^Filesystem|tmpfs|cdrom' | awk '{printf "%-25s %-8s %-8s %-8s %-6s %-6s\n", $1, $2, $3, $4, $5, (100-$5)"%"}'; echo

