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

- PostgreSQL critical review: SQLite and unused GPG tools removed; application separated from the bootstrap superuser. Findings went from 412 to 350, with two critical findings retained. libxml2 remains affected with compensating controls; Debian packaging and binary inspection support that the zlib MiniZip code is absent. No gate exception was added. API, privilege, in-place upgrade, Kubernetes and tracing checks passed. [Analysis and evidence](https://github.com/tommmdl/security-lab/blob/main/docs/postgresql-critical.en.md).

- PostgreSQL alternative: Alpine 3.24.2 / PostgreSQL 17.11 with libxml2 2.13.9-r2, the corrected static helper and updated zlib. The tested candidate has zero reported findings in the recorded Trivy snapshot, with no exceptions. Seven Unicode notes survived logical migration, API/lifecycle checks and a reverse restore to Debian; private backups from the existing labs also restored successfully. The alternative uses its own volume and localhost:8015; original databases remain unchanged. [Comparison and evidence](https://github.com/tommmdl/security-lab/blob/main/docs/postgres-alternative.en.md).

### PostgreSQL Alpine adopted with a real rollback

Docker and Kubernetes now use the tested Alpine digest. We paused writes, restored logical backups into fresh volumes and retained the Debian originals. A post-cutover note survived an actual API rollback through another restored Debian volume/PVC; then both labs returned to Alpine. Argo self-heal, logs and traces were checked. Full findings remain visible, including the affected recovery image. [Procedure and bilingual evidence](https://github.com/tommmdl/security-lab/blob/main/docs/postgres-adoption.en.md).

### Looking closer at the API HIGH findings

The 44 HIGH occurrences map to eight operating-system CVEs. Stable package candidates still match installed versions. We tested privilege boundaries and component presence, then bounded API resources in Compose and Kubernetes. Full findings remain visible and blocking; mitigation is not reported as a binary patch. [Bilingual review](https://github.com/tommmdl/security-lab/blob/main/docs/api-high-review.en.md).

### Testing Alpine for the API

Both basic and OpenTelemetry variants recorded zero findings with full inventory, after removing unused installer tooling and updating zlib. Each passed 23 API and 20 database-security checks; tracing was verified through real Collector/Tempo and through Grafana/Loki in a separate Kubernetes workload. The main Debian API and its 44 HIGH findings are preserved. [Experiment and evidence](https://github.com/tommmdl/security-lab/blob/main/docs/api-alpine.en.md).
