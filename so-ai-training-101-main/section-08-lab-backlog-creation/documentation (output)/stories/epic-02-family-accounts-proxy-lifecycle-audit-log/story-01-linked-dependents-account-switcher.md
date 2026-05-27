---
title: "Single account with linked dependents and one-tap account switcher"
parent_epic: "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
summary: "A single signed-in user with verified linked dependents sees an account switcher that lets them act on any account they're authorized for in one tap, with dual-identity audit attribution on every write."
owner: "Identity & Access Platform Team — Family & Proxy squad"
priority: "P0"
sprint: "Family/Proxy Sprint 1"
story_points: 5
personas:
  - "Marcus T. — Busy Parent (self + three kids)"
dependencies:
  - "Identity, Authentication & Account Recovery epic (session + RBAC claims)"
  - "Immutable audit store (PRD §5.4 `NF-032`)"
  - "Verified family-link records (data model task in this story)"
  - "Mobile parity infrastructure (PRD §13.9 F-080)"
acceptance_criteria:
  - "Logged-in user with ≥ 1 verified linked dependent sees an account switcher (PRD §13.1 F-001)"
  - "Switching is one tap / click and preserves task context where safe (PRD §13.1 F-001; §5.1 `NF-015`)"
  - "Any record-writing action on a dependent records both actor + patient identity in audit within 5 min (PRD §13.1 F-001; §5.4 `NF-032`)"
  - "Switcher ships at parity on web, iOS, Android in the same release, WCAG 2.1 AA (PRD §13.9 F-080; §5.1 `NF-010`–`NF-013`)"
  - "Switcher pages emit zero third-party tracking SDK requests (PRD §5.10 `NF-080b`)"
tasks:
  - "Define family-link data model + verified-relationship invariant"
  - "Implement account-switcher UI on web, iOS, Android with shared design tokens"
  - "Propagate active-patient context through API gateway / BFF"
  - "Emit dual-identity audit event on every record-writing action"
  - "axe-core in CI; manual accessibility audit on switcher"
  - "Feature flag + pilot-cohort rollout plan"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** Marcus is on his phone during the school day and needs to book a same-day sick visit for his middle child, then message the pediatrician about a rash on his youngest. Today the legacy portal forces him to log out and back in between accounts — he abandons more often than he completes the task. He needs a one-tap switcher that keeps him signed in while clearly showing which account is active (PRD §3.1 Marcus T.; UC-03).

As a **busy parent (Marcus)**, I can **switch in one tap between my own account and each of my verified linked dependents** so that **I can book, message, and view records for my whole family without re-authenticating or losing my place**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Switcher visible with verified dependents | A logged-in user with ≥ 1 verified linked dependent | They open any primary surface (dashboard, messages, appointments) | An account switcher is visible and lists every account they are authorized to act on | (PRD §13.1 F-001) |
| 2 | One-tap switch | An active session with the switcher visible | The user taps a dependent | The active patient context switches in one tap; the active account is clearly indicated; downstream tasks complete in ≤ 3 taps | (PRD §13.1 F-001; §5.1 `NF-015`) |
| 3 | Dual-identity audit on write | A user acting on behalf of a dependent | They perform any record-writing action (message, book, request refill) | The audit event records both actor identity AND patient identity, written within 5 min | (PRD §13.1 F-001; §5.4 `NF-032`) |
| 4 | Mobile + web parity | The release ships to GA | Web, iOS, Android builds publish | The switcher is available and functionally identical on all three in the same release | (PRD §13.9 F-080) |
| 5 | No tracking SDKs | The switcher page loads | Network traffic is captured | Zero third-party tracking-SDK requests emitted | (PRD §5.10 `NF-080a`, `NF-080b`; §8 R-REG-01) |
| 6 | Accessibility | A user with VoiceOver / TalkBack and 200% text scale | They navigate the switcher | All controls are labeled, focusable, meet ≥44pt/48dp touch targets, pass WCAG 2.1 AA | (PRD §5.1 `NF-010`–`NF-013`) |

## Non-Functional / Compliance Notes

- Performance: switch action completes ≤ 1.5s p95; downstream surfaces inherit `NF-026`–`NF-028` budgets (PRD §5.2).
- Security: only verified family-link records yield switcher entries; session and RBAC claims propagate via OIDC; no static credentials (PRD §5.3 `NF-030c`, `NF-030e`).
- Privacy / Data handling: only non-PHI correlation IDs in telemetry; OCR-compliant baseline (PRD §5.10 `NF-080a`, `NF-080b`).
- Regulatory: HIPAA access control + audit (PRD §6.5; §5.4 `NF-032`); information-blocking — switcher cannot become a covert barrier (PRD §5.9 `NF-074`).
- Accessibility / UX: WCAG 2.1 AA, text scaling, high-contrast, ≥44pt/48dp touch targets, sub-3-tap (PRD §5.1 `NF-010`–`NF-015`).

## Telemetry and Reporting

- Events emitted: `family.switcher.viewed`, `family.account.switched`, `family.action.dual_identity_recorded`, with non-PHI correlation IDs.
- Metrics tracked: switcher impressions, switch rate per active user, switch latency p95, sub-3-tap completion rate for downstream tasks, dual-identity audit coverage % (target 100%).
- Dashboards / alerts: alert on dual-identity coverage < 100%; alert on switcher latency p95 regression > 20% wow.
- Audit logging: every dependent-acting write event includes actor + patient identity, ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: OIDC IdP, immutable audit store, BFF / API gateway with active-patient header propagation, mobile shells.
- Data sources / documents: verified family-link records (data model task in this story).
- Teams / sign-offs: Privacy Officer, Accessibility audit, Identity epic team.
- Blocking stories or epics: Identity epic (parent of session + RBAC); upstream of all proxy-grant stories.

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Stale session context after switch leaks data across accounts | Med | High | Server-side active-patient invariant on every API call; contract tests across domain services | Identity Platform |
| Active-account indicator is missed and Marcus posts to the wrong child | Med | High | Persistent, high-contrast indicator + confirmation on first write per switch; usability test | Design + Product |
| Audit-event omission on a domain service | Med | High | CI contract test asserts dual-identity emit on every record-writing endpoint | Audit Platform + Domain teams |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off
- [ ] Feature flag / rollout plan defined (pilot cohort of parent users first)
- [ ] Documentation updated (runbooks, user guides)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-02-family-accounts-proxy-lifecycle-audit-log.md](../epic-02-family-accounts-proxy-lifecycle-audit-log.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §2.1 BO-1, §3.1 Marcus, §3.2 UC-03, §5.1 `NF-010`–`NF-015`, §5.2 `NF-026`–`NF-028`, §5.3 `NF-030c`/`NF-030e`, §5.4 `NF-032`, §5.9 `NF-074`, §5.10 `NF-080a`/`NF-080b`, §6.5, §13.1 F-001, §13.9 F-080.
- Design / architecture docs: PRD §6.2 (Proxy / Family service).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
