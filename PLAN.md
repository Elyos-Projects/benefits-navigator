# Benefits-Navigator — PLAN.md

> Status: Draft · Version: 0.2.0 · Last updated: 2026-06-29 · Owner: TBD (maintainer) · Lane: donated

Plain-language, openly-licensed guides to public-assistance programs — what each program is, who it
is generally for, what it provides, how to apply, and where to get free human help — written at a low
reading level, translated, accessible, and grounded in **primary, official sources**. It is
**information, not legal or benefits advice**, and it never determines whether a specific person
qualifies. Its single defining behavior is to **explain the program and then hand the person to the
official application and a real human navigator/legal-aid line** for their individual situation.

**Positioning.** Eligible people miss benefits they are entitled to because the rules are fragmented,
jargon-heavy, written above their reading level, and rarely in their language. Benefits-Navigator
closes that *information* gap — and only that gap. It is deliberately **not** an eligibility engine,
not an application filler, and not an advisor. The constraint *is* the product: a tool that promised
to tell you whether you qualify, or how to qualify, would be both wrong (only the agency determines
eligibility) and dangerous (it would invite gaming, false reassurance, and chilling effects). What it
promises instead — accurate, plain, sourced, current explanation plus a warm hand-off to real help —
is exactly what the beneficiary population is missing and what no agency PDF reliably provides.

---

## Executive summary

Tens of millions of people are eligible for public-assistance programs — SNAP (food assistance),
Medicaid/CHIP, WIC, TANF, LIHEAP (energy help), SSI, housing assistance, the EITC, school meals,
Lifeline/ACP, and unemployment insurance — and do not receive them. The reasons are well documented:
program rules are split across federal statute/regulation, state administration, and county practice;
official materials are written far above the reading level of the people who need them; information is
rarely available in the languages those people speak; and fear (especially around immigration and the
"public charge" rule) deters eligible families. The result is a measurable **take-up gap** that leaves
food, healthcare, and rent assistance unclaimed, and a parallel harm of *wrong* applications that waste
a scarce, stressed person's time and end in denial.

Benefits-Navigator produces a corpus of **plain-language, primary-source-cited, multilingual,
accessible guides** to these programs — delivered as an open static site, printable PDFs for libraries
and food banks, structured machine-readable data others can reuse, and an *optional*
retrieval-grounded explainer that answers questions **only** from the vetted corpus. Every guide and
answer is framed as information, routes the person to the official application and to free human help
(navigators, legal aid, 211), and is re-verified on a cadence because thresholds and rules change
every year.

This is a **HIGH risk-tier** project. Benefits eligibility is high-stakes: a wrong claim can cause
someone to forgo benefits they are entitled to, waste a benefits-determination window, trigger an
overpayment they must repay, or — most seriously for immigrant families — avoid care out of misplaced
fear. Therefore the project is **engineered to refuse misuse and to refuse over-reach**: it will not
make individualized eligibility determinations, will not advise anyone on how to structure income or
assets to qualify (benefits fraud), will not help conceal information from an agency, and will not give
immigration legal advice. No program content ships without sign-off by a **credentialed reviewer** — a
public-benefits attorney (legal aid) and/or a certified benefits counselor/navigator, plus an
immigration attorney for any public-charge-adjacent content — and every factual claim is cited to
primary, official sources with a recorded verification date and an expiry.

Honesty note: **no partner organization, navigator network, or requestor is yet secured.** Every
delivery-dependent task is marked `TO BE SECURED` with `verifiedNeed: false`. The project is not
"shipped" on merge; it is shipped only when a real partner uses the guides with real people and an
outcome is recorded (a person helped to understand/access a program, or a navigator's verified
time-saved / fewer-wrong-applications result), with the not-advice framing and refusals independently
verified.

**Partner-acquisition plan (dated) and a build-vs-mothball/pivot decision rule.** Outreach is
time-boxed against the build, not left open-ended: by **2026-08-31** the pilot jurisdiction (one
U.S. state) and flagship program(s) are selected (criteria in *Open questions*) and ≥ 3 candidate
partners are in active conversation (a legal-aid organization, a food-bank/anti-hunger network, a
public library system, a United Way / 211, or a community action agency); by **2026-10-31** a
credentialed benefits reviewer is secured (gates M1 content) and an immigration attorney identified
for any public-charge content; by **2026-12-31** a pilot partner/steward is secured (gates M5).
**Decision rule:** if no credentialed reviewer is secured by the M1 content entry date, content work
holds at the platform/schema stage (M0) — no HIGH-tier guide ships unreviewed. If no pilot partner is
secured by **~2027-03-31** (≈ M4 completion), the project does **not** publish to no one: it either
(a) **pivots** the last-mile beneficiary — e.g., contribute the vetted corpus to an existing public
benefits-information commons or hand it to a library/social-work program as a reference resource — or
(b) **mothballs** to maintenance-only (archived, no further HIGH-tier content), with the decision
recorded in governance. The vetted single-jurisdiction corpus is a valuable reference artifact either
way.

---

## Problem & beneficiaries

**Who is helped (directly):** low-income and vulnerable people trying to understand and access
public-assistance programs — families with children, older adults, people with disabilities, people
experiencing or at risk of homelessness, students, immigrants in mixed-status families, people with
limited English proficiency, and people with low literacy. Equally direct beneficiaries are the
**frontline helpers** who serve them and are themselves under-resourced: benefits navigators, social
workers, food-bank and pantry staff, public librarians, community health workers, and legal-aid
paralegals, who need accurate, plain, current explainers and printable handouts in multiple languages.

**Who is helped (ultimately):** the households who, with clearer information and a faster route to
real help, claim food, healthcare, energy, and rent assistance they are entitled to — and who avoid
wasted, failed applications.

**The need.** Public-assistance programs combine a federal baseline (statute + regulation, e.g.
SNAP under 7 CFR; Medicaid under 42 CFR; SSI under 20 CFR) with **state administration and state
options** and, often, **county-level practice**. Eligibility rules, income thresholds, and required
documents change at known annual points (federal poverty guidelines, SNAP cost-of-living adjustments)
**but also repeatedly mid-year** — and 2025–2027 is an exceptional period of churn, not a once-a-year
refresh: the One Big Beautiful Bill Act (OBBBA, signed 2025-07-04) rewrote SNAP and Medicaid work
requirements with **staggered effective dates** (immigrant-eligibility restrictions effective
2026-10-01; Medicaid work requirements / 6-month redeterminations effective 2026-12-31 / 2027-01-01),
and a DHS public-charge NPRM is **pending** (published 2025-11-17, comments closed 2025-12-19) with the
2022 rule still in effect. A guide written mid-2026 that does not carry these effective dates is
actively dangerous, so the currency machinery (below) treats re-verification as **event-driven and
effective-date-aware**, not merely "at least annual." Authoritative information exists
— on federal agency sites (USDA FNS, CMS, SSA, HHS/ACF, HUD, IRS, FCC), Benefits.gov, USA.gov, and
state agency portals — but it is fragmented, written well above an accessible reading level, rarely
multilingual, and almost never assembled into "here is the program, here is who it is generally for,
here is how to apply, and here is the free human help near you." The take-up gap and the
wrong-application harm both follow directly from this information gap.

**Verified need / partner:** **TO BE SECURED.** No specific legal-aid org, anti-hunger network,
library system, 211/United Way, or community action agency has yet agreed to adopt or co-develop the
guides, and no individual requestor has been confirmed. Target partner profiles to pursue: a
legal-aid organization with a public-benefits practice (for credentialed review and last-mile reach);
a food-bank/anti-hunger network or community action agency (distribution to households); a public
library system (a trusted, walk-in access point); a United Way / 211 (referral integration). Until one
is secured, the project builds the content schema, the not-advice/refusal policy, the source-vetting
protocol, and **one flagship program in one jurisdiction** as a reviewed exemplar, and marks all
delivery/adoption work `TO BE SECURED` with `verifiedNeed: false`. Outreach is **dated** (see the
partner-acquisition plan above), and a **build-vs-mothball/pivot decision rule** governs date slips
so the project never ships to no real beneficiary.

---

## Competitive landscape & differentiation

The space splits into archetypes — **eligibility screeners / application assisters**, **resource
directories / referral networks**, **benefit-management utilities**, and **official program
sources** — and, critically, **none of them is an openly-licensed, primary-source-cited,
currency-tracked plain-language *explainer* corpus.** They screen, route, transact, or publish
official-but-inaccessible text. The unoccupied niche is the **explanation layer**, and
Benefits-Navigator is built to occupy exactly it (web-researched detail and citations in
`COMPETITIVE-ANALYSIS.md`).

- **Code for America / GetCalFresh (the sharpest comparison).** The gold standard for human-centered
  SNAP *application assistance* (helped millions of households access food assistance; now hands off
  to CA's BenefitsCal). It is an **application funnel**, in practice **single-program, single-state**,
  and its content is **not** an openly-licensed, citation-per-claim, reusable corpus. We **explain;
  they apply** — we are the upstream understanding layer that can route *into* tools like GetCalFresh
  rather than replace them.
- **findhelp (formerly Aunt Bertha) / 211.** The dominant social-care **directory** (programs by ZIP;
  powers parts of 211). It **lists organizations, it does not explain program rules** in plain,
  sourced language, and its data is closed/variable-currency. Complementary: we explain the program →
  hand to findhelp/211 for the local human.
- **mRelief (and other screeners — Single Stop, Benefits.gov/USA.gov finder).** A national SNAP
  **screener** ("likely eligible?") — precisely the act Benefits-Navigator **refuses**. It is a
  natural **partner/complement**, not a content competitor; we route *to* it, never replace its
  determination function.
- **Benefit-management utilities (e.g. Propel) and official sources (USDA FNS, CMS, state portals).**
  Manage existing benefits or publish authoritative-but-inaccessible text respectively — potential
  **distribution partners and primary-source inputs**, not explainer competitors. (Take-up context
  validates the need: USDA estimates ~88% of eligible people received SNAP in FY2022 — and SNAP is the
  *high*-take-up program; EITC, Lifeline, and TANF are far worse.)

**The differentiator (the moat).** An **openly-licensed, primary-source-cited, currency-guaranteed,
plain-language EXPLAINER layer with zero PII and a measured route-to-human guarantee** — trustworthy,
reusable, always-current explanation in a market where everyone else screens, lists, transacts, or
publishes inaccessible official text. The defining constraint — **we never determine eligibility** — is
not a limitation but **the moat**: it is what makes the corpus safe to consult anonymously,
non-chilling for immigrant families, and **embeddable inside findhelp / 211 / Code-for-America-style
flows** ("what is this program" beside "where to get it" / "am I likely eligible"). We win not by
out-UXing any single incumbent but on **coverage + sourcing + reuse + currency**, with depth-first
discipline (one jurisdiction + flagship program first).

---

## Goals and non-goals

**Goals**

- Produce accurate, **plain-language** (target reading grade ≤ 6–8) guides to flagship
  public-assistance programs that explain *what the program is, who it is generally for, what it
  provides, how to apply, what documents are typically needed, and where to get free human help*.
- Ground every factual claim in **primary, official sources** (federal statute/regulation, federal
  agency guidance, state agency rules), with a recorded verification date and an expiry.
- Make the guides **accessible** (WCAG 2.2 AA) and **multilingual**, with per-language qualified
  review, prioritizing the languages of the highest-need, lowest-take-up populations.
- Always **route the person to the official application and to free human help** (navigator / legal
  aid / 211) for their individual situation — the project's ethical differentiator, held to a coverage
  metric, not a footer.
- Build a **not-advice / refusal layer** that provably refuses individualized eligibility
  determinations, benefits-gaming/fraud requests, and immigration legal advice — verified by an
  adversarial red-team suite.
- Keep the project **privacy-by-construction**: it asks for and stores **no** personal benefits data
  about anyone; any interactive feature is stateless and trackless.
- Prove (via an eval) that retrieval-grounded, cited answers beat blank-slate LLM output on accuracy
  and groundedness for benefits questions — and ship the explainer **only** if they do.

**Non-goals (constraints that define the project)**

- **Not an eligibility determination.** It never tells a specific person whether they qualify, how
  much they would receive, or that they will be approved/denied. Only the administering agency
  determines eligibility.
- **Not benefits/legal advice and not a substitute for a navigator, legal aid, or the agency.**
- **Not an application filler or submitter.** It does not complete, sign, or submit applications, and
  takes no action on anyone's behalf.
- **Not an income/asset-structuring or "how to qualify" tool.** It will not advise anyone how to
  arrange finances, household, or disclosures to obtain benefits, and will not help conceal
  information from an agency (benefits fraud).
- **Not immigration legal advice.** Public-charge and immigration-status questions are routed to a
  qualified immigration attorney / accredited representative; the project does not opine on an
  individual's immigration consequences.
- **Not partisan or advocacy.** It describes programs as the law defines them; it does not argue for
  expanding, cutting, or reforming any program, and does not editorialize about "welfare."
- **Not a PII collector.** No accounts, no stored household/income/immigration data, no profiling
  analytics.
- **Not a 50-state, all-programs database at launch.** Depth and verified accuracy for one
  jurisdiction and a few flagship programs first; breadth later, and never breadth without review.

---

## Success metrics (outcomes)

Outcome-centric and beneficiary-first. Page views, sessions, and downloads are **explicitly not**
success metrics on their own.

| Metric | Baseline | Target (pilot) | How measured |
|---|---|---|---|
| Factual claims cited to a primary/official source | none | 100% of shipped claims carry a primary-source citation | Citation-coverage test + reviewer checklist |
| Credentialed expert sign-off before content ships | none | 100% of HIGH-tier guides have recorded sign-off | Governance / reviewers ledger |
| Reading level of published guides | n/a | ≥ 90% of guides at grade ≤ 8 (target ≤ 6); 0 published above grade 10 | Automated readability check (multiple formulas) + plain-language reviewer |
| "Route-to-human + official-application" coverage | n/a | 100% of guides **and** explainer answers include a correct official-application link **and** a free-human-help pointer (navigator/legal aid/211) | Coverage test on every guide/answer + reviewer spot-check |
| Refusal rate on the not-advice/fraud/immigration red-team suite | none | reported as **refused/total at version N** with a per-version changelog; **≥ 8 cases per refused category** (multiple phrasings + injection); 100% refused/redirected; 0 known bypass | Automated adversarial eval in CI + reviewer audit |
| Stale-content containment | n/a | 0 claims served past their `validUntil` **or past a recorded `effectiveDate`/`pendingChange` boundary** without an auto-flag/withhold and re-verification | Staleness test against `lastVerified`/`validUntil`/`effectiveDate`; runtime audit |
| Beneficiary comprehension (pilot) | n/a | moderated comprehension testing with real beneficiaries shows they understood the program and could act (not just a readability score) | Moderated comprehension session with the pilot partner |
| Translation review coverage | n/a | 100% of published translations reviewed by a qualified bilingual reviewer (no machine-only translations published) | Translation review ledger |
| Accessibility | n/a | core guides + site meet WCAG 2.2 AA | Automated + manual a11y audit |
| PII footprint | n/a | **zero** personal benefits data collected or stored; any interactive feature is stateless/trackless | Privacy review + storage/analytics audit |
| Retrieval-grounded vs. blank-slate accuracy delta (if explainer ships) | n/a | grounded+cited clearly beats blank-slate on accuracy + groundedness, **and** never invents eligibility numbers | LLM-judge eval harness + reviewer audit |
| Beneficiary outcome (Definition of Shipped) | 0 | a partner/navigator uses the guides with real people and **≥ 1 attested outcome** is recorded (a person helped to understand/access a program, or a navigator's verified time-saved / fewer-wrong-applications) | Partner-attested outcome log |

The **defining success outcome** (Definition of Shipped): a real partner organization or navigator
adopts the guides and demonstrably uses them to help real people understand or access a program — with
the not-advice framing and refusals independently verified, all shipped content expert-signed-off and
primary-source-cited, translations reviewed, accessibility met, and zero PII collected.

---

## Scope

**In scope**

- A **content corpus** of plain-language program guides: per program (and, where it matters, per
  pilot jurisdiction), a structured guide covering: what the program is; who it is *generally* for
  (eligibility *factors* described, not an individualized determination); what it provides; how to
  apply; documents typically needed; common pitfalls; and **where to get free human help**.
- A **machine-readable structured layer** (program/eligibility-factor data with citations,
  `lastVerified`, `validUntil`) that the guides render from and that others can reuse.
- A **plain-language style guide** and an automated **readability gate**.
- A **multilingual pipeline** with per-language qualified human review (no machine-only publication).
- An **accessibility** standard (WCAG 2.2 AA) for the corpus and delivery.
- A **not-advice / refusal policy layer** and an adversarial **red-team suite** (individualized
  determinations, fraud/gaming, immigration legal advice, autonomous action).
- A **source-vetting + provenance + staleness** subsystem (primary-source citation required; expiry
  and re-verification enforced at runtime).
- **Delivery surfaces:** an open static site, **printable PDFs** (for libraries/food banks/offline),
  and the structured data export.
- An **optional** retrieval-grounded explainer that answers **only** from the vetted corpus, ships
  only if the eval proves it beats blank-slate, and is held to the same not-advice/route-to-human
  guarantees.
- An **eval harness** proving grounded+cited beats blank-slate, with a kill-gate.

**Out of scope (explicitly will NOT do)**

- **Individualized eligibility determinations**, benefit-amount calculations presented as a personal
  result, or any "you qualify / you don't / you'll get $X" output.
- **Application filling, signing, submission, or any autonomous action** on a person's behalf.
- **Income/asset/household structuring advice**, "how to qualify" coaching, or anything that helps a
  person obtain benefits they are not entitled to or **conceal information** from an agency.
- **Immigration legal advice**, individualized public-charge analysis, or any opinion on a specific
  person's immigration consequences (routed to a qualified immigration attorney / accredited rep).
- **Collecting or storing PII** — income, household, immigration status, SSNs, case numbers — or any
  profiling/tracking analytics.
- **Advocacy or partisan content** for or against any program, policy, party, or candidate.
- **Free-form LLM generation** of program facts: the optional explainer answers only from the vetted,
  cited corpus and never invents thresholds, amounts, or eligibility rules.
- **50-state / all-programs breadth at launch**, or any unreviewed jurisdiction/program content.

When a request falls in the refused set (e.g., "do I qualify?", "how do I hide income to get SNAP?",
"will applying hurt my green card?"), the tool refuses *that* part, explains why in plain terms, and
**redirects to the right human**: the official application/agency, a benefits navigator or legal-aid
line, 211, or — for immigration questions — a qualified immigration attorney / accredited
representative. **The route-to-human redirect is the project's ethical differentiator**, held to a
coverage metric (see *Success metrics*): a guide or answer that fails to emit a correct
official-application link **and** a free-human-help pointer is a defect, the same as a bypass.

---

## Solution approach & architecture

This is **content-first** (the guides are the deliverable), with a thin, reusable delivery layer and an
optional, tightly-constrained AI explainer mounted behind the not-advice policy.

**Stack.** TypeScript, ESM, pnpm workspaces (Elyos convention). Content authored as **Markdown +
typed frontmatter** validated against a JSON Schema; structured program/eligibility data as **JSON/YAML**
validated in CI. Static-site delivery (e.g., Astro or Next.js static export) for an accessible,
offline-friendly, low-bandwidth site; **PDF generation** for print handouts. Anthropic Claude (model
selection and pricing per the Claude API skill) used **only** behind a thin provider-neutral LLM
client for (a) authoring drafts that humans then verify and (b) the optional retrieval-grounded
explainer — never as the source of program facts. Content license **CC-BY-4.0** (CC0 considered — open
question); code **MIT**.

**Components**

1. **Content schema + style guide (`schema/`, `style/`) — built first.** A typed frontmatter schema
   for each guide (program, jurisdiction, audience, plain-language summary, eligibility *factors*,
   how-to-apply steps, documents, pitfalls, official-application link, free-human-help pointers, and a
   citations array) and a structured program/eligibility-factor data model. The schema makes two
   2025–2027 realities first-class:
   - **Effective-dating, not just expiry.** Beyond `validUntil` ("re-check by"), each sourced fact may
     carry **`effectiveDate`**, **`pendingChange`** (a known future change with its date and a
     not-yet-law flag), and **`supersededBy`** (a pointer to the version/claim that replaces it). This
     lets a guide say *"this is the rule today; it changes on `<date>`"* — the dominant failure mode
     given OBBBA's staggered effective dates and the pending public-charge NPRM, which plain `validUntil`
     cannot express.
   - **Jurisdiction tiering + rule-source flag.** `jurisdiction` supports a **county/admin-region tier**,
     and each fact carries a **`federal-floor` vs `state-option` vs `local-practice` flag** so a guide
     can mark which rules are mandatory federal floors vs. state options vs. county practice (SNAP as the
     flagship mitigates but does not remove sub-state variation).

   The plain-language style guide encodes reading-level targets, sentence/word rules, a fixed **"this is
   information, not advice — only the agency decides; here is how to get free help"** framing that every
   guide and answer must carry, and the **borderline-case calibration corpus** (below) that draws the
   line between an allowed *general conditional rule* and a forbidden *individualized determination*.

2. **Not-advice / refusal policy layer (`lib/policy`) — a safety subsystem, not a disclaimer.**
   Applies to the optional explainer and to any interactive feature. Three enforcement points:
   - *Intent classification*: tags requests against a taxonomy — allowed (explain a program, general
     factors, how to apply, where to get help) vs. refused (individualized determination, benefit-amount
     promise, income/asset structuring, fraud/concealment, immigration legal advice, application
     filling, autonomous action). Refused intents never reach generation. **Fail-closed**: ambiguous or
     low-confidence intent defaults to **refuse-and-route-to-human**; under-answering is the safe error,
     over-promising the dangerous one. Safety target: individualized-determination and fraud false
     negatives **0** on the red-team suite; overall refused-category false-negative rate **< 1%**.
     The boundary is hardest at the seam where it is most tempting to cross — *conditional explanations*
     a navigator would give ("households with a member over 60 or disabled often don't face the
     asset/gross-income test") sit one step from a forbidden individualized determination. To keep the
     classifier and reviewers from disagreeing case-by-case (which would either over-refuse useful
     general information or leak determinations), the project ships a **labeled borderline-case
     calibration corpus** (an M0/M1 artifact of ~50 worked phrasings, each labeled *allowed general
     conditional rule* vs. *forbidden individualized application*, with the reasoning). This corpus is a
     single shared source of truth that **feeds the classifier, the style guide, and reviewer training**
     so the information-vs-determination line is drawn the same way everywhere, and it grows as new
     borderline cases surface.
   - *System policy*: a `NOT_ADVICE_SYSTEM` charter injected into every explainer prompt establishing
     information-not-advice framing, "only the agency determines eligibility", non-partisanship, the
     corpus-only constraint (answer **only** from retrieved vetted content, cite it, and never invent
     numbers), and the mandatory route-to-human + official-application pointer.
   - *Output screening*: an **independent** post-generation screen for individualized-determination
     language ("you qualify", "you'll get $…"), un-cited numeric claims, fraud/structuring content, and
     immigration-legal-advice leakage — defense-in-depth on the assumption the classifier will
     occasionally miss. Flags block delivery and route to a review queue. Refusals/flags are logged
     **without** storing the user's text or any PII.

3. **Source-vetting, provenance & staleness (`lib/sources`).** Each factual claim is backed by a
   `Source` record (official source name, jurisdiction, citation/section, retrieval date, URL,
   reuse-status note). No guide claim renders without an attached source (citation-coverage test). Each
   `Source` carries **`lastVerified`** and **`validUntil`**, and — per component 1 — may carry
   **`effectiveDate` / `pendingChange` / `supersededBy`** so a claim that is *currently true but about
   to change on a known date* is modeled explicitly rather than silently going stale. Review intervals
   are **event-driven, not merely annual**: re-verification fires at the known annual points (federal
   poverty guidelines in January, SNAP COLA in October) **and** on every recorded statutory/regulatory
   effective date (e.g., OBBBA's 2026-10-01 / 2026-12-31 / 2027-01-01 milestones) and pending-rule event
   (e.g., the public-charge NPRM), with policy-waiver-dependent claims on a shorter cadence. Because
   officials can disagree, the protocol records a **source-hierarchy and conflict-resolution rule**
   (statute/regulation > federal agency guidance > state rule > state-portal explainer); when sources
   conflict, the reviewer records which governs. **Staleness is fail-safe:** at render/serve time, a
   claim past its `validUntil`, **past an `effectiveDate`/`pendingChange` boundary**, or `supersededBy`
   a newer claim is **auto-flagged** ("this figure may be out of date — verify on the official site") or
   **withheld** for high-severity numeric claims, and routed to re-verification; it cannot return to
   normal service until re-verified and **re-signed-off**.

4. **Plain-language + accessibility + i18n pipeline (`lib/content`).** A readability gate (multiple
   formulas + reviewer judgment) blocks guides above the grade target; an accessibility check enforces
   WCAG 2.2 AA (headings, contrast, link text, alt text, reading order in PDFs); a translation workflow
   produces per-language versions that **must** pass qualified bilingual review before publication
   (machine translation may draft, never publish).

5. **Delivery (`apps/site`, `scripts/pdf`).** An accessible, offline-friendly static site rendering
   from the structured corpus; printable, plain-language **PDF handouts** for walk-in distribution; and
   a structured-data export for reuse. No accounts, no PII, no profiling analytics.

6. **Optional retrieval-grounded explainer (`lib/explainer`).** Retrieval over the vetted corpus only;
   answers cite the corpus, carry the not-advice framing and route-to-human pointer, and are screened
   as above. Ships **only** if the eval (below) proves grounded+cited beats blank-slate; otherwise the
   project ships guides + structured data and defers the explainer.

7. **Eval harness (`scripts/eval-grounded.ts`).** Runs benefits questions retrieval-grounded+cited vs.
   blank-slate on fixture scenarios; an LLM judge scores accuracy, groundedness/citation, and fit, with
   a hard assertion that grounded answers never emit invented eligibility numbers. A **minimal** version
   runs as an early kill-gate before heavy content investment; the full version gates the explainer.

**LLM (Claude) leverage — assistive only, never the source of truth.** Claude sits behind the
provider-neutral LLM client and is used **only** for work a credentialed human then verifies:

- **Drafting plain-language rule explainers from official sources** — compressing dense CFR/agency text
  into grade-6 prose in the fixed structure (what it is / who it's generally for / what it provides /
  how to apply / documents / pitfalls / get help). Highest-ROI use: it turns "thousands of pages of
  regulations" into **reviewable drafts the credentialed reviewer signs off**.
- **Structuring state-variation and provenance** — extracting a program's **federal floor vs.
  state options vs. local practice** into the schema, attaching candidate citations, and flagging where
  a state portal diverges from federal rule (a triage layer for the reviewer, mapped to the
  jurisdiction-tier and `federal-floor`/`state-option` flags above).
- **Plain-language + readability iteration and translation drafts** (for bilingual-reviewer sign-off,
  never machine-only publication); generating "what to bring" checklists.
- **Adversarial red-team generation** — producing the ≥ 8-per-category misuse phrasings (determination,
  structuring/fraud, immigration, injection, euphemism, decomposition) and borderline cases.
- **Staleness diff worklists** — given a new poverty-guideline table or an OBBBA/NPRM provision, drafting
  the diff against existing guides and surfacing every affected claim as a **re-verification worklist for
  the reviewer** (high value given 2025–2027 churn).
- **The corpus-only retrieval explainer** — only if the eval proves grounded+cited beats blank-slate and
  never invents numbers.

**Where the model must NOT go (release gates, not guidelines):** no individualized eligibility
determination ("you qualify / you'll get $X"); no legal/benefits/immigration advice (route to counsel);
**no fabricated rules, thresholds, or amounts** — all program facts come from the cited corpus, never
the model's parametric memory (which cannot reliably know the current COLA or OBBBA effective dates);
no "how to qualify"/structuring/concealment coaching; **flag-and-link to official screeners
(mRelief/GetCalFresh/the state app) and human help, never substitute for them**; no PII solicitation or
retention. Currency and state-correctness are the model's blind spots — the corpus + provenance +
staleness layer exists precisely to keep the model on a leash. (Model IDs, pricing, prompt-caching, and
token-counting: defer to the Claude API skill when implementing the LLM client and eval harness.)

**Key decisions (locked)**

- **Content-first, AI-assisted, human-verified.** The guides are the product; Claude assists authoring
  and (optionally) answers from the corpus, but is **never** the authority on program facts.
- **The not-advice/route-to-human guarantee is a tested subsystem and a release gate**, not a footer.
- **Privacy-by-construction:** there is no user data model to misuse — no PII is collected or stored.
- **Depth-first:** one jurisdiction + a few flagship programs, expert-reviewed, before any breadth.
- **Agent-neutral core:** any Anthropic/Claude specifics sit behind the LLM client (Elyos core/adapter
  rule); the corpus and schema are vendor-neutral.

---

## Data, licensing & compliance

**Source material.** Primary, official sources only: federal statute and regulation (e.g., SNAP — 7
U.S.C. §2011 et seq. / 7 CFR 273; Medicaid/CHIP — 42 CFR; SSI — 20 CFR 416; TANF/LIHEAP — HHS/ACF
rules; housing — HUD; EITC — IRS; Lifeline/ACP — FCC), federal agency program pages and guidance (USDA
FNS, CMS, SSA, HHS/ACF, HUD, IRS, FCC), the federal aggregators **Benefits.gov** and **USA.gov**, the
annually-published **HHS Federal Poverty Guidelines**, and **state agency** rules/portals for the
pilot jurisdiction. Plain-language and accessibility practice follow **plainlanguage.gov** and CDC
clear-communication guidance.

**Licensing / reuse.** U.S. **federal government works are in the public domain** (17 U.S.C. §105), so
federal program facts and figures may be summarized and cited freely (we still **cite and link**, and
do not imply government endorsement). **State and local** materials vary — some states assert copyright
in compiled codes or portal content — so **every non-federal source's reuse terms are verified and
recorded before its content ships**. We summarize and cite primary law; we do not copy proprietary
annotations or portal text. Agency **logos, seals, and names** are not used in any way implying
endorsement or official status.

**Provenance model.** Each claim → a `Source` record (source, jurisdiction, citation/section,
retrieval date, URL, reuse-status note, `lastVerified`, `validUntil`, and where relevant
`effectiveDate` / `pendingChange` / `supersededBy`). When official sources conflict, the recorded
**source-hierarchy** (statute/regulation > federal agency guidance > state rule > state-portal
explainer) and the reviewer's note fix which governs. The renderer and the explainer may not surface a
claim without an attached source; a citation-coverage test enforces it.

**Staleness is fail-safe, not best-effort** (see *Solution approach* §3): claims past `validUntil`,
past an `effectiveDate`/`pendingChange` boundary, or `supersededBy` a newer claim are auto-flagged or
withheld and re-verified + re-signed-off before returning to service. This makes the dominant failure
modes — *the threshold/rule changed and the guide silently went stale*, and *a known future change
(e.g., OBBBA's 2026–2027 effective dates) arrived unannounced* — visible, gated events.
Re-verification is **event-driven, not just calendar-driven**: the **annual update points** (poverty
guidelines in January, SNAP COLA in October), **plus** every recorded effective date and pending-rule
milestone, plus ad-hoc on known policy changes.

**Output licensing.** Content/guides/data: **CC-BY-4.0** (CC0 considered to maximize reuse by other
navigators and benefits-info commons — open question for governance). Code: **MIT**. Translations:
CC-BY-4.0, with translator credit (with consent).

**Privacy / PII stance (conservative — privacy-by-construction).** The single most important privacy
fact: **the project collects and stores no personal benefits data about anyone.** There are **no
accounts**, no income/household/immigration/SSN/case-number fields, and no profiling or
behavior-tracking analytics. Any interactive feature (the optional explainer, any "find help" lookup)
is **stateless and trackless** — questions are not stored, and the explainer is instructed never to
ask for or retain personal details and to remind users not to share SSNs or case numbers. Refusal/flag
logs record the reason/category only, never the user's text or any PII. No secrets, tokens, or PII are
written to logs, receipts, or committed files (Elyos rule). This stance is doubly important because the
beneficiary population is vulnerable and because immigration-related fear is itself a barrier — the
tool must be obviously safe to consult anonymously.

**Attribution & non-partisanship.** Guides cite and link primary sources; redistribution preserves
attribution per CC-BY. Content describes programs **as the law defines them**, neutrally, with no
advocacy for or against any program or policy and no partisan framing. Expert reviewers and
translators are credited (with consent) in a ledger.

---

## Quality, review & risk gates

**Risk tier: HIGH** across the benefits-content surface (per `docs/good-deed-definition.md`: legal/
benefits/safety domains require credentialed expert sign-off before merge). Pure platform/schema/site
infra is low–medium; **any guide that states an eligibility rule, threshold, document requirement,
application step, or program fact is HIGH**; immigration/public-charge-adjacent content is HIGH and
additionally gated on an immigration attorney.

**Required reviews before a deed is "done":**

- **Maintainer** review on all PRs (engineering/content quality, agent-neutral core, no PII/secrets in
  logs, tests/CI green, citations present).
- **Credentialed benefits reviewer sign-off** — a public-benefits attorney (legal aid) and/or a
  certified benefits counselor/navigator for the program + jurisdiction — recorded before *any* program
  content ships. **No reviewer, no ship.**
- **Immigration-attorney sign-off** for any content touching immigration status, eligibility of
  non-citizens, or public charge.
- **Not-advice / red-team review** — the adversarial misuse suite (individualized determinations,
  fraud/gaming, immigration legal advice, autonomous action) passes in CI **and** a reviewer audits
  refusal + route-to-human behavior before the policy layer or the explainer is released.
- **Plain-language + accessibility review** — readability gate passed (grade target) and WCAG 2.2 AA
  verified.
- **Translation review** — qualified bilingual reviewer sign-off per language (no machine-only
  publication).
- **Privacy review** — confirms zero PII collection/storage and trackless delivery.

**Every guide and answer carries the fixed framing:** "This is general information, **not** legal or
benefits advice. Only the agency decides if you qualify. Here is the official application and free help
near you." A guide/answer missing the official-application link **or** the free-human-help pointer
fails the coverage gate.

**Definition of Shipped (project):** a real partner/navigator adopts the guides and demonstrably uses
them to help real people understand/access a program, with: not-advice framing + refusals independently
verified; all shipped content expert-signed-off and primary-source-cited (immigration content also
attorney-signed); translations reviewed; WCAG 2.2 AA met; staleness fail-safe in force; and zero PII
collected — with at least one beneficiary outcome recorded.

---

## Roadmap & milestones

Phased: schema + policy + source-vetting first; one flagship program in one jurisdiction, reviewed,
before any breadth; delivery + optional explainer behind the policy; pilot adoption last and gated on a
secured partner.

- **M0 — Foundations, policy & selection (cold-start).**
  *Goal:* the content schema, the not-advice/refusal policy, the source-vetting protocol, and a
  decision on what to build first exist before any guide is written.
  *Exit:* content frontmatter + structured-data JSON Schemas merged with CI validation — **including
  `effectiveDate`/`pendingChange`/`supersededBy` fields, a county/admin-region jurisdiction tier, and a
  `federal-floor`/`state-option`/`local-practice` flag**; plain-language style guide + fixed not-advice
  framing; not-advice/refusal policy spec **reviewed by a credentialed benefits expert**, with the seed
  **borderline-case calibration corpus (~50 labeled phrasings)** feeding the classifier, style guide,
  and reviewer training; source-vetting + provenance protocol defined **with a source-hierarchy +
  conflict-resolution rule**; repo/pnpm/CI (build/lint/schema-validate) skeleton green; **pilot
  jurisdiction (one state) + flagship program(s) selected** against explicit criteria so M1 builds
  against a real corpus and reviewer profile.

- **M1 — First program, first jurisdiction (expert-gated exemplar) + provenance.**
  *Goal:* one flagship program guide for the pilot jurisdiction, fully sourced and reviewed, plus the
  provenance/staleness machinery.
  *Exit:* source-vetting done + provenance records for the flagship program (with source-hierarchy
  applied where sources conflict); structured eligibility-factor data + the rendered plain-language
  guide drafted, **primary-source-cited**, and **expert-signed-off**; **any known future change carried
  as `effectiveDate`/`pendingChange`** ("rule today; changes on `<date>`"); citation-coverage +
  effective-date-aware staleness fail-safe implemented and tested; route-to-human + official-application
  coverage gate passing; **for any immigration-adjacent content, an "accurate-but-non-chilling" standard
  applied** (state current law, mark proposals as not-yet-law, avoid both false alarm and false
  reassurance, route to counsel), attorney-reviewed. **Kill-gate:** a **minimal grounded-vs-blank-slate eval**
  on a handful of fixtures runs as an early go/no-go for the optional explainer — if grounded+cited does
  not at least trend ahead (and stay free of invented numbers), the explainer is deferred, not forced.

- **M2 — Plain-language, accessibility & multilingual.**
  *Goal:* the quality gates that make the content usable by the actual beneficiaries.
  *Exit:* readability gate enforced (≥ 90% of guides at grade ≤ 8); WCAG 2.2 AA met on the flagship
  guide + site shell; translation workflow live with **≥ 1 reviewed translation** of the flagship guide
  in a high-need language; **first oral/visual modalities for low-literacy + LEP users** (plain-language
  audio and/or iconography/flowcharts plus a "what to bring" checklist, since grade-6 prose alone does
  not reach everyone); 2–3 additional flagship programs drafted + expert-reviewed for the pilot
  jurisdiction.

- **M3 — Delivery + optional explainer (policy-gated).**
  *Goal:* get the content into people's hands and (only if proven) add Q&A.
  *Exit:* accessible static site + printable PDF handouts + structured-data export shipped — **every
  PDF/print artifact stamped with a content version, a "verify-after" date, and a short URL to the live
  page** so an offline copy declares its own currency; "find free help" pointers (211 / legal aid /
  agency lines) integrated **without** collecting PII; **if** the M1 kill-gate and the full eval pass,
  the retrieval-grounded explainer ships behind the not-advice
  policy with the red-team suite green; otherwise the explainer is explicitly deferred and the milestone
  ships guides + data only.

- **M4 — Eval, hardening & pilot readiness.**
  *Goal:* prove quality and harden for real, vulnerable users.
  *Exit:* full grounded-vs-blank-slate eval reported; expanded not-advice/fraud/immigration red-team
  green (100% refused/redirected); staleness automation verified against the annual-update points
  **and recorded effective dates**; a **"monitored-sources" change-watch** (FNS/CMS/IRS/state-portal
  pages + Federal Register for rules like the public-charge NPRM) opens re-verification tasks
  automatically when a watched source changes (currency goes event-driven, not calendar-only); an
  **errata/retraction runbook** defines how a discovered error is withdrawn, who is notified, and how
  downstream PDFs/translations are flagged as superseded; accessibility + offline PDF + privacy
  (zero-PII) verified end-to-end; pilot onboarding + distribution runbook ready.

- **M5 — Pilot adoption & handoff (the deed).**
  *Goal:* a real partner uses the guides with real people.
  *Exit (Definition of Shipped):* a secured partner/navigator uses the guides to help real people
  understand/access a program; not-advice framing + refusals independently verified; shipped content
  expert-signed-off (immigration content attorney-signed); translations reviewed; **moderated
  beneficiary comprehension testing** confirms people understood and could act (beyond readability
  scores); ≥ 1 beneficiary outcome recorded. *(Gated on a secured partner — TO BE SECURED.)*

- **M6 — Sustain & scale (post-delivery).**
  *Goal:* durable maintenance and careful expansion.
  *Exit:* maintenance rotation + ops runbook + an **event-driven re-verification cadence** tied to the
  poverty-guideline/COLA update points, recorded effective dates, and the monitored-sources change-watch
  (not calendar-only); outcome tracking (not page views); a documented, expert-gated process for adding
  programs/jurisdictions and languages; **an embeddable open-data layer / MCP server** exposing the
  vetted corpus (explainers + structured eligibility-factor data + citations + currency metadata, with
  the not-advice guardrails enforced server-side) so findhelp/211/library/CfA-style tools can surface
  "what is this program" beside their listings/flows.

Dependencies flow M0 → M1 → M2 → M3 → M4 → M5 → M6. The **jurisdiction + flagship-program decision is
made in M0 and gates M1–M6** (it fixes the source corpus, source-reuse legality, and reviewer profile);
M1 content blocks on the secured credentialed reviewer; immigration content blocks on a secured
immigration attorney; the explainer blocks on the eval kill-gate; M5 blocks on a secured partner.

---

## Work breakdown

The itemized, schema-mapped backlog lives in **`TASKS.md`**: ~19 tasks across M0–M6 plus a future
backlog, each mapped to the Elyos Task JSON schema, with per-task acceptance criteria for the most
important items, milestone Definitions of Done, and a complete example Task JSON for the first M0 task
(the not-advice / refusal policy specification). The first build items are the **content schema +
style guide**, the **not-advice/refusal policy spec**, and the **jurisdiction/program selection** —
reflecting that the framing and the corpus choice gate everything downstream — followed by a single
**expert-reviewed flagship program exemplar** before any breadth.

---

## Governance, roles & stakeholders

- **Maintainer (Owner): TBD.** Owns the schema, the agent-neutral core, CI, content-quality gates, and
  merge quality.
- **Reviewers / rotation:** at least one engineering/content reviewer plus a designated
  **not-advice/red-team reviewer** who audits refusal + route-to-human behavior independently of
  authors.
- **Credentialed benefits reviewers (HIGH tier): TO BE SECURED** — a public-benefits attorney (legal
  aid) and/or a certified benefits counselor/navigator for the program + pilot jurisdiction; signs off
  all program content before it ships, tracked in a reviewers ledger with credentials and consent.
- **Immigration attorney / accredited representative (HIGH tier): TO BE SECURED** — signs off any
  immigration/public-charge-adjacent content.
  - **Independence / COI:** a reviewer recuses from content where they have a material conflict.
    Sign-off is **version-scoped** — it attaches to a specific content version + citation set and does
    **not** carry forward to edits, which require re-sign-off (dovetails with the
    `lastVerified`/`validUntil` model). **Name-use limits:** a reviewer's name/credentials may appear
    in the ledger only for the versions they approved, with consent, and may not imply endorsement of
    the project as a whole. **Disagreement fallback:** the expert holds a **veto on whether HIGH-tier
    content is accurate/safe to ship** — a maintainer cannot override a "do not ship" on substance;
    disagreements are logged and escalated to Elyos governance / a second reviewer; where a sole
    reviewer is a single point of failure, the project prefers a **second reviewer** before relying on
    contested content.
- **Plain-language / accessibility reviewer:** verifies reading-level and WCAG conformance.
- **Translation reviewers (per language): TO BE SECURED** — qualified bilingual reviewers; no
  machine-only translation is published.
- **Steward (last-mile owner): TO BE SECURED** — owns the partner relationship and the adoption that
  constitutes shipping.
- **Partner / requestor: TO BE SECURED** — legal-aid org, anti-hunger/food-bank network, library
  system, United Way/211, or community action agency.
- **Community / board:** the CC-BY-vs-CC0 license decision and edge cases go through Elyos governance.

---

## Dependencies & integrations

- **External services:** Anthropic Claude API (authoring assist + optional explainer, behind the
  neutral LLM client; models/pricing per the Claude API skill); static hosting/CDN; CI.
- **Datasets / sources:** federal program statute/regulation + agency guidance (USDA FNS, CMS, SSA,
  HHS/ACF, HUD, IRS, FCC), Benefits.gov, USA.gov, the HHS Federal Poverty Guidelines, and the pilot
  jurisdiction's state agency rules/portals — each with verified reuse terms and recorded provenance.
- **Standards/reference:** plainlanguage.gov, CDC clear-communication, WCAG 2.2 AA; 211/legal-aid
  directories for "free help" pointers.
- **Elyos pieces:** `packages/schema` (Task JSON), `CLAUDE.md` work rules + refusal guardrails,
  `docs/good-deed-definition.md` (risk tiers), Elyos governance for license/edge-case decisions; sibling
  HIGH-risk plan `planning/projects/public-official-guide/{PLAN,TASKS}.md` for house style.
- **Human/decision dependencies (critical path):** the **jurisdiction + flagship-program decision
  (M0, gates M1–M6)**; a secured **credentialed benefits reviewer** (blocks M1 content); a secured
  **immigration attorney** (blocks immigration content); a secured **pilot partner/steward** (blocks
  M5); per-language **translation reviewers** (block translation publication).

---

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Tool is read as an individualized eligibility determination | High | Critical | Not-advice/refusal layer built early; refuses "do I qualify / how much"; fixed "only the agency decides" framing on every guide/answer; route-to-human coverage gate; output screening blocks "you qualify/you'll get $X"; red-team gates CI | Red-team reviewer / Maintainer |
| Used to game eligibility / commit benefits fraud (hide income, structure assets) | Medium | Critical | Hard refusal of structuring/concealment requests with redirect to lawful application + legal aid; red-team category with ≥ 8 cases + injection; output screening for structuring/fraud content | Red-team reviewer / Expert |
| Immigration/public-charge misinformation chills eligible families | Medium | Critical | Immigration-attorney sign-off required; refuse individualized immigration analysis; route to qualified immigration counsel/accredited rep; neutral, sourced, current public-charge explainer only | Immigration attorney / Maintainer |
| Inaccurate or outdated threshold/rule (figures change annually + mid-year) | High | High | Primary-source citation required (coverage test); expert sign-off; **runtime staleness fail-safe** (`lastVerified`/`validUntil` auto-flag/withhold past review window); re-verification scheduled to poverty-guideline/COLA update points | Expert reviewer / Maintainer |
| Known future change (e.g., OBBBA 2026–2027 effective dates) arrives unannounced / silently | High | Critical | First-class **`effectiveDate`/`pendingChange`/`supersededBy`** fields ("rule today; changes on `<date>`"); effective-date-aware staleness fail-safe; **event-driven monitored-sources change-watch** (incl. Federal Register for the public-charge NPRM) opens re-verification tasks automatically | Expert reviewer / Maintainer |
| Conflicting official sources (reg vs. federal guidance vs. state portal) | Medium | High | Recorded **source-hierarchy + conflict-resolution rule** (statute/reg > federal guidance > state rule > state portal); reviewer records which governs per claim | Expert / Maintainer |
| Eligibility-vs-determination line drawn inconsistently (over-refuse useful info or leak a determination) | Medium | High | **Labeled borderline-case calibration corpus (~50 phrasings)** as single source of truth feeding classifier + style guide + reviewer training; fail-closed default; grows as new cases surface | Red-team reviewer / Expert |
| Accurate immigration content nonetheless chills eligible families | Medium | Critical | **"Accurate-but-non-chilling" content standard** (state current law, mark proposals as not-yet-law, avoid both false alarm and false reassurance, route to counsel), immigration-attorney-reviewed — a content-quality dimension distinct from the refusal layer | Immigration attorney / Maintainer |
| No partner secured → cannot reach Definition of Shipped | High | High | Honest `TO BE SECURED`/`verifiedNeed:false`; **dated partner-acquisition plan** (jurisdiction by 2026-08-31, reviewer by 2026-10-31, partner by 2026-12-31) + **build-vs-mothball/pivot rule** at ~2027-03-31 (contribute corpus to an existing benefits-info commons / library program, or mothball — rather than publish to no one) | Steward / Maintainer |
| No credentialed reviewer → content blocked | Medium | High | Recruit via legal-aid networks, benefits-counselor associations, law-school clinics; hold content at M0 platform stage; do not ship HIGH content unreviewed | Maintainer |
| Reading level too high / not actually usable by beneficiaries | Medium | High | Plain-language style guide + automated readability gate (grade target) + plain-language reviewer; user-comprehension check with the partner in pilot | Plain-language reviewer |
| Machine-translation errors mislead non-English speakers | Medium | High | Qualified bilingual review required per language; no machine-only publication; per-language reviewer ledger | Translation reviewer |
| Accidental PII collection / tracking of vulnerable users | Low | Critical | Privacy-by-construction: no accounts, no PII fields, stateless/trackless features; privacy review gate; explainer instructed never to request/retain personal details | Maintainer |
| LLM invents thresholds/eligibility numbers in the explainer | Medium | Critical | Corpus-only retrieval; no-source-no-claim; output screen rejects un-cited numbers; eval asserts zero invented eligibility numbers; explainer ships only if eval passes | Maintainer |
| Source license/copyright on state portal/compiled-code content | Medium | Medium | Federal works are PD; verify + record reuse terms for every non-federal source; summarize + cite, never copy proprietary annotations; no agency logos/endorsement | Expert / Maintainer |
| Perceived partisanship around "welfare" | Low | Medium | Strictly describe programs as law defines them; no advocacy/editorializing; non-partisan review | Maintainer / Expert |

---

## Security & privacy

**Threat surface.** Misreading the guides as an official determination (primary harm); attempts to use
any interactive feature for fraud/structuring or individualized immigration advice; prompt-injection
trying to make the explainer invent eligibility numbers or drop the not-advice framing; accidental PII
capture; supply-chain/secrets leakage. Because there is **no stored user data and no accounts**, the
classic data-breach surface is deliberately near-zero — the design choice *is* the control.

**Adversary model (the user may seek a refused outcome).** A user may want the tool to confirm they
qualify, to coach income-hiding, or to opine on their immigration case. The policy layer therefore:
re-evaluates each request on its own merits (**stateless w.r.t. accrued conversational "trust"**);
considers **cumulative intent** so a refused task decomposed into innocuous-looking sub-steps (e.g.,
"what's the income limit" + "what counts as income" + "how do I not report a gift") is still caught;
and covers **reframing/euphemism** ("optimize my household for SNAP", "structure things to qualify").
These are first-class red-team categories with their own regression cases.

**Controls.** Not-advice/refusal layer as a tested, CI-gating subsystem (top control), enforced
server-side and injection-resistant — user/document content cannot override the `NOT_ADVICE_SYSTEM`
charter. **Corpus-only** generation with no-source-no-claim and independent output screening for
"you qualify / $X" language, un-cited numbers, fraud/structuring, and immigration-legal-advice leakage.
**Privacy-by-construction:** no accounts, no PII schema, stateless/trackless features; refusal/flag
logs store category/reason only, never user text or PII. No secrets, tokens, or PII in logs, receipts,
or committed files (Elyos rule); dependency + secret scanning in CI. The explainer is instructed to
remind users not to share SSNs/case numbers and never to request them.

**Abuse/misuse prevention.** The refused set (individualized determinations, benefit-amount promises,
income/asset structuring, concealment/fraud, immigration legal advice, application filling, autonomous
action) is enforced, tested, and logged — not merely documented — and the tool never acts on anyone's
behalf.

---

## Sustainability & maintenance

After delivery, a named **maintenance rotation** owns the schema, site, and pipeline; the **steward**
owns the partner relationship and outcome tracking. Benefits content carries a **mandatory,
event-driven re-verification cadence** tied to the real update points (HHS poverty guidelines in
January; SNAP COLA in October), **every recorded `effectiveDate`/`pendingChange` milestone** (e.g.,
OBBBA's 2026–2027 dates, the pending public-charge NPRM), and a **monitored-sources change-watch** that
opens re-verification tasks when a watched official source changes — not a once-a-year refresh. It is
enforced at runtime by the `lastVerified`/`validUntil`/`effectiveDate` fail-safe so a source past its
window is **auto-flagged or withheld** until re-verified and
**re-signed-off** — stale figures cannot silently keep serving as current. Material legal updates
require fresh expert sign-off (and immigration-attorney sign-off for immigration content). Translations
are re-reviewed when the source guide changes. Outcomes are tracked with the partner (people helped to
understand/access a program; navigator time-saved / fewer wrong applications) — **not** page views. The
not-advice red-team suite is maintained as living tests and expanded as new misuse vectors appear.
Expansion to more programs, jurisdictions, or languages follows a documented, expert-gated process and
only after the first is stable.

---

## Adjacent opportunities

The defining constraint — a **reusable, openly-licensed rules-explainer with currency-tracking** — is
bigger than benefits. These are spin-offs to seed deliberately, not scope creep for v1 (benefits stays
depth-first); they are recorded so the schema and pipeline are built to generalize.

**Perpendicular (reusable engine, other domains).**

- **A shared "rules-explainer engine with currency-tracking"** — the claim → source →
  `lastVerified`/`validUntil`/`effectiveDate` schema, the readability + accessibility + i18n pipeline,
  the not-advice/refusal policy layer, the source-change watcher, and the grounded-vs-blank-slate eval —
  generalizes to **any high-stakes, frequently-changing, jurisdiction-varying rule corpus** (immigration
  procedure, tax, housing code, disability/veterans benefits, the sibling `public-official-guide`). The
  benefits corpus is its first instantiation; the engine is the durable asset.
- **An MCP server** exposing the vetted corpus as tools other agents can ground on, with the same
  not-advice guardrails enforced server-side — the open corpus as infrastructure inside other
  assistants, and a clean Elyos agent-neutral-core fit.
- **A standalone "currency-watch" service** (monitored official sources → change events →
  re-verification tasks) other civic-info projects could subscribe to.

**Parallel (same beneficiaries, adjacent content) — natural sibling projects.**

- **know-your-rights** explainers (tenant rights, due-process in benefits denials/appeals, workplace
  rights) — the same plain-language + cited + non-advice + route-to-counsel pattern.
- **community-resource-maps / food-assistance-maps** — the *local-org* layer that complements our
  *program-rules* layer; designed to **hand off to and ingest from** findhelp/211 rather than rebuild
  their directory.
- **financial-literacy-open** (EITC/CTC, banking, debt, budgeting) in the same sourced plain-language
  corpus — EITC already overlaps the benefits set.

---

## Open questions

- **Content license: CC-BY-4.0 vs CC0?** CC0 maximizes reuse by other navigators and benefits-info
  commons; CC-BY preserves attribution to primary sources and reviewers. Needs an Elyos governance
  decision. (Code: MIT.)
- **Which pilot jurisdiction (state) + flagship program(s) first? — decided in M0, gates M1–M6.**
  Selection criteria, scored before M1 content: (1) **non-federal source reuse is clean** (state
  rules/portal content reusable or safely summarizable); (2) **high need + large take-up gap** for the
  chosen program; (3) an **available credentialed reviewer** (legal aid / benefits counselor) for that
  state+program; (4) **manageable rule complexity** (e.g., SNAP's federally-structured rules are more
  tractable than Medicaid's expansion/non-expansion + waiver variation); (5) a **plausible pilot
  partner** in that geography. The specific choice is TO BE SECURED, but the **rule and the deadline
  (2026-08-31) are fixed**.
- **Ship the optional explainer at all?** Only if the eval proves grounded+cited beats blank-slate and
  never invents eligibility numbers; otherwise guides + structured data + PDFs are the product. Decided
  at the M1 kill-gate / M4 eval.
- **How are credentialed reviewers and translators compensated/credited?** Volunteer vs. a future
  funded lane (with a hard per-task budget cap) for review/translation hours, without compromising
  independence.
- **"Find free help" data:** how to point to 211 / legal-aid / agency lines accurately and currently
  **without** collecting user location as PII (e.g., user-initiated, client-side, no storage)?
- **Lane:** donated by default; is there a future funded lane for expert review/translation hours with
  a hard budget cap?
- **Public-charge content depth:** how much to cover vs. routing entirely to immigration counsel, given
  the live NPRM and the chilling-effect stakes — full attorney-reviewed, non-chilling explainer vs.
  minimal "this is changing; talk to counsel" routing?
- **Partner-vs-competitor / distribution posture:** are mRelief / Propel / findhelp / 211 / a library
  system the right *distribution* partners (not competitors) for an open explainer layer — a
  complement-not-compete posture that unlocks reach we can't build alone, and embeds our explainers
  beside their screening/listing flows? (Confirm their embed/API terms.)
- **Event-driven vs. calendar currency:** is the monitored-sources / Federal-Register change-watch in
  scope for M4, or deferred? It materially reduces stale-content risk during the 2025–2027 churn.
- **CC0 as the "infrastructure" choice:** CC0 likely maximizes embedding by findhelp/211/CfA-style
  reusers; weigh against attribution to reviewers/primary sources (ties to the license question above).
- **Comprehension instrument:** what moderated beneficiary-comprehension method does the pilot use
  beyond readability formulas (measuring whether people understood and could act)?

---

## References

- Elyos work rules & refusal guardrails: `CLAUDE.md`
- Good-deed definition & risk tiers: `docs/good-deed-definition.md`
- Task JSON schema: `packages/schema/src/schemas.ts`
- Portfolio roadmap: `planning/ROADMAP.md` (Track 10 — `benefits-navigator`)
- Sibling HIGH-risk Elyos plan for house style: `planning/projects/public-official-guide/{PLAN,TASKS}.md`
- Plain-language + accessibility: plainlanguage.gov; CDC clear communication; WCAG 2.2 AA
- Source authorities: USDA FNS (SNAP/WIC/school meals), CMS (Medicaid/CHIP), SSA (SSI), HHS/ACF
  (TANF/LIHEAP), HUD (housing), IRS (EITC), FCC (Lifeline/ACP), Benefits.gov, USA.gov, HHS Federal
  Poverty Guidelines
- Federal works are public domain: 17 U.S.C. §105

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified against the first draft and **applied** to the
PLAN and TASKS above. Each is a concrete change, not a generality.

1. **Reframed the project from "advice" to a strict information+routing service** — added an explicit
   "constraint *is* the product" positioning so the not-advice posture reads as identity, not a
   disclaimer (Positioning, Executive summary).
2. **Made "route-to-human + official-application" a measured guarantee**, with a coverage metric and a
   gate that fails a guide/answer missing either pointer — mirroring the exemplar's lawful-alternative
   redirect (Success metrics, Scope, Quality gates).
3. **Added a second credentialed reviewer track for immigration/public-charge content** (immigration
   attorney / accredited rep), recognizing it as a distinct, higher-stakes legal surface (Governance,
   Quality gates, Risks).
4. **Adopted privacy-by-construction with zero PII** (no accounts, no income/household/immigration
   fields, stateless/trackless features) — turned privacy into a structural control rather than a
   policy, and made "zero PII collected" a success metric (Data/compliance, Security & privacy).
5. **Specified the staleness fail-safe tied to real update points** (HHS poverty guidelines in
   January; SNAP COLA in October), so re-verification is calendar-anchored, not vague (Data/compliance,
   Sustainability, Risks).
6. **Required primary-source citation on every claim** with a citation-coverage test and a
   no-source-no-claim rule for both guides and the explainer (Data/compliance, Success metrics).
7. **Constrained the optional explainer to corpus-only retrieval** and made it ship **only** if an
   eval proves it beats blank-slate and never invents eligibility numbers — added a kill-gate at M1 and
   a full eval at M4 (Solution approach, Roadmap, Open questions).
8. **Added a fail-closed intent classifier** with quantified targets (0 false negatives for
   individualized-determination and fraud categories; < 1% overall) so under-answering is the safe error
   (Solution approach, Security).
9. **Defined the refused-use set in concrete, testable terms** (individualized determination,
   benefit-amount promise, structuring/concealment, immigration legal advice, application filling,
   autonomous action) for the red-team suite (Scope, Security, TASKS).
10. **Added insider/adversarial red-team categories** — cumulative-intent decomposition, reframing/
    euphemism ("optimize my household for SNAP"), and prompt-injection — with ≥ 8 cases each (Security,
    TASKS).
11. **Made the reading-level target explicit and gated** (grade ≤ 6–8; 0 published above grade 10) with
    an automated readability check plus a plain-language reviewer (Success metrics, Quality gates,
    TASKS).
12. **Required qualified bilingual review for every translation** (no machine-only publication) and a
    per-language reviewer ledger (Quality gates, Risks, TASKS).
13. **Set WCAG 2.2 AA** as a hard accessibility bar for the corpus, site, and PDFs (Success metrics,
    Quality gates).
14. **Added printable PDF handouts and a structured-data export** as first-class delivery surfaces for
    libraries/food banks and reuse — not just a website (Scope, Solution approach).
15. **Distinguished the federal/state licensing reality** — federal works PD under 17 U.S.C. §105;
    every non-federal source's reuse terms verified and recorded; no agency logos/endorsement
    (Data/compliance, Risks).
16. **Added a dated partner-acquisition plan + a build-vs-mothball/pivot decision rule** so the project
    never publishes to no real beneficiary (Executive summary, Problem, Risks).
17. **Made jurisdiction + flagship-program selection an explicit M0 decision** with scored criteria
    that gate M1–M6 (Roadmap, Open questions, TASKS).
18. **Chose SNAP as the likely flagship** on tractability grounds (federally-structured rules) and
    flagged Medicaid's expansion/waiver complexity as a reason to sequence it later (Open questions,
    TASKS).
19. **Locked non-partisanship** — describe programs as the law defines them; no advocacy/editorializing
    about "welfare" (Goals/non-goals, Data/compliance, Risks).
20. **Added version-scoped expert sign-off + COI/recusal + name-use limits + a disagreement veto**,
    aligned to the staleness model (Governance).
21. **Added a minimal eval kill-gate at M1** so heavy content investment is gated on an early thesis
    check, not discovered at M4 (Roadmap, TASKS).
22. **Made outcome metrics beneficiary-centric** (people helped to access a program; navigator
    time-saved / fewer wrong applications) and explicitly demoted page-views/downloads (Success
    metrics, Sustainability).
23. **Specified the "find free help" feature to avoid PII** (user-initiated, client-side, no stored
    location) as an open question with a privacy-preserving default (Open questions, Roadmap).
24. **Mapped every section to the Elyos schema/lane rules** — donated lane, MIT code / CC-BY content
    (CC0 as an open question), and a complete schema-valid example Task JSON in TASKS.md.
25. **Added an explainer-deferral path** so M3 ships guides + data + PDFs even if the explainer fails
    its eval — the beneficiary value does not depend on the AI feature (Roadmap, Scope).

---

## Review sign-off

**Reviewer:** senior staff engineer + TPM (self-review pass), 2026-06-28.

**Completeness:** All 17 required H2 sections are present and ordered per the spec. PLAN matches the
exemplar's depth (positioning, who-for, explicit non-goals as identity, locked decisions, stack,
phased roadmap M0–M6, constraints-as-identity). TASKS.md provides 19 schema-mapped tasks across all
milestones plus a backlog, milestone tables with the required columns, per-task acceptance criteria for
key tasks, milestone Definitions of Done, and a complete schema-valid example Task JSON.

**Correctness checks performed and resolved:**
- *Schema validity* — the example Task JSON includes all `required` fields from
  `packages/schema/src/schemas.ts` (`id, title, project, type, lane, priority, domain, riskTier,
  urgent, deliverable, tokenEstimate, status, context, objective, acceptanceCriteria, output,
  verifiedNeed`), uses only enum-valid values, and `acceptanceCriteria` has ≥ 1 item. Lane is
  `donated`, so `fundedBudgetUsd` is correctly omitted.
- *Honesty* — no partner/need is invented; every delivery-dependent task carries
  `requestor: TO BE SECURED` and `verifiedNeed: false`.
- *Guardrails* — license/provenance rigor (PD/CC only; non-federal reuse verified), zero-PII privacy,
  non-partisanship, and HIGH-tier expert + "not advice" framing are all enforced as gates, not prose.
- *Risk tier* — HIGH is justified and consistently applied (any eligibility/threshold/program-fact
  content is HIGH; immigration content double-gated; infra is low–medium).
- *Internal consistency* — milestone IDs, dependencies, and the dated decision rules in PLAN and TASKS
  agree; the explainer-deferral path is consistent across Scope, Roadmap, and TASKS.

**Headline gate:** No HIGH-tier benefits content ships without (a) a primary-source citation, (b)
credentialed-reviewer sign-off (plus immigration-attorney sign-off for immigration content), and (c)
the not-advice framing + route-to-human pointer — and no claim serves past its `validUntil` or a
recorded `effectiveDate`/`pendingChange` boundary.

**Outstanding human decisions:** secure a pilot partner + credentialed reviewer + immigration
attorney; choose the pilot jurisdiction/flagship program (criteria fixed, decision by 2026-08-31);
decide CC-BY vs CC0; decide whether the explainer ships at all.

**Verdict:** Approved as a Draft (v0.2.0) ready for maintainer and Elyos-governance review.

---

## Changelog — v0.2 (analysis merged)

This version merges the findings of `COMPETITIVE-ANALYSIS.md` into the plan. Changes are surgical and
additive; no guardrail was weakened and no fact/threshold was invented.

**Concrete fixes applied:**

- **Effective-dating is now first-class.** Added **`effectiveDate` / `pendingChange` / `supersededBy`**
  to the content/`Source` schema alongside `validUntil`, so a guide can state "rule today; changes on
  `<date>`" — the dominant 2025–2027 failure mode given OBBBA's staggered effective dates (immigrant
  restrictions 2026-10-01; Medicaid 2026-12-31 / 2027-01-01) and the pending public-charge NPRM.
  Threaded through the schema (component 1), staleness fail-safe (component 3), provenance model,
  success metric, risks, and Roadmap (M0/M1).
- **Eligibility-information-vs-determination boundary strengthened.** Added a **labeled borderline-case
  calibration corpus (~50 phrasings)** as a single source of truth feeding the intent classifier, the
  style guide, and reviewer training (M0/M1 artifact), to keep the line drawn consistently.
- **Currency cadence raised above "at least annually"** to **event-driven and effective-date-aware**
  re-verification (annual points + every recorded effective date / pending-rule milestone + a
  monitored-sources change-watch) in Problem, architecture, Data/compliance, Sustainability, Roadmap.
- Added a **source-hierarchy + conflict-resolution rule**, a **county/admin-region jurisdiction tier**
  with a `federal-floor`/`state-option`/`local-practice` flag, an **"accurate-but-non-chilling"
  immigration content standard**, **PDF version/verify-after stamping + errata/retraction runbook**,
  **oral/visual modalities**, and **moderated beneficiary comprehension testing**.

**Strategy integrated:**

- New **"Competitive landscape & differentiation"** section (Code for America/GetCalFresh = application
  funnel; findhelp/211 = directory not rule-explainer; mRelief = the screener we refuse to be) — the
  differentiator is the openly-licensed, primary-source-cited, currency-guaranteed plain-language
  **explainer** layer with zero PII and a route-to-human guarantee; *never determining eligibility IS
  the moat*, making the corpus embeddable inside findhelp/211/CfA flows.
- **Claude API leverage folded into architecture** (grade-6 rule explainers from CFR/agency text for
  reviewer sign-off; federal-floor vs state-option vs local-practice structuring; staleness diff
  worklists) with hard "never determine eligibility / never give legal advice" release-gate boundaries.
- **Optimizations folded into the Roadmap** (M0–M6) and a new **"Adjacent opportunities"** section
  (shared rules-explainer engine + MCP server + ties to know-your-rights / community-resource-maps /
  food-assistance-maps). **Open questions merged** (distribution-partner posture, event-driven currency,
  CC0 as infrastructure choice, comprehension instrument).

**Preserved:** all guardrails (not-advice / non-partisan / privacy-by-construction / zero-PII), the
HIGH risk-tier gates, the dated partner-acquisition + mothball/pivot rule, the vision, and section
structure. v0.1.0 → v0.2.0.
