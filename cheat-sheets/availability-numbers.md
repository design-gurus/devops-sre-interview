# Availability Numbers

Availability is the share of time, or the share of requests, in which a service works. It is written as a percentage, and each added nine reduces the allowed downtime by a factor of ten. Memorize the 99.9 and 99.99 rows, because interviewers ask for them most often.

## Allowed downtime

The table uses a 365-day year and a 30-day month.

| Availability | Common name | Per year | Per 30-day month | Per day |
|---|---|---|---|---|
| 99 percent | Two nines | 3.65 days | 7.2 hours | 14.4 minutes |
| 99.5 percent | | 1.83 days | 3.6 hours | 7.2 minutes |
| 99.9 percent | Three nines | 8.76 hours | 43.2 minutes | 1.44 minutes |
| 99.95 percent | | 4.38 hours | 21.6 minutes | 43.2 seconds |
| 99.99 percent | Four nines | 52.6 minutes | 4.32 minutes | 8.64 seconds |
| 99.999 percent | Five nines | 5.26 minutes | 25.9 seconds | 0.86 seconds |

## The formula

Allowed downtime equals the length of the window multiplied by 1 minus the availability.

For 99.9 percent over 30 days: 30 x 24 x 60 minutes is 43,200 minutes. Multiply by 0.001 to get 43.2 minutes.

A fast mental method: one year is about 525,600 minutes. Three nines allow one thousandth of that, about 526 minutes, which is 8.76 hours. Each further nine divides by ten.

## Requests instead of time

Many teams measure availability by requests, because an outage at 03:00 harms fewer users than one at noon.

| Requests in the window | Target | Allowed failures |
|---|---|---|
| 1,000,000 | 99.9 percent | 1,000 |
| 43,200,000 | 99.9 percent | 43,200 |
| 43,200,000 | 99.99 percent | 4,320 |

## Dependencies in series

When a request needs every component in a chain, multiply the availabilities.

| Chain | Calculation | Result |
|---|---|---|
| Two services at 99.9 percent | 0.999 x 0.999 | 99.8 percent |
| Three services at 99.9 percent | 0.999 x 0.999 x 0.999 | 99.7 percent |
| Ten services at 99.99 percent | 0.9999 multiplied 10 times | 99.9 percent |

A service cannot be more available than the product of the things it must call. This is why designs reduce hard dependencies with caches, defaults, and queues.

## Redundancy in parallel

When any one of several copies can serve the request, multiply the failure probabilities.

| Setup | Calculation | Result |
|---|---|---|
| Two copies at 99 percent | 1 - (0.01 x 0.01) | 99.99 percent |
| Three copies at 99 percent | 1 - (0.01 x 0.01 x 0.01) | 99.9999 percent |
| Two copies at 99.9 percent | 1 - (0.001 x 0.001) | 99.9999 percent |

These results assume that the copies fail independently. In practice they share a deployment system, a configuration, and often a bug, so real availability is lower. State that assumption in an interview.

## What each level demands

| Target | What a team needs in practice |
|---|---|
| 99 percent | Basic monitoring and manual recovery |
| 99.9 percent | On-call, tested rollback, redundancy across zones |
| 99.99 percent | Automatic failover, staged releases, no manual step in recovery |
| 99.999 percent | Several regions, automatic everything, strict change control |

At 99.99 percent, the monthly allowance is 4.32 minutes. A person who is paged needs longer than that to open a laptop, so recovery must be automatic.

## Questions to expect

1. How much downtime does 99.95 percent allow in a month?
2. A service calls four dependencies at 99.9 percent each. What can it promise?
3. Why is five nines so much harder than four?
4. Should availability be measured in time or in requests?
5. Planned maintenance takes 2 hours a month. Which targets does that rule out?

For question 5, 2 hours is 120 minutes. That exceeds the 43.2 minutes that 99.9 percent allows, so the target cannot be met unless maintenance happens without downtime.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=cheat-sheets-availability-numbers) uses these numbers in its chapters on SLOs and infrastructure design.
- [SLIs, SLOs, and error budgets](../concepts/slis-slos-and-error-budgets.md) shows how a target becomes a budget.
- [System Design Numbers](https://github.com/design-gurus/system-design-numbers) is a free reference for latency, storage, and traffic estimates.
