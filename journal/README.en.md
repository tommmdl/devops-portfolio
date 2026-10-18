# Learning journal

[Português](README.md) · [Back to the portfolio](../README.en.md)

This is a place to keep track of changes, mistakes and things worth trying again. The entries below link to results already recorded in each lab.

- Day 001: diagnostics prepared in `linux-operations-lab`; script checked by the assistant in WSL, author analysis pending.
- Jenkins: environment configured; builds #1 SUCCESS and #2 FAILURE verified on 2026-10-17, with artifacts and persistence after recreation. [Evidence](https://github.com/tommmdl/jenkins-lab/blob/main/docs/validation.en.md).
- Docker: bilingual notes application with PostgreSQL published on 2026-10-17; 23 checks verified CRUD, persistence and outage recovery. [Evidence](https://github.com/tommmdl/docker-lab/blob/main/docs/validation.en.md).
- GitHub Actions: pipeline published on 2026-10-17; 23 checks passed, the exact tested image was published to GHCR, and anonymous pull/local consumption were verified. [Evidence](https://github.com/tommmdl/github-actions-lab/blob/main/docs/validation.en.md).
- Terraform: modular Docker infrastructure published on 2026-10-17; 22 checks covered apply, idempotence, persistence, drift and destroy. Validation CI passed. [Evidence](https://github.com/tommmdl/terraform-lab/blob/main/docs/validation.en.md).

- Ansible: two targets configured by one role; 16 local and CI checks covered idempotence, limited changes, check mode, handlers and drift repair. [Results](https://github.com/tommmdl/ansible-lab/blob/main/docs/validation.en.md).

- Kubernetes: the notes app moved into a dedicated kind cluster; 24 local and CI checks covered replicas, Pod recovery, PVC, scaling and rollback. [Results](https://github.com/tommmdl/kubernetes-lab/blob/main/docs/validation.en.md).

- Monitoring: Prometheus and Grafana watch the application through HTTP probes; 14 local checks covered collection, dashboard queries, a controlled 404 alert and recovery. [Results](https://github.com/tommmdl/monitoring-lab/blob/main/docs/validation.en.md).

- Logging: Alloy collects API and PostgreSQL logs through the Kubernetes API; 16 local checks covered Loki and Grafana queries, persistence after replacing the Loki Pod and restricted collector permissions. [Results](https://github.com/tommmdl/logging-lab/blob/main/docs/validation.en.md).

- Tracing: 19 local checks followed real Flask/Psycopg requests through Collector and Tempo, verified parent propagation, queried Grafana and correlated logs by trace ID. [Results](https://github.com/tommmdl/tracing-lab/blob/main/docs/validation.en.md).

- Kubernetes configuration: six modules and 26 original local exercises inspired by the iximiuz outline; 39 checks covered environment, files, update semantics, immutable ConfigMaps and verified TLS. [Results](https://github.com/tommmdl/kubernetes-config-lab/blob/main/docs/validation.en.md).

- Image security: 15 local tests exercised policy decisions and actual Trivy Dockerfile scans. Real image gates blocked 48 HIGH occurrences in the basic API and 95 HIGH / 4 CRITICAL in PostgreSQL. [Results](https://github.com/tommmdl/security-lab/blob/main/docs/validation.en.md).

Use the [template](../templates/daily-log.en.md) for future entries. Describe what happened and what you understood, without adding entries just to keep a streak.

- Image remediation: the API dropped from 173 to 164 findings and PostgreSQL from 472 to 412. No remaining finding has a published fix in this Trivy snapshot; the gate still blocks 44 HIGH in the API and 71 HIGH / 3 CRITICAL in the database. The changes reached Compose and Argo CD with integration, restore and tracing checks. [Complete before/after reports](https://github.com/tommmdl/security-lab/blob/main/docs/remediation.en.md).
