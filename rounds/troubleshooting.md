# The Troubleshooting Round

In the troubleshooting round, the interviewer describes a failure and the candidate investigates it one step at a time. The interviewer supplies the result of each check. The grade depends on the method, because a candidate who guesses the cause correctly has shown nothing that can be repeated.

Most reports describe a spoken exercise. A few describe a shell, which is a command line, on a real failing machine. Ask the recruiter which form to expect.

## A five-step method

| Step | What to do | What to say aloud |
|---|---|---|
| 1. Confirm | Reproduce or measure the failure | "First I want to see the failure myself." |
| 2. Scope | Find who is affected and since when | "Is it all users, one region, or one endpoint?" |
| 3. Recent change | Ask what changed before it started | "Was there a deployment or a configuration change?" |
| 4. Narrow | Split the request path in half and test the middle | "I will check whether the request reaches the application." |
| 5. Mitigate, then fix | Restore service first, then find the root cause | "I would roll back now and investigate afterward." |

Step 5 matters most in a real incident. If a rollback is available at step 3, a senior candidate proposes it before the cause is known.

## Worked example: a slow web service

The interviewer says: "Users report that the checkout page is slow. You have access to the servers."

**Confirm.** Ask for the latency graph. The 95th percentile latency, the time under which 95 percent of requests finish, rose from 400 milliseconds to 1,600 milliseconds.

**Scope.** The slowdown affects every user of checkout and no other page. It began 12 minutes ago. One endpoint failing points to the application or its dependencies, not to the network as a whole.

**Recent change.** A new version of checkout was deployed 15 minutes ago. This is now the leading hypothesis, and a rollback is the fastest mitigation. State that, then continue to show the investigation.

**Narrow.** Check each layer in the order a request passes through it.

| Check | Command or source | Result | Conclusion |
|---|---|---|---|
| Is the host short of CPU? | `top`, `uptime` | Load is normal | Not CPU |
| Is memory exhausted? | `free -m`, `vmstat 1` | No swapping | Not memory |
| Is the disk slow? | `iostat -x 1` | Low wait time | Not local disk |
| Is the application waiting? | Application traces | Most time is spent in one database call | Dependency |
| Is the database slow? | Slow query log | A new query scans a full table | Cause found |

**Mitigate, then fix.** Roll back the release, which restores latency in about 5 minutes. Then add the missing index, release again, and change the canary rule so that it also checks latency.

## What the interviewer listens for

- Each check has a stated reason and a stated expected result.
- The candidate removes whole layers from suspicion instead of testing at random.
- The candidate asks what changed before reading any log.
- Mitigation is proposed as soon as it is possible.
- The answer ends with prevention, not only with the fix.

## Common follow-up questions

1. The rollback did not help. What would you check next?
2. Only 5 percent of requests are slow. How does that change the search?
3. The host looks idle, but the service is slow. Where is the time going?
4. How would you have detected this before users reported it?

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-troubleshooting) has six full drills, including a website that is down, a failure after a deployment, high CPU, and intermittent HTTP 500 errors.
- Lesson: [A Method for Troubleshooting](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/a-method-for-troubleshooting?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-troubleshooting), in Grokking DevOps and SRE Interviews
- Lesson: [Drill: The Website Is Down](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/drill-the-website-is-down?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-troubleshooting), in Grokking DevOps and SRE Interviews
- Lesson: [A Method for Performance Problems](https://www.designgurus.io/course-play/grokking-operating-systems-and-networking-for-backend-engineers/doc/a-method-for-performance-problems?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-troubleshooting), in Operating Systems and Networking for Backend Engineers
- [Linux commands for troubleshooting](../cheat-sheets/linux-commands-for-troubleshooting.md) lists each command with the question it answers.
- [Observability](../concepts/observability.md) explains the signals used in step 1.
