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

### Alpine APIs adopted with actual image rollback

Main Docker/basic Kubernetes now use the released basic Alpine digest; GitOps tracing uses the released instrumented digest. We restored private backups separately and proved notes written after cutover survived Debian image rollback and return. PostgreSQL containers/PVCs and schema remain unchanged. Active and retained recovery images have separate scan targets. [Procedure and evidence](https://github.com/tommmdl/security-lab/blob/main/docs/api-adoption.en.md).

- Alerting: 23 local checks followed real API and database failures through Alertmanager to an HTTP receiver, covering resolution, grouping, inhibition, silences and persistence. Application and GitOps state were restored afterward. [Results in English and Portuguese](https://github.com/tommmdl/alerting-lab/blob/main/docs/validation.en.md).

- Backup and recovery: 25 local checks recovered the application and a PostgreSQL logical dump with Velero/Kopia into a new namespace and fresh PVCs. Hook failure, invalid checksum, data, schema, indexes and identity sequence were checked; a post-backup write remained only at the source. [Results and retained warnings](https://github.com/tommmdl/backup-restore-lab/blob/main/docs/validation.en.md).

- Cross-cluster recovery: 32 local checks recovered the application and PostgreSQL into another kind cluster with the study source stopped and its API fenced from the destination. Data, volume identities, certificates, writes and persistence were checked before restoring source service. [Results and limits](https://github.com/tommmdl/disaster-recovery-lab/blob/main/docs/validation.en.md).

- Failover and failback: 48 local checks and 48 CI checks passed with synchronous replication, refusal to promote while the previous writer is unfenced, reconciliation of an uncertain write without retrying, and controller resumption after interruption. Notes written on the second cluster returned home and previous volumes were retained. Both clusters share a host; this does not demonstrate automatic elections or recovery after losing the machine. [Results](https://github.com/tommmdl/failover-lab/blob/main/docs/validation.en.md).

- Chaos Mesh: 43 local checks and 43 CI checks covered five real Pod/network experiments, three alerts with firing/resolved delivery, duration-based recovery and PostgreSQL data on the same PVC. The first local replica-removal experiment caused two connection failures in 16 samples; this limit remains documented. Other labs retained their workloads, images and PVCs. [Results](https://github.com/tommmdl/chaos-lab/blob/main/docs/validation.en.md).

### Investigating transient connections during replica removal

In the chaos-lab local comparison, graceful removal went from seven failures in 1,592 direct requests to none in 1,645 after a five-second draining wait. Abrupt removal still failed; zero-grace deletion skips the hook. Bounded GET retries report internal connection failures and do not retry writes. A lost POST response test confirmed a single database commit. All 70 checks passed locally and in CI, which still recorded one direct failure in 1,425 requests with draining; the original failures and complete samples remain available. [Investigation in English and Portuguese](https://github.com/tommmdl/chaos-lab/blob/main/docs/connections.en.md).

### Revisiting the CI timeout

The six-second timeout started during draining, before observed SIGTERM; the old record cannot distinguish TCP from HTTP waiting. We added connection phases and tested a 500 ms TCP limit for GET only. With actual SYN drops, three attempts fit in about 1.5 seconds of connection waiting, versus two in almost four seconds. All 90 checks passed locally and in CI while preserving data and earlier reports. The timeout did not recur; six direct CI errors during abrupt removals were classified as resets or refusals. No additional graceful-removal failure-rate reduction was demonstrated, and the historical cause remains open. [Bilingual investigation and results](https://github.com/tommmdl/chaos-lab/blob/main/docs/connection-timeout.en.md).

### 2026-10-20 — A clearer starting point

The portfolio now connects all 18 labs through an architecture map, a study route and selected results with direct evidence links. [Start with the guide](../README.en.md) or open the [results](../docs/results.en.md). Older entries describe their own stage of the work.

The latest chaos investigation passed 146 CI checks and reproduced five TCP connect timeouts. Four had packet matches to departing Pods; the fifth began before the experiment and has no identified backend. Original HTTP errors, controls and the local observation gap remain in the [bilingual account](https://github.com/tommmdl/chaos-lab/blob/main/docs/resilience-timeouts.en.md). This portfolio update reorganizes those records; it does not report a new runtime test.

### 2026-10-20 — Firecracker joins the public portfolio

The catalog grows to 19 labs with an independent microVM route. Firecracker records a build from pinned sources, a shutdown failure due to missing AT/i8042/VT support, and two passing boots after the correction. Ten regressions and a modified-source control complete the record. [Results and pending hardening](../docs/results.en.md#9-build-a-microvm-and-verify-shutdown-too).

Publication keeps CPU findings, BusyBox verification limits and missing validation of `jailer`, console/networking and untrusted-code isolation visible. This organization uses the recorded tests and adds no new runtime executions.
