# Benefits-Navigator — TASKS.md

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Backlog for **Benefits-Navigator** (slug: `benefits-navigator`), an openly-licensed corpus of
**plain-language, primary-source-cited, multilingual, accessible** guides to public-assistance
programs — delivered as a static site, printable PDFs, and structured data, with an *optional*
retrieval-grounded explainer. It is **information, not legal/benefits advice**; it never makes an
individualized eligibility determination; it always routes people to the official application and free
human help. See `PLAN.md` for full context.

This is a **HIGH risk-tier** project: any task that states an eligibility rule, threshold, document
requirement, application step, or program fact requires **credentialed benefits-reviewer sign-off**
(public-benefits attorney / certified benefits counselor) before content ships; immigration/
public-charge content additionally requires **immigration-attorney sign-off**. **No partner,
reviewer, or requestor is yet secured**, so delivery-dependent tasks carry `requestor: TO BE SECURED`
and `verifiedNeed: false`.

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against `packages/schema/src/schemas.ts`.
Field mapping:

- **id** — stable slug `benefits-navigator-<area>-NNN` (e.g. `benefits-navigator-policy-001`).
- **title** — the task title in the milestone table.
- **project** — `benefits-navigator`.
- **type** — one of `code | research | writing | data | design-spec | maintenance`.
- **lane** — `donated` (default; no funded tasks planned. Any `funded` task must add `fundedBudgetUsd`
  with a hard cap).
- **priority** — `high | medium | low`.
- **domain** — array, e.g. `["civic","public-benefits","social-services","plain-language","accessibility"]`.
- **riskTier** — `low | medium | high`. Any program-fact/eligibility/threshold/application content is
  `high`; immigration content is `high` (double-gated); translation/accessibility of HIGH content is
  `high`/`medium`; pure schema/site/infra is `low`.
- **urgent** — boolean (no urgent tasks at cold-start).
- **deliverable** — `pr | dataset | document | translation`.
- **tokenEstimate** — `small | medium | large` (maps to the Size column).
- **status** — `open | in-progress | review | delivered | done` (all start `open`).
- **context / objective / acceptanceCriteria[] / resources[] / output** — per task.
- **requestor** — partner/steward/reviewer; `TO BE SECURED` where unknown.
- **verifiedNeed** — `true` only once a specific partner/need is confirmed; otherwise `false`
  (currently `false` everywhere — no partner secured).
- **outputLicense** — code: `MIT`; content/data/translations: `CC-BY-4.0` (CC0 under governance review).

Size legend: small ≈ tokenEstimate `small`, med ≈ `medium`, large ≈ `large`.
Reviewer "Expert (benefits)" = credentialed public-benefits attorney and/or certified benefits
counselor/navigator (**TO BE SECURED**). "Expert (immigration)" = immigration attorney / accredited
representative (**TO BE SECURED**).

---

## Milestone M0 — Foundations, policy & selection (cold-start)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| benefits-navigator-selection-000 | Pilot jurisdiction (state) + flagship program(s) selection, scored against explicit criteria — gates M1–M6 | research | small | medium | document | — | Maintainer + Expert (benefits) |
| benefits-navigator-policy-001 | Not-advice / refusal policy specification (no individualized determinations, no fraud/structuring, no immigration legal advice, route-to-human) | design-spec | medium | high | document | — | Expert (benefits) + Red-team reviewer |
| benefits-navigator-schema-002 | Content frontmatter schema + structured program/eligibility-factor data model + CI schema validation | code | medium | low | pr | — | Maintainer |
| benefits-navigator-style-003 | Plain-language style guide + fixed "information, not advice / only the agency decides / get free help" framing + readability targets | design-spec | small | medium | document | — | Plain-language reviewer + Expert (benefits) |
| benefits-navigator-sourcing-004 | Source-vetting + provenance protocol (primary-source citation, reuse-terms verification, `lastVerified`/`validUntil`) | design-spec | small | medium | document | 002 | Maintainer + Expert (benefits) |
| benefits-navigator-repo-005 | Monorepo + pnpm + TS/ESM + CI (build/lint/schema-validate) skeleton | code | small | low | pr | — | Maintainer |

**Acceptance criteria — key tasks**

- **benefits-navigator-selection-000** (jurisdiction + program selection)
  - Scores candidates against explicit criteria: (1) non-federal source reuse is clean/safely
    summarizable; (2) high need + large take-up gap for the program; (3) an available credentialed
    reviewer for that state+program; (4) manageable rule complexity (e.g., SNAP's federally-structured
    rules over Medicaid's expansion/waiver variation); (5) a plausible pilot partner in that geography.
  - Records the decision (or shortlist + the fixed 2026-08-31 deadline) with rationale; the chosen
    jurisdiction+program become dependencies for M1 source/content tasks.
  - The *specific* jurisdiction remains `TO BE SECURED` until confirmed, but the decision rule and
    deadline are fixed; this task gates M1–M6 sequencing.

- **benefits-navigator-policy-001** (not-advice / refusal policy spec)
  - Enumerates the refused-use set in concrete, testable terms: individualized eligibility
    determinations; benefit-amount promises ("you'll get $X"); income/asset/household **structuring**
    or "how to qualify" coaching; **concealment/fraud** (hiding income/assets from an agency);
    **immigration legal advice** / individualized public-charge analysis; **application filling/
    submission**; any autonomous action on a person's behalf.
  - Defines allowed categories (explain a program, general eligibility *factors*, how to apply, what
    documents are typically needed, where to get free human help) and the information-not-advice,
    non-partisan, "only the agency decides" framing.
  - Specifies the three enforcement points (intent classification, injected `NOT_ADVICE_SYSTEM` policy,
    independent output screening), a **fail-closed** default (ambiguous → refuse-and-route-to-human),
    quantified false-negative targets (**0** for individualized-determination + fraud; **< 1%**
    overall), and **corpus-only** generation with no-source-no-claim.
  - Defines the refusal/redirect behavior: refuse the offending part, explain plainly, and emit a
    correct official-application link **and** a free-human-help pointer (navigator/legal aid/211; for
    immigration, qualified counsel/accredited rep).
  - Defines the adversarial test taxonomy the red-team suite must cover, **including** cumulative-intent
    decomposition, reframing/euphemism, and prompt-injection, with a minimum number of cases per
    refused category.
  - Mandates the persistent not-advice labeling, the credentialed-reviewer gate, and the
    immigration-attorney gate for immigration content.
  - Reviewed and signed off by a credentialed benefits expert (recorded in the reviewers ledger).

- **benefits-navigator-schema-002** (content + data schema)
  - Typed frontmatter schema per guide: program, jurisdiction, audience, plain-language summary,
    eligibility **factors** (described, not a determination), how-to-apply steps, documents, pitfalls,
    `officialApplicationUrl`, `freeHelpPointers[]`, and a `citations[]` array with provenance fields.
  - Structured program/eligibility-factor data model with `lastVerified`/`validUntil` on every sourced
    figure; CI fails on schema-invalid content or any claim missing a citation.
  - Schema enforces presence of an official-application link **and** ≥ 1 free-help pointer on every
    guide (the route-to-human coverage gate).

- **benefits-navigator-style-003** (style guide + framing)
  - Encodes reading-level targets (grade ≤ 6–8; never publish above grade 10) and concrete
    sentence/word/structure rules; specifies the fixed not-advice + non-partisan framing block that
    every guide and answer must carry verbatim.

**M0 Definition of Done:** content + data schemas merged with CI validation (citation + route-to-human
gates enforced); not-advice/refusal policy spec **expert-reviewed**; plain-language style guide + fixed
framing; source-vetting/provenance protocol defined; TS/ESM skeleton + green CI; **pilot jurisdiction +
flagship program(s) selected (or shortlisted with the fixed 2026-08-31 decision)** so M1 builds against
the right corpus and reviewer profile.

---

## Milestone M1 — First program, first jurisdiction (expert-gated) + provenance

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| benefits-navigator-sources-006 | Vet + record sources for the flagship program in the pilot jurisdiction (reuse terms + provenance) | data | medium | high | dataset | 000, 004 | Expert (benefits) + Maintainer |
| benefits-navigator-provenance-007 | Provenance + citation-coverage enforcement ("no source, no claim") + staleness fail-safe (`lastVerified`/`validUntil`) | code | medium | medium | pr | 002, 006 | Maintainer |
| benefits-navigator-guide-008 | Flagship program guide (e.g. SNAP) for the pilot jurisdiction — structured data + plain-language guide, cited, expert-reviewed | writing | large | high | document | 001, 003, 006, 007 | Expert (benefits) |
| benefits-navigator-eval-009 | Minimal grounded-vs-blank-slate eval as an early go/no-go kill-gate for the optional explainer (handful of fixtures) | code | small | medium | pr | 007, 008 | Maintainer |

**Acceptance criteria — key tasks**

- **benefits-navigator-sources-006** (source vetting + provenance)
  - Reuse terms verified and recorded per source: federal works treated as public domain (17 U.S.C.
    §105, cited not copied); every non-federal/state source's reuse terms verified before enabling.
  - Provenance recorded per source (name, jurisdiction, citation/section, retrieval date, URL,
    reuse-status note, `lastVerified`, `validUntil`).
  - Expert sign-off recorded before sources are enabled for content.

- **benefits-navigator-provenance-007** (citation coverage + staleness)
  - No guide claim renders without an attached `Source` (citation-coverage test).
  - Each `Source` carries `lastVerified` + `validUntil`; at render/serve time a claim past `validUntil`
    is **auto-flagged or withheld** (withheld for high-severity numeric figures) until re-verified and
    **re-signed-off**; a staleness test asserts no claim serves as current past its window.

- **benefits-navigator-guide-008** (flagship program guide)
  - Covers, in plain language: what the program is; who it is *generally* for (factors, **not** an
    individualized determination); what it provides; how to apply; documents typically needed; common
    pitfalls; the **official application link**; and **free human help** pointers.
  - Every factual claim (including every threshold/figure) carries a primary-source citation; reading
    level meets the grade target; the fixed not-advice + non-partisan framing is present.
  - Contains **no** "you qualify / you'll get $X" language and **no** structuring/"how to qualify"
    guidance; **expert sign-off recorded** before it ships (immigration-attorney sign-off if any
    non-citizen-eligibility content is included).

- **benefits-navigator-eval-009** (minimal kill-gate)
  - Runs benefits questions retrieval-grounded+cited vs. blank-slate on a small fixture set; reports the
    delta as an early **go/no-go** for the explainer; asserts grounded answers emit **zero** invented
    eligibility numbers. If grounded+cited does not at least trend ahead, the explainer is **deferred**
    (guides + data remain the product) rather than forced.

**M1 Definition of Done:** flagship program sources vetted + provenance recorded; citation-coverage +
staleness fail-safe implemented and tested; the flagship guide drafted, **primary-source-cited**, and
**expert-signed-off**, with route-to-human + official-application coverage passing; the minimal
grounded-vs-blank-slate kill-gate run, with an explicit go/no-go recorded for the optional explainer.

---

## Milestone M2 — Plain-language, accessibility & multilingual

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| benefits-navigator-readability-010 | Automated readability gate (multi-formula) + plain-language reviewer workflow | code | small | medium | pr | 003, 008 | Plain-language reviewer + Maintainer |
| benefits-navigator-a11y-011 | Accessibility conformance (WCAG 2.2 AA) for guide rendering + site shell + PDF reading order | code | medium | medium | pr | 008 | Maintainer + Plain-language reviewer |
| benefits-navigator-i18n-012 | Translation workflow + first reviewed translation of the flagship guide (high-need language) | translation | medium | high | translation | 008, 010 | Translation reviewer + Expert (benefits) |
| benefits-navigator-programs-013 | 2–3 additional flagship program guides for the pilot jurisdiction (cited, expert-reviewed) | writing | large | high | document | 007, 008 | Expert (benefits) |

**Acceptance criteria — key tasks**

- **benefits-navigator-readability-010** (readability gate)
  - CI computes reading level (multiple formulas) and **blocks** any guide above the grade target
    (≤ 8; never above 10); a plain-language reviewer signs off before publication.

- **benefits-navigator-i18n-012** (translation workflow + first translation)
  - Workflow allows machine translation as a **draft only**; publication requires a **qualified
    bilingual reviewer** sign-off (recorded in the per-language reviewer ledger).
  - The translated guide preserves citations, the not-advice framing, and the route-to-human pointers;
    benefits terminology checked by the bilingual reviewer; benefits-accuracy confirmed against the
    source guide.

- **benefits-navigator-programs-013** (additional flagship programs)
  - Each new program guide meets the same bar as the flagship: primary-source-cited, reading-level
    compliant, route-to-human coverage, **expert-signed-off**, no determination/structuring content;
    immigration-attorney sign-off where non-citizen eligibility is addressed.

**M2 Definition of Done:** readability gate enforced (≥ 90% of guides at grade ≤ 8); WCAG 2.2 AA met on
the flagship guide + site shell + PDFs; translation workflow live with ≥ 1 reviewer-approved
translation; 2–3 additional flagship programs drafted, cited, and expert-signed-off.

---

## Milestone M3 — Delivery + optional explainer (policy-gated)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| benefits-navigator-site-014 | Accessible static site + printable PDF handouts + structured-data export (no accounts, no PII, no tracking) | code | medium | medium | pr | 011, 012, 013 | Maintainer + Plain-language reviewer |
| benefits-navigator-help-015 | "Find free help" pointers (211 / legal aid / agency lines) integrated without collecting PII | code | small | medium | pr | 014 | Maintainer + Expert (benefits) |
| benefits-navigator-explainer-016 | Optional retrieval-grounded explainer (corpus-only) behind the not-advice policy — ships only if eval passes | code | large | high | pr | 001, 007, 009 | Red-team reviewer + Expert (benefits) |
| benefits-navigator-redteam-017 | Not-advice/fraud/immigration red-team suite wired into CI (build fails on bypass or missing redirect) | code | medium | high | pr | 001, 016 | Red-team reviewer |

**Acceptance criteria — key tasks**

- **benefits-navigator-site-014** (delivery)
  - Renders the corpus as an accessible (WCAG 2.2 AA), offline-friendly, low-bandwidth site; generates
    print-ready plain-language PDF handouts; exports the structured data for reuse.
  - **No accounts, no PII fields, no profiling/tracking analytics**; privacy review confirms
    zero-PII/trackless delivery.

- **benefits-navigator-explainer-016** (optional explainer)
  - Answers **only** from the vetted corpus, cites it, carries the not-advice framing + route-to-human
    pointer, and **never invents** thresholds/amounts/eligibility rules (no-source-no-claim; output
    screen rejects un-cited numbers).
  - Mounted behind the not-advice policy layer (fail-closed; refused intents never reach generation);
    stateless/trackless; instructed never to request/retain personal details.
  - **Ships only if** the eval (009 + full eval-018) shows grounded+cited beats blank-slate; otherwise
    the milestone ships **guides + PDFs + data only** and the explainer is explicitly deferred.

- **benefits-navigator-redteam-017** (red-team suite)
  - Covers every refused category from the policy spec with **≥ 8 cases each** (multiple phrasings +
    injection) **plus** cumulative-intent decomposition and reframing/euphemism attacks.
  - Runs in CI; a bypass **or** a missing/incorrect route-to-human redirect **fails the build**; suite
    size is non-decreasing; new bypass vectors become regression cases within one release.
  - Reports the metric as **refused/total at version N** with a per-version changelog; target 100%
    refused/redirected, 0 known bypass; 0 individualized-determination or fraud false negatives.

**M3 Definition of Done:** accessible site + printable PDFs + structured-data export shipped with zero
PII / no tracking; "find free help" pointers integrated privately; **either** the explainer ships behind
the not-advice policy with the red-team suite green **or** it is explicitly deferred with guides + data
shipped regardless.

---

## Milestone M4 — Eval, hardening & pilot readiness

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| benefits-navigator-eval-018 | Full grounded-vs-blank-slate eval (accuracy/groundedness/fit; zero invented numbers) — full version of eval-009 | code | medium | medium | pr | 009, 016 | Maintainer + Expert (benefits) |
| benefits-navigator-hardening-019 | Hardening: staleness automation vs. annual update points, expanded red-team, a11y/PDF/privacy verification + pilot runbook | code | medium | high | pr | 007, 014, 017 | Red-team reviewer + Maintainer |

**Acceptance criteria — key tasks**

- **benefits-navigator-eval-018** (full eval)
  - Runs the explainer (if built) grounded+cited vs. blank-slate on fixtures; LLM judge scores
    accuracy, groundedness/citation, and fit; asserts zero invented eligibility numbers; reports the
    delta. Grounded+cited must clearly beat blank-slate or the explainer is withheld.

- **benefits-navigator-hardening-019** (hardening + pilot readiness)
  - Staleness re-verification automation tied to the real update points (HHS poverty guidelines in
    January; SNAP COLA in October) verified; expanded red-team still 100% refused/redirected;
    WCAG 2.2 AA + offline PDF + zero-PII verified end-to-end; pilot onboarding + distribution runbook
    written (for libraries/food banks/navigators).

**M4 Definition of Done:** full eval reported (explainer ships only if it passes); expanded red-team
green; staleness automation verified; accessibility + offline + privacy verified; pilot-ready with an
onboarding/distribution runbook.

---

## Milestone M5 — Pilot adoption & handoff (the deed)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| benefits-navigator-pilot-020 | Secure pilot partner/steward + independent not-advice audit + expert sign-off of shipped content | research | medium | high | document | 018, 019 | Steward + Expert (benefits) + Red-team reviewer |
| benefits-navigator-handoff-021 | Pilot adoption: partner/navigator uses the guides to help real people (outcome recorded) | maintenance | medium | high | document | 020 | Steward + Expert (benefits) |

**Acceptance criteria — key tasks**

- **benefits-navigator-pilot-020** (secure pilot + audits)
  - A real partner (legal-aid org / anti-hunger network / library system / 211 / community action
    agency) is secured; steward assigned; `verifiedNeed` flips to `true`.
  - An independent reviewer audits not-advice + route-to-human behavior; all shipped content has
    recorded expert sign-off (immigration content attorney-signed); translations reviewed; zero-PII
    confirmed.
  - Driven by the **dated partner-acquisition plan** (jurisdiction/program by 2026-08-31, reviewer by
    2026-10-31, partner by 2026-12-31). If no partner is secured by **~2027-03-31**, apply the
    **build-vs-mothball/pivot rule** (PLAN exec summary): contribute the vetted corpus to an existing
    benefits-info commons / hand it to a library/social-work program as a reference resource, or
    mothball to maintenance-only — recorded in governance — rather than publish to no real beneficiary.

- **benefits-navigator-handoff-021** (closed loop — the deed)
  - The pilot partner/navigator demonstrably uses the guides to help real people understand/access a
    program; ≥ 1 outcome is recorded (a person helped, or a navigator's verified time-saved /
    fewer-wrong-applications result), with the partner's attestation.
  - Not-advice framing + route-to-human upheld throughout; figures current (no stale claims served).

**M5 Definition of Done:** project-level **Definition of Shipped** met — a real partner adopts the
guides and uses them to help real people, with not-advice/refusals independently verified, shipped
content expert-signed-off, translations reviewed, accessibility met, zero PII, and ≥ 1 beneficiary
outcome recorded. *(Gated on a secured partner — TO BE SECURED.)*

---

## Milestone M6 — Sustain & scale (post-delivery)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| benefits-navigator-ops-022 | Ops runbook + outcome tracking + maintenance rotation + annual re-verification cadence + gated expansion process | maintenance | medium | medium | document | 021 | Maintainer + Steward |

**Acceptance criteria — benefits-navigator-ops-022**
- Runbook covers deploy, content updates, source re-verification, translation re-review, and partner
  support.
- Outcome tracking records people helped / navigator time-saved / fewer wrong applications (not page
  views); annual re-verification cadence tied to poverty-guideline (January) + SNAP COLA (October)
  update points, enforced by the staleness fail-safe.
- Named maintenance rotation; documented, **expert-gated** process for adding programs, jurisdictions,
  and languages.

**M6 Definition of Done:** project sustainably maintained with beneficiary outcomes tracked, a rotation
owning it, an annual legal-content re-verification cadence, and a gated expansion process.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
|---|---|---|---|---|---|---|
| benefits-navigator-program-023 | Additional program packs (Medicaid/CHIP, WIC, LIHEAP, SSI, housing, EITC, Lifeline/ACP) | writing | large | high | document | Sequence after flagship; Medicaid's expansion/waiver complexity gated on a strong reviewer |
| benefits-navigator-jurisdiction-024 | Second jurisdiction (state) content pack | data | large | high | dataset | Only after M6; full source-vetting + expert sign-off |
| benefits-navigator-languages-025 | Additional languages for the flagship guides | translation | medium | high | translation | Prioritize highest-need / lowest-take-up populations; per-language review |
| benefits-navigator-public-charge-026 | Dedicated public-charge / non-citizen-eligibility explainer | writing | medium | high | document | Immigration-attorney sign-off mandatory; neutral, current, route-to-counsel |
| benefits-navigator-doc-helper-027 | "Documents you may need" interactive checklist (informational, no PII stored) | code | small | medium | pr | Client-side only; never stores answers; not a determination |
| benefits-navigator-print-028 | Print-ready bilingual one-page handouts for walk-in distribution | design-spec | small | medium | document | For food banks/libraries; derived from cited content |

---

## Generated task index

The Elyos CLI executes the machine-readable `tasks/*.json` files (validated against
`packages/schema`), not this `TASKS.md`. Every backlog row above now has a corresponding
schema-valid `tasks/<id>.json`. All 29 task files validate clean (`filename == id`, no
duplicates, no extra keys).

**Authoring notes**
- **`type` vs. `deliverable` for translation rows.** `translation` is a *deliverable*, not a
  schema `type`. The i18n/languages rows (`benefits-navigator-i18n-012`,
  `benefits-navigator-languages-025`) are encoded as `type: "writing"` + `deliverable: "translation"`.
- **Defaults (per "How these tasks map to Elyos").** Every task is `lane: donated`,
  `status: open`, `urgent: false`, `verifiedNeed: false`, `requestor: "TO BE SECURED"` (no partner,
  reviewer, or requestor is yet secured). `outputLicense` is `MIT` for code/`pr` deliverables and
  `CC-BY-4.0` for content/data/document/translation deliverables.
- **No fan-out — representative tasks only.** No dimension in `PLAN.md`/`TASKS.md` is concretely
  enumerated: the pilot jurisdiction, flagship program(s), additional programs, second jurisdiction,
  and translation languages are all open-ended / `TO BE SECURED`. Per the bounded fan-out policy,
  template rows (`-programs-013`, `-program-023`, `-jurisdiction-024`, `-languages-025`,
  `-i18n-012`) are kept as **one representative task each**; they expand to per-item tasks only once
  the jurisdiction/program/language set is confirmed. No languages, programs, jurisdictions, or
  beneficiaries were fabricated.
- **Guardrails preserved.** HIGH risk-tier framing is carried verbatim into the relevant tasks:
  credentialed benefits-reviewer sign-off for any eligibility/threshold/application content;
  immigration-attorney sign-off for public-charge / non-citizen-eligibility content
  (`-guide-008`, `-programs-013`, `-public-charge-026`); the not-advice / refusal policy
  (`-policy-001`) and its executable enforcement (`-explainer-016`, `-redteam-017`). No task
  authors refused content (no individualized determinations, no fraud/structuring coaching, no
  immigration legal advice) — those remain refusal/guardrail tasks.

**Index (id — milestone):**

- M0: `benefits-navigator-selection-000`, `benefits-navigator-policy-001` (seed),
  `benefits-navigator-schema-002`, `benefits-navigator-style-003`,
  `benefits-navigator-sourcing-004`, `benefits-navigator-repo-005`
- M1: `benefits-navigator-sources-006`, `benefits-navigator-provenance-007`,
  `benefits-navigator-guide-008`, `benefits-navigator-eval-009`
- M2: `benefits-navigator-readability-010`, `benefits-navigator-a11y-011`,
  `benefits-navigator-i18n-012`, `benefits-navigator-programs-013`
- M3: `benefits-navigator-site-014`, `benefits-navigator-help-015`,
  `benefits-navigator-explainer-016`, `benefits-navigator-redteam-017`
- M4: `benefits-navigator-eval-018`, `benefits-navigator-hardening-019`
- M5: `benefits-navigator-pilot-020`, `benefits-navigator-handoff-021`
- M6: `benefits-navigator-ops-022`
- Backlog/future: `benefits-navigator-program-023`, `benefits-navigator-jurisdiction-024`,
  `benefits-navigator-languages-025`, `benefits-navigator-public-charge-026`,
  `benefits-navigator-doc-helper-027`, `benefits-navigator-print-028`

---

## Example task JSON

Complete, schema-valid Task JSON for the first M0 build item (`benefits-navigator-policy-001`):

```json
{
  "id": "benefits-navigator-policy-001",
  "title": "Not-advice / refusal policy specification (no individualized determinations, no fraud/structuring, no immigration legal advice, route-to-human)",
  "project": "benefits-navigator",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["civic", "public-benefits", "social-services", "plain-language", "accessibility"],
  "riskTier": "high",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "Benefits-Navigator produces plain-language, primary-source-cited, multilingual, accessible guides to public-assistance programs (SNAP, Medicaid/CHIP, WIC, TANF, LIHEAP, SSI, housing, EITC, Lifeline/ACP). It is a HIGH risk-tier project: benefits eligibility is high-stakes, and wrong or over-reaching information can cause a person to forgo benefits they are entitled to, waste a determination window, incur an overpayment, or - most seriously for immigrant families - avoid care out of misplaced fear. The project is therefore engineered to refuse both misuse and over-reach: it never makes an individualized eligibility determination, never advises how to structure income/assets or conceal information to qualify (benefits fraud), and never gives immigration legal advice. It is information, not advice, and it always routes the person to the official application and to free human help. This cold-start task specifies that not-advice/refusal policy before any guide or interactive feature is built. No partner, credentialed reviewer, or requestor is yet secured.",
  "objective": "Write the authoritative not-advice / refusal policy specification that all later content and the optional retrieval-grounded explainer must implement and be tested against: the information-not-advice and non-partisan framing, the concrete refused-use set, the allowed categories, the three enforcement points (intent classification, injected NOT_ADVICE_SYSTEM policy, independent output screening), the fail-closed default, the corpus-only no-source-no-claim rule, the refusal/route-to-human behavior, the adversarial test taxonomy, and the credentialed-reviewer and immigration-attorney gates.",
  "acceptanceCriteria": [
    "Enumerates the refused-use set in concrete, testable terms: individualized eligibility determinations; benefit-amount promises ('you'll get $X'); income/asset/household structuring or 'how to qualify' coaching; concealment/fraud (hiding income/assets from an agency); immigration legal advice / individualized public-charge analysis; application filling/submission; and any autonomous action on a person's behalf",
    "Defines the allowed categories (explain a program, general eligibility factors, how to apply, documents typically needed, where to get free human help) and the information-not-advice, non-partisan, 'only the agency decides' framing",
    "Specifies three enforcement points - input intent classification, injected NOT_ADVICE_SYSTEM policy, and independent output screening - with server-side, injection-resistant enforcement that user/document content cannot override, plus corpus-only generation and a no-source-no-claim rule that rejects un-cited eligibility numbers",
    "Sets a fail-closed default (ambiguous/low-confidence intent -> refuse-and-route-to-human) and quantified false-negative targets (0 for individualized-determination and fraud categories; < 1% overall on the red-team suite)",
    "Defines the refusal/redirect behavior: refuse the offending part, explain plainly, and emit a correct official-application link AND a free-human-help pointer (navigator/legal aid/211; for immigration, qualified counsel/accredited representative)",
    "Defines the adversarial test taxonomy the red-team suite must cover - multiple phrasings + prompt-injection per refused category, plus cumulative-intent decomposition and reframing/euphemism attacks - with a minimum number of cases per category and a 100%-refused/redirected, zero-bypass target",
    "Mandates the persistent 'information, not legal/benefits advice' labeling, the credentialed benefits-reviewer sign-off gate, and the immigration-attorney sign-off gate for any immigration/public-charge content",
    "Reviewed and signed off by a credentialed public-benefits attorney and/or certified benefits counselor (recorded in the reviewers ledger)"
  ],
  "resources": [
    "planning/projects/benefits-navigator/PLAN.md",
    "CLAUDE.md",
    "docs/good-deed-definition.md",
    "packages/schema/src/schemas.ts",
    "planning/projects/public-official-guide/PLAN.md"
  ],
  "output": "A reviewed policy-specification document (the not-advice / refusal charter) defining the refused-use set, allowed categories, three enforcement points, fail-closed default, corpus-only no-source-no-claim rule, refusal/route-to-human behavior, adversarial test taxonomy, and review/labeling gates - the contract that benefits-navigator-explainer-016 (explainer) and benefits-navigator-redteam-017 (red-team suite) implement and verify.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```
