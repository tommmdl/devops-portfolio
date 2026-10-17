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

If you are new to these topics, I would start with Linux and Docker. Later projects reuse the same application so the focus stays on the tools rather than learning a new product each time.

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

Ansible, Kubernetes, GitOps, observability and security are next on this route. Projects join the index as they are developed; the roadmap is not a list of completed work.

## Keeping notes

The [journal](journal/README.en.md) tracks progress. The [daily template](templates/daily-log.en.md) helps capture decisions, mistakes and next steps alongside the code. Automatic daily publication is not configured.

Projects have Portuguese and English documentation. Passwords and infrastructure state stay out of Git. Future paid-cloud exercises should include expected costs and resource cleanup instructions.

[About the history update](docs/history.md)
