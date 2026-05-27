---
title: "Proxy revoke and time-bound expiration auto-remove access within 60 seconds"
parent_epic: "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
summary: "Delegator (and, in defined scenarios, delegate) can revoke proxy at any time; time-bound expirations auto-remove access at the configured moment. Both paths remove access within 60 seconds and notify both parties."
owner: "Identity & Access Platform Team — Family & Proxy squad"
priority: "P0"
sprint: "Family/Proxy Sprint 3"
story_points: 5
personas:
  - "Eleanor W. — Tech-Limited Senior (75+) — delegator-initiated revoke"
  - "All patients — auto-expiration enforcement"
acceptance_criteria:
  - "Revoke removes access within 60 seconds p95 and notifies both parties (PRD §13.1 F-002)"
  - "Time-bound expiration auto-removes access at the configured moment and logs the event (PRD §13.1 F-002)"
  - "Defined delegate-initiated revoke paths supported per policy (PRD §13.1 F-002)"
  - "All revoke / expiration events appear in patient-visible audit within 5 min (PRD §13.1 F-003; §5.4 `NF-032`)"
  - "Active sessions of the delegate for that patient are terminated on revoke / expiration (PRD §5.2 `NF-022`; §5.3 `NF-030d`)"
dependencies:
  - "Story 02 (grant)"
  - "Notifications service with channel preferences (`F-070`)"
  - "Session-termination capability in OIDC IdP / session store"
  - "Scheduler / job runner for expiration sweeps"
acceptance_criteria_notes: "Mirror Gherkin scenarios below."
tasks:
  - "Implement delegator-initiated revoke UI + API"
  - "Implement delegate-initiated revoke for defined scenarios (per policy)"
  - "Implement expiration sweep job with idempotent processing"
  - "Terminate active sessions of the delegate scoped to the revoked patient"
  - "Emit revoke / expiration audit events"
  - "Wire both-party notifications honoring channel preferences"
  - "Load-test sweep job for backlog scenarios (PRD §5.2 `NF-029e`)"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** Eleanor has recovered and no longer needs her granddaughter to manage her appointments. She wants to revoke access immediately and be sure it took effect. Separately, every proxy in the system has a mandatory expiration (from Story 02) that must auto-enforce on the dot — otherwise the program has "permanent" grants by neglect (PRD §8 R-SEC-01).

As a **patient (delegator)**, I can **revoke an active proxy at any time and trust that time-bound expirations auto-remove access** so that **my caregiver loses access immediately when I want them to, and no grant outlives its authorized window**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Delegator-initiated revoke | A delegator with an active proxy grant | They submit a revoke action | Access for the delegate on that patient is removed within 60 seconds p95; both parties notified | (PRD §13.1 F-002) |
| 2 | Active sessions terminated | A delegate currently signed in and viewing the patient's record | The grant is revoked | The delegate's active session for that patient is terminated; subsequent API calls return 403 | (PRD §5.2 `NF-022`; §5.3 `NF-030d`) |
| 3 | Time-bound expiration | A grant with an expiration timestamp | The expiration time is reached | Access is auto-removed and an expiration audit event is logged within 60 seconds of the expiration moment | (PRD §13.1 F-002; §5.4 `NF-032`) |
| 4 | Delegate-initiated revoke (defined scenarios) | A delegate per the configured policy | They invoke the self-revoke action | Their access is removed within 60 seconds p95 and both parties notified | (PRD §13.1 F-002) |
| 5 | Audit visibility | Any revoke or expiration event | The patient opens the patient-visible audit log | The event is visible within 5 minutes | (PRD §13.1 F-003; §5.4 `NF-032`) |
| 6 | No missed expirations | A backlog of expirations queued by the sweep job | The sweep runs | 100% of due expirations are processed; alert fires on any miss | (PRD §13.1 F-002; §5.2 `NF-029e`) |

## Non-Functional / Compliance Notes

- Performance: revoke → access-removed ≤ 60s p95; expiration sweep processes due grants within 60s of due moment (PRD §13.1 F-002).
- Security: revoke is server-authoritative; cached claims invalidated; session termination is mandatory not advisory (PRD §5.3 `NF-030c`, `NF-030d`).
- Privacy / Data handling: telemetry non-PHI; OCR-compliant (PRD §5.10 `NF-080a`, `NF-080b`).
- Regulatory: HIPAA access control + audit (PRD §6.5; §5.4 `NF-032`); information-blocking (revoke is intentional, not a covert denial) (PRD §5.9 `NF-074`).
- Accessibility: revoke UI meets WCAG 2.1 AA; voice-call helpdesk path for revoke available (PRD §5.1 `NF-010`; §13.5 F-035).

## Telemetry and Reporting

- Events emitted: `proxy.revoke.requested`, `proxy.revoke.completed`, `proxy.expiration.fired`, `proxy.session.terminated`, `proxy.notification.sent`.
- Metrics tracked: revoke → access-removed latency p95, expiration-miss count (target 0), notification-delivery success, delegate-initiated revoke rate.
- Dashboards / alerts: alert on any expiration miss; alert on revoke latency p95 > 60s; anomaly alert on revoke spikes.
- Audit logging: every revoke / expiration / session-termination event in immutable audit ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: OIDC IdP with session-termination, scheduler, Notifications, immutable audit store.
- Data sources / documents: revocation-policy doc (delegate-initiated scenarios).
- Teams / sign-offs: Privacy Officer, CISO, SRE (sweep reliability), Clinical Operations (helpdesk).
- Blocking stories or epics: Story 02 (grant); audit-emission infrastructure.

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Cached claim grants access after revoke (R-SEC-01) | Med | High | Server-side revoke check on every PHI API call; short claim TTL; session termination | Identity Platform |
| Expiration sweep job lag / outage leaves grants live | Med | High | Idempotent sweep with at-least-once semantics; lag alarm; runbook (`NF-029h`) | SRE |
| User cannot find revoke control | Med | Med | Revoke surfaced in audit-log entry context + account-settings; usability test with 75+ | Design + Product |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off
- [ ] Feature flag / rollout plan defined
- [ ] Documentation updated (runbooks, user guides, helpdesk script)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-02-family-accounts-proxy-lifecycle-audit-log.md](../epic-02-family-accounts-proxy-lifecycle-audit-log.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §5.1 `NF-010`, §5.2 `NF-022`/`NF-029e`/`NF-029h`, §5.3 `NF-030c`/`NF-030d`, §5.4 `NF-032`, §5.9 `NF-074`, §5.10 `NF-080a`/`NF-080b`, §6.5, §8 R-SEC-01, §13.1 F-002/F-003, §13.5 F-035.
- Design / architecture docs: PRD §6.2 (Proxy / Family + Audit / Logging services).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
