# An order for studying and repeating the work

[Português](study-guide.md) · [Home](../README.en.md) · [Architecture](architecture.en.md) · [Evidence](results.en.md)

This route connects the topics without imposing a calendar. Pick a stage, run its exercise and record what you can explain. Links open the README containing that project's commands and operating notes.

## Before starting

Have Git and, for container labs, Docker working on Linux/WSL. Check versions, tools and ports in the selected README; requirements vary. Ansible, Terraform and Jenkins use their own environments. Observability exercises integrate components in the main cluster.

When an integration expects neighboring projects, keep checkouts arranged like this example. It illustrates directory layout, rather than a requirement to install everything at once:

```text
studies/
├── devops-portfolio/
├── docker-lab/
├── kubernetes-lab/
├── argocd-lab/
├── monitoring-lab/
├── logging-lab/
└── tracing-lab/
```

## The route

| Stage | Projects and exercise | What to explain before moving on |
| --- | --- | --- |
| 1 · Read the system | [Linux](https://github.com/tommmdl/linux-operations-lab/blob/main/README.en.md): run the diagnostic and compare its output with individual queries. | What load, available memory and disk space tell you, and what the script does not measure. |
| 2 · Run the application | [Docker](https://github.com/tommmdl/docker-lab/blob/main/README.en.md): create a note, recreate containers, stop and restart the database. | Why data survives, how the API finds the database and the difference between liveness and readiness. |
| 3 · Deliver a revision | [Jenkins](https://github.com/tommmdl/jenkins-lab/blob/main/README.en.md): trigger a failed build. [GitHub Actions](https://github.com/tommmdl/github-actions-lab/blob/main/README.en.md): follow the image to GHCR. | Which stage failed, which artifact survived and how to verify the published image's identity. |
| 4 · Describe changes | [Terraform](https://github.com/tommmdl/terraform-lab/blob/main/README.en.md): plan/apply, drift and destroy in local Docker. [Ansible](https://github.com/tommmdl/ansible-lab/blob/main/README.en.md): repeated runs, limited changes and drift repair. | The role of state, the meaning of a plan and why a role's second execution can report `changed=0`. |
| 5 · Understand the cluster | [Kubernetes](https://github.com/tommmdl/kubernetes-lab/blob/main/README.en.md): replicas, Service, PVC and rollback. [Configuration](https://github.com/tommmdl/kubernetes-config-lab/blob/main/README.en.md): ConfigMaps, Secrets, TLS and Downward API. | What replaces a Pod, how readiness changes endpoints and what a PVC preserves. |
| 6 · Follow Git and assess images | [Argo CD](https://github.com/tommmdl/argocd-lab/blob/main/README.en.md): compare drift with self-heal off/on. [Security](https://github.com/tommmdl/security-lab/blob/main/README.en.md): read a blocked gate and the alternative-image reports. | Who controls desired state, why publication does not mean gate approval, and how findings, fixes and mitigations differ. |
| 7 · Observe the whole path | [Monitoring](https://github.com/tommmdl/monitoring-lab/blob/main/README.en.md) → [Logging](https://github.com/tommmdl/logging-lab/blob/main/README.en.md) → [Tracing](https://github.com/tommmdl/tracing-lab/blob/main/README.en.md) → [Alerting](https://github.com/tommmdl/alerting-lab/blob/main/README.en.md). Send a request, then introduce a fault. | How to move from a probe or alert to logs and spans, and verify recovery and notification delivery. |
| 8 · Recover and return | [Backup](https://github.com/tommmdl/backup-restore-lab/blob/main/README.en.md) → [DR](https://github.com/tommmdl/disaster-recovery-lab/blob/main/README.en.md) → [Failover](https://github.com/tommmdl/failover-lab/blob/main/README.en.md). Compare the backup point, restored data and destination writes. | Why replication and backup solve different problems, why the previous writer must be fenced and how to reconcile an uncertain response. |
| 9 · Investigate faults | [Chaos Mesh](https://github.com/tommmdl/chaos-lab/blob/main/README.en.md): follow HTTP, alerts, events, packets and recovery during removals. | The difference between recovered replicas and successful requests, what an unanswered SYN proves and what remains unknown. |

You can run the first security-lab scan just after Docker and revisit it when changing images. Terraform and Ansible teach different approaches in separate environments; this portfolio's Terraform project does not provision the kind clusters.

## Dependencies to keep in mind

**Kubernetes-lab** provides the integrated environment's base. **ArgoCD-lab** adopts its application. **Monitoring-lab** prepares Prometheus and Grafana; **logging-lab** adds Loki and Alloy; **tracing-lab** uses those components to link traces and logs. **Alerting-lab** reuses the probes and Prometheus.

Before DR, complete backup-restore-lab and retain the kit described in disaster-recovery-lab. Failover-lab uses both clusters with its own databases. Chaos-lab installs an isolated application and observation stack in the study cluster; follow its kernel and permission prerequisites.

After Argo CD adopts the application, make persistent changes through its Git source. To revisit earlier manual exercises, follow that lab's coexistence procedure; reapplying an old bootstrap can compete with desired state.

## A study cycle for any stage

1. Read the exercise's goal, scope and cleanup procedure.
2. Check the starting state and form a hypothesis: what should happen when the database stops or a Pod disappears?
3. Run the scenario and compare your prediction with logs, responses, resources and data.
4. Record the revision and outcome, including errors and recovery.
5. Repeat a small variation and explain the outcome in your own words.

Use the [notes template](../templates/daily-log.en.md) and add what you learned to the [journal](../journal/README.en.md). A clearly bounded open question is a useful result too.

## Presenting the portfolio

Start with the Docker lab application, show the publication path and choose an investigation or recovery exercise. Open its report from the [selected results](results.en.md) and explain the hypothesis, test, conclusion and a limit. Be ready to explain why a test passed while recording HTTP failures, or why a completed restore still had warnings.

This route follows the published work. Understanding comes from repeating, interpreting and defending decisions; projects disclose assisted implementation. The next step can be investigating an observed gap rather than adding another tool.
