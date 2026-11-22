# Observability

Observability is the ability to understand what a system is doing from the data it emits. Monitoring answers questions that were chosen in advance, such as "is the error rate above 1 percent?" Observability also supports questions that nobody planned, such as "why are requests from one customer slow?"

## The three data types

| Type | What it is | Best for | Cost concern |
|---|---|---|---|
| Metrics | Numbers measured over time, such as requests per second | Alerts, dashboards, trends | Cheap, unless labels have many distinct values |
| Logs | Timestamped records of single events | The detail of one failure | Volume grows with traffic |
| Traces | The path of one request across services, with the time spent in each | Finding which service is slow | Usually sampled, so some requests are not recorded |

A trace is made of spans. Each span records one operation, its start time, and its duration. The spans of one request share a trace identifier, which lets a tool join them.

The three types work together. A metric shows that latency rose. A trace shows which service added the delay. A log from that service shows the error.

## The four golden signals

Google's book *Site Reliability Engineering* names four signals to measure for any user-facing system.

| Signal | Meaning | Example metric |
|---|---|---|
| Latency | How long requests take | 95th percentile response time |
| Traffic | How much demand the system receives | Requests per second |
| Errors | The rate of failed requests | Share of responses with a 5xx status |
| Saturation | How full the system is | Queue length, memory in use |

Measure the latency of failed requests separately. A fast error can lower the average and hide a real slowdown.

## Why percentiles, not averages

Take 100 requests, of which 95 finish in 100 milliseconds and 5 take 3,000 milliseconds.

| Statistic | Value |
|---|---|
| Average | (95 x 100 + 5 x 3,000) / 100 = 245 milliseconds |
| Median | 100 milliseconds |
| 99th percentile | 3,000 milliseconds |

The average suggests a healthy service. One user in 20 waits 3 seconds, and only the high percentile shows it.

## Alerting on symptoms

A symptom is what a user experiences, such as failed requests. A cause is an internal condition, such as high CPU.

| Alert on | Example | Result |
|---|---|---|
| Symptoms | Error rate consumes the error budget too fast | Every page reflects real user harm |
| Causes | CPU above 80 percent | Many pages with no user harm, and missed failures with normal CPU |

Page a person only when the alert is urgent, concerns users, and requires an action. Send everything else to a ticket or a dashboard. An on-call engineer who receives many pages without action begins to ignore them, an effect called alert fatigue.

## Questions to expect

1. What would you put on the first dashboard for a new service?
2. A dashboard shows a healthy average latency, but users complain. Why?
3. How do you reduce a noisy alert without missing real failures?
4. What does a label with many distinct values do to a metrics system?
5. How does a trace identifier travel between services?

For question 4, each distinct label value creates a separate time series. A label such as a user identifier can create millions of series and exhaust the metrics store. This property is called cardinality.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-observability) covers metrics, logs, traces, and alert design, and includes the design of a metrics and alerting pipeline.
- Lesson: [Metrics, Logs, and Traces](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/metrics-logs-and-traces?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-observability), in Grokking DevOps and SRE Interviews
- Lesson: [Designing Alerts That Matter](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/designing-alerts-that-matter?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-observability), in Grokking DevOps and SRE Interviews
- Lesson: [Monitoring and Observability](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/monitoring-and-observability?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-observability), in Grokking System Design Fundamentals
- [SLIs, SLOs, and error budgets](slis-slos-and-error-budgets.md) shows how to turn these signals into targets.
- [Troubleshooting](../rounds/troubleshooting.md) uses them in a worked example.
- Free article: [OpenTelemetry and modern observability](https://www.designgurus.io/blog/guide-to-modern-observability?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-observability), a beginner guide to collecting metrics, logs, and traces.
- Free answer: [How to design a monitoring and alerting system](https://www.designgurus.io/answers/detail/how-would-you-design-a-system-for-monitoring-and-alerting-collecting-metrics-storing-them-and-triggering-alerts?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-observability), which covers metric collection, storage, and alert triggering.
