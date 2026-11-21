# DevOps and SRE Interview Question Bank

This page lists 60 questions that candidates commonly report, grouped by round. Each has a one-line pointer, not a full answer. Practice by answering aloud for two minutes, then compare your answer with the linked page.

## Linux and networking

Guide: [Linux and networking](../rounds/linux-and-networking.md)

| # | Question | Pointer |
|---|---|---|
| 1 | What happens when you type a web address and press Enter? | DNS, TCP, TLS, HTTP, load balancer, application |
| 2 | What does load average measure? | Tasks running, waiting to run, or blocked on input and output |
| 3 | What is a zombie process? | A finished child whose parent has not read its exit status |
| 4 | What is an inode? | The record of a file's metadata and block locations |
| 5 | How does a hard link differ from a symbolic link? | Same inode against a path that points to another path |
| 6 | Why can a disk with free space refuse writes? | Inodes are exhausted |
| 7 | What does the out-of-memory killer do? | The kernel stops a process to free memory |
| 8 | How does a TCP connection open? | SYN, SYN-ACK, ACK |
| 9 | How does a refused connection differ from a timeout? | An answer that nothing listens against no answer |
| 10 | What does a DNS time to live control? | How long a resolver may cache an answer |
| 11 | What does a TLS handshake establish? | Server identity and shared encryption keys |
| 12 | What is the difference between SIGTERM and SIGKILL? | A request that can be handled against one that cannot |

## Troubleshooting

Guide: [Troubleshooting](../rounds/troubleshooting.md)

| # | Question | Pointer |
|---|---|---|
| 13 | The website is down. What do you check first? | Confirm, scope, and ask what changed |
| 14 | A server has high CPU. How do you investigate? | Find the process, then the thread, then the cause |
| 15 | A server is slow but not busy. Why? | Waiting on disk, network, or a dependency |
| 16 | You cannot connect over SSH. What are the causes? | Network path, firewall, service, keys, full disk |
| 17 | About 2 percent of requests return HTTP 500. How do you find them? | Group by host, version, endpoint, and dependency |
| 18 | The failure began after a deployment. What now? | Roll back first, then compare the versions |
| 19 | A disk fills every night. How do you find the source? | Largest directories, open deleted files, log rotation |
| 20 | Memory use grows until the process is stopped. What next? | Leak against a wrong limit, measured over time |
| 21 | One of 20 servers is slow. Where do you look? | What differs on that host |
| 22 | DNS works on one host and not another. Why? | Resolver configuration and local cache |

## Coding and scripting

Guide: [Coding and scripting](../rounds/coding-and-scripting.md)

| # | Question | Pointer |
|---|---|---|
| 23 | Count requests per status code in a log. | Read line by line and use a counter |
| 24 | Print the 10 most frequent client addresses. | Count, then sort by count |
| 25 | Follow a log and print new error lines. | Keep the file open and read as it grows |
| 26 | Check 50 hosts and report failures. | A loop with timeouts, then run in parallel |
| 27 | Merge overlapping maintenance windows. | Sort by start time, then merge in one pass |
| 28 | Implement a rate limiter. | Token bucket or sliding window |
| 29 | Find the largest files under a directory. | Walk the tree and keep the top entries |
| 30 | Retry a failing call safely. | A retry limit and an increasing delay |

## Containers, pipelines, and infrastructure as code

Guides: [Containers and Kubernetes](../concepts/containers-and-kubernetes.md), [CI/CD](../concepts/ci-cd-and-deployment-strategies.md), [Infrastructure as code](../concepts/infrastructure-as-code.md)

| # | Question | Pointer |
|---|---|---|
| 31 | How does a container differ from a virtual machine? | Shared kernel against a separate kernel |
| 32 | A pod is in CrashLoopBackOff. What do you do? | Describe, read previous logs, check exit code |
| 33 | What is the difference between readiness and liveness probes? | Receive traffic against restart |
| 34 | A pod stays Pending. Why? | No node satisfies its requests or rules |
| 35 | How does a rolling update avoid dropped requests? | Readiness checks and graceful shutdown |
| 36 | Compare blue-green and canary releases. | Full switch against gradual exposure |
| 37 | How do you release a schema change? | Expand, migrate, switch, contract |
| 38 | What is in a Terraform state file? | The map from code to real resources |
| 39 | What is drift, and how do you handle it? | Manual change; reapply, adopt, or import |
| 40 | A plan shows a database will be replaced. What do you do? | Stop and find out why before applying |
| 41 | How do you manage secrets in a pipeline? | A secret store, short-lived credentials, no secrets in code |
| 42 | The pipeline takes 50 minutes. How do you shorten it? | Cache, run stages in parallel, split tests |

## Reliability and design

Guides: [SRE system design](../rounds/sre-system-design.md), [SLIs, SLOs, and error budgets](../concepts/slis-slos-and-error-budgets.md), [Capacity planning](../concepts/capacity-planning.md)

| # | Question | Pointer |
|---|---|---|
| 43 | What is the difference between an SLI, an SLO, and an SLA? | Measurement, target, contract |
| 44 | Why not target 100 percent availability? | Cost rises steeply and users cannot tell the difference |
| 45 | What do you do when the error budget is spent? | Slow releases and prioritize reliability work |
| 46 | What are the four golden signals? | Latency, traffic, errors, saturation |
| 47 | Why use percentiles for latency? | Averages hide slow requests |
| 48 | Design a metrics and alerting pipeline. | Collect, store, query, alert, and survive its own failure |
| 49 | Distribute a file to 10,000 servers. | Regional caches and a staged rollout |
| 50 | Run a service in two regions. | Data replication, traffic routing, failover test |
| 51 | How many servers does this service need? | Peak load, per-instance capacity, spare for failure |
| 52 | How do you protect a service from overload? | Load shedding, limits, and bounded retries |

## Incidents and behavioral

Guides: [Incident response](../rounds/incident-response.md), [Behavioral](../rounds/behavioral.md), [Postmortems](../concepts/postmortems.md)

| # | Question | Pointer |
|---|---|---|
| 53 | You are paged for a 30 percent error rate. What do you do? | Declare, assign roles, mitigate, communicate |
| 54 | What does an incident commander do? | Decides and coordinates, and does not debug |
| 55 | What is a blameless postmortem? | A review of the system, not of a person |
| 56 | Tell me about an outage you caused. | Plain account, numbers, and a lasting change |
| 57 | Describe manual work that you automated. | Hours before and after |
| 58 | Describe a time you delayed a release. | The risk, the data, and how the conflict ended |
| 59 | How did you improve an on-call rotation? | Fewer pages, better runbooks, fair schedule |
| 60 | What is toil, and how do you reduce it? | Manual, repetitive work; measure, then automate |

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-question-bank) answers these questions in full, with a mid-level answer, a senior answer, and follow-up questions for each.
- [Grokking the Coding Interview](https://www.designgurus.io/course/grokking-the-coding-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-question-bank) covers the patterns behind questions 27 and 28.
