# Infrastructure as Code

Infrastructure as code means describing servers, networks, and other resources in files that are kept in version control and applied by a tool. The files become the record of what should exist. Changes are reviewed like application code, and an environment can be rebuilt from them.

## Why interviewers ask about it

| Without it | With it |
|---|---|
| Resources are created by hand in a console | Resources are created from reviewed files |
| Nobody knows why a setting has its value | The commit history explains each change |
| Two environments differ in unknown ways | Environments come from the same definitions |
| Recovery depends on memory | Recovery is a command |

## Declarative and imperative tools

| Style | The file states | Example tools |
|---|---|---|
| Declarative | The desired end state | Terraform, CloudFormation, Kubernetes manifests |
| Imperative | The steps to perform | A shell script, some configuration management runs |

A declarative tool compares the desired state with the real state and computes the difference. Applying the same file twice changes nothing the second time. An operation with that property is called idempotent.

## State, plan, and apply

Terraform is the tool that candidates report most often, and three of its ideas appear in most questions.

| Idea | Meaning |
|---|---|
| State | A file that maps each resource in the code to a real resource |
| Plan | A preview of what the tool would create, change, or destroy |
| Apply | The step that carries out the plan |

Store the state remotely and lock it during a run. Two people who apply at once without a lock can corrupt the state. The state can also contain secrets, so restrict access to it.

## Drift

Drift is a difference between the code and the real infrastructure. It appears when someone changes a resource by hand, often during an incident.

| Response | When it fits |
|---|---|
| Apply the code again and overwrite the manual change | The manual change was a mistake |
| Update the code to match | The manual change was a correct emergency fix |
| Import the resource into the state | The resource was created outside the tool |

Run a plan on a schedule to detect drift early. A plan that shows changes when nobody changed the code is the signal.

## Making changes safely

1. Review the plan, not only the code. The plan shows what will be destroyed.
2. Treat any line that says "destroy" or "replace" on a database or a disk as a reason to stop and investigate.
3. Split the state by environment and by component, so one error cannot affect everything.
4. Apply through a pipeline, not from a laptop, so every change is logged.
5. Pin the versions of providers and modules, so a run next month behaves like a run today.

A module is a reusable group of resources with inputs and outputs. Modules keep teams consistent, but a change to a shared module reaches every user of it. Version them.

## Worked example: a dangerous plan

An engineer renames a database resource in the code to follow a new naming rule. The plan shows 1 resource to destroy and 1 to add. The tool sees a new name as a new resource, so applying the plan would delete the production database and create an empty one. The correct change moves the resource within the state to its new name, after which the plan shows no changes.

## Questions to expect

1. What is in the state file, and what happens if it is lost?
2. Two engineers run apply at the same moment. What happens?
3. Someone changed a security rule by hand during an incident. What do you do afterward?
4. How do you manage secrets in infrastructure code?
5. How do you structure code for three environments and ten teams?

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-infrastructure-as-code) has a chapter on Terraform and infrastructure as code, and a chapter on take-home tasks that use it.
- [CI/CD and deployment strategies](ci-cd-and-deployment-strategies.md) covers the pipeline that applies these changes.
