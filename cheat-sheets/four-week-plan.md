# Four-Week Preparation Plan

This plan prepares a working engineer for a DevOps or SRE loop in four weeks at about eight hours a week. It assumes production experience and little recent interview practice. Each week has a finish condition, so progress can be checked instead of assumed.

## Before week 1

Ask the recruiter which rounds are in the loop, using the questions on the [interview loop](../rounds/interview-loop.md) page. Then adjust the hours below. An SRE loop needs more coding time. A DevOps loop needs more time on tools.

## The four weeks

| Week | Focus | Hours |
|---|---|---|
| 1 | Linux, networking, and the troubleshooting method | 8 |
| 2 | Coding and scripting, plus tools | 8 |
| 3 | Reliability concepts and design | 8 |
| 4 | Incidents, behavioral stories, and full practice | 8 |

### Week 1: systems and troubleshooting

| Task | Hours |
|---|---|
| Read [Linux and networking](../rounds/linux-and-networking.md) and explain each topic aloud | 3 |
| Run every command in the [command table](linux-commands-for-troubleshooting.md) on a real machine | 2 |
| Learn the five-step method in [troubleshooting](../rounds/troubleshooting.md) | 1 |
| Practice 4 spoken troubleshooting drills with a partner or a recorder | 2 |

**Finish condition:** you can explain what happens after typing a web address in 4 minutes, with one level of extra depth at each stage.

### Week 2: coding and tools

| Task | Hours |
|---|---|
| Write 6 practical scripts from an empty file, such as a log parser and a host checker | 3 |
| Solve 10 easy or medium algorithm problems, timed | 3 |
| Read [containers and Kubernetes](../concepts/containers-and-kubernetes.md) and [infrastructure as code](../concepts/infrastructure-as-code.md) | 2 |

**Finish condition:** you can write a working log parser with error handling in 20 minutes while explaining it.

### Week 3: reliability and design

| Task | Hours |
|---|---|
| Read [SLIs, SLOs, and error budgets](../concepts/slis-slos-and-error-budgets.md) and repeat the calculation with your own numbers | 1.5 |
| Read [observability](../concepts/observability.md) and [deployment strategies](../concepts/ci-cd-and-deployment-strategies.md) | 1.5 |
| Read [SRE system design](../rounds/sre-system-design.md) and [capacity planning](../concepts/capacity-planning.md) | 2 |
| Practice 3 designs aloud, 45 minutes each, following the seven steps | 3 |

**Finish condition:** for any design, you can state the target, the failure domains, an instance count with arithmetic, and the rollout plan.

### Week 4: incidents, stories, and full practice

| Task | Hours |
|---|---|
| Read [incident response](../rounds/incident-response.md) and [postmortems](../concepts/postmortems.md) | 1.5 |
| Write 6 stories in the STAR structure from [behavioral](../rounds/behavioral.md), each with a number | 2.5 |
| Complete 2 full practice interviews of 2 rounds each | 3 |
| Review recordings against the self-check in [common mistakes](common-mistakes.md) | 1 |

**Finish condition:** you can tell your main incident story in 3 minutes with the timeline, the impact, your decision, and the lasting change.

## If the time is shorter

| Time available | What to keep |
|---|---|
| Two weeks | Weeks 1 and 3, plus 3 stories and 1 practice interview |
| One week | The troubleshooting method, error budgets, 1 design, and 3 stories |
| Two days | The [question bank](question-bank.md), [availability numbers](availability-numbers.md), and your main incident story |

## Practice rules

- Speak every answer aloud. Reading silently does not prepare the explanation.
- Time every session. Rounds last 45 to 60 minutes, and pacing is a skill.
- Record at least two sessions and listen to them.
- After each session, write down one thing to change and practice only that next time.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-four-week-plan) supplies the drills, graded exercises, chapter assessments, and full practice interviews that this plan schedules.
- [Skill-building exercises for DevOps-oriented interviews](https://www.designgurus.io/answers/detail/skill-building-exercises-for-devops-oriented-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-four-week-plan) is a Design Gurus answer with more practice ideas.
- [Grokking the Coding Interview](https://www.designgurus.io/course/grokking-the-coding-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-four-week-plan) structures the algorithm practice in week 2.
