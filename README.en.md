# DevOps in practice

English · [Português](README.md)

This is where I collect my DevOps projects and the things I am exploring to understand each tool. The idea is to get something running, introduce a few failures and learn how to investigate and recover the environment.

Each lab has its own repository with code, instructions and a record of what was tested. Follow the sequence or pick a topic that interests you.

## Where to start

| Project | What you will find |
| --- | --- |
| [Linux](https://github.com/tommmdl/linux-operations-lab) | A script to inspect memory, disk and system load while practising basic diagnostics. |
| [Docker](https://github.com/tommmdl/docker-lab) | A notes app with PostgreSQL for exploring networks, volumes and what happens when the database stops. |
| [Jenkins](https://github.com/tommmdl/jenkins-lab) | A first pipeline, a successful build and a deliberate failure to help make sense of the logs. |
| [GitHub Actions](https://github.com/tommmdl/github-actions-lab) | Testing the application before publishing its image to GHCR. |
| [Terraform](https://github.com/tommmdl/terraform-lab) | Describing the same environment as code: creating it, reviewing changes, fixing drift and cleaning up. |
| [Ansible](https://github.com/tommmdl/ansible-lab) | One role configures two targets, followed by unchanged reruns, templates, handlers and drift repair. |
| [Kubernetes](https://github.com/tommmdl/kubernetes-lab) | The app gains replicas, a database volume and local-cluster exercises in recovery, scaling and rollback. |
| [Kubernetes configuration](https://github.com/tommmdl/kubernetes-config-lab) | 26 exercises with ConfigMaps, Secrets, TLS, volumes and Downward API, with solutions and tests. |
| [Argo CD](https://github.com/tommmdl/argocd-lab) | The application follows Git, with drift and automatic self-heal exercises. |
| [Prometheus and Grafana](https://github.com/tommmdl/monitoring-lab) | Probes watch the app, a dashboard shows the signals and a drill tests alerting and recovery. |
| [Loki and Grafana](https://github.com/tommmdl/logging-lab) | API and database logs reach Loki; a marker follows a message all the way to Grafana. |
| [OpenTelemetry and Tempo](https://github.com/tommmdl/tracing-lab) | A request gains API and database spans, with the same trace ID available in logs. |
| [Prometheus and Alertmanager alerts](https://github.com/tommmdl/alerting-lab) | Real API and database failures become notifications, with grouping, inhibition, silences and recovery. |
| [Velero backup and recovery](https://github.com/tommmdl/backup-restore-lab) | A consistent PostgreSQL dump goes to S3 and returns in a new namespace, with application and data checks. |
| [Trivy and image security](https://github.com/tommmdl/security-lab) | Real scan reports and a gate that blocks images with severe findings while keeping the reasons visible in CI. |

If you are new to these topics, I would start with Linux and Docker. Several projects reuse the notes app to connect the topics. Ansible uses two small targets to explore server configuration.

## What has been tried

The repositories include commands and results from Jenkins success/failure builds, database integration tests, image publication and the Terraform infrastructure lifecycle. Each project also explains the limits of those checks.

These are learning environments. The records distinguish assistant-assisted execution from work still awaiting the author's exploration.

## A route to follow

The 100-day roadmap gives the work some direction. The pace can change as exercises become more interesting or difficult.

| Days | Topic |
| --- | --- |
| 01–10 | Linux, Bash and Git |
| 11–20 | Networking, DNS, HTTP and TLS |
| 21–30 | Docker and Compose |
| 31–40 | Jenkins and GitHub Actions |
| 41–50 | Terraform |
| 51–60 | Ansible and cloud |
| 61–70 | Kubernetes |
| 71–80 | GitOps and security |
| 81–90 | Observability and SRE |
| 91–100 | Integration, recovery and presenting the projects |

GitOps, availability metrics, logs, traces and a first image security gate are now part of this route. Richer internal metrics, triage of the remaining findings and recovery are paths to explore next. Projects join the index as they are developed; the roadmap is not a list of completed work.

## Keeping notes

The [journal](journal/README.en.md) tracks progress. The [daily template](templates/daily-log.en.md) helps capture decisions, mistakes and next steps alongside the code. Automatic daily publication is not configured.

Projects have Portuguese and English documentation. Passwords and infrastructure state stay out of Git. Future paid-cloud exercises should include expected costs and resource cleanup instructions.

[About the history update](docs/history.md)
