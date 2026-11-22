# Containers and Kubernetes

A container is a process that runs with its own view of the file system, the network, and the process list. It shares the kernel of its host. Kubernetes is a system that runs containers across many machines and keeps the running state equal to a declared state.

## Containers and virtual machines

| Property | Container | Virtual machine |
|---|---|---|
| Isolation | Kernel features: namespaces and control groups | A separate kernel on virtual hardware |
| Start time | Seconds or less | Tens of seconds or more |
| Overhead | Low | A full operating system per machine |
| Security boundary | Weaker, because the kernel is shared | Stronger |

A namespace limits what a process can see. A control group, usually written cgroup, limits what a process can use, such as memory and CPU time. An image is the packaged file system from which a container starts.

## The Kubernetes objects to know

| Object | Purpose |
|---|---|
| Pod | One or more containers that share a network address and are scheduled together |
| Deployment | Keeps a set number of identical pods running and manages rolling updates |
| Service | A stable address that distributes traffic across matching pods |
| Ingress | Routes outside HTTP traffic to services |
| ConfigMap and Secret | Supply configuration and sensitive values to pods |
| StatefulSet | Runs pods that need a stable identity and storage |
| Namespace | Divides a cluster among teams or environments |

The control plane holds the declared state and makes decisions. The scheduler assigns each pod to a node, which is a worker machine. The kubelet on each node starts the containers.

## Probes, requests, and limits

| Setting | What it controls |
|---|---|
| Readiness probe | Whether the pod receives traffic |
| Liveness probe | Whether the container is restarted |
| Resource request | What the scheduler reserves for the container |
| Resource limit | The maximum the container may use |

A container that exceeds its memory limit is stopped by the kernel. A container that exceeds its CPU limit is slowed down, not stopped.

## Failure states and their usual causes

| State | Meaning | First checks |
|---|---|---|
| Pending | No node can accept the pod | Requests larger than free capacity, or scheduling rules that match no node |
| ImagePullBackOff | The image cannot be downloaded | Image name, tag, and registry credentials |
| CrashLoopBackOff | The container starts and exits repeatedly | Logs of the previous run, configuration, a missing dependency |
| OOMKilled | Memory use exceeded the limit | The limit against real usage, or a memory leak |
| Running but not ready | The readiness probe fails | Probe path and port, and slow startup |

A method for any pod problem takes four commands in order.

```bash
kubectl get pods                      # which state is the pod in?
kubectl describe pod <name>           # what do the events say?
kubectl logs <name> --previous        # what did the last run print?
kubectl get events --sort-by=.lastTimestamp
```

## Worked example: a pod that keeps restarting

A pod shows CrashLoopBackOff after a release. The events show exit code 137, and the reason is OOMKilled. The memory limit is 256 MB. The previous version used about 200 MB, and the new version loads a larger data file at startup. The fix for today is to roll back. The lasting fix is to measure the real usage, set the limit above it with spare room, and add a memory alert.

## Questions to expect

1. What happens, step by step, when you apply a Deployment?
2. A pod is running, but the service returns no response. Where do you look?
3. What is the difference between a readiness probe and a liveness probe?
4. How does a rolling update avoid dropping requests?
5. When would you not use Kubernetes?

For question 2, check that the service selector matches the pod labels, that the pod is ready, and that the target port is correct.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-containers-and-kubernetes) has a seven-lesson chapter on containers and Kubernetes, taught through failures and follow-up questions.
- Lesson: [How Containers Work](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/how-containers-work?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-containers-and-kubernetes), in Grokking DevOps and SRE Interviews
- Lesson: [Kubernetes Core Objects](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/kubernetes-core-objects?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-containers-and-kubernetes), in Grokking DevOps and SRE Interviews
- Lesson: [Probes, Rolling Updates, and Shutdown](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/probes-rolling-updates-and-shutdown?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-containers-and-kubernetes), in Grokking DevOps and SRE Interviews
- [CI/CD and deployment strategies](ci-cd-and-deployment-strategies.md) explains the release methods a cluster supports.
- Free article: [The Kubernetes guide for system design](https://www.designgurus.io/blog/kubernetes-ultimate-guide?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-containers-and-kubernetes), a longer explanation of the cluster components.
- Free article: [Virtual machines vs containers](https://www.designgurus.io/blog/virtual-machines-vs-containers?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=concepts-containers-and-kubernetes), a beginner guide to the two isolation models.
