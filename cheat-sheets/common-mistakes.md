# Common Mistakes in DevOps and SRE Interviews

Most rejected candidates in these loops knew the tools. They lost points on method, order, and communication. This page lists ten frequent mistakes, the round in which each appears, and the correction.

## The ten mistakes

| # | Mistake | Round | Correction |
|---|---|---|---|
| 1 | Guessing a cause immediately | Troubleshooting | Confirm and scope the failure first |
| 2 | Not asking what changed | Troubleshooting | Ask about recent deployments before reading logs |
| 3 | Seeking the root cause while users are affected | Incidents | Mitigate first, diagnose afterward |
| 4 | Naming commands without explaining behavior | Linux | Explain what the system does, then the command |
| 5 | Designing only the working path | Design | For each component, state what happens when it fails |
| 6 | Giving no numbers | Design | State a target, a peak load, and an instance count |
| 7 | Ignoring rollout and rollback | Design | Describe the staged release and how to reverse it |
| 8 | Writing code that handles only clean input | Coding | Handle empty lines, missing files, and timeouts |
| 9 | Listing tools as experience | Tool depth | Describe a failure you solved with the tool |
| 10 | Assigning fault to a person | Behavioral | Describe the system condition that allowed the error |

## Three mistakes in detail

### Guessing a cause immediately

The interviewer says that the website is down. The weak answer begins with "It is probably the database." The interviewer then reveals that the database is healthy, and the candidate has no next step.

The strong answer begins with questions. "Is it down for all users or some? Since when? What do we see: a timeout, an error page, or a DNS failure?" Each answer removes part of the system from suspicion. See the method on the [troubleshooting](../rounds/troubleshooting.md) page.

### Seeking the root cause while users are affected

A candidate describes an incident in which checkout failed for 40 minutes. For 30 of those minutes, the team read logs to understand a release that could have been rolled back in 5. The interviewer hears that the candidate values understanding over users.

The correction is a rule: when a mitigation exists, use it, and preserve the evidence for later. Save the logs and note the failing version before rolling back.

### Designing only the working path

A candidate draws a load balancer, three application servers, and a database, and stops. The interviewer asks what happens when the database fails, and the candidate has not considered it.

The correction is to review the diagram before the interviewer does. Point to each component and state its failure mode, how the failure is detected, and what the user sees. See [SRE system design](../rounds/sre-system-design.md).

## Communication mistakes across all rounds

- **Silence while thinking.** The interviewer cannot grade reasoning that is not spoken. Say what you are considering.
- **No stated assumptions.** An unstated assumption looks like an error when it differs from the interviewer's.
- **Pretending to know.** "I have not used that tool, but here is how I would approach the problem" earns more than a wrong answer delivered with confidence.
- **Answers without an end.** State the conclusion, give the reasons, and stop. The interviewer will ask for more.
- **Ignoring hints.** A hint is information about where the interviewer wants to go. Follow it.

## A self-check after each practice answer

1. Did I state what I was checking and why, before each step?
2. Did I ask what changed?
3. Did I propose a mitigation as early as one existed?
4. Did I give at least one number?
5. Did I describe how the failure would be detected and prevented next time?
6. Did I say "I" for the actions that I took?

Record practice sessions and review them against this list. Most candidates find that they skip the same two items every time.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-common-mistakes) places a mid-level answer beside a senior answer for each question, which makes these differences visible.
- [Grokking Modern Behavioral Interview](https://www.designgurus.io/course/grokking-behavioral-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-common-mistakes) addresses the communication mistakes in depth.
