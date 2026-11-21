# The DevOps and SRE Interview Loop

An interview loop is the full sequence of interviews for one role, and each interview in it is a round. A DevOps or SRE loop commonly has one or two screens followed by four or five rounds on one day. Each round tests one part of the job on a small problem.

No company publishes a standard loop. Everything on this page comes from what candidates commonly report, and the mix changes by company, team, and level.

## The round types

| Round | Typical length | What happens |
|---|---|---|
| Recruiter or manager screen | 30 minutes | Background, motivation, and one or two incidents the candidate handled |
| Coding and scripting | 45 to 60 minutes | A practical program in Python or Bash, sometimes an easy to medium algorithm question |
| Linux and networking | 45 minutes | Processes, memory, file systems, DNS, TCP, and TLS |
| Troubleshooting | 45 to 60 minutes | The interviewer describes a failure, and the candidate investigates it |
| Tool depth | 45 minutes | Kubernetes, Terraform, a build pipeline, or one cloud provider |
| System or infrastructure design | 45 to 60 minutes | A design judged on reliability, capacity, and rollout |
| Incident and reliability practice | 45 minutes | Service level objectives, alerting, severity, and postmortems |
| Take-home task | 2 to 4 hours | A small project, such as a pipeline or infrastructure code, defended later |
| Behavioral and project review | 45 minutes | Past decisions, conflicts, failures, and one project in depth |

A single loop rarely includes all nine. A company selects the rounds that match its version of the job.

## How the title changes the loop

| Title | Rounds that candidates report most often |
|---|---|
| Site reliability engineer or production engineer | Coding, Linux internals, troubleshooting, system design |
| DevOps engineer | Tool depth, build pipelines, infrastructure as code, troubleshooting |
| Platform engineer | Design of internal platforms, Kubernetes, developer experience |

These are tendencies in a small sample, not rules. Two jobs with the same title can have different rounds.

## What changes with level

The same question is judged by a wider scope at each level. Take the question "Deployments sometimes break checkout. What would you do?"

| Level | A strong answer shows |
|---|---|
| Mid-level | Reverses the change, finds the cause, and adds a check |
| Senior | Also limits harm with a canary release, sets rollback rules, and leads the incident |
| Staff | Also changes the standard for many teams and agrees on acceptable risk with leaders |

A canary release sends a small share of traffic to a new version before the rest. The [deployment strategies](../concepts/ci-cd-and-deployment-strategies.md) page explains it.

## Questions to ask the recruiter

The recruiter can remove most of the uncertainty. Ask these when the interviews are scheduled.

1. Which round types are included, and how long is each one?
2. Does troubleshooting use a real system or a spoken discussion?
3. Which languages are allowed in the coding round?
4. Which tools or cloud provider should I expect?
5. Is the design round about a product system or about infrastructure?

## How to divide preparation time

| Round | Share of time for an SRE loop | Share for a DevOps loop |
|---|---|---|
| Coding and scripting | 25 percent | 15 percent |
| Linux, networking, and troubleshooting | 30 percent | 25 percent |
| Tools (Kubernetes, pipelines, infrastructure as code) | 10 percent | 30 percent |
| Design | 20 percent | 15 percent |
| Incidents and behavioral | 15 percent | 15 percent |

These shares are a starting point. Adjust them after the recruiter confirms the rounds. The [four-week plan](../cheat-sheets/four-week-plan.md) turns them into a schedule.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-interview-loop) maps each round to the job skill it tests and has a chapter for every round.
- [Role-specific interview prep for SRE](https://www.designgurus.io/answers/detail/role-specific-interview-prep-for-sre-site-reliability-engineer?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-interview-loop) is a longer Design Gurus answer on preparing for the SRE version of the loop.
- Free article: [What to expect in a production engineering interview](https://www.designgurus.io/blog/what-to-expect-in-a-production-engineering-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-interview-loop), which describes the loop for a closely related role.
- Free article: [An interview strategy for site reliability engineering](https://www.designgurus.io/blog/site-reliability-engineering-crafting-an-sre-centric-interview-strategy?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-interview-loop), a preparation approach built around SRE topics.
