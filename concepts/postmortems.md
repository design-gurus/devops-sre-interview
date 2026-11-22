# Postmortems

A postmortem is a written review of an incident: what happened, why, what it cost, and what will change. A blameless postmortem examines the system and the decisions that the system allowed. It does not assign fault to a person. The purpose is to make the same failure less likely, and people share the facts only when they are not punished for doing so.

## Why blameless

| Blame-based review | Blameless review |
|---|---|
| Asks "who caused this?" | Asks "what made this action possible and reasonable?" |
| People hide details | People report details early |
| The fix is "be more careful" | The fix is a change to a tool, a check, or a process |
| The same failure returns with a different person | The failure becomes harder for anyone to repeat |

Blameless does not mean without accountability. Each action item still has a named owner and a date.

## What a postmortem contains

| Section | Content |
|---|---|
| Summary | Three sentences: what failed, for how long, and the user impact |
| Impact | Numbers: failed requests, affected users, error budget consumed |
| Timeline | Timestamped events from the first signal to full recovery |
| Root causes and contributing factors | Why the failure happened and why it was not caught earlier |
| What went well | Detection, tooling, or decisions that reduced harm |
| What went poorly | Delays, missing alerts, confusing runbooks |
| Action items | Each with an owner, a priority, and a due date |

A runbook is a written procedure for a known operational task.

## Four time measurements

| Measure | From | To |
|---|---|---|
| Time to detect | Start of the failure | First alert or report |
| Time to acknowledge | First alert | A person responding |
| Time to mitigate | Start of the failure | Users no longer affected |
| Time to resolve | Start of the failure | Root cause fixed |

The longest of the first three shows where to invest. A 20-minute detection time points to alerting. A long mitigation time points to rollback tooling.

## Worked example

A release at 14:02 added a database query with no index. Checkout latency rose from 400 milliseconds to 1,600 milliseconds. The on-call engineer was paged at 14:08, rolled back at 14:10, and latency recovered at 14:14.

| Item | Value |
|---|---|
| Time to detect | 6 minutes |
| Time to mitigate | 12 minutes |
| Impact | About 600 checkouts missed the 1 second target |
| Root cause | A query scanned a full table |
| Contributing factor | The canary compared error rate only, so a slow release passed |

The weak action item is "review queries more carefully." The strong action items change the system.

1. The canary fails when 95th percentile latency is more than 20 percent above the current version.
2. The pipeline runs new queries against a copy of production data and reports any full table scan.
3. A latency alert pages after 2 minutes, not 6.

## Asking why more than once

The Five Whys technique asks "why" repeatedly until the answer is a condition in the system. Its weakness is that it follows one chain. Most incidents have several contributing factors, so list each one and ask what would have stopped the failure at that point.

## Questions to expect

1. Walk me through a postmortem you wrote.
2. An engineer ran the wrong command in production. How do you write that up?
3. How do you make sure action items are completed?
4. Which incidents deserve a postmortem?
5. What is wrong with "human error" as a root cause?

For question 5, a person's error is where the investigation begins. The useful finding is why the system allowed the error to reach production.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-postmortems) has a chapter on incident response and postmortems with full written examples.
- Lesson: [Writing a Blameless Postmortem](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/writing-a-blameless-postmortem?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-postmortems), in Grokking DevOps and SRE Interviews
- Lesson: [Lessons From Public Outages](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/lessons-from-public-outages?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-postmortems), in Grokking DevOps and SRE Interviews
- [Incident response](../rounds/incident-response.md) covers the steps before the review.
- [Behavioral](../rounds/behavioral.md) shows how to tell an incident as an interview story.
