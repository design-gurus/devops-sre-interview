# CI/CD and Deployment Strategies

Continuous integration (CI) builds and tests every change as soon as it is merged. Continuous delivery (CD) keeps every tested change ready to release, and continuous deployment releases it without a manual step. A deployment strategy is the method by which a new version replaces the old one in production.

## The stages of a pipeline

A pipeline is the automated sequence that carries a change from a commit to production.

| Stage | What it does | Fails when |
|---|---|---|
| Build | Compiles the code and produces an artifact, such as a container image | The code does not compile |
| Unit tests | Tests small pieces in isolation | A function returns the wrong result |
| Scan | Checks dependencies and the image for known vulnerabilities | A risky package is present |
| Deploy to staging | Installs the artifact in a test environment | Configuration is invalid |
| Integration tests | Tests the service with its real dependencies | Services disagree about an interface |
| Deploy to production | Releases with one of the strategies below | Health checks fail |

Build the artifact once and promote the same artifact through every environment. Rebuilding for production means that production runs something that was never tested.

## Three strategies compared

| Strategy | How it works | Extra capacity | Rollback | Main risk |
|---|---|---|---|---|
| Rolling | Replaces instances a few at a time | Small | Roll back in the same gradual way | Old and new versions serve together |
| Blue-green | Runs a full second environment, then switches all traffic | Double | Switch traffic back at once | All users change version together |
| Canary | Sends a small share of traffic to the new version, then increases it | Small | Send the share back to the old version | Needs good metrics to judge the canary |

In a blue-green release, "blue" is the current environment and "green" is the new one.

## Worked example: a canary

A service runs 20 instances and receives 2,000 requests a minute.

1. Deploy the new version to 1 instance, which receives 5 percent of traffic.
2. Wait 10 minutes. The canary handles about 1,000 requests in that time.
3. Compare the canary with the current version on error rate and on 95th percentile latency.
4. If both are within the limits, continue to 25 percent, 50 percent, and 100 percent.
5. If either fails, remove the canary automatically.

The comparison must include latency. A canary that checks only the error rate passes a release that returns correct answers four times slower.

## Database changes

A rollback is safe only when the old code can run against the new database schema. The expand and contract pattern keeps that true.

| Step | Change | Old code works? |
|---|---|---|
| 1. Expand | Add the new column, and leave the old one | Yes |
| 2. Migrate | New code writes both columns, and a job copies old rows | Yes |
| 3. Switch | New code reads the new column | Yes |
| 4. Contract | Remove the old column after the old code is gone | Not needed |

## Feature flags

A feature flag turns a feature on or off without a deployment. It separates releasing code from enabling behavior, so a faulty feature can be disabled in seconds. Flags need an owner and a removal date, because unused flags make code harder to read.

## Questions to expect

1. How would you choose between blue-green and canary for a given service?
2. A rollback failed. What are the likely reasons?
3. How do you release a change that alters a database schema?
4. The pipeline takes 50 minutes. How would you shorten it?
5. Which metrics decide whether a canary passes?

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-ci-cd-and-deployment-strategies) has a chapter on CI/CD and safe releases and a full design of a deployment platform for many teams.
- [Containers and Kubernetes](containers-and-kubernetes.md) covers how rolling updates work in a cluster.
