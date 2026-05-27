---
title: "Unified Patient Dashboard & Personalized Variants"
summary: "Deliver a single, personalized patient home surface that consolidates appointments, results, messages, medications, and billing into one coherent view, with user-selectable variants (Essentials, Family, Health Tracking) so each persona lands on the right defaults without ever being auto-segmented by demographics. Primary personas: all patient personas — the dashboard is the daily entry point that makes the rest of Phase 1 discoverable and reduces fragmentation that suppressed legacy adoption."
owner: "Patient Experience Team"
priority: "P0"
phase: "Phase 1 (Patient Foundation, Q3 2026 launch)"
personas:
  - "Linda R. — Chronic Condition Manager"
  - "Marcus T. — Busy Parent"
  - "Eleanor W. — Tech-Limited Senior (75+)"
  - "Dr. K. Alvarez — Primary Care Physician (secondary, via patient context)"
okrs:
  objective: "Make HealthConnect's home surface the highest-value, lowest-friction daily entry point for every patient persona, so adoption and task-completion targets are achievable."
  key_results:
    - description: "Dashboard task completion rate across the four headline tasks (refill, reschedule, view immunizations, pay bill)"
      target: "≥ 90%"
      timeframe: "First 12 months post-Phase-1"
    - description: "Monthly active users landing on the dashboard at least once per month"
      target: "40% MAU (toward `BO-1`)"
      timeframe: "18 months post-Phase-1"
    - description: "Common dashboard actions response time"
      target: "p95 ≤ 1.5s; web TTI ≤ 3s on broadband"
      timeframe: "From GA"
    - description: "Dashboard adoption stratified by age / language / accessibility cohort"
      target: "No cohort declines; 75+ cohort trends positive"
      timeframe: "First 6 months post-launch"
    - description: "Variant switch success (user-initiated, not auto-applied)"
      target: "100% of variant changes are user-initiated; 0 auto-segmentation events in audit"
      timeframe: "Ongoing from launch"
business_value: "The dashboard is the single surface that converts identity-authenticated patients into engaged users — without it, adoption (`BO-1`), self-service (`BO-3`), and satisfaction (`BO-2`) targets are unreachable because each capability is invisible."
success_metrics:
  - "Task completion rate ≥ 90% across headline tasks (PRD §7.3)"
  - "Self-service rate per task category trending up (PRD §7.3)"
  - "Time-to-result-acknowledgement decreasing quarter over quarter (PRD §7.3)"
  - "Adoption registration + MAU trajectory toward `BO-1` (PRD §2.1)"
  - "Stratified adoption shows no cohort decline (PRD §5.8 `NF-072`; §2.1 BO-6)"
  - "CAHPS / NPS portal-experience improvements toward `BO-2` (PRD §2.1, §7.1)"
regulatory_requirements:
  - "21st Century Cures Act / information-blocking — dashboard must not silently suppress patient access during partial outages (PRD §5.9 `NF-074`; §4.1 `F-076`)"
  - "HIPAA — RBAC and audit-by-default for any PHI surfaced on the home (PRD §6.5, §5.4 `NF-032`)"
  - "OCR online-tracking guidance — no third-party tracking SDKs on PHI-bearing dashboard pages (PRD §5.10 `NF-080b`)"
  - "WCAG 2.1 AA accessibility conformance with independent audit (PRD §5.1 `NF-010`)"
security_considerations:
  - "PHI minimization in dashboard telemetry; OCR-compliant tracking-tech posture (PRD §5.10 `NF-080a`, `NF-080b`)"
  - "Session policy honored on shared workstations + personal devices (PRD §5.2–5.3 `NF-022`, `NF-023`, `NF-030d`)"
  - "Granular sharing controls and sensitive-category data must not appear on the home for unauthorized viewers/proxies (PRD §5.4 `NF-038`; §4.1 `F-095`)"
  - "Vulnerable-population / shared-device safeguards on the home surface (PRD §5.7 `NF-061`)"
  - "No marketing content commingled with clinical content on the home (PRD §5.4 `NF-033`; §4.1 `F-071`)"
dependencies:
  - "Identity, Authentication & Account Recovery epic (session + RBAC claims)"
  - "Family Accounts & Proxy Lifecycle epic (account-switcher affordance, audit of proxy views)"
  - "Domain services for Appointments, Messaging, Results, Medications, Billing (read-only summaries on the home)"
  - "Notifications & Channel Preferences (per-event channel routing surfaced on home)"
  - "Privacy & Consent (sensitive-category gating on home tiles)"
  - "Content service for curated tiles, plain-language summaries, and contextual help (`F-022`, `F-193`)"
  - "Feature flags / kill-switch capability (PRD §5.2 `NF-029g`)"
  - "Independent accessibility audit vendor (PRD §5.1 `NF-010`)"
  - "Multi-language launch content for `F-195` (PRD §10 decision 14; `A-036`)"
  - "Status page + degraded-mode UX (PRD §4.1 `F-075`, `F-076`; §5.2 `NF-029d`)"
estimated_effort: "5-7 sprints (Phase 1, runs in parallel with domain services once identity GA'd)"
monitoring_metrics:
  - "Dashboard load time p50/p95 across web + iOS + Android; cold-start ≤ 3s on mid-tier devices (PRD §5.2 `NF-026`–`NF-028`); alert on p95 regression > 20% week over week"
  - "Task completion funnel per headline task with drop-off attribution (PRD §7.3); alert on drop-off > 10% vs. baseline"
  - "Variant selection mix and switch frequency; auto-application events = 0 (PRD §13.10 F-090)"
  - "Stratified adoption / MAU by age / language / accessibility cohort, with disparity-remediation trigger (PRD §5.8 `NF-072`)"
  - "Degraded-mode surface impressions (partial-data banner) per dependency outage (PRD §4.1 `F-075`, `F-076`)"
  - "Third-party request inventory on dashboard pages = empty (PRD §5.10 `NF-080b`)"
  - "Per-capability SLO error-budget consumption tied to status page (PRD §5.2 `NF-029d`)"
acceptance_criteria:
  - "Given a logged-in user, when they open the home dashboard, then one of the variants (Essentials, Family, Health Tracking) is rendered based on the user's selected default; default is never auto-applied based on a demographic attribute (PRD §13.10 F-090)"
  - "The user can switch variants in one tap/click and the preference is persisted across sessions and devices (PRD §13.10 F-090)"
  - "Headline tiles (upcoming appointments, recent results, unread messages, medications due refill, balance due) load within 1.5s p95 and meet sub-3-tap access for common tasks (PRD §5.1 `NF-015`; §5.2 `NF-028`)"
  - "Given a dependency outage (Epic, Surescripts, payments, telehealth), when the home renders, then affected tiles show a visible 'partial / loading' state, do not silently suppress access, and audit-log the suppressed-data event (PRD §13.8 F-075, F-076)"
  - "Marketing content is opt-in and physically separated from clinical content/channels on the home (PRD §13.8 F-071)"
  - "Sensitive-category data (per `NF-038`) is gated by sharing controls; the home does not surface restricted items to unauthorized proxies (PRD §5.4 `NF-038`; §4.1 `F-095`)"
  - "Dashboard meets WCAG 2.1 AA, supports user-configurable text scaling, high-contrast / no color-alone, ≥44pt/48dp touch targets, and passes independent accessibility audit (PRD §5.1 `NF-010`–`NF-013`)"
  - "Dashboard is shipped at parity on web, iOS, and Android in the same release (PRD §13.9 F-080)"
  - "All home-surface text meets the plain-language reading-level target and is available in the launch languages (PRD §5.1 `NF-017`; §10 decision 14)"
  - "Dashboard pages emit zero third-party tracking-SDK requests; telemetry follows the OCR-compliant baseline (PRD §5.10 `NF-080a`, `NF-080b`; §8 R-REG-01)"
  - "Every dashboard capability is wrapped in a feature flag / kill switch (PRD §5.2 `NF-029g`)"
  - "A/B testing on the home is restricted to non-clinical UX surfaces (PRD §5.10 `NF-080e`)"
out_of_scope:
  - "Authoring / lifecycle of the underlying clinical content (owned by Patient Education Content Lifecycle epic, `F-175`, `NF-082`)"
  - "Provider 'patient at a glance' view (owned by Provider Workflow epic, `F-050`, `F-081`)"
  - "Dashboard variants driven by autonomous AI personalization (PRD §3.3 out-of-scope; `NF-040`)"
  - "Auto-selection of variant based on demographic attribute (explicitly prohibited by `F-090`)"
  - "Wearable trend tiles for provider review (Phase 2 — `F-200`, `F-211`)"
  - "Population-health surfaces and care-gap tiles (Phase 3 — `F-170`, `F-171`)"
  - "In-visit interrupting popups / non-emergency alert modals (PRD §5.5 `NF-042`)"
stakeholders:
  - "Product Owner — Patient Experience"
  - "Design / UX Lead"
  - "Accessibility Lead + independent audit vendor"
  - "Health Equity Lead"
  - "Clinical Informatics (content tile review)"
  - "Privacy Officer (sensitive-category gating, telemetry posture)"
  - "Security / CISO (tracking-tech inventory, session policy)"
  - "Engineering: Web, iOS, Android, BFF/Experience API, SRE"
  - "Domain leads: Appointments, Messaging, Results, Medications, Billing, Notifications, Proxy"
  - "Localization / Translation Governance lead"
  - "QA"
links:
  - "context (ingestion)/prd.md"
---

> **Author reminder:** Cite the source PRD (`context (ingestion)/prd.md`) for every metric, target, regulatory requirement, and constraint referenced below. Use inline references like `(PRD §<section>)` so reviewers can trace each item to the originating requirement.

## Summary

The dashboard is HealthConnect's daily front door. It pulls together appointments, results, messages, medications, and billing into a single coherent view, with user-selectable variants — Essentials, Family, Health Tracking — so Linda, Marcus, and Eleanor each land on relevant defaults without being silently auto-segmented by demographics. The expected outcome is the unified entry point that converts authenticated patients into engaged users and unblocks the Phase 1 adoption and self-service objectives (PRD §1, §2.1).

## OKRs

**Objective:** Make HealthConnect's home surface the highest-value, lowest-friction daily entry point for every patient persona, so adoption and task-completion targets are achievable.

**Key Results** (3-5 measurable KRs):

- KR 1 — Description: "Dashboard task completion rate (refill, reschedule, view immunizations, pay bill)" | Target: "≥ 90%" | Timeframe: "First 12 months" | Source: "(PRD §7.3)"
- KR 2 — Description: "Monthly active users landing on the dashboard ≥ once/month" | Target: "40% MAU" | Timeframe: "18 months post-Ph1" | Source: "(PRD §2.1 BO-1; §7.1)"
- KR 3 — Description: "Common dashboard actions response time" | Target: "p95 ≤ 1.5s; web TTI ≤ 3s" | Timeframe: "From GA" | Source: "(PRD §5.2 `NF-027`, `NF-028`)"
- KR 4 — Description: "Stratified dashboard adoption — no cohort declines; 75+ trends positive" | Target: "Non-negative variance for all cohorts" | Timeframe: "First 6 months" | Source: "(PRD §2.1 BO-6; §5.8 `NF-072`; §8 R-ORG-03)"
- KR 5 — Description: "Variant changes are user-initiated; zero auto-segmentation events" | Target: "100% user-initiated; 0 auto events" | Timeframe: "Ongoing" | Source: "(PRD §13.10 F-090)"

## Objective and Business Value

The dashboard is the single surface that determines whether identity-authenticated users become engaged users. It directly enables `BO-1` (60% registered / 40% MAU), `BO-2` (CAHPS 85th percentile, NPS ≥ 50), and `BO-3` (75% self-scheduled, displaceable-call reduction) by making every Phase 1 capability discoverable in sub-3 taps (PRD §2.1, §5.1 `NF-015`). It is also the most visible test of the equity-at-launch principle: stratified adoption and accessibility are launch requirements, not future-state goals (PRD §1 principle 3; §2.1 BO-6; §5.8 `NF-072`).

## Personas Impacted

- Primary: **Linda R.** — Health Tracking variant surfaces medication adherence, lab trends, and shared-care-plan touchpoints in one view (PRD §3.1; F-021, F-143, F-178 dependencies).
- Primary: **Marcus T.** — Family variant surfaces unified family appointment view, consolidated billing entry, and same-day booking tile (PRD §3.1; F-001, F-031, F-032, F-150 dependencies).
- Primary: **Eleanor W.** — Essentials variant + large text + high-contrast + voice-call affordances; trusted-clinic branding visible on the home so anti-scam signals are immediate (PRD §3.1; §5.1 `NF-011`, `NF-012`, `NF-014`; `F-191`).
- Secondary: **Dr. K. Alvarez and Dr. Okonkwo** — benefit indirectly because better dashboard-driven self-service reduces inbox / scheduling noise routed to them (PRD §3.1; `F-011`).

## Acceptance Criteria

- Given a logged-in user, when they open the home, then one of the variants is rendered from the user's selected default; defaults are never auto-applied based on a demographic attribute (PRD §13.10 F-090).
- The user can switch variants in one tap/click; preference is persisted across sessions and devices (PRD §13.10 F-090).
- Headline tiles meet sub-3-tap access; common tile actions ≤ 1.5s p95; web TTI ≤ 3s; mobile cold start ≤ 3s on mid-tier devices (PRD §5.1 `NF-015`; §5.2 `NF-026`–`NF-028`).
- During a dependency outage, affected tiles show a visible "partial / loading" state, never silently suppress access, and audit-log the suppressed-data event (PRD §13.8 F-075, F-076).
- Marketing content is opt-in and physically separated from clinical content on the home (PRD §13.8 F-071).
- Sensitive-category data is gated by `F-095` / `NF-038`; restricted items do not surface to unauthorized proxies (PRD §5.4 `NF-038`).
- Dashboard meets WCAG 2.1 AA with independent audit; supports text scaling, high-contrast, ≥44pt/48dp touch targets; UI changes follow opt-in preview + advance notice for 70+ (PRD §5.1 `NF-010`–`NF-014`).
- Web, iOS, and Android dashboard parity ship in the same release (PRD §13.9 F-080).
- Plain-language reading level + launch-language coverage on all home-surface text (PRD §5.1 `NF-017`; §10 decision 14).
- Zero third-party tracking-SDK requests on dashboard pages; OCR-compliant telemetry only (PRD §5.10 `NF-080a`, `NF-080b`; §8 R-REG-01).
- Every dashboard capability is wrapped in a feature flag / kill switch (PRD §5.2 `NF-029g`).
- A/B testing on the home is restricted to non-clinical UX surfaces (PRD §5.10 `NF-080e`).

## Validation / QA Plan

- **Unit / service tests:** tile composition, variant selection, sharing-gate enforcement, degraded-mode rendering.
- **Contract tests:** consumer-driven contracts with Appointments, Messaging, Results, Medications, Billing, Notifications, Proxy services (per PRD §15.1).
- **Integration tests:** end-to-end variant render + switch on web, iOS, Android, including partial-outage scenarios for each upstream dependency (PRD §13.8 F-075, F-076).
- **Accessibility:** axe-core in CI on every PR; independent WCAG 2.1 AA audit with remediation SLAs; usability sessions with low-vision and elderly users (PRD §5.1 `NF-010`; §5.15 `NF-095`).
- **Performance:** SLO validation against `NF-026`–`NF-028`; load-test per `NF-029e`; CDN behavior verified per `NF-029f` for non-PHI static assets.
- **Privacy data-flow tests:** verify no PHI leaks to non-BAA destinations from dashboard telemetry; verify zero third-party SDKs (PRD §5.10 `NF-080a`, `NF-080b`).
- **Compliance gates:** Privacy Officer + Security sign-off on tracking-tech inventory; Clinical Informatics sign-off on tile content; Health Equity sign-off on stratified-cohort dashboards before GA.
- **UAT:** representative cohorts — Linda-like, Marcus-like, Eleanor-like, plus low-vision and non-English-speaker users — exercising each variant against the headline tasks.
- **Localization QA:** UI + content rendering in launch languages with translation-governance review for any clinical-adjacent strings (PRD §5.11 `NF-081`).
- **Pilot validation:** per-cohort adoption + task completion reviewed before broader rollout (PRD §16 pilot framework; §5.8 `NF-072`).

## Monitoring and Metrics

- Dashboard load time p50/p95 across web + iOS + Android; alert on p95 regression > 20% week over week (PRD §5.2 `NF-026`–`NF-028`).
- Task-completion funnel per headline task with drop-off attribution; alert if drop-off > 10% vs. baseline (PRD §7.3).
- Variant selection mix and switch frequency; auto-application events must equal 0 (PRD §13.10 F-090).
- Stratified MAU and task completion by age / language / accessibility cohort; disparity threshold triggers remediation per `NF-072` (PRD §5.8).
- Degraded-mode surface impressions per dependency outage; correlated with status-page incidents (PRD §4.1 `F-075`, `F-076`; §5.2 `NF-029d`).
- Automated third-party-request inventory on dashboard pages = empty (PRD §5.10 `NF-080b`; §8 R-REG-01).
- Per-capability SLO error-budget consumption surfaced on status page (PRD §5.2 `NF-029d`).
- Push-notification deep-link → dashboard conversion rate (informs notification template tuning) (PRD §5.2 `NF-025`).

## Out of Scope

- Authoring / lifecycle of clinical content tiles — owned by the Patient Education Content Lifecycle epic (`F-175`, `NF-082`).
- Provider "patient at a glance" view — owned by the Provider Workflow epic (`F-050`, `F-081`).
- Autonomous AI personalization or recommendation of variants (PRD §3.3 out-of-scope; §5.5 `NF-040`).
- Auto-selection of variant based on demographic attribute — explicitly prohibited (PRD §13.10 F-090).
- Wearable trend tiles for provider review — Phase 2 (`F-200`, `F-211`).
- Population-health and care-gap tiles — Phase 3 (`F-170`, `F-171`).
- In-visit interrupting popups / non-emergency alert modals (PRD §5.5 `NF-042`).
- Symptom triage tile (`F-121`) — gated on clinical / legal / AI-governance sign-off.

## Dependencies

- Identity, Authentication & Account Recovery epic (session + RBAC claims).
- Family Accounts & Proxy Lifecycle epic (account-switcher affordance, proxy-view audit hooks).
- Domain services for Appointments, Messaging, Results, Medications, Billing (read-only home summaries).
- Notifications & Channel Preferences epic (`F-070`).
- Privacy & Consent epic (sensitive-category gating on tiles, `F-095`, `NF-038`).
- Content service for curated tiles, plain-language summaries, contextual help (`F-022`, `F-193`).
- Feature-flag / kill-switch capability (PRD §5.2 `NF-029g`).
- Status page + degraded-mode UX components (PRD §4.1 `F-075`, `F-076`; §5.2 `NF-029d`).
- Independent accessibility audit vendor (PRD §5.1 `NF-010`).
- Multi-language launch content (PRD §10 decision 14; `A-036`).
- Trusted-clinic branding assets (`F-191`).

## Stakeholders / Reviewers

- Owner: Patient Experience Team product owner
- Product: HealthConnect Product lead
- Engineering: Web, iOS, Android, Experience API / BFF, SRE
- Compliance / Regulatory: Privacy Officer, Compliance, Legal
- QA: QA lead, independent accessibility audit vendor
- Other reviewers: CISO, Clinical Informatics, Health Equity lead, Design/UX lead, Domain leads for Appointments / Messaging / Results / Medications / Billing / Notifications / Proxy, Localization / Translation Governance lead

## Notes and Links

- Source PRD: [context (ingestion)/prd.md](../../context%20(ingestion)/prd.md)
- Key PRD sections: §1, §2.1 (BO-1, BO-2, BO-3, BO-6), §3.1 personas, §4.1 Dashboard (`F-090`), §4.1 Notifications/Errors (`F-070`–`F-076`), §5.1 Accessibility (`NF-010`–`NF-017`), §5.2 Performance (`NF-026`–`NF-029g`), §5.4 Sensitive-category (`NF-038`), §5.5 AI (`NF-040`, `NF-042`), §5.7 Patient Safety (`NF-061`), §5.8 Equity (`NF-072`), §5.10 Observability (`NF-080a`, `NF-080b`, `NF-080e`), §5.11 Content (`NF-081`, `NF-082`), §6.2 Architecture, §7.1–7.3 Metrics, §8 risks R-REG-01 / R-ORG-03, §13.10 Acceptance Criteria for F-090, §13.8 degraded-mode acceptance, §15 Testing Strategy.
- Architecture diagrams: PRD §6.2 logical architecture — Experience APIs (BFF) + domain services.
- Related epics / stories:
  - Identity, Authentication & Account Recovery (upstream)
  - Family Accounts, Proxy Lifecycle & Patient-Visible Audit Log (account switcher + audit)
  - Secure Messaging, Lab Results, Self-Service Scheduling, Prescription Management, Consolidated Billing (provide the tile data)
  - Notifications, Channel Preferences & Anti-Phishing Safeguards (push deep-links land here)
  - Privacy, Sharing & Consent (gates sensitive-category tiles)
  - WCAG 2.1 AA Accessibility & Equity-at-Launch Program (shared audit + remediation)
- Additional references: WCAG 2.1 AA, OCR online-tracking guidance, NIST 800-63-3 (session/cookie hardening), market analysis on portal home patterns.

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Every numeric target, regulatory requirement, and security control must cite the source PRD section it derives from.
- Keep the YAML frontmatter and narrative sections in sync — planning tools read the frontmatter; humans read the body.
