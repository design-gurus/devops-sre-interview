# The SRE System Design Round

The SRE system design round asks for a design and then asks how that design fails, how it is released, and how it is measured. A product design round spends most of its time on features, data models, and scale. This round spends most of its time on operation. Some companies call it the infrastructure design round.

## How it differs from a product design round

| Topic | Product system design | SRE system design |
|---|---|---|
| Typical question | "Design a photo sharing service" | "Design a metrics and alerting pipeline" |
| Starting point | Features and users | A reliability target and the existing system |
| Main trade-off | Consistency against latency | Reliability against cost and release speed |
| Failure | One section near the end | The center of the discussion |
| Rollout | Rarely discussed | Expected: staged release, rollback, migration |
| Measurement | Often omitted | Expected: indicators, alerts, dashboards |
| Ownership | Rarely discussed | Who is paged, and how often |

## Questions that candidates report

- Design a deployment platform that many teams share.
- Distribute a file to 10,000 servers.
- Design a metrics and alerting pipeline.
- Design a feature flag service, which turns features on and off without a deployment.
- Run an existing service in more than one region.
- Build the platform for an application that already exists.

## A method for the round

| Step | Minutes | What to produce |
|---|---|---|
| 1. Clarify the target | 5 | The users, the load, and a service level objective such as 99.9 percent |
| 2. Sketch the simplest design | 8 | Components and the path of one request |
| 3. Find the failure domains | 10 | What is lost when a host, a zone, or a region fails |
| 4. Size it | 7 | Instance counts from peak load, with spare capacity |
| 5. Plan the rollout | 7 | Staged release, rollback, and data migration |
| 6. Decide what to measure | 5 | Indicators, alerts, and who responds |
| 7. State the costs | 3 | What the design costs in money and in operational work |

A failure domain is the set of things that fail together. One server is a failure domain. So is a zone, which is one data center location, and so is a region.

## Worked example: a file to 10,000 servers

**Target.** A 2 GB file must reach 10,000 servers within 30 minutes, and a bad file must not reach all of them.

**Simplest design.** Every server downloads from one central store. The total is 20,000 GB. Within 30 minutes, the store must serve about 11 GB each second, which one source cannot do.

**Improve it.** Place a cache in each of 20 data centers, so each cache serves 500 servers. Alternatively, let servers that already hold the file serve it to their neighbors.

**Failure domains.** If one cache fails, its 500 servers fall back to a neighboring cache at a lower rate.

**Rollout.** Send the file to 1 percent of servers first, which is 100 servers. Verify a checksum and a health signal, then continue to 10 percent and to the rest. Keep the previous file so that a rollback is a pointer change.

**Measure.** Track the share of servers on the new version and the time to reach 99 percent. Alert when progress stops for 5 minutes.

## What the interviewer listens for

- The reliability target is stated before the design begins.
- Every component has an answer to "what happens when this fails?"
- Numbers support the sizing. See [capacity planning](../concepts/capacity-planning.md).
- The release is staged, and the rollback is described.
- The candidate names the operational cost, including who is paged.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-sre-system-design) works through six infrastructure designs with a mid-level and a senior answer for each.
- [Grokking the System Design Interview](https://www.designgurus.io/course/grokking-the-system-design-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-sre-system-design) teaches the product design method that this round extends.
- [System Design Numbers](https://github.com/design-gurus/system-design-numbers) is a free reference for the estimates used in step 4.
- Free article: [The DevOps system design interview](https://www.designgurus.io/blog/devops-system-design-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-sre-system-design), which explains how infrastructure design rounds work.
- Free article: [Active-active vs active-passive architecture](https://www.designgurus.io/blog/active-active-vs-active-passive-architecture?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-sre-system-design), a comparison of the two multi-region designs.
