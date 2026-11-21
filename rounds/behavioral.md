# The Behavioral Round

The behavioral round asks how a candidate acted in real situations. For DevOps and SRE roles, the questions concentrate on incidents, disagreements about risk, and work done for other teams. Some loops add a project review, in which the candidate explains one past project in depth for 30 minutes or more.

## The story types to prepare

| Story type | Sample question | What the interviewer measures |
|---|---|---|
| An incident | "Tell me about a production failure you handled." | Calm, order of actions, ownership |
| A mistake | "Tell me about an outage you caused." | Honesty and what changed afterward |
| A disagreement about risk | "Describe a time you blocked or delayed a release." | Judgment and how the conflict was resolved |
| Automation | "Describe manual work that you removed." | Initiative and measured benefit |
| Influence | "How did you get other teams to adopt a tool or standard?" | Persuasion without authority |
| Priorities | "Reliability work competed with feature work. What happened?" | Use of data, such as an error budget |
| On-call | "How did you improve an on-call rotation?" | Care for the team and sustainable operations |

Six or seven stories cover most questions, because one story can answer several question types.

## Structure: STAR with a number

STAR stands for Situation, Task, Action, and Result. It gives a story a fixed order so that the listener can follow it.

| Part | Length | Content |
|---|---|---|
| Situation | 2 sentences | The system and the problem, with one number |
| Task | 1 sentence | What you were responsible for |
| Action | 4 to 6 sentences | What you did, in the first person, including one decision and its alternative |
| Result | 2 sentences | A measured outcome and what changed permanently |

## A weak answer and a strong answer

The question: "Tell me about an outage you caused."

> "We had an outage once from a configuration change. We fixed it quickly, and we learned to be more careful with changes."

This answer has no number, no decision, and no lasting change.

> "I changed a connection limit on our load balancers and applied it to all 12 at once. The new value was too low, and for 9 minutes about 40 percent of requests were rejected. I recognized the cause from the timing, reverted the change, and confirmed recovery on the error graph. In the review I proposed two changes, and I built both. Configuration changes now go to 1 load balancer first and wait 10 minutes. A check also rejects any limit below the measured peak. We have had no outage from this type of change in the 14 months since."

The strong answer states the candidate's own error plainly, gives the impact as numbers, and ends with a change to the system.

## The project review

When a loop includes a project review, the interviewer asks successive questions about one project. Prepare it in four parts.

1. **Context.** The system, the team, and the problem, with numbers.
2. **Constraints.** Time, people, budget, and what could not change.
3. **Choices.** Two or three decisions, each with the alternative that was rejected and the reason.
4. **Results.** What was measured before and after, and what you would do differently.

Choose a project in which you made the main technical decisions yourself. A larger project in which you had a small part produces weaker answers.

## Mistakes specific to this round

- Saying "we" throughout, so the interviewer cannot tell what the candidate did.
- Assigning fault to a person. Operations teams expect a blameless account, which examines the system and not the individual.
- Describing an incident without its impact in numbers.
- Ending the story at the fix, with no prevention.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-behavioral) has a chapter on behavioral answers and the project review for operations roles.
- [Grokking Modern Behavioral Interview](https://www.designgurus.io/course/grokking-behavioral-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-behavioral) teaches STAR, story banks, and company frameworks in full.
- [Postmortems](../concepts/postmortems.md) explains the blameless approach.
