# DevOps vs SRE

DevOps is a way of working in which the people who build software and the people who run it share responsibility for delivery. Site reliability engineering (SRE) is a specific practice that applies software engineering to operations, with reliability as a measured target. The two overlap heavily, and job titles do not follow the definitions closely. Read the job description, not the title.

## The roles side by side

| Aspect | DevOps engineer | Site reliability engineer |
|---|---|---|
| Main goal | Fast, safe delivery of changes | A reliability target met at sustainable cost |
| Central artifact | The delivery pipeline | The service level objective and its error budget |
| Typical daily work | Pipelines, infrastructure code, tooling for teams | On-call, capacity, automation, reliability reviews |
| Measure of success | Deployment frequency, lead time, failure rate | Objectives met, incidents, toil reduced |
| Relationship to developers | Often embedded with, or serving, product teams | Often a separate team with rules for taking on a service |
| Coding expectation | Scripting and automation | Closer to a software engineer |

Two related titles also appear. A platform engineer builds the internal tools and systems that product teams use to deploy and run services. A production engineer is the name some companies give to a role that resembles SRE.

## The interviews side by side

These differences come from candidate reports and are tendencies, not rules.

| Round | DevOps loop | SRE loop |
|---|---|---|
| Coding | Practical scripts | Practical scripts, and often algorithm questions |
| Linux | Working knowledge and commands | Internals: processes, memory, the kernel |
| Tools | Central: Kubernetes, Terraform, a build system, a cloud provider | Present, but often secondary |
| Troubleshooting | Often framed around a pipeline or a cluster | Often framed around a host or a distributed service |
| Design | Design a pipeline or a platform | Design for reliability at large scale |
| Reliability practice | Monitoring and rollback | Objectives, error budgets, incident command |

## Which one are you interviewing for?

The job description usually reveals the loop. Count the mentions.

| The description emphasizes | The loop probably emphasizes |
|---|---|
| Named tools, such as Terraform, Jenkins, or Helm | Tool depth and practical tasks |
| "Software engineering", "distributed systems", "large scale" | Coding and system design |
| "On-call", "incident", "SLO" | Reliability practice and troubleshooting |
| "Developer experience", "internal platform" | Platform design |

Then confirm with the recruiter. The [interview loop](../rounds/interview-loop.md) page lists the questions to ask.

## Shared ground

About two thirds of the preparation is the same for both roles.

- A method for troubleshooting.
- Linux and networking fundamentals.
- Safe releases: canary, rollback, schema changes.
- Observability: metrics, logs, traces, and alerting on symptoms.
- Incident response and blameless postmortems.
- Behavioral stories about incidents, automation, and disagreement.

A candidate who prepares these well can adjust the remaining third after learning the rounds.

## Common questions about the difference

**Is SRE a senior form of DevOps?** No. They are different practices with different central measures. Both have junior and senior levels.

**Can a DevOps engineer move to SRE?** Yes, and it is a common move. The gap is usually coding depth and operating system internals.

**Which role writes more code?** SRE roles usually expect more. Some DevOps roles are also heavy in code, especially on platform teams.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-devops-vs-sre) opens with a lesson that compares DevOps, SRE, platform, and production engineers, then covers the rounds for all four.
- [Role-specific interview prep for SRE](https://www.designgurus.io/answers/detail/role-specific-interview-prep-for-sre-site-reliability-engineer?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-devops-vs-sre) is a Design Gurus answer on the SRE loop specifically.
