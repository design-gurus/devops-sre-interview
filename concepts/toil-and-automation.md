# Toil and Automation

Toil is operational work that is manual, repetitive, and automatable, and that grows as the service grows. Google's book *Site Reliability Engineering* gave the term this meaning. Restarting a stuck job by hand every morning is toil. Designing a fix so that the job never sticks is engineering.

## How to recognize toil

Work is toil when most of these properties apply.

| Property | Question to ask |
|---|---|
| Manual | Does a person have to run it? |
| Repetitive | Has it been done more than twice? |
| Automatable | Could a program do it with no human judgment? |
| Reactive | Is it triggered by an alert or a request, not by a plan? |
| No lasting value | Is the service the same afterward as before? |
| Scales with the service | Does the work double when the service doubles? |

Not all operational work is toil. Planning, writing a postmortem, and a meeting are overhead, not toil. The same book suggests that an SRE team keep toil below 50 percent of its time, so the rest goes to engineering.

## Why it matters in an interview

Toil questions test whether a candidate treats operations as an engineering problem. A team that only does toil cannot improve its systems, and its work grows with every new customer. Interviewers ask for a story in which the candidate measured manual work and then removed it.

## When automation pays back

Automation has a cost: the time to build it, test it, and maintain it. Compare that cost with the time it saves.

| Step | Example |
|---|---|
| Time per manual run | 20 minutes |
| Runs per week | 15 |
| Manual cost per week | 20 x 15 = 300 minutes, which is 5 hours |
| Cost to automate | 40 hours |
| Time to recover the cost | 40 / 5 = 8 weeks |
| Saving in the first year | 5 x 52 - 40 = 220 hours |

Eight weeks is a clear case. A task that takes 10 minutes twice a year does not justify 40 hours of work, unless an error in it would cause an outage.

Time saved is one benefit. Automation also removes mistakes from tired people, makes the task auditable, and lets any team member run it.

## Levels of automation

| Level | Description | Example |
|---|---|---|
| 0 | No documentation | One person knows how to fail over the database |
| 1 | A written runbook | The steps are in a shared document |
| 2 | A script run by a person | One command performs the failover |
| 3 | A script run by the system, with a person approving | An alert proposes the failover |
| 4 | Fully automatic | The system fails over and reports afterward |

Moving one level at a time is safer than jumping to level 4. A script that a person runs for a month reveals the cases that the author missed.

## Risks of automation

- An automated action repeats a mistake across every server in seconds. Add limits, such as "never act on more than 10 percent of hosts at once."
- Automation hides knowledge. When it fails, nobody remembers the manual steps. Keep the runbook current.
- Automating a bad process makes it a fast bad process. Ask first whether the task can be removed entirely.

## Questions to expect

1. Describe manual work that you removed. How did you measure the benefit?
2. How do you decide what to automate first?
3. An automation caused an outage. What safeguards would you add?
4. Your team spends 70 percent of its time on tickets. What do you do?
5. When is it correct to leave a task manual?

For question 2, rank tasks by hours per month and by the harm of an error, then start at the top.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-toil-and-automation) has a lesson on toil and automation decisions, plus lessons on production readiness, game days, and on-call health.
- Lesson: [Toil and Automation Decisions](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/toil-and-automation-decisions?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-toil-and-automation), in Grokking DevOps and SRE Interviews
- [Behavioral](../rounds/behavioral.md) shows how to present an automation story.
