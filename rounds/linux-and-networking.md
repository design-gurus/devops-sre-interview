# The Linux and Networking Round

The Linux and networking round checks whether a candidate understands how the operating system and the network behave. Naming a command is not enough. A strong answer explains what the system is doing and then names the command that would confirm it.

## The topics that recur

| Area | What to be able to explain |
|---|---|
| Processes | How a process starts with `fork` and `exec`, process states, signals, and zombie processes |
| Memory | Virtual memory, the page cache, swapping, and the out-of-memory killer |
| File systems | Inodes, hard and symbolic links, file descriptors, and permissions |
| Boot and services | How a service starts under systemd and where its logs go |
| Load | What load average counts, and why high load can occur with idle CPUs |
| DNS | How a name is resolved step by step, and what a time to live value does |
| TCP | The three-way handshake, retransmission, and connection states |
| TLS | What the handshake establishes and how a certificate is verified |
| HTTP | Methods, status code classes, and keep-alive connections |
| Routing | Subnets, routes, and network address translation |

## Explain behavior, then the command

Take the question "What does load average measure?"

| Answer | What it shows |
|---|---|
| "It is the CPU usage. I would run `uptime`." | A command and an incorrect definition |
| "On Linux it is the average number of tasks that are running or waiting to run, plus tasks blocked on input and output. A load of 8 on a machine with 4 cores can mean CPU pressure or a slow disk. I would run `vmstat 1` to see which." | The behavior, a consequence, and a way to confirm it |

The second answer invites a harder follow-up question, which is how a candidate earns a higher rating.

## The classic question

"What happens when you type a web address into a browser and press Enter?" This question appears in many reports because it can be extended in any direction. A complete answer has six stages.

1. The browser resolves the name through DNS, using cached answers when their time to live has not expired.
2. The client opens a TCP connection with a three-way handshake.
3. The TLS handshake verifies the server certificate and agrees on encryption keys.
4. The client sends an HTTP request, which usually reaches a load balancer first.
5. The load balancer forwards the request to an application server, which may call a database or a cache.
6. The response returns over the same connection, and the browser renders it.

Prepare one level of extra depth for each stage. For stage 1, that might be the order of resolvers. For stage 2, it might be what happens when a packet is lost.

## Sample questions with pointers

| Question | Pointer |
|---|---|
| A disk shows free space, but writes fail with "no space left". Why? | Inodes can be exhausted before blocks are. Check with `df -i`. |
| A deleted log file still uses disk space. Why? | A running process still holds the file descriptor open. |
| A process ignores `kill`. What next? | The default signal is SIGTERM, which a process may handle. SIGKILL cannot be handled. |
| A service resolves a name on one host and not on another. Where do you look? | The resolver configuration, the local hosts file, and cached answers. |
| What is the difference between a refused connection and a timeout? | Refused means a host answered that no process listens. A timeout means no answer arrived. |

## How to prepare

- Explain each topic aloud in two minutes without notes.
- For each command in the [Linux command table](../cheat-sheets/linux-commands-for-troubleshooting.md), state the question that it answers.
- Run the commands on a real machine and read the output columns.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-linux-and-networking) has a seven-lesson chapter on Linux and networking fundamentals, taught through failures.
- [Grokking System Design Fundamentals](https://www.designgurus.io/course/grokking-system-design-fundamentals?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-linux-and-networking) covers DNS, load balancing, and proxies at the design level.
