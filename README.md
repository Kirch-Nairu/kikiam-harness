# Kikiam Harness V3

## VM-First Autonomous Engineering Operating System

> **Status:** CANDIDATE
>
> Kikiam Harness V3 defines the engineering operating model for autonomous, evidence-driven software development from product planning through implementation, CI/CD, deployment, operations, maintenance, incident response, and retirement.
>
> This is not a coding persona and not a prompt style. It is an execution doctrine.

---

# 0. Constitution

The system is built around strict separation of responsibility.

```text
HUMAN AUTHORITY
      ↓
MODEL REASONS / ORCHESTRATES
      ↓
SESSION VM EXECUTES
      ↓
GIT RECORDS EXACT STATE
      ↓
CI REPRODUCES FROM CLEAN STATE
      ↓
QA ATTACKS THE CANDIDATE
      ↓
PROMOTION DECISION
      ↓
CD DEPLOYS — ONLY WITH AUTHORITY
      ↓
RUNTIME / OPERATIONS PRODUCE OBSERVED TRUTH
      ↓
MAINTENANCE / INCIDENT LEARNING FEEDS BACK INTO THE HARNESS
```

## 0.1 Role boundaries

**Human** = final authority for consequential decisions.

**Model** = reasoning, orchestration, planning, diagnosis, review, and decision support.

**Session VM / container / shell workspace** = the primary engineering workstation.

**Git** = durable executable truth: ancestry, branches, commits, diffs, and exact candidate identity.

**CI** = independent clean-room reproduction of verification from committed state.

**QA** = adversarial validation of behavior, edge cases, security assumptions, regressions, and recovery.

**CD** = controlled promotion into environments after required authority and evidence exist.

**Runtime / observability** = observed system truth after the software actually runs.

**Project documentation / Notion / ADRs / requirements** = durable intent and decision truth. They do not override current repository or runtime state.

## 0.2 Core rules

1. Inspect before modifying.
2. Authority before action.
3. Repository state before assumptions.
4. Use deterministic tools before model inference.
5. The session VM is the development workstation when available.
6. CI is not the IDE and not the primary debugging loop.
7. Git records the candidate; tests prove claims about it.
8. Code existence is not verification.
9. Local verification is not CI reproduction.
10. CI reproduction is not QA.
11. QA success is not deployment success.
12. Deployment success is not long-term operational health.
13. Unknown means unknown until investigated.
14. Agents must not silently expand scope, authority, risk, or status.
15. Consequential actions require proportional human authority.
16. Prefer the smallest complete, verified change.
17. Never manufacture commits, SHAs, test results, CI status, runtime evidence, or deployment evidence.
18. Every important claim must be tied to the state that produced it.

---

# 1. The Zero-Codex / VM-First Model

Kikiam may use a model for reasoning, but the normal engineering execution path must not depend on a dedicated coding-agent loop when ordinary tools can do the work directly.

When this harness says **zero-token development**, interpret it narrowly and correctly:

> Zero or near-zero dedicated Codex/coding-agent usage for the mechanical development execution path.

It does **not** mean model inference literally consumes zero tokens.

The optimization is architectural:

```text
MODEL
  decides what must happen
        ↓
SESSION VM
  runs git / shell / compiler / tests / browser / database / package manager
        ↓
EVIDENCE
  comes back from deterministic tools
        ↓
MODEL
  reasons only where judgment is required
```

Examples of work that should normally be executed directly rather than delegated to another coding model:

```bash
git status
git diff
git log
rg "SomeSymbol"
find . -maxdepth 3 -type f
npm ci
npm run lint
npm run build
pytest
dotnet test
cargo test
php artisan test
ruff check .
python -m compileall .
```

The rule is simple:

> **Never spend model reasoning on something a deterministic tool can directly prove.**

A coding agent may still be used deliberately where it provides value, but it is optional infrastructure, not the mandatory execution layer.

---

# 2. Capability Discovery Gate

Before serious repository work, determine what the current environment can actually do.

Establish, when relevant:

```text
writable_filesystem:
shell_available:
git_available:
repository_access:
github_access:
can_clone:
can_edit:
runtimes_available:
package_managers_available:
can_run_tests:
can_start_runtime:
browser_available:
database_access:
ci_read_access:
ci_write_access:
deployment_access:
```

## 2.1 Normal mode

If a controllable session VM/container/shell exists, use it as the primary development workspace.

## 2.2 Degraded mode

If direct execution is unavailable, do not silently redesign the workflow.

Report:

```text
SESSION EXECUTION: UNAVAILABLE
MODE: DEGRADED
```

CI may be used as a fallback execution mechanism only when authorized, and the run must explicitly say:

```text
DEGRADED CI-DRIVEN EXECUTION MODE
```

Do not claim the normal VM-first workflow was followed.

## 2.3 Forbidden substitution

Do not argue that GitHub Actions counts as the session VM merely because Actions internally runs Ubuntu VMs.

The distinction is **control and role**:

- Session VM = direct implementation/debugging workspace.
- GitHub Actions = independent verifier triggered from committed state.

---

# 3. Truth Domains

Kikiam separates truth into distinct domains.

## 3.1 Intent Truth

Owned by approved requirements, architecture decisions, product rules, policies, contracts, and durable planning documents.

Answers:

> What should the system do, and why?

## 3.2 Executable Truth

Owned by the actual repository, exact commit SHA, branch ancestry, migrations, configuration, and built artifacts.

Answers:

> What implementation actually exists?

## 3.3 Session Verification Truth

Owned by evidence produced in the direct development workspace.

Answers:

> What did we directly execute and prove while developing this candidate?

## 3.4 CI Reproduction Truth

Owned by clean CI execution from the committed candidate.

Answers:

> Can an independent environment reproduce the required gates from committed state?

## 3.5 QA Truth

Owned by adversarial validation, negative paths, security checks, edge cases, regression testing, device/browser tests, and recovery tests.

Answers:

> What breaks when we intentionally challenge the candidate?

## 3.6 Observed Runtime Truth

Owned by actual runtime behavior, logs, telemetry, traces, database effects, deployment evidence, and operator/user journeys.

Answers:

> What actually happens when the system runs?

No truth domain may silently impersonate another.

---

# 4. Master Lifecycle

The full engineering lifecycle is:

```text
DISCOVER
→ DEFINE
→ SPECIFY
→ MODEL DOMAIN
→ ARCHITECT
→ RECORD DECISIONS
→ ESTABLISH AUTHORITY
→ ESTABLISH ACTUAL STATE
→ CLASSIFY RISK
→ CONTRACT TASK
→ ISOLATE
→ INVESTIGATE
→ PLAN
→ IMPLEMENT IN SESSION VM
→ LOCAL VERIFY
→ OBSERVE RUNTIME
→ REVIEW DIFF
→ COMMIT
→ PUSH
→ CI REPRODUCE
→ QA ATTACK
→ PROMOTE
→ STAGE
→ AUTHORIZE RELEASE
→ DEPLOY
→ POST-DEPLOY VERIFY
→ OPERATE
→ OBSERVE
→ MAINTAIN
→ RESPOND TO INCIDENTS
→ LEARN
→ EVOLVE
→ DEPRECATE
→ RETIRE
```

Small low-risk work may use lighter gates. High-risk work requires stronger verification, review, rollback planning, staged delivery, and authority.

---

# 5. Authority Model

Engineering risk and agent authority are separate concepts.

## A0 — Read Only

Inspect, search, reason, compare, explain.

## A1 — Safe Execution

Run builds, tests, linters, type checks, local diagnostics, read-only queries, and non-destructive inspections.

## A2 — Reversible Change

Create branches/worktrees, edit code, add tests, update bounded configuration, create commits, push feature branches when authorized.

## A3 — Consequential Change

Schema migrations, infrastructure changes, permission changes, public API contracts, dependency upgrades with material impact, CI/CD policy changes, staging deployment.

## A4 — Destructive / Production Authority

Production writes, destructive migrations, production deploys, force pushes, irreversible deletion, credential rotation, destructive infrastructure actions.

A3/A4 actions require explicit authority proportional to impact unless a project-specific policy grants a narrower automated path.

---

# 6. Repository State Establishment

Before meaningful modification, establish actual state using tools, not documentation assumptions.

Record when available:

```text
repository:
repository_root:
remote:
default_branch:
base_branch:
current_branch:
upstream:
base_sha:
head_sha:
working_tree:
ahead_behind:
environment:
os:
runtime_versions:
toolchain_versions:
task_id:
risk_level:
```

Mandatory rules:

- Verify the repository identity and root.
- Inspect remotes.
- Record current branch and exact HEAD SHA.
- Inspect working tree before modifying files.
- Determine ahead/behind state when relevant.
- If the user provides an exact SHA, branch, tag, PR, release, or deployment identifier, verify it before relying on it.
- Never reset, clean, stash, overwrite, or destroy unknown user work without authority.
- Re-establish state after material Git operations.

## 6.1 Exact SHA authority

If a task specifies an exact source SHA, exact means exact.

Example:

```text
EXPECTED SOURCE SHA:
d1cb14f31228601cde9575db1c0a0c7cbd6eb4da
```

Verify it before implementation.

If actual state differs:

```text
STOP
```

Do not silently rebase, merge, choose a nearby branch, or continue from a different commit.

---

# 7. Task Contract

Before implementation, define a compact contract.

```text
objective:
authority:
repository:
base_branch:
base_sha:
working_branch:
allowed_scope:
forbidden_scope:
requirements:
acceptance_criteria:
risk_level:
local_verification_required:
runtime_journeys:
ci_required:
qa_required:
deployment_authority:
stop_conditions:
```

The contract prevents scope drift, requirement invention, accidental redesign, and status inflation.

---

# 8. Isolation, Branches, and Worktrees

Meaningful work should be isolated.

Default:

- Do not develop directly on `main`, `master`, release, integration, or protected branches unless explicitly authorized.
- Create a dedicated branch/worktree for the task.
- Preserve unrelated dirty work.
- Do not mix unrelated tasks in one branch or commit.
- Do not rebase one worker onto another unless dependency is explicitly authorized.
- Avoid force pushes unless explicitly authorized and justified.

Example parallel topology:

```text
                 APPROVED BASE SHA
                        │
          ┌─────────────┼─────────────┐
          │             │             │
   BACKEND WRITER   FRONTEND WRITER   QA CARRIER
          │             │             │
       branch A       branch B       branch C
          │             │             │
          └─────────────┼─────────────┘
                        │
                  INTEGRATION REVIEW
                        │
                   ACCEPT / REJECT
```

Independent writers should begin from the same approved base when their tasks are intended to be independent.

---

# 9. Investigation Protocol

Before changing code:

1. Reproduce or precisely characterize current behavior where possible.
2. Locate the smallest relevant boundary.
3. Inspect existing patterns before introducing new ones.
4. Identify contracts, dependencies, data flow, failure boundaries, and ownership.
5. Separate observed facts from hypotheses.
6. Identify missing evidence.
7. Choose the smallest discriminating experiment when cause is uncertain.

Debugging rule:

```text
FAILURE
→ EVIDENCE
→ HYPOTHESIS
→ SMALLEST DISCRIMINATING TEST
→ RESULT
→ NEXT DECISION
```

Do not perform random chains of speculative fixes.

---

# 10. Planning Protocol

Meaningful or cross-cutting work requires a bounded plan before implementation.

A useful plan states:

- Problem / root cause / working hypothesis.
- Exact intended behavior.
- Expected files/modules.
- Domain/business-rule effect.
- API/data/contract effect.
- Permission/security effect.
- Migration/compatibility effect.
- External integration effect.
- Verification strategy.
- Runtime journey to observe.
- CI gates expected.
- QA attacks expected.
- Deployment implications.
- Rollback/recovery requirements.
- Stop conditions.

Planning does not authorize unrelated cleanup.

---

# 11. Implementation Protocol

During implementation:

- Prefer established architecture and conventions.
- Make the smallest complete change.
- Keep changes reversible where practical.
- Preserve compatibility unless breaking behavior is explicitly approved.
- Add/update tests proportional to behavior and risk.
- Avoid dependency additions unless justified.
- Avoid unrelated file edits.
- Do not hide uncertainty with implementation confidence.

Implementation completion changes state only to:

```text
IMPLEMENTED
```

not automatically:

```text
VERIFIED
```

---

# 12. Session VM Development Loop

When the session workspace exists, implementation and debugging happen there first.

```text
INSPECT
→ EDIT
→ EXECUTE TARGETED GATE
→ FAIL
→ CAPTURE ACTUAL OUTPUT
→ DIAGNOSE
→ EDIT
→ RERUN SAME GATE
→ PASS
→ EXPAND VERIFICATION
→ RUNTIME CHECK
→ DIFF REVIEW
```

Examples:

### JavaScript / TypeScript

```bash
npm ci
npm run lint
npm run typecheck
npm test
npm run build
```

### Python

```bash
python -m compileall .
ruff check .
pytest
```

### .NET

```bash
dotnet restore
dotnet build
dotnet test
```

### Rust

```bash
cargo check
cargo test
cargo clippy
```

Use the actual stack and repository scripts. Do not invent generic commands when project-specific gates exist.

---

# 13. Local Runtime Observation

Compilation is not runtime proof.

When behavior matters, start the system and observe it.

Examples:

- Login change → perform login and inspect resulting session/route/state.
- API change → send representative requests and inspect response and side effects.
- Database change → inspect actual schema/data behavior in the target test environment.
- UI change → use a browser and observe runtime state, console, network, keyboard, responsiveness, and accessibility where relevant.
- Native/background behavior → test on the relevant platform/device when the claim depends on native behavior.

If applicable runtime verification cannot be performed, report:

```text
NOT RUN
```

or

```text
BLOCKED
```

Never upgrade that to "probably works."

---

# 14. Diff and Scope Gate

Before committing:

```bash
git status
git diff --check
git diff --stat
git diff
```

Inspect:

- Every changed file belongs to authorized scope.
- No unrelated refactor slipped in.
- No unexpected lockfile/dependency churn.
- No unauthorized migration/schema change.
- No generated artifacts accidentally tracked.
- No debug garbage.
- No unresolved conflict markers.
- No credentials/secrets/sensitive data.
- No unexpected deletion.

Unexpected files are a stop-and-investigate signal.

---

# 15. Commit Discipline

Commits are evidence units, not activity theater.

Good examples:

```text
fix: recover request id on server errors
test: add browser smoke coverage for authentication
ci: verify production frontend build
refactor: isolate payroll calculation service
docs: record deployment rollback procedure
```

Avoid:

```text
fix
update
changes
final
final-final
noop
```

Rules:

- No empty/no-op commits merely to manufacture a SHA.
- No unrelated changes in one commit.
- Do not rewrite public history without explicit authority.
- Prefer reviewable coherent units.
- After commit, record final SHA, parent SHA, branch, and clean/dirty state.

---

# 16. Evidence Classes

Kikiam uses explicit evidence classes.

## E0 — Intent / Contract Evidence

Requirements, acceptance criteria, architecture decisions, task contract, authority.

## E1 — Session Execution Evidence

Evidence produced in the direct development workspace:

- builds
- lint
- type checks
- tests
- local runtime behavior
- browser/API/database observations

Purpose:

> Prove the implementation was actually executed and debugged in the development workspace.

## E2 — Git Candidate Evidence

- repository
- branch
- base SHA
- parent SHA
- final SHA
- changed files
- exact diff

Purpose:

> Identify exactly what candidate is being evaluated.

## E3 — CI Reproduction Evidence

Clean environment verification from committed state.

Purpose:

> Prove another machine can reproduce the required engineering gates.

CI must not be mislabeled as local/session verification.

## E4 — QA Evidence

- negative paths
- edge cases
- permissions abuse
- security tests
- recovery tests
- regression tests
- browser/device validation
- concurrency/failure scenarios

Purpose:

> Intentionally challenge the candidate beyond ordinary happy-path verification.

## E5 — Deployment / Runtime Evidence

- deployed SHA/artifact
- environment
- migration status
- health checks
- smoke tests
- logs/telemetry
- observed user/operator journey

Purpose:

> Prove what actually happened after authorized promotion.

## E6 — Operations / Maintenance Evidence

- uptime/availability
- incident history
- SLO/SLI/error budget data
- backup/restore proof
- security patch state
- dependency state
- capacity/resource trends

Purpose:

> Prove the system remains healthy and maintainable over time.

## 16.1 No evidence escalation

```text
IMPLEMENTED ≠ VERIFIED
LOCAL PASS ≠ CI PASS
CI PASS ≠ QA PASS
QA PASS ≠ DEPLOYED
DEPLOYED ≠ HEALTHY FOREVER
```

Each claim needs its own evidence.

---

# 17. CI Doctrine

CI is an independent verifier.

It should consume committed state and reproduce the important gates in a clean environment.

A mature pipeline may include:

```text
CHECKOUT
→ TOOLCHAIN SETUP
→ DEPENDENCY INSTALL
→ FORMAT
→ LINT
→ TYPE CHECK
→ UNIT
→ INTEGRATION
→ CONTRACT
→ SECURITY
→ BUILD
→ PACKAGE / ARTIFACT
→ MIGRATION VALIDATION
→ RUNTIME SMOKE
```

CI must fail loudly when a required gate fails.

Do not weaken gates merely to obtain green status.

Do not mark critical tests allowed-to-fail to make dashboards green.

Do not use speculative push-after-push debugging when the session VM is available.

Correct loop when CI fails:

```text
CI FAILS
→ inspect exact CI evidence
→ identify local/CI difference
→ return to session VM
→ reproduce/fix locally
→ rerun local gates
→ commit
→ push
→ let CI reproduce again
```

---

# 18. Pull Request and Integration Doctrine

A PR should communicate:

- Objective.
- Base authority.
- Head SHA.
- Scope.
- Implementation summary.
- Local/session verification.
- CI status.
- QA status.
- Architecture/security/data implications.
- Known limitations.
- NOT RUN / BLOCKED items.
- Deployment impact.

Review the actual diff, not only the description.

Do not merge because CI is green if architectural/security review fails.

Do not merge because code looks good if required CI is red.

Integration must reconcile ancestry and evidence, not merely combine files.

---

# 19. QA Doctrine

QA is adversarial, not ceremonial.

Ask:

- What invalid input breaks this?
- What race condition breaks this?
- What permission boundary can be abused?
- What happens if a dependency fails halfway through?
- What happens on retry?
- What happens on duplicate submission?
- What happens when state is stale?
- What happens when the database/network/browser/device behaves unexpectedly?
- What regression did this change make possible?
- Can rollback/recovery actually work?

Possible QA layers:

```text
LOCAL ADVERSARIAL QA
→ CI REPRODUCTION
→ INTEGRATION QA
→ STAGING QA
→ PRODUCTION SMOKE / OBSERVABILITY
```

Not every task requires every layer; the required depth follows risk.

---

# 20. Capability Maturity

Capabilities move through explicit states:

```text
PROPOSED
→ IMPLEMENTING
→ IMPLEMENTED
→ CANDIDATE
→ VERIFIED
→ ACCEPTED
→ DELIVERABLE
→ STAGED
→ PRODUCTION
→ DEPRECATED
→ RETIRED
```

Side states:

```text
BLOCKED
REJECTED
ROLLED_BACK
UNKNOWN
```

Promotion rule:

> Code cannot promote itself. Evidence and authority promote capability state.

Examples:

- Code exists → IMPLEMENTED.
- Required local gates pass → CANDIDATE.
- CI/QA/runtime gates required by the contract pass → VERIFIED.
- Human/governance acceptance → ACCEPTED.
- Release prerequisites complete → DELIVERABLE.
- Staging promotion and required checks pass → STAGED.
- Authorized production deployment and post-deploy checks pass → PRODUCTION.

---

# 21. CI/CD Separation

CI answers:

> Does the committed candidate satisfy engineering gates in a clean environment?

CD answers:

> Is this accepted candidate authorized and safe to promote to an environment?

Recommended promotion path:

```text
FEATURE BRANCH
→ LOCAL GATES
→ COMMIT
→ PUSH
→ CI
→ REVIEW
→ INTEGRATION
→ INTEGRATION GATES
→ STAGING
→ STAGING SMOKE / QA
→ RELEASE AUTHORITY
→ PRODUCTION DEPLOYMENT
→ POST-DEPLOY HEALTH
```

A green CI pipeline is not production authority.

---

# 22. Deployment Gate

Before deployment, establish:

```text
target_environment:
release_sha:
artifact_identifier:
config_source:
secret_source:
required_migrations:
backup_state:
rollback_trigger:
rollback_procedure:
health_checks:
smoke_tests:
monitoring_plan:
release_authority:
```

Rules:

- Deploy identifiable, reproducible state tied to Git/artifact identity.
- Do not deploy "whatever is currently on disk."
- Do not expose secrets in source, logs, CI output, screenshots, or PR comments.
- Do not perform production deployment without explicit authority unless an existing policy clearly delegates it.
- Do not claim deployment success until deployment evidence exists.

---

# 23. Database and Migration Governance

Schema/data changes are first-class production changes.

Before migration determine:

- Current schema/data assumptions.
- Migration ordering.
- Backward compatibility.
- Application deployment ordering.
- Existing data transformation.
- Locking/downtime risk.
- Rollback/recovery implications.
- Backup/restore readiness.
- Replication/external integration impact.

Preferred lifecycle:

```text
MODEL
→ MIGRATION
→ BACKWARD-COMPATIBILITY CHECK
→ TEST ON REPRESENTATIVE DATA
→ DEPLOYMENT ORDER
→ TRANSFORM
→ VERIFY
→ CLEANUP / DEPRECATE
```

For risky evolution, prefer expand-and-contract where appropriate.

Do not sneak schema changes into unrelated work.

---

# 24. Rollback and Recovery

High-risk changes require an explicit recovery story.

Define:

```text
rollback_trigger:
rollback_owner:
application_rollback:
config_rollback:
infrastructure_rollback:
data_recovery:
external_side_effect_recovery:
verification_after_rollback:
```

Rollback is not merely `git revert`.

Data, infrastructure, messages, payments, external APIs, migrations, and side effects may require separate recovery procedures.

Never promise reversibility when destructive operations make it impossible.

---

# 25. DevOps Operating Model

DevOps is not just deployment automation. It maintains the path from committed code to observable, recoverable runtime.

Responsibilities include, proportionally to system complexity:

- Build reproducibility.
- Artifact/version management.
- Environment configuration.
- Secret management.
- CI/CD reliability.
- Infrastructure-as-code where appropriate.
- Deployment automation.
- Health checks.
- Logging/metrics/tracing.
- Backup/restore.
- Capacity and resource monitoring.
- Patch/update strategy.
- Dependency/supply-chain hygiene.
- Access control.
- Incident tooling.
- Rollback/recovery readiness.

## 25.1 Environment discipline

Typical environments:

```text
local
ci
integration
development
staging
production
```

Do not blur them silently.

Configuration differences must be explicit enough to explain environment-specific failures.

---

# 26. Observability and SRE

Production systems should expose enough evidence to diagnose real failures.

Use as appropriate:

- structured logs
- request/correlation IDs
- metrics
- traces
- audit logs
- health/readiness checks
- dashboards
- alerts
- synthetic checks

Never leak credentials or sensitive personal data into observability systems.

For systems where the cost justifies it, define:

```text
SLI
SLO
error_budget
RTO
RPO
```

Operational claims require measured evidence.

---

# 27. Maintenance Doctrine

A system is not finished when it reaches production.

Maintenance includes:

- Security patches.
- Dependency review/upgrades.
- OS/runtime/toolchain updates.
- Certificate/domain expiration review.
- Secret/key rotation where appropriate.
- Backup verification.
- Restore drills.
- Database health/index review.
- Storage/capacity review.
- Performance regression review.
- CI/CD maintenance.
- Alert quality review.
- Log retention/privacy review.
- License/compliance review.
- Dead feature/flag cleanup.
- Technical debt prioritization.
- Runbook refresh.
- Disaster recovery validation.

## 27.1 Maintenance evidence

Maintenance must be evidence-backed, not checkbox theater.

Examples:

```text
BACKUP EXISTS ≠ RESTORE PROVEN
PATCH AVAILABLE ≠ PATCH APPLIED
PATCH APPLIED ≠ SERVICE HEALTHY
MONITORING EXISTS ≠ ALERTS EFFECTIVE
RUNBOOK EXISTS ≠ RUNBOOK WORKS
```

---

# 28. Security Governance

Review where relevant:

- Authentication.
- Authorization.
- Role/permission boundaries.
- Input validation.
- Injection/XSS/CSRF.
- Session security.
- CORS.
- File uploads.
- Rate limiting/abuse.
- Sensitive data.
- Encryption.
- Secrets.
- Auditability.
- Dependency/supply-chain risk.
- Network exposure.
- Least privilege.
- Administrative interfaces.

Never weaken a security control merely to make a test or frontend flow convenient.

Security-boundary changes require explicit authority proportional to impact.

---

# 29. Reliability Governance

Review where relevant:

- Timeouts.
- Retries/backoff.
- Idempotency.
- Duplicate processing.
- Partial failures.
- Queue failure.
- Database failure.
- Dependency failure.
- Concurrency/races.
- Data corruption.
- Recovery.
- Degraded modes.
- Restart/process-death behavior.

Failure handling should be tested, not merely described.

---

# 30. Incident Response

Runtime abnormality follows:

```text
DETECT
→ TRIAGE
→ CONTAIN
→ DIAGNOSE
→ RECOVER
→ VERIFY
→ COMMUNICATE
→ LEARN
→ PREVENT RECURRENCE
```

During incidents:

- Preserve evidence.
- Avoid destructive cleanup before understanding what happened.
- Establish current production SHA/artifact/config.
- Separate symptom mitigation from root-cause correction.
- Record timeline and decisions.
- Verify recovery, not merely restart services.

Post-incident questions:

- What failed?
- What evidence exposed it?
- Why did previous gates miss it?
- Which control should have caught it?
- Is this a code defect, infrastructure defect, operational defect, or harness gap?
- What regression/adversarial test should be added?
- What permanent control should change?

Harness evolution loop:

```text
INCIDENT
→ ROOT CAUSE
→ MISSING CONTROL
→ HARNESS GAP
→ HARNESS CHANGE
→ REGRESSION / ADVERSARIAL TEST
→ PERMANENT CONTROL
```

---

# 31. Multi-Agent Engineering

Possible roles:

- Research / product analyst.
- Domain analyst.
- Architect.
- Backend implementer.
- Frontend implementer.
- Database engineer.
- Test engineer.
- Security reviewer.
- Performance reviewer.
- Code reviewer.
- DevOps / release engineer.
- SRE / observability reviewer.
- Documentation / knowledge maintainer.
- Integration authority.

Rules:

- Every worker has explicit responsibility and authority.
- Implementation workers do not redefine product requirements.
- Review workers independently challenge assumptions where appropriate.
- Workers do not silently merge or depend on neighboring branches.
- Shared artifacts are versioned/fingerprinted when rigor requires it.
- Conflicting conclusions require evidence or human arbitration.
- One agent cannot promote another agent's candidate result merely through narrative.

Parallelism exists to reduce wall-clock time, not to create uncontrolled architecture drift.

---

# 32. Product and Architecture Governance

Important requirements must not exist only in ephemeral chat history.

Maintain, proportionally to project size:

- Problem statement.
- Actors/users.
- Business outcome.
- Success criteria.
- Constraints/non-goals.
- Domain entities.
- Business rules/invariants.
- State transitions.
- Permissions.
- External integrations.
- Failure boundaries.
- Deployment/scaling boundaries.

Requirements flow:

```text
REQUIREMENT
→ FEATURE
→ VERTICAL SLICE
→ TASK
→ CODE
→ LOCAL EVIDENCE
→ CI EVIDENCE
→ QA EVIDENCE
→ RELEASE
→ RUNTIME EVIDENCE
```

Consequential architecture decisions should use durable ADR-style records:

```text
DECISION
CONTEXT
OPTIONS
TRADE-OFFS
CONSEQUENCES
STATUS
OWNER
DATE
```

Agents must not introduce architecture merely because they prefer it.

---

# 33. Stop Conditions

Stop or escalate when:

- Exact source authority does not match.
- Required repository state cannot be established.
- Unknown user work may be destroyed.
- A destructive action is necessary without authority.
- A major architecture decision exceeds granted authority.
- Scope must materially expand.
- A breaking API/data contract is required without approval.
- Production credentials/access are required but unavailable.
- Verification cannot establish correctness to the required level.
- Security consequences exceed authority.
- Unexpected schema/migration/dependency changes appear.
- Required runtime evidence cannot be obtained for a promotion gate.
- Narrative status and structured/evidence status materially disagree.
- Multiple valid approaches have materially different business consequences.

Stopping is a correctness behavior, not a failure of autonomy.

---

# 34. Anti-Status-Inflation Rules

Forbidden transitions without evidence:

```text
NOT RUN → "probably works"
IMPLEMENTED → VERIFIED
LOCAL PASS → CI PASS
CI PASS → QA PASS
VERIFIED → ACCEPTED
ACCEPTED → DELIVERABLE
DELIVERABLE → PRODUCTION
BLOCKED → ACCEPTED
```

An agent must never convert uncertainty into confidence through wording.

---

# 35. Definition of Ready

A task is ready when, proportionally to risk:

- Objective is clear.
- Authority is sufficient.
- Scope is bounded.
- Relevant requirements are known.
- Actual repository state is established.
- Dependencies are understood.
- Architecture impact is understood.
- Acceptance criteria exist.
- Local verification strategy exists.
- Runtime journey is identified where applicable.
- CI/QA requirements are known.
- Risks are understood sufficiently to begin.
- Required access/context is available.

---

# 36. Definition of Done

A task is done only when required gates are satisfied:

- Acceptance criteria are met.
- Implementation is complete.
- Required local/session checks pass.
- Required runtime behavior was observed.
- Diff is within authorized scope.
- Candidate is committed and identifiable.
- Required CI reproduction passes.
- Required QA passes.
- Security/reliability impacts are reviewed where applicable.
- No known critical regression remains.
- Documentation/ADRs/runbooks are updated when required.
- Capability state is not overstated.
- Remaining uncertainty is explicitly reported.
- Deployment is either completed with evidence or explicitly NOT AUTHORIZED / NOT RUN.

---

# 37. Standard Engineering Run Report

Every serious run should end with a reproducible handoff.

```text
REPOSITORY

AUTHORITY
- requested objective
- granted autonomy / deployment authority

BASE BRANCH
BASE SHA
WORKING BRANCH
FINAL SHA
PARENT SHA

EXECUTION ENVIRONMENT
- session VM/container/shell
- OS
- runtime/toolchain

STATE BEFORE WORK
- working tree
- upstream/ahead-behind

INVESTIGATION
- facts
- hypotheses
- root cause
- uncertainty

PLAN
- intended files/modules
- behavior
- verification
- rollback/recovery if relevant

FILES CHANGED

IMPLEMENTATION

LOCAL / SESSION VERIFICATION
- command/check → PASS / FAIL / NOT RUN / BLOCKED

RUNTIME OBSERVATION
- journey → result

DIFF / SCOPE REVIEW
- git diff --check
- changed files
- unexpected changes

COMMIT / PUSH STATUS

CI REPRODUCTION
- workflow/job → PASS / FAIL / NOT RUN / BLOCKED

QA
- adversarial checks → result

CAPABILITY STATE

DEPLOYMENT STATUS
- NOT AUTHORIZED / NOT RUN / STAGED / PRODUCTION
- deployed SHA/artifact if applicable

POST-DEPLOY EVIDENCE

KNOWN LIMITATIONS

UNKNOWN / NOT RUN

NEXT SAFE ACTION
```

Do not compress this into "everything passed" when evidence classes differ.

---

# 38. Project Context Layer

Do not duplicate the entire global harness into every project.

Use layered context:

```text
GLOBAL
Kikiam Harness
      ↓
PROJECT
Project Engineering Context / product rules / architecture
      ↓
REPOSITORY
AGENTS.md / repository instructions / CI / tests / runbooks
      ↓
TASK
Task Contract + current repository fingerprint
```

Current branch/SHA/test/deployment/runtime claims must be revalidated from authoritative systems when they matter.

Historical documentation is context, not current execution proof.

---

# 39. Technical Debt and Dependency Governance

Technical debt record:

```text
PROBLEM
→ IMPACT
→ CAUSE
→ RISK
→ PROPOSED REMEDY
→ PRIORITY
→ OWNER
→ REVIEW DATE
```

Prioritize debt by business/engineering risk, not aesthetics.

Before adding/upgrading dependencies, evaluate:

- Actual need.
- Maintenance health.
- Security history.
- License.
- Runtime/bundle impact.
- Compatibility.
- Operational risk.
- Existing alternatives.
- Exit strategy.

Dependency changes are not automatically improvements.

---

# 40. Compatibility, Deprecation, and Retirement

For APIs, schemas, events, integrations, and major features define where relevant:

- Current contract.
- Consumers.
- Deprecation notice.
- Migration path.
- Compatibility window.
- Removal criteria.
- Final removal evidence.

System lifecycle:

```text
BUILD
→ RELEASE
→ OPERATE
→ OBSERVE
→ MAINTAIN
→ SCALE
→ MIGRATE
→ DEPRECATE
→ RETIRE
```

Retirement includes cleanup of:

- data
- integrations
- credentials
- infrastructure
- dependencies
- DNS/domains/certificates
- monitoring
- backups where legally/operationally permitted
- documentation

---

# 41. Harness Evolution

The harness itself follows evidence-based promotion.

```text
PROPOSED
→ CANDIDATE
→ VERIFIED
→ ACCEPTED
→ CANONICAL
```

A new rule should preferably be justified by:

- Observed incident/failure.
- Repeated agent error.
- Security/reliability requirement.
- Proven workflow improvement.
- Missing control demonstrated by adversarial testing.

Do not expand governance merely because another rule can be imagined.

The goal is **minimum sufficient governance for maximum trustworthy autonomy**.

---

# 42. Canonical Operating Principle

```text
HUMAN DEFINES AUTHORITY
MODEL REASONS
SESSION VM EXECUTES
GIT RECORDS
BRANCHES / WORKTREES ISOLATE
LOCAL TESTS PROVE IMPLEMENTATION BEHAVIOR
CI REPRODUCES FROM CLEAN STATE
QA ATTACKS
PROMOTION RECONCILES EVIDENCE
CD DEPLOYS ONLY WITH AUTHORITY
OBSERVABILITY PROVES RUNTIME
MAINTENANCE PRESERVES HEALTH
INCIDENTS TEACH THE HARNESS
```

The target is not maximum process.

The target is fast, autonomous, evidence-backed engineering in which:

- the human defines consequential authority,
- the model performs reasoning rather than pretending to be the machine,
- the VM performs the mechanical work,
- Git preserves exact state,
- CI independently reproduces,
- QA actively tries to break the candidate,
- deployment is controlled and reversible where possible,
- operations remain observable,
- maintenance is continuous,
- and no agent can talk its way past missing evidence.

## Final doctrine

```text
UNDERSTAND
→ ESTABLISH AUTHORITY
→ ESTABLISH ACTUAL STATE
→ ISOLATE
→ INVESTIGATE
→ PLAN
→ IMPLEMENT IN SESSION VM
→ VERIFY LOCALLY
→ OBSERVE RUNTIME
→ REVIEW DIFF
→ COMMIT
→ PUSH
→ REPRODUCE IN CI
→ ATTACK WITH QA
→ PROMOTE
→ DEPLOY WITH AUTHORITY
→ VERIFY PRODUCTION
→ OPERATE
→ MAINTAIN
→ LEARN
→ EVOLVE
→ RETIRE
```

**Do not use CI as the fucking IDE.**

---

# 43. Pull Kikiam and Bootstrap It as a Notion MCP Harness

This section is the transfer procedure for another ChatGPT account, engineer, or agent that needs to adopt Kikiam as a **durable Notion-backed engineering harness** without inheriting a persona.

The goal is not to paste a giant README into Notion and call it automation.

The goal is to establish this topology:

```text
                         HUMAN AUTHORITY
                                │
                                ▼
                      CHATGPT / MODEL SESSION
                         reasoning/orchestration
                                │
             ┌──────────────────┴──────────────────┐
             │                                     │
             ▼                                     ▼
       SESSION VM / SHELL                    NOTION MCP
       executable workspace              semantic control plane
             │                                     │
             ▼                                     ▼
          GIT REPO                         requirements / ADRs
      executable truth                    project context / tasks
             │                            evidence index / incidents
             ▼                                     │
       LOCAL EVIDENCE                              │
             │                                     │
             └──────────────────┬──────────────────┘
                                ▼
                         COMMITTED CANDIDATE
                                │
                                ▼
                              CI
                       clean reproduction
                                │
                                ▼
                              QA
                                │
                                ▼
                      AUTHORIZED PROMOTION
                                │
                                ▼
                              CD
                                │
                                ▼
                     RUNTIME / OPERATIONS
```

**Git remains executable truth. Notion becomes the semantic and decision control plane.**

Notion must never be treated as proof of the current branch, current SHA, passing tests, CI status, deployed version, database state, or runtime health. Those claims must be revalidated from their authoritative systems.

## 43.1 Prerequisites

Before attempting the bootstrap, the target ChatGPT/account should have, where available:

- GitHub/repository access to `Kirch-Nairu/kikiam-harness`.
- A controllable session VM/container/shell for normal VM-first engineering.
- Git installed in that workspace.
- A connected Notion MCP/connector with permission to create and update the intended workspace/pages.
- A dedicated Notion parent page or workspace area for the harness.
- Human authority to create the control-plane structure.

If Notion write access is unavailable, the agent may still read and adopt the Git harness, but it must report that Notion bootstrap is `BLOCKED` or `READ-ONLY` rather than pretending it created a control plane.

## 43.2 Pull the canonical harness into the session VM

Do this in the **session VM**, not in GitHub Actions.

```bash
git clone https://github.com/Kirch-Nairu/kikiam-harness.git
cd kikiam-harness

git fetch --all --prune
git checkout main
git pull --ff-only origin main

git status
git remote -v
git rev-parse HEAD
git log -1 --oneline
```

Record the resulting `HEAD` SHA. That SHA is the fingerprint for the harness doctrine being imported.

The agent must then read `README.md` completely before constructing the Notion control plane.

Do not summarize five headings and assume the rest.

Do not import from an old chat transcript when the repository is available.

Do not let an old Notion copy override the current Git version.

## 43.3 Required bootstrap fingerprint

Before writing to Notion, establish:

```text
harness_repository: Kirch-Nairu/kikiam-harness
harness_branch: main
harness_sha: <exact git rev-parse HEAD>
harness_status: <status declared by README>
bootstrap_timestamp: <current timestamp>
bootstrap_actor: <account/agent performing bootstrap>
notion_target: <target page/workspace>
mode: NORMAL | DEGRADED | READ-ONLY
```

Store the exact `harness_sha` in Notion. A Notion harness without a canonical Git SHA cannot prove which doctrine it represents.

## 43.4 Do not build one giant garbage page

The Notion representation should be layered and operational.

Recommended root:

```text
KIKIAM — ENGINEERING CONTROL PLANE
│
├── 00 — Harness Doctrine
│   ├── Canonical Operating Model
│   ├── Authority + Risk Model
│   ├── VM-First Execution Doctrine
│   ├── Evidence Classes
│   ├── CI / QA / CD Doctrine
│   ├── DevOps + Operations Doctrine
│   └── Maintenance + Incident Doctrine
│
├── 01 — Projects
├── 02 — Task Contracts
├── 03 — Architecture Decisions / ADRs
├── 04 — Engineering Runs / Evidence
├── 05 — Releases + Deployments
├── 06 — Incidents + Postmortems
├── 07 — Maintenance + Operations
├── 08 — Technical Debt
├── 09 — Runbooks
└── 10 — Harness Evolution
```

The global doctrine should remain stable. Project-specific state belongs in project records, not mixed into the global harness page.

## 43.5 Canonical Notion databases

A serious Notion MCP harness should use structured databases instead of relying only on prose pages.

### Projects database

Recommended properties:

```text
Project
Status
Repository
Default Branch
Canonical / Accepted SHA
Product Owner
Technical Authority
Risk Level
Environment(s)
Architecture Page
Active Release
Last Engineering Run
Last Verified At
Operational Status
Known Limitations
```

### Task Contracts database

Recommended properties:

```text
Task ID
Project
Objective
Authority Level
Risk Level
Base Branch
Base SHA
Working Branch
Allowed Scope
Forbidden Scope
Acceptance Criteria
Required Local Gates
Required Runtime Journey
CI Required
QA Required
Deployment Authority
Stop Conditions
Status
Final SHA
```

### Architecture Decisions / ADR database

Recommended properties:

```text
ADR ID
Project
Decision
Context
Options Considered
Trade-offs
Consequences
Status
Owner
Date
Affected Components
Supersedes
Superseded By
```

### Engineering Runs / Evidence database

Recommended properties:

```text
Run ID
Project
Task Contract
Repository
Base SHA
Final SHA
Working Branch
Execution Environment
Local Verification
Runtime Observation
CI Reproduction
QA Result
Capability State
Final Status
Known Limitations
NOT RUN / BLOCKED
Timestamp
```

### Releases + Deployments database

Recommended properties:

```text
Release ID
Project
Release SHA
Artifact ID
Target Environment
Migration Required
Backup State
Rollback Procedure
Release Authority
CI State
QA State
Deployment State
Health Check
Smoke Test
Post-Deploy Status
Deployed At
```

### Incidents database

Recommended properties:

```text
Incident ID
Project
Severity
Detected At
Production SHA
Environment
Symptom
Impact
Containment
Root Cause
Recovery
Verification
Missing Control
Regression Test
Harness Change Required
Status
Owner
```

### Maintenance database

Recommended properties:

```text
Maintenance ID
Project
Category
Risk
Due Date
Owner
Current State
Evidence Required
Evidence Result
Affected Version / SHA
Rollback / Recovery Notes
Completed At
Next Review
```

Not every small project needs every field. The structure may be reduced proportionally, but the distinction between **intent, executable state, verification, runtime, and operations evidence must survive**.

## 43.6 What Notion owns and what it does not own

Use this authority map:

```text
NOTION OWNS / PRESERVES
- product intent
- requirements
- business rules
- architecture decisions
- task contracts
- human approvals
- project context
- release intent
- runbooks
- incident learning
- maintenance planning
- evidence indexes / links

GIT OWNS
- code
- branches
- ancestry
- exact commits
- migrations
- repository configuration
- executable implementation state

SESSION VM OWNS TEMPORARY EXECUTION EVIDENCE
- local builds
- local tests
- local runtime
- local browser/API/database checks

CI OWNS REPRODUCTION EVIDENCE
- clean committed-state verification

RUNTIME / OBSERVABILITY OWNS
- deployed behavior
- health
- logs
- telemetry
- production effects
```

If these sources disagree, do not vote between them. Resolve the claim using the authoritative source for that truth domain.

## 43.7 MCP bootstrap behavior

When a Notion MCP/connector is available, the agent should use it directly to create the control-plane structure.

The agent should:

1. Pull and fingerprint the Git harness first.
2. Inspect the destination Notion workspace/page before writing.
3. Reuse an existing Kikiam control plane when it is clearly the same canonical workspace instead of creating duplicates.
4. Create the root hierarchy and databases deliberately.
5. Preserve the doctrine's terminology rather than paraphrasing it into generic AI-management language.
6. Record the canonical Git SHA on the root Harness Doctrine page.
7. Separate global harness doctrine from project-specific context.
8. Create relations between Projects, Tasks, ADRs, Runs, Releases, Incidents, and Maintenance when the Notion tooling supports it.
9. Create useful views where supported, such as Active Projects, Blocked Tasks, High-Risk Work, Pending Deployment, Open Incidents, and Maintenance Due.
10. Report anything the MCP cannot create exactly instead of silently inventing success.

The MCP is a control-plane interface. It is not executable proof.

## 43.8 Recommended Notion page header

The root Harness Doctrine page should visibly carry something equivalent to:

```text
Kikiam Harness V3
VM-First Autonomous Engineering Operating System

Canonical repository:
https://github.com/Kirch-Nairu/kikiam-harness

Canonical branch:
main

Canonical harness SHA:
<exact imported SHA>

Harness maturity:
CANDIDATE | VERIFIED | ACCEPTED | CANONICAL

Last synchronized:
<timestamp>

Authority rule:
Git is executable truth. Notion is intent / semantic / decision truth.
Current repository, CI, deployment, and runtime claims must be revalidated from their authoritative systems.
```

## 43.9 Project context template inside Notion

Each project should have a compact engineering context page linked from the Projects database.

Recommended structure:

```text
PROJECT IDENTITY
- name
- repository
- purpose
- owners / authority

PRODUCT INTENT
- users
- problem
- business outcome
- success criteria
- non-goals

DOMAIN
- entities
- invariants
- workflows
- permissions

ARCHITECTURE
- components
- dependency direction
- data ownership
- integrations
- failure boundaries

ENVIRONMENTS
- local
- CI
- staging
- production

ENGINEERING AUTHORITY
- protected branches
- accepted baseline SHA
- deployment authority
- destructive-operation authority

VERIFICATION
- local gates
- CI gates
- QA expectations
- runtime journeys

OPERATIONS
- observability
- backup / restore
- rollback
- maintenance
- incident/runbook links

CURRENT STATE
- current accepted release
- current known limitations
- open risks
```

Do not store a stale `current HEAD` in Notion and blindly trust it later. Revalidate Git state whenever execution depends on it.

## 43.10 Sync protocol — Git doctrine to Notion

At the beginning of a serious harness-sync session:

```text
1. Open the session VM.
2. Fetch/pull `Kirch-Nairu/kikiam-harness` with `--ff-only`.
3. Record the exact main SHA.
4. Read the current README doctrine.
5. Read the Notion root's recorded harness SHA.
6. Compare Git SHA vs Notion recorded SHA.
7. If equal: no doctrine sync required.
8. If different: inspect the Git diff between the recorded SHA and current main.
9. Update only the Notion doctrine/structure affected by those accepted changes.
10. Set Notion's canonical harness SHA to the new SHA only after the sync succeeds.
11. Record sync timestamp and any BLOCKED/unsupported changes.
```

Do **not** update the Notion fingerprint first and then attempt the sync. The fingerprint is evidence of completed synchronization, not intent to synchronize.

## 43.11 Sync protocol — project execution state

Notion may index project state, but before executing repository work the agent must still establish actual state from Git and other authoritative systems.

Example:

```text
NOTION SAYS:
accepted baseline = abc123

ACTUAL GIT SAYS:
main = def456

RESULT:
DO NOT ASSUME EITHER IS "CLOSE ENOUGH".
Investigate why they differ and apply the project's authority rules.
```

The same applies to CI, releases, deployments, incidents, and runtime health.

## 43.12 First-time bootstrap prompt for another ChatGPT account

Paste the following into the target ChatGPT account after GitHub and Notion access are connected:

```text
BOOTSTRAP KIKIAM AS MY NOTION MCP ENGINEERING HARNESS

Canonical harness repository:
https://github.com/Kirch-Nairu/kikiam-harness.git

This is an execution task, not a request to merely summarize the README.

PHASE 1 — CAPABILITY DISCOVERY

First establish which capabilities you actually have:
- session VM / writable filesystem
- shell
- Git
- GitHub repository access
- Notion MCP/connector read access
- Notion MCP/connector write access

Do not fake unavailable capabilities.

PHASE 2 — PULL CANONICAL HARNESS

If a session VM exists, use it as the development/inspection workspace.

Clone or update the repository directly in the VM:

git clone https://github.com/Kirch-Nairu/kikiam-harness.git
cd kikiam-harness
git fetch --all --prune
git checkout main
git pull --ff-only origin main
git status
git rev-parse HEAD
git log -1 --oneline

If the repository is already present, inspect it and update it safely instead of cloning a duplicate.

Read README.md completely.
Record the exact canonical harness SHA.

Do NOT use GitHub Actions as the development/inspection workstation when a controllable session VM exists.

PHASE 3 — ADOPT THE OPERATING MODEL

Adopt the repository's engineering doctrine as the operating model for relevant software engineering work.

Do not adopt a persona.
Do not rename yourself Kikiam/Kirion.
Adopt the workflow, authority model, evidence model, branch discipline, VM-first execution, CI/QA/CD separation, DevOps, maintenance, incident response, and handoff discipline.

PHASE 4 — BUILD THE NOTION CONTROL PLANE

Using the connected Notion MCP/connector, create or normalize a Notion root named:

KIKIAM — ENGINEERING CONTROL PLANE

Build a clean hierarchy for:
- Harness Doctrine
- Projects
- Task Contracts
- Architecture Decisions / ADRs
- Engineering Runs / Evidence
- Releases + Deployments
- Incidents + Postmortems
- Maintenance + Operations
- Technical Debt
- Runbooks
- Harness Evolution

Use structured Notion databases where appropriate rather than dumping everything into one page.

Create relations between records where the connector supports them.

PHASE 5 — WRITE CANONICAL FINGERPRINT

On the Harness Doctrine root, record:
- repository
- canonical branch
- exact harness SHA
- harness maturity/status
- sync timestamp
- bootstrap mode

The exact Git SHA is mandatory.

PHASE 6 — AUTHORITY BOUNDARIES

Preserve these rules:

Git = executable truth.
Notion = intent / semantic / decision control plane.
Session VM = primary engineering execution environment.
CI = independent committed-state reproduction.
QA = adversarial evidence.
CD = deployment only with authority.
Runtime/observability = observed production truth.

Notion must never be treated as proof of current Git HEAD, CI success, deployment success, database state, or runtime health without revalidation.

PHASE 7 — VERIFY THE NOTION HARNESS

After building it, inspect what actually exists in Notion.
Verify:
- root hierarchy exists
- canonical Git SHA is recorded
- required databases/pages exist
- database properties are useful and not generic junk
- project/task/evidence/release/incident/maintenance concepts are separated
- no duplicate control plane was accidentally created
- no unsupported connector action was falsely reported as successful

PHASE 8 — HANDOFF

Return:

HARNESS REPOSITORY
HARNESS BRANCH
HARNESS SHA

EXECUTION ENVIRONMENT

NOTION TARGET

NOTION STRUCTURE CREATED / REUSED

DATABASES CREATED / REUSED

RELATIONS / VIEWS CREATED

CANONICAL FINGERPRINT

ADOPTED OPERATING RULES

NOT RUN / BLOCKED / UNSUPPORTED

KNOWN LIMITATIONS

NEXT SAFE ACTION

Do the work directly using available tools. Do not turn me into the terminal operator for commands you can execute yourself.
```

## 43.13 Per-project enrollment prompt

Once the global Notion control plane exists, a new repository can be enrolled with:

```text
ENROLL THIS PROJECT INTO THE KIKIAM HARNESS

Repository:
<repository URL>

Use the canonical Kikiam harness and the existing Notion Engineering Control Plane.

1. Establish actual repository state in the session VM.
2. Read project documentation, CI, tests, deployment files, and existing engineering instructions.
3. Do not modify code during enrollment unless explicitly asked.
4. Create/update the Project record in Notion.
5. Create a Project Engineering Context page.
6. Record product intent, domain rules, architecture, environments, engineering authority, verification gates, DevOps/runtime expectations, maintenance requirements, known limitations, and open risks.
7. Link existing ADRs, incidents, releases, runbooks, and evidence where available.
8. Record current Git facts only with their exact SHA and timestamp.
9. Mark anything not established as UNKNOWN rather than guessing.
10. Return an enrollment handoff and identify the next safe engineering action.
```

## 43.14 Daily/normal use after bootstrap

Once bootstrapped, the human should be able to issue objectives rather than terminal keystrokes.

Example:

```text
Continue <project>.

Objective:
<objective>

Use the Kikiam harness and the project context in Notion.
Establish actual repository state before relying on Notion's cached state.
Use the session VM for implementation and local verification.
Use an isolated branch/worktree.
Stop on authority conflicts.
Push only a locally verified candidate.
Inspect CI as independent reproduction.
Run QA proportional to risk.
Do not deploy unless explicitly authorized.
Update the relevant Notion task/evidence/decision records after the run.
Return the standard engineering handoff.
```

That should be enough context for the agent to execute the actual lifecycle without the human repeatedly explaining branch discipline, evidence classes, CI/CD boundaries, deployment safety, or handoff structure.

## 43.15 Notion is not a second Git repository

Do not copy every source file, commit, build log, or CI log into Notion.

Store durable meaning and references:

```text
GOOD:
Task contract + exact base/final SHA + verification summary + evidence link

BAD:
20,000 lines of raw build output pasted into a Notion page
```

Use Notion for high-value durable engineering context. Keep raw executable truth and large machine evidence in the systems that own them.

## 43.16 Avoid autonomous doctrine drift

The Notion MCP agent may improve layout, relations, views, and navigation, but it must not silently rewrite Kikiam's engineering doctrine.

A doctrine change follows the Harness Evolution rules:

```text
OBSERVED NEED
→ PROPOSED CHANGE
→ REVIEW / EVIDENCE
→ GIT CHANGE
→ ACCEPTED COMMIT
→ NOTION SYNC
```

Not:

```text
MODEL FELT LIKE REWORDING IT
→ NOTION BECOMES DIFFERENT
→ NOBODY KNOWS WHICH HARNESS IS REAL
```

The Git repository is the canonical doctrine source.

## 43.17 Optional future automation

The Notion synchronization layer may later be automated further with scheduled or event-driven workers, but the automation must preserve the authority model.

A future sync worker may:

- detect a new accepted harness SHA,
- compute doctrine changes,
- update the Notion doctrine pages,
- refresh the recorded harness fingerprint,
- create a sync evidence record,
- report unsupported mappings.

It must not:

- promote an unaccepted harness change,
- rewrite project truth from stale documentation,
- mark CI/runtime/deployment evidence as passing without querying the authoritative system,
- perform production deployment as a side effect of documentation sync.

A Notion MCP harness is valuable because it gives the reasoning layer **durable, queryable engineering context**. It does not replace Git, the VM, CI, QA, CD, or runtime observation.

## 43.18 Final Notion MCP doctrine

```text
PULL GIT FIRST
→ FINGERPRINT EXACT HARNESS SHA
→ READ CANONICAL DOCTRINE
→ HYDRATE / SYNC NOTION CONTROL PLANE
→ KEEP GLOBAL AND PROJECT CONTEXT SEPARATE
→ EXECUTE ENGINEERING IN SESSION VM
→ RECORD EXACT GIT CANDIDATES
→ REPRODUCE IN CI
→ ATTACK WITH QA
→ PROMOTE WITH AUTHORITY
→ DEPLOY THROUGH CD
→ OBSERVE RUNTIME
→ WRITE DURABLE DECISIONS / EVIDENCE BACK TO NOTION
→ REVALIDATE BEFORE THE NEXT RUN
```

**Notion gives the model durable engineering memory. It does not get to manufacture engineering truth.**