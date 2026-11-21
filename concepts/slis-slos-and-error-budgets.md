# SLIs, SLOs, and Error Budgets

A service level indicator (SLI) is a measurement of how well a service behaves. A service level objective (SLO) is the target for that measurement. An error budget is the amount of failure that the target still allows. Together they turn the question "is the service reliable enough?" into arithmetic.

## The three terms, and one more

| Term | Definition | Example |
|---|---|---|
| SLI | A measured ratio of good events to all events | The share of checkout requests that succeed within 1 second |
| SLO | A target for the SLI over a time window | 99.9 percent over 30 days |
| Error budget | 100 percent minus the SLO, applied to the window | 0.1 percent of requests may fail |
| SLA | A service level agreement: a contract with a penalty | A refund when monthly availability falls below 99.5 percent |

The SLO is an internal target and is set stricter than the SLA. The space between them gives the team time to react before a contract is broken.

## Choosing a good indicator

A useful SLI measures what the user experiences. CPU usage is not an SLI, because a user does not see it.

| Service type | Common indicators |
|---|---|
| Request and response | Availability (successful requests), latency (requests faster than a threshold) |
| Data pipeline | Freshness (age of the newest data), correctness |
| Storage | Durability (data that can still be read) |

Measure as close to the user as possible. A load balancer log records requests that never reached the application, and application metrics do not.

## Worked example: an error budget

A checkout service receives 1,440,000 requests a day, which is 1,000 a minute. Its SLO is 99.9 percent success over 30 days.

| Step | Calculation | Result |
|---|---|---|
| Requests in the window | 1,440,000 x 30 | 43,200,000 |
| Error budget | 43,200,000 x 0.001 | 43,200 failed requests |
| The same budget as time | 30 days x 0.001 | 43.2 minutes of full outage |

An incident then causes 40 percent of requests to fail for 25 minutes.

| Step | Calculation | Result |
|---|---|---|
| Failed requests | 25 x 1,000 x 0.40 | 10,000 |
| Share of budget used | 10,000 / 43,200 | About 23 percent |
| Budget remaining | 43,200 - 10,000 | 33,200 requests |

One incident consumed almost a quarter of the month. Three more of the same size would leave about 3,200 requests, and a fifth would break the objective.

## What the budget is for

The budget is a decision tool shared by engineering and product teams.

- **Budget remains:** the team releases at its normal pace and can take risks, such as a migration.
- **Budget is nearly spent:** the team slows releases and gives priority to reliability work.
- **Budget is never touched:** the objective may be stricter than users need, and the team may be releasing too cautiously.

## Burn rate alerts

Burn rate is how fast the budget is being consumed, relative to a rate that would spend it exactly by the end of the window. A burn rate of 1 uses the whole budget in 30 days. A burn rate of 14.4 uses 2 percent of a 30-day budget in 1 hour, which is why that value is a common threshold for an urgent page. Alerting on burn rate pages people for events that threaten the objective and stays quiet for brief errors.

## Questions to expect

1. Why not set the objective to 100 percent?
2. Who decides the SLO, and what happens when the budget is spent?
3. How would you choose an SLI for a batch pipeline?
4. Availability is 99.95 percent, but users complain. What is wrong with the indicator?
5. A service depends on three others, each at 99.9 percent. What can it promise?

For question 5, serial dependencies multiply: 0.999 x 0.999 x 0.999 is about 0.997, so the service cannot promise more than about 99.7 percent without redundancy.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-slis-slos-and-error-budgets) has a chapter on observability and SLOs, including alert design from an error budget.
- [Availability numbers](../cheat-sheets/availability-numbers.md) lists allowed downtime for each target.
- [Observability](observability.md) covers how indicators are collected.
- Free answer: [What an error budget policy is](https://www.designgurus.io/answers/detail/what-is-an-error-budget-policy?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-slis-slos-and-error-budgets), which explains what a team does when the budget is spent.
