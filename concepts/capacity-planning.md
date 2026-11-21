# Capacity Planning

Capacity planning is the work of deciding how much hardware a service needs to meet its targets at peak load, with enough spare to survive a failure. In an interview it turns a design into numbers: a peak request rate becomes an instance count, and the candidate explains each assumption.

## The inputs

| Input | Where it comes from |
|---|---|
| Peak load | Measured traffic, or an estimate from the number of users |
| Capacity of one instance | A load test at the target latency, not a guess |
| Target utilization | The share of capacity used at peak, commonly 50 to 70 percent |
| Redundancy | The largest failure the service must survive, such as one zone |
| Growth | The expected increase over the planning period |

A load test sends artificial traffic to a system and increases it until latency or errors exceed the target. The rate just before that point is the usable capacity of one instance.

## Worked example

A service has a peak of 3,000 requests per second. A load test shows that one instance handles 250 requests per second while latency stays within the target.

| Step | Calculation | Result |
|---|---|---|
| Planned load per instance at 60 percent utilization | 250 x 0.60 | 150 requests per second |
| Instances needed for peak | 3,000 / 150 | 20 |
| Instances per zone to survive the loss of 1 of 3 zones | 20 / 2 | 10 |
| Total across 3 zones | 10 x 3 | 30 |

The service must carry the full peak on two zones, so each zone holds half of the 20. That raises the total from 20 to 30, which is the cost of surviving a zone failure.

Now add growth of 10 percent a month for 6 months.

| Step | Calculation | Result |
|---|---|---|
| Growth factor | 1.10 multiplied by itself 6 times | About 1.77 |
| Peak in 6 months | 3,000 x 1.77 | About 5,315 requests per second |
| Instances needed for peak | 5,315 / 150 | 36 (rounded up) |
| Total across 3 zones | 18 x 3 | 54 |

## Why not run at 100 percent

| Reason | Effect |
|---|---|
| Latency rises sharply near full utilization | Queues form, and response time grows faster than load |
| Traffic has short peaks above the measured peak | A one-minute average hides ten-second spikes |
| Instances fail and deploys remove capacity | A rolling update takes some instances out of service |

## Autoscaling

Autoscaling adds and removes instances as load changes. It lowers cost, but it does not replace planning.

- New instances take time to start. Capacity must cover the load during that time.
- Scaling on CPU alone can miss a service that is limited by memory or by a dependency.
- A dependency, such as a database, may not scale with the service in front of it.
- Set a maximum, so a traffic flood or a bug cannot create unlimited cost.

## Protecting a full system

When load exceeds capacity, a system should reject extra work quickly instead of slowing down for everyone. Rejecting excess requests is called load shedding. Retries need a limit and an increasing delay, because clients that retry immediately multiply the load on a system that is already full.

## Questions to expect

1. How many servers does this design need? Show the arithmetic.
2. Traffic will be five times higher for one day next month. How do you prepare?
3. Which resource runs out first, and how do you know?
4. The service scales, but the database does not. What do you do?
5. How do you find the capacity of one instance?

State each assumption aloud before using it. Interviewers accept a reasonable assumption and correct an unreasonable one, and both outcomes are better than silence.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-capacity-planning) covers capacity planning, load testing, retries, timeouts, and overload in its reliability engineering chapter.
- [System Design Numbers](https://github.com/design-gurus/system-design-numbers) is a free reference for estimation.
- [SRE system design](../rounds/sre-system-design.md) shows where sizing fits in the round.
- Free article: [Autoscaling strategies every developer should know](https://www.designgurus.io/blog/autoscaling-strategies?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-capacity-planning), which covers how capacity follows demand automatically.
- Free answer: [What load testing is and why it matters](https://www.designgurus.io/answers/detail/what-is-load-testing-and-why-is-it-critical-for-evaluating-system-performance?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-capacity-planning), the test that confirms a capacity estimate.
