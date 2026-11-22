# Linux Commands for Troubleshooting

In a troubleshooting round, a command is useful only when the candidate can state the question it answers. This page groups standard Linux commands by that question. Say the question first, then the command, then the result that you expect.

## Is the machine short of a resource?

| Command | The question it answers |
|---|---|
| `uptime` | What is the load average over 1, 5, and 15 minutes? |
| `top` | Which processes use the most CPU and memory now? |
| `vmstat 1` | Is the system swapping, and are tasks waiting on input and output? |
| `free -m` | How much memory is free, and how much is page cache? |
| `iostat -x 1` | Which disk is busy, and how long do requests wait? |
| `df -h` | Which file system is full? |
| `df -i` | Which file system has no inodes left? |
| `du -sh *` | Which directory here uses the most space? |

`iostat` is part of the sysstat package and may need to be installed.

## What is a process doing?

| Command | The question it answers |
|---|---|
| `ps aux` | Which processes are running, and who owns them? |
| `pgrep -a <name>` | Is a process with this name running? |
| `strace -p <pid>` | Which system calls is this process making? |
| `lsof -p <pid>` | Which files and sockets does this process hold open? |
| `lsof +L1` | Which deleted files are still held open and using space? |
| `cat /proc/<pid>/status` | What are the memory figures and state of this process? |

## What do the logs say?

| Command | The question it answers |
|---|---|
| `journalctl -u <service> --since "10 minutes ago"` | What did this service log recently? |
| `systemctl status <service>` | Is the service running, and why did it last stop? |
| `dmesg -T` | Did the kernel report an error, such as stopping a process for memory? |
| `tail -f <file>` | What is being written to this log now? |
| `grep -c " 500 " access.log` | How many lines contain this status code? |

## Can the machine reach the network?

| Command | The question it answers |
|---|---|
| `ip addr` | Which addresses does this host have? |
| `ip route` | Where does traffic to a given network go? |
| `ping <host>` | Does the host answer, and how long does it take? |
| `traceroute <host>` | At which step along the path do packets stop? |
| `dig <name>` | Which address does this name resolve to, and from which server? |
| `ss -tlnp` | Which ports are listening, and which process owns each? |
| `nc -zv <host> <port>` | Is this port reachable from here? |
| `curl -v <url>` | What does the service return, with headers and timing? |
| `tcpdump -i <interface> port <port>` | Which packets arrive on this port? |

Some networks block the packets that `ping` uses. A failed ping does not prove that a host is down, so confirm with a check on the real port.

## An order for the first minute

When a host is slow and nothing else is known, a fixed order prevents random searching.

1. `uptime`: is the load unusual, and is it rising or falling?
2. `dmesg -T | tail`: did the kernel report an error?
3. `vmstat 1`: is the time going to CPU, to swapping, or to waiting?
4. `free -m`: is memory exhausted?
5. `iostat -x 1`: is a disk saturated?
6. `df -h` and `df -i`: is a file system full?
7. `top`: which process is responsible?
8. `ss -tlnp` and `curl -v`: does the service answer locally?

## Reading the results

| Observation | Likely direction |
|---|---|
| High load, high CPU use | A process is computing. Find it with `top`. |
| High load, low CPU use, high wait | Tasks are blocked on a disk or the network. |
| Free memory near zero, but large page cache | Normal. The kernel uses spare memory for caching. |
| Swap activity in `vmstat` | Memory is truly short. |
| `df -h` shows space, but writes fail | Check inodes with `df -i`. |
| `du` total is far below `df` usage | A deleted file is still held open. |

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-linux-commands-for-troubleshooting) has a lesson on Linux tools for investigation, followed by six troubleshooting drills that use them.
- Lesson: [Linux Tools for Investigation](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/linux-tools-for-investigation?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-linux-commands-for-troubleshooting), in Grokking DevOps and SRE Interviews
- Lesson: [CPU, Memory and Disk Tools](https://www.designgurus.io/course-play/grokking-operating-systems-and-networking-for-backend-engineers/doc/cpu-memory-and-disk-tools?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-linux-commands-for-troubleshooting), in Operating Systems and Networking for Backend Engineers
- Lesson: [Network State Tools](https://www.designgurus.io/course-play/grokking-operating-systems-and-networking-for-backend-engineers/doc/network-state-tools?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-linux-commands-for-troubleshooting), in Operating Systems and Networking for Backend Engineers
- [Troubleshooting](../rounds/troubleshooting.md) shows the method that these commands support.
