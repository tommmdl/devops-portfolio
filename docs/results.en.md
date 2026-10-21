# Results that explain the work

[Português](results.md) · [Home](../README.en.md) · [Architecture](architecture.en.md) · [Study order](study-guide.en.md)

Selection reviewed on **2026-10-21**. These records show decisions, failures or recoveries that can be inspected. Counts belong to the cited executions; they are not a cumulative score or a promise about the next run.

## 1. Publish what was tested

GitHub Actions lab records a run with **23 integration tests** and verifies image identity while transferring between jobs, publishing and pulling from GHCR. It also retains the failed run that prevented publication.

[Account and provenance](https://github.com/tommmdl/github-actions-lab/blob/main/docs/validation.en.md) · [Cited CI run](https://github.com/tommmdl/github-actions-lab/actions/runs/39073184363)

This demonstrates that delivery path. The workflow uses a pinned application revision, and vulnerability gating is separate. Successful publication does not imply security approval.

## 2. Watch self-heal happen

In the local Argo CD exercise, the application stayed at three replicas for 30 seconds with self-heal disabled. Enabling it restored two replicas and Synced/Healthy state. A second drift was corrected while preserving the PVC and test note.

[Self-heal report](https://github.com/tommmdl/argocd-lab/blob/main/evidence/notes-self-heal.json) · [Procedure](https://github.com/tommmdl/argocd-lab/blob/main/README.en.md)

The record includes a revision and timestamp. This notes self-heal exercise ran locally; the repository pipeline validates manifests without running that exercise.

## 3. Follow a request into SQL and logs

Tracing-lab records **19 local checks**, including propagation of a known `traceparent`, Flask/Psycopg span relationships and queries through Tempo/Grafana. The same trace ID locates logs in Loki. A recorded CI execution repeats the checks.

[Validation](https://github.com/tommmdl/tracing-lab/blob/main/docs/validation.en.md) · [Span summary](https://github.com/tommmdl/tracing-lab/blob/main/evidence/trace-summary.json) · [Cited CI run](https://github.com/tommmdl/tracing-lab/actions/runs/39128753855)

The SQL span observes the database client, not the internals of the PostgreSQL process. Comparing it with metrics and logs helps explain each signal's scope.

## 4. Change images with recovery exercised

Adoption of the basic and OpenTelemetry Alpine APIs included backup and actual image rollback, preserving notes written after the switch. PostgreSQL used logical migration: dump, restore into a new volume and a return test, while retaining original volumes.

[API adoption](https://github.com/tommmdl/security-lab/blob/main/docs/api-adoption.en.md) · [PostgreSQL adoption](https://github.com/tommmdl/security-lab/blob/main/docs/postgres-adoption.en.md) · [Scans and policy](https://github.com/tommmdl/security-lab/blob/main/README.en.md)

Findings for retained recovery images remain published and can keep the overall gate blocked. A scan without findings describes that digest and that execution's vulnerability database.

## 5. Recover the backup elsewhere

Backup-restore-lab passed **25 checks locally and in CI**, recovering resources and a dump into another namespace. Disaster-recovery-lab passed **32 locally and in CI**, restoring into another cluster while the exercise source was stopped and its API fenced from the destination. Tests distinguish backup data from a later write.

[Backup validation](https://github.com/tommmdl/backup-restore-lab/blob/main/docs/validation.en.md) · [Backup CI](https://github.com/tommmdl/backup-restore-lab/actions/runs/39292524227) · [DR validation](https://github.com/tommmdl/disaster-recovery-lab/blob/main/docs/validation.en.md) · [DR CI](https://github.com/tommmdl/disaster-recovery-lab/actions/runs/39295149820)

Restores completed with zero errors and two retained warnings. Clusters and local S3 share a host. The isolated source was interrupted without destroying the main application or simulating machine loss.

## 6. Fail over and bring new writes back

Failover-lab passed **48 checks locally and in CI**. Switching requires fencing the previous writer; failback returns notes created at the destination. Tests also interrupt the controller and reconcile a write that received an HTTP error without automatically retrying it.

[Validation and earlier failures](https://github.com/tommmdl/failover-lab/blob/main/docs/validation.en.md) · [Runner report](https://github.com/tommmdl/failover-lab/blob/main/evidence/ci-verification.json) · [Cited CI run](https://github.com/tommmdl/failover-lab/actions/runs/39310992536)

This is a controlled procedure requiring access to both clusters. It does not demonstrate automatic elections or general zero RPO. The mistaken assumption that ID sequence state had to stay identical also remains documented.

## 7. Fix a check that accepted recovery too early

The Pod replacement check combined a readiness read with a separate UID read. A real-removal control reproduced the false positive. The correction uses a coherent observation and confirms disappearance of the Chaos Mesh target. That stage passed **116 local checks** and **123 in each of two CI runs**.

[Investigation](https://github.com/tommmdl/chaos-lab/blob/main/docs/pod-replacement.en.md) · [Real control](https://github.com/tommmdl/chaos-lab/blob/main/evidence/pod-replacement-local-regression.json) · [Correction CI](https://github.com/tommmdl/chaos-lab/actions/runs/39417441792)

Earlier failed reports remain available. This correction did not eliminate the connection errors that motivated the next stage.

## 8. Reproduce the six-second waits with capture in the matrix

The next CI passed **146 checks** and reproduced **five TCP connect timeouts**, with retransmitted SYNs and no SYN-ACK. Four had packet matches to departing Pods; the fifth started before experiment application and still has no identified backend.

[Full investigation](https://github.com/tommmdl/chaos-lab/blob/main/docs/resilience-timeouts.en.md) · [Cases and packets](https://github.com/tommmdl/chaos-lab/blob/main/evidence/matrix-timeouts-ci-39421860854-cases.json) · [CI summary](https://github.com/tommmdl/chaos-lab/blob/main/evidence/matrix-timeouts-ci-39421860854-summary.json) · [Cited CI run](https://github.com/tommmdl/chaos-lab/actions/runs/39421860854)

The matrix's 32 captures retained 432,610 frames with no reported drops; archive re-analysis reproduced the result. Connection and header-wait controls are separate from API timeouts. The local matrix did not reproduce a six-second timeout and retained a slow connection without a match inside its observed interval.

A forwarding-update window and a persistent NAT mapping are consistent with four cases. Missing conntrack, rule and routing-decision records for those tuples prevent an exact causal attribution. Passing recovery and capture-integrity checks does not mean every request succeeded.

## 9. Build a microVM and verify shutdown too

Firecracker-lab compiles Linux **6.12.113** with a verified OpenPGP signature and BusyBox **1.38.0** with a pinned SHA256. Its ext4 image is assembled from scratch. The first attempt reached the shell but lacked AT/i8042/VT support for Ctrl+Alt+Del: the API returned 204 and shutdown required a forced stop. The test remained failed and its record was preserved.

After the correction, **two local boots** passed on fresh disk copies, with guest responses, root remounted read-only, HTTP 204 and exit zero. Original hashes remained unchanged. There are **ten passing regressions** and a real control rejecting a modified source archive before extraction.

[Build and tests](https://github.com/tommmdl/firecracker-lab/blob/main/docs/build-from-source.en.md) · [Full reports](https://github.com/tommmdl/firecracker-lab/blob/main/evidence/source-build-results.json) · [Pending hardening](https://github.com/tommmdl/firecracker-lab/blob/main/README.en.md#hardening-still-to-do)

These are local WSL2/KVM tests, with no CI boot or notes application integration. Console findings for Spectre V2/Speculative Store Bypass remain visible. Kernel/console hardening, networking/egress, a hermetic toolchain and complete isolation still need work. BusyBox uses checksum/HTTPS verification, without the kernel's signature guarantee. The lab does not yet validate secure execution of untrusted code.

### First jailer controls

The next stage passed two local runs of six scenarios, observing UID/GID, capabilities, namespaces, root and seccomp after boot. Controls exercised CPU throttling, task/descriptor rejection, OOM and deadline enforcement. Negative profiles and killed guests are not declared approved. [Tests and limits](https://github.com/tommmdl/firecracker-lab/blob/main/docs/jailer.en.md) · [Evidence](https://github.com/tommmdl/firecracker-lab/blob/main/evidence/jailer-results.json).

The preparation helper is privileged. `CapBnd` remains broad and some namespaces are shared with it. A shutdown panic under a tight quota ended with SIGSEGV and remains recorded; waiting for load workers and enlarging the shutdown quota passed repeat runs without proving cause or elimination. CPU hardening, guest networking and untrusted-code isolation still have gaps.

The follow-up added static musl binary validation and corrected keyboard readiness and tracer collection. Under concurrent host CPU load, the corrected comparison completed ten clean shutdowns per variant. A five-second wait candidate tolerated a controlled 1.5-second vCPU delay and still failed the long-delay control. Earlier failed campaigns remain published; the historical panic trigger is unresolved and the candidate remains experimental. [Investigation, results and limits](https://github.com/tommmdl/firecracker-lab/blob/main/docs/shutdown-investigation.en.md).

The [scheduler and signal captures](https://github.com/tommmdl/firecracker-lab/blob/main/docs/vcpu-scheduling.en.md) added two sequential campaigns with 24 clean shutdowns and 12 valid traces under host load, with untraced controls and a task-limit test. The longest runnable wait was 13.262 ms. Two half-CPU shutdowns encountered throttling and both exited cleanly; the spontaneous panic did not recur. An initially empty capture and overlapping campaigns were retained and excluded from the final comparison.

The [protocol investigation with kernel stacks](https://github.com/tommmdl/firecracker-lab/blob/main/docs/vcpu-protocol.en.md) followed the official binary through 20 clean shutdowns, ten instrumented. Channel waiting reached 5.867 ms and the join interval reached 83 µs. One futex stack was correlated with the channel-wait window. Setup, validator, and read errors remain visible; the historical panic did not recur and its cause remains unresolved.

The [helper memory investigation](https://github.com/tommmdl/firecracker-lab/blob/main/docs/helper-memory.en.md) released clone cache only after each VM stopped, preserving disks. With unchanged ceilings, the observed peak fell from 768 to 262.45 MiB and limit events from 7,434 to zero. The pair completed 24 clean shutdowns with verified file hashes. Regression evidence retains an API readiness failure, its correction, and negative controls; the historical vCPU panic remains unexplained.

The [expanded repeat with corrected memory handling](https://github.com/tommmdl/firecracker-lab/blob/main/docs/shutdown-repetitions.en.md) added 72 clean shutdowns under load and 36 valid captures, retaining jailer isolation and the official one-second internal deadline. Helper peaks ranged from 322.23 to 326.75 MiB, with no limit events or OOM; all 144 clone files retained their hashes. Empty stacks, read errors and small PSI increments remain visible. The historical panic did not recur; its cause remains unresolved.

The [memory-stall investigation](https://github.com/tommmdl/firecracker-lab/blob/main/docs/memory-stalls.en.md) captured helper readahead and allocation slowpaths, separating memory PSI from I/O and container limits. All 50 completed shutdowns were clean; a campaign interrupted by an empty PID read remains marked as failed. The correction passed a loaded repeat, six original controls and 39 automated tests. Stacks identify paths in this reproduction without retroactively assigning every historical stall or resolving the historical panic.

## Evaluating or repeating the work

Open the account, locate its revision and report, and check what was actually injected and compared. Complete JSON reports live in their repositories; credentials, dumps and private content stay outside Git. Expected failures are identified, and limits are not relabeled as success.

To repeat the work, follow the [study order](study-guide.en.md) and selected lab's setup. This organization reviewed documentation and links; it did not rerun every environment or create new operational results.
