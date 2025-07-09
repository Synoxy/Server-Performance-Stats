# 🖥️ Server Monitoring Commands & Usage Guide
This README contains the commands used to fetch and display various **server statistics** related to CPU, memory, disk, and process usage.
---

## 📊 1. Total CPU Usage
```bash
mpstat | grep "all" | awk '{printf "User: %.2f%% System: %.2f%% Idle: %.2f%%\n", $3, $5, $11}'
```
This command extracts user, system, and idle CPU usage percentages.
---
## 🧠 2. Total Memory Usage (Free vs Used)
```bash
free -m | awk 'NR==2{printf "Total: %s Used: %s Free: %s Usage: %.2f%%\n", $2, $3, $4, ($3/$2)*100}'
```
Displays total, used, free memory and calculates the usage percentage.
---
## 💾 3. Total Disk Usage (Free vs Used)
```bash
df -h | grep '^/dev/' | awk 'NR==2{printf "Total: %s Used: %s Free: %s Usage: %.2f%%\n", $2, $3, $4, ($3/$2)*100}'
```
Shows disk usage details of the root filesystem.
---
## 🔥 4. Top 5 Processes by CPU Usage
### In Script (with header):
```bash
top -b -n 1 | awk 'NR==4'       # Print column headers
top -b -n 1 | awk 'NR>4' | sort -k9 -nr | head -n 5   # Print top 5 processes by %CPU
```
### In Terminal (without proper sort):
```bash
top -b -n 1 | awk 'NR>3' | head -n 6
```
⚠️ *Note:* If you use `sort` **after** `head`, the header line may be sorted incorrectly into the list. Always sort **after filtering** and add header separately if needed.
---
## 🧮 5. Top 5 Processes by Memory Usage
### With header:
```bash
ps -o user,pid,comm,rss,vsz,time,etime | awk 'NR==1'
```
### Sorted by memory (VSZ):
```bash
ps -o user,pid,comm,rss,vsz,time,etime | sort -nr -k5 | head -n 5
```
---
## 🧪 Online Testing Environments
You can try these commands in online Linux terminals:
### ✅ [VFSync - Online Linux VM](https://vfsync.org/signup)
1. Sign up for free.
2. Use `vflogin <your_username>` to log in inside the terminal.
3. Use the password provided on the signup page to authenticate.
---
### ✅ [JSLinux (In-browser OS)](https://bellard.org/jslinux/)
1. Open the link and select a Linux OS from the dropdown.
2. Click the **"Start"** link to launch the virtual Linux environment.
3. Terminal opens in-browser — ready to test your commands!
---
Happy scripting! 💻🛠
Please feel free to let me know how I can improve by raising a PR. Feel free to provide new challenges as DevOps Engineer. 
This project is part of:✅ [Roadmap.sh Challenge](https://roadmap.sh/projects/server-stats)
