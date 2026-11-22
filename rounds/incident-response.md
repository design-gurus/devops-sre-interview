# The Incident Response Round

The incident response round tests whether a candidate can lead while production is failing. The interviewer either describes a live incident and asks what the candidate would do, or asks about a real incident from the candidate's past. In both forms, the order of actions matters more than technical depth.

## The order of work

| Order | Action | Reason |
|---|---|---|
| 1 | Declare the incident and assign roles | People act faster when ownership is clear |
| 2 | Assess the impact and set a severity | Severity decides who is called and how often updates go out |
| 3 | Mitigate | Restoring service comes before understanding the cause |
| 4 | Communicate at a fixed interval | Silence causes duplicate work and escalations |
| 5 | Find and fix the root cause | Done after users are no longer affected |
| 6 | Write the postmortem | The organization learns only if the review is written |

Mitigation means reducing harm without yet knowing the cause. Rolling back a release, shifting traffic away from a zone, and turning off a feature are mitigations.

## Roles in an incident

| Role | Responsibility |
|---|---|
| Incident commander | Makes decisions, assigns work, and does not debug |
| Operations lead | Investigates and changes the system |
| Communications lead | Writes updates for customers and for other teams |
| Scribe | Records the timeline as events happen |

In a small incident, one person may hold several roles. Naming the roles still helps, because it makes clear who decides.

## Severity levels

Companies define their own levels. A common shape has three or four.

| Level | Typical meaning | Typical response |
|---|---|---|
| Severity 1 | Most users cannot use a core function | Page immediately, updates every 15 to 30 minutes |
| Severity 2 | A core function is degraded, or one group is blocked | Page during any hour, updates every hour |
| Severity 3 | A minor function fails, and a workaround exists | Handle during working hours |

## A worked answer

The interviewer says: "You are on call. Alerts show that 30 percent of checkout requests are failing. What do you do?"

A strong answer follows the order above. "I acknowledge the page and open an incident channel. Checkout is a core function and 30 percent of requests fail, so I declare a severity 1 and take the incident commander role until someone else can. I ask one engineer to check what changed in the last hour. If a deployment went out, we roll it back first, because that takes about 5 minutes and needs no diagnosis. I post an update every 15 minutes with the impact, the current action, and the time of the next update. After the error rate returns to normal, I keep the incident open for 30 minutes to confirm it holds. Then we schedule the postmortem."

## What separates the levels

| Mid-level answer | Senior answer |
|---|---|
| Starts debugging immediately | Declares, assigns roles, then mitigates |
| Seeks the root cause first | Restores service first |
| Communicates when asked | Sends updates on a fixed interval |
| Ends at the fix | Ends at prevention and a written review |

## Questions to expect

1. Describe the worst incident you handled. What was your role?
2. When do you escalate, and to whom?
3. Two mitigations are possible, and each carries risk. How do you choose?
4. How do you hand over an incident at the end of a shift?
5. How do you decide that an incident is over?

Prepare one real incident in detail: the timeline in minutes, the impact as a number, the decision you made, and what changed afterward.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-incident-response) has a chapter on incident response and postmortems, with full answers at two levels.
- Lesson: [Severity and the First Ten Minutes](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/severity-and-the-first-ten-minutes?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-incident-response), in Grokking DevOps and SRE Interviews
- Lesson: [Mitigate Before You Diagnose](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/mitigate-before-you-diagnose?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-incident-response), in Grokking DevOps and SRE Interviews
- Lesson: [Communicating During an Incident](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/communicating-during-an-incident?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-incident-response), in Grokking DevOps and SRE Interviews
- [Postmortems](../concepts/postmortems.md) covers step 6.
- [SLIs, SLOs, and error budgets](../concepts/slis-slos-and-error-budgets.md) explains how impact is measured.
