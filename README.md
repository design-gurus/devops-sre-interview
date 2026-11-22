# DevOps and SRE Interview

> The free, open companion to **Grokking DevOps and SRE Interviews** by [DesignGurus.io](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme), created by Arslan Ahmad.

[![GitHub stars](https://img.shields.io/github/stars/design-gurus/devops-sre-interview?style=social)](https://github.com/design-gurus/devops-sre-interview/stargazers)
[![Last commit](https://img.shields.io/github/last-commit/design-gurus/devops-sre-interview)](https://github.com/design-gurus/devops-sre-interview/commits/main)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](LICENSE)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A DevOps or site reliability engineering (SRE) interview tests how a candidate behaves when a production system fails. A software engineering interview asks the candidate to build something. This one asks the candidate to find a fault, limit the harm, and prevent the next one. Most public material for these interviews is a list of several thousand questions with one-line answers. That format trains recall, and the rounds reward reasoning.

This repository takes the opposite approach. It explains each round, the method behind a strong answer, and the small set of concepts that interviewers return to. Every page is short. For worked drills, graded exercises, and full practice interviews, see the course.

## Start here

| Your situation | Read first |
|---|---|
| The interview is scheduled and the rounds are unknown | [The interview loop](rounds/interview-loop.md) |
| The troubleshooting round is the main concern | [Troubleshooting](rounds/troubleshooting.md), then [Linux commands](cheat-sheets/linux-commands-for-troubleshooting.md) |
| The background is software engineering, and SRE is new | [DevOps vs SRE](cheat-sheets/devops-vs-sre.md), then [SLIs, SLOs, and error budgets](concepts/slis-slos-and-error-budgets.md) |
| The design round is the main concern | [SRE system design](rounds/sre-system-design.md), then [Capacity planning](concepts/capacity-planning.md) |
| Four weeks are available | [The four-week plan](cheat-sheets/four-week-plan.md) |

## The loop at a glance

The rounds below are commonly reported by candidates. No company publishes a standard loop, and the mix changes by team and level.

| Round | What it measures | Guide |
|---|---|---|
| Recruiter or manager screen | Fit, background, and incidents handled | [Interview loop](rounds/interview-loop.md) |
| Coding and scripting | Automation with Python or Bash | [Coding and scripting](rounds/coding-and-scripting.md) |
| Linux and networking | How the operating system and the network behave | [Linux and networking](rounds/linux-and-networking.md) |
| Troubleshooting | A method for finding a fault under time pressure | [Troubleshooting](rounds/troubleshooting.md) |
| System or infrastructure design | Reliability, failure domains, capacity, rollout | [SRE system design](rounds/sre-system-design.md) |
| Incident and reliability practice | Running an incident and learning from it | [Incident response](rounds/incident-response.md) |
| Behavioral and project review | Judgment, ownership, communication | [Behavioral](rounds/behavioral.md) |

## Every page

### Rounds

| Page | What it covers |
|---|---|
| [Interview loop](rounds/interview-loop.md) | The round types, how a loop is assembled, and what to ask the recruiter |
| [Troubleshooting](rounds/troubleshooting.md) | A five-step method and a worked example on a slow web service |
| [Linux and networking](rounds/linux-and-networking.md) | The topics that recur, and how to explain behavior instead of commands |
| [SRE system design](rounds/sre-system-design.md) | How this round differs from a product design round |
| [Coding and scripting](rounds/coding-and-scripting.md) | Typical tasks, with a log parsing example |
| [Incident response](rounds/incident-response.md) | Roles, severity, mitigation before diagnosis, and communication |
| [Behavioral](rounds/behavioral.md) | The story types that operations interviewers ask for |

### Concepts

| Page | What it covers |
|---|---|
| [SLIs, SLOs, and error budgets](concepts/slis-slos-and-error-budgets.md) | Definitions and a worked error budget calculation |
| [Observability](concepts/observability.md) | Metrics, logs, traces, and the four golden signals |
| [CI/CD and deployment strategies](concepts/ci-cd-and-deployment-strategies.md) | Rolling, blue-green, and canary releases compared |
| [Containers and Kubernetes](concepts/containers-and-kubernetes.md) | The objects and failure states that interviews ask about |
| [Infrastructure as code](concepts/infrastructure-as-code.md) | State, drift, plans, and safe changes |
| [Postmortems](concepts/postmortems.md) | The blameless review and what a good one contains |
| [Capacity planning](concepts/capacity-planning.md) | From peak traffic to an instance count, with arithmetic |
| [Toil and automation](concepts/toil-and-automation.md) | What toil is and when automating it pays back |

### Cheat sheets

| Page | What it covers |
|---|---|
| [Question bank](cheat-sheets/question-bank.md) | About 60 questions grouped by round, each with a pointer |
| [Linux commands for troubleshooting](cheat-sheets/linux-commands-for-troubleshooting.md) | Each command and the question it answers |
| [DevOps vs SRE](cheat-sheets/devops-vs-sre.md) | The two roles and their interviews side by side |
| [Availability numbers](cheat-sheets/availability-numbers.md) | Allowed downtime from 99 to 99.999 percent |
| [Common mistakes](cheat-sheets/common-mistakes.md) | Ten errors that cost candidates the round |
| [Four-week plan](cheat-sheets/four-week-plan.md) | A week-by-week preparation schedule |

## FAQ

### What is asked in an SRE interview?

An SRE loop commonly includes coding, Linux and networking, troubleshooting, a system design round focused on reliability, and a behavioral round. The [interview loop](rounds/interview-loop.md) page describes each one.

### What is the difference between a DevOps interview and an SRE interview?

Candidate reports suggest that DevOps loops ask more about daily tools such as Kubernetes, Terraform, and build pipelines. SRE loops ask more about coding, operating system internals, and reliability targets. The [comparison page](cheat-sheets/devops-vs-sre.md) lists the differences.

### Is there coding in a DevOps interview?

In most reported loops, yes. The tasks are usually practical, such as parsing a log file or writing a small tool. See [coding and scripting](rounds/coding-and-scripting.md) and the Design Gurus answer on [whether coding is asked in a DevOps interview](https://www.designgurus.io/answers/detail/is-coding-asked-in-devops-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme).

### What is a troubleshooting interview?

The interviewer describes a failure, and the candidate investigates it one step at a time. The interviewer supplies the result of each check. The grade depends on the method, not on guessing the cause. See [troubleshooting](rounds/troubleshooting.md).

### What is asked in an SRE system design interview?

The candidate designs a system and is then asked how it fails, how it is rolled out, and how it is measured. Typical questions include a metrics pipeline, a deployment platform, and a service that runs in several regions. See [SRE system design](rounds/sre-system-design.md).

### How long does it take to prepare?

A working engineer with production experience usually needs about four weeks at eight hours a week. The [four-week plan](cheat-sheets/four-week-plan.md) divides that time by round.

## Course lessons to start with

- [How DevOps and SRE Interview Loops Test the Job](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/how-devops-interview-loops-test-the-job?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): what each round measures, in Grokking DevOps and SRE Interviews
- [A Method for Troubleshooting](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/a-method-for-troubleshooting?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): the steps for finding a fault in a live system, in Grokking DevOps and SRE Interviews
- [Drill: The Website Is Down](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/drill-the-website-is-down?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): a full troubleshooting answer from the first check to the cause, in Grokking DevOps and SRE Interviews
- [What Happens When You Type a URL](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/what-happens-when-you-type-a-url?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): DNS, TCP, TLS, and HTTP in one request, in Grokking DevOps and SRE Interviews
- [Kubernetes Core Objects](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/kubernetes-core-objects?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): pods, deployments, and services and how they relate, in Grokking DevOps and SRE Interviews
- [Rolling, Blue Green, and Canary Releases](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/rolling-blue-green-and-canary-releases?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): how the three release methods differ and when to use each, in Grokking DevOps and SRE Interviews
- [SLIs, SLOs, and Error Budgets](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/slis-slos-and-error-budgets?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): how a reliability target becomes a budget, in Grokking DevOps and SRE Interviews
- [Mitigate Before You Diagnose](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/mitigate-before-you-diagnose?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): why an incident answer restores service first, in Grokking DevOps and SRE Interviews
- [A Method for Infrastructure Design](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/a-method-for-infrastructure-design?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): the steps for the SRE design round, in Grokking DevOps and SRE Interviews
- [Reading Load Average and CPU Usage](https://www.designgurus.io/course-play/grokking-operating-systems-and-networking-for-backend-engineers/doc/reading-load-average-and-cpu-usage?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): what the load numbers on a Linux server count, in Operating Systems and Networking for Backend Engineers

## Free reading on DesignGurus.io

- Free article: [DevOps vs SRE vs platform engineer interviews](https://www.designgurus.io/blog/devops-vs-sre-vs-platform-engineer-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): what each of the three interviews tests.
- Free article: [The DevOps system design interview](https://www.designgurus.io/blog/devops-system-design-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): how infrastructure design rounds work.
- Free article: [What to expect in a production engineering interview](https://www.designgurus.io/blog/what-to-expect-in-a-production-engineering-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): the loop for a closely related role.
- Free article: [An interview strategy for site reliability engineering](https://www.designgurus.io/blog/site-reliability-engineering-crafting-an-sre-centric-interview-strategy?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): a preparation approach built around SRE topics.
- Free article: [OpenTelemetry and modern observability](https://www.designgurus.io/blog/guide-to-modern-observability?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): a beginner guide to metrics, logs, and traces.
- Free article: [The Kubernetes guide for system design](https://www.designgurus.io/blog/kubernetes-ultimate-guide?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): the cluster components and how they work together.
- Free article: [High availability in system design](https://www.designgurus.io/blog/high-availability-system-design-basics?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): 15 strategies for keeping a system available.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): the full course, with troubleshooting drills, mid-level and senior answers side by side, graded Python exercises, and full practice interviews.
- [Grokking the System Design Interview](https://www.designgurus.io/course/grokking-the-system-design-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): the design method that the SRE design round builds on.
- [Grokking System Design Fundamentals](https://www.designgurus.io/course/grokking-system-design-fundamentals?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=readme): load balancers, caches, queues, and replication from the beginning.

Related free repositories: [Grokking System Design](https://github.com/design-gurus/grokking-system-design) and [System Design Numbers](https://github.com/design-gurus/system-design-numbers).

For the system design round, see [Grokking System Design](https://github.com/design-gurus/grokking-system-design), the free companion guide with 30 patterns, 59 question walkthroughs, and 35 cheat sheets.

## More free guides

Every guide below is free, follows the same short-page format, and comes from DesignGurus.io.

- **Core guides:** [Grokking System Design](https://github.com/design-gurus/grokking-system-design), [Grokking Coding Interview](https://github.com/design-gurus/grokking-coding-interview), [Grokking AI System Design](https://github.com/design-gurus/grokking-ai-system-design), [Design Patterns](https://github.com/design-gurus/design-patterns), [Best System Design Resources](https://github.com/design-gurus/best-system-design-resources), [Best System Design Courses](https://github.com/design-gurus/best-system-design-courses)
- **By interview round:** [System Design Numbers](https://github.com/design-gurus/system-design-numbers), [API Design Interview](https://github.com/design-gurus/api-design-interview), [Frontend System Design Interview](https://github.com/design-gurus/frontend-system-design-interview), [Mobile System Design Interview](https://github.com/design-gurus/mobile-system-design-interview), [Microservices Interview Questions](https://github.com/design-gurus/microservices-interview-questions), [Concurrency Interview](https://github.com/design-gurus/concurrency-interview)
- **By role:** [Data Engineering Interview](https://github.com/design-gurus/data-engineering-interview), [Forward Deployed Engineer Interview](https://github.com/design-gurus/forward-deployed-engineer-interview), [Solutions Architect Interview](https://github.com/design-gurus/solutions-architect-interview)
- **Seniority and behavioral:** [Staff Engineer Interview](https://github.com/design-gurus/staff-engineer-interview), [Engineering Manager Interview](https://github.com/design-gurus/engineering-manager-interview), [Amazon Leadership Principles](https://github.com/design-gurus/amazon-leadership-principles), [Software Engineer Levels](https://github.com/design-gurus/software-engineer-levels)
- **By company:** [Google Interview Guide](https://github.com/design-gurus/google-interview-guide), [Meta Interview Guide](https://github.com/design-gurus/meta-interview-guide), [Amazon Interview Guide](https://github.com/design-gurus/amazon-interview-guide), [Microsoft Interview Guide](https://github.com/design-gurus/microsoft-interview-guide), [Apple Interview Guide](https://github.com/design-gurus/apple-interview-guide), [Netflix Interview Guide](https://github.com/design-gurus/netflix-interview-guide), [OpenAI Interview Guide](https://github.com/design-gurus/openai-interview-guide), [Anthropic Interview Guide](https://github.com/design-gurus/anthropic-interview-guide)

## Contributing

Corrections and additions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) first.

## License

The content is licensed under [CC BY 4.0](LICENSE). See [NOTICE.md](NOTICE.md) for what the license covers and how to attribute.
