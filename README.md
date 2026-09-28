Project: [https://roadmap.sh/projects/server-stats](https://roadmap.sh/projects/server-stats?utm_source=chatgpt.com)

# Server Stats

This project is a Bash script that checks basic server performance information on a Linux server.

The script is called `server-stats.sh`.

## 1. Create the project folder

I created a folder for the project:

```bash
mkdir ~/server-stats
cd ~/server-stats
```

## 2. Create the script

I created the script using:

```bash
nano server-stats.sh
```

The script contains commands to check:

* CPU usage
* Memory usage
* Disk usage
* Top 5 processes by CPU usage
* Top 5 processes by memory usage

## 3. Make the script executable

After creating the script, I gave it execute permission:

```bash
chmod +x server-stats.sh
```

## 4. Run the script

I ran the script with:

```bash
./server-stats.sh
```

The script displays the current server statistics.

Example:

```text
==============================
       SERVER STATS
==============================

CPU Usage:
Used: 0.00%

Memory Usage:
Used: 319Mi / 909Mi (35.09%)

Disk Usage:
Used: 2.6G / 6.8G (38%)
Free: 4.2G

Top 5 Processes by CPU:
...

Top 5 Processes by Memory:
...
```

## 5. CPU usage

For CPU usage, I used `top` to get the current CPU information and `awk` to calculate the total usage.

```bash
top -bn1 | grep "Cpu(s)" | awk '{printf "Used: %.2f%%\n", $2 + $4}'
```

## 6. Memory usage

I used the `free` command to get the total, used and free memory.

```bash
free -h
```

The script also calculates the percentage of memory currently being used.

## 7. Disk usage

I used `df` to check the disk space:

```bash
df -h /
```

The script displays the used space, free space and usage percentage.

## 8. Top processes

I used `ps` to list running processes and sort them by CPU usage:

```bash
ps aux --sort=-%cpu | head -n 6
```

And by memory usage:

```bash
ps aux --sort=-%mem | head -n 6
```

The first line is the table header, so the commands display the top 5 processes.

## 9. Stretch goal

I also added the OS version as an additional statistic:

```bash
grep PRETTY_NAME /etc/os-release
```

This displays the Linux distribution and version running on the server.

## Result

The final script can be run with:

```bash
./server-stats.sh
```

It provides the required server performance statistics and also displays the OS version.
