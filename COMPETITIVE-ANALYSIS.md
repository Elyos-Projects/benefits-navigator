# Benefits-Navigator — Competitive & Improvement Analysis

> Analyst review of `PLAN.md` (v0.1.0, 2026-06-28) and `TASKS.md`. Project: open, plain-language,
> primary-source-cited, multilingual guides to public-assistance programs (SNAP, Medicaid/CHIP, WIC,
> TANF, LIHEAP, SSI, housing, EITC, Lifeline/ACP, UI). HIGH risk-tier. Information + routing only —
> **not** eligibility determination, not legal advice. Web-researched and cited throughout.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually strong for a HIGH-stakes civic project. It already internalizes the hardest
constraints as identity rather than disclaimers. The review below confirms what is right, then flags
gaps, weighed against the eight dimensions in the brief.

**What the plan gets right (verified against the domain):**

- **The information-vs-determination boundary is the spine of the design, not a footer.** The plan
  refuses "do I qualify / how much / will I be approved," frames every artifact "only the agency
  decides," and enforces a route-to-human + official-application *coverage gate* (a guide missing
  either pointer is a defect). This is the correct and defensible posture. It is also the single
  feature that legally and ethically separates this from a "benefits calculator."
- **Currency is engineered, not hoped for.** The `lastVerified`/`validUntil` staleness fail-safe,
  anchored to real update points (HHS poverty guidelines in January, SNAP COLA in October), with
  auto-flag/withhold past expiry, is exactly right. This matters acutely right now: the **One Big
  Beautiful Bill Act (OBBBA, signed July 4, 2025)** rewrote SNAP and Medicaid work requirements,
  raised the SNAP able-bodied work-requirement age ceiling from 54 to 64, narrowed the dependent-child
  exemption from under-18 to under-14, and set immigrant-eligibility restrictions effective Oct 1,
  2026 and Medicaid work requirements/6-month redeterminations effective Dec 31, 2026 / Jan 1, 2027
  ([KFF](https://www.kff.org/medicaid/a-closer-look-at-the-work-requirement-provisions-in-the-2025-federal-budget-reconciliation-law/),
  [CRS R48755](https://www.congress.gov/crs-product/R48755)). A guide written in mid-2026 that does not
  carry these effective dates is actively dangerous. **The plan's currency machinery is its biggest
  competitive moat — but the plan understates how much mid-year churn there is right now; "at least
  annually" undersells the 2025–2027 cadence.**
- **Privacy-by-construction (zero PII, stateless/trackless)** is correctly framed as a structural
  control, and is doubly load-bearing given the chilling effect (below).
- **Immigration content is double-gated** (immigration attorney sign-off) and public-charge questions
  are routed out. This is correct and timely.
- **Non-partisan framing** ("describe programs as the law defines them") and the corpus-only,
  no-source-no-claim explainer constraint are correct.

**Gaps and corrections (ordered by importance):**

1. **The eligibility-boundary is sound in policy but underspecified at the seam where it is most
   tempting to cross.** "Explain the factors but don't determine" is clean in the abstract, but the
   hardest real cases are *conditional explanations* a navigator would give ("households with a member
   over 60 or disabled often don't face the asset/gross-income test"). The plan should add an explicit
   **calibration rubric and worked examples** distinguishing allowed *general conditional rules* from
   forbidden *individualized application*, because the red-team and reviewers will otherwise disagree
   case-by-case. Without this, the fail-closed classifier will either over-refuse useful general
   information (degrading the product) or leak determinations. Recommend a labeled corpus of ~50
   borderline phrasings as a M0/M1 artifact feeding both the classifier and the style guide.

2. **Currency: the plan should treat "effective-dated future changes" as a first-class data field, not
   just `validUntil`.** Right now a rule can be simultaneously *currently true* and *about to change on
   a known date* (e.g., immigrant eligibility on Oct 1, 2026). `validUntil` models "re-check by," but
   the corpus also needs an **`effectiveDate` / `supersededBy` / `pendingChange`** concept so a guide
   can say "this is the rule today; it changes on <date>." This is the dominant failure mode in
   2025–2027 and the schema doesn't yet name it.

3. **State-specificity is asserted but the hardest variation axis (county/local administration) is
   thin.** The plan acknowledges "county practice," but SNAP/Medicaid/TANF are administered with
   genuine sub-state variation (categorical eligibility options, broad-based categorical eligibility,
   state income disregards, county offices). The schema's `jurisdiction` should explicitly support a
   **county/admin-region tier and a "state-option" flag** so a guide can mark which facts are federal
   floors vs. state options vs. local practice. Picking SNAP as flagship (good call on tractability)
   mitigates but does not remove this.

4. **Accuracy/sourcing: "primary, official sources" needs a tie-break and conflict policy.** Federal
   regulation, federal sub-regulatory guidance, and a state portal can disagree (or the portal can lag
   the law). The provenance protocol should specify a **source-hierarchy and a conflict-resolution
   rule** (statute/reg > federal agency guidance > state rule > state portal explainer), and require
   the reviewer to record which governs when they conflict. Citing "an official source" is necessary
   but not sufficient when officials contradict each other.

5. **Harm-from-wrong-info: there is no published correction/retraction path or incident runbook.** For
   a HIGH-tier project the plan needs a stated **errata/notification process** (how a discovered
   error is withdrawn, who is notified, how downstream PDF/printed copies and translations are flagged
   as superseded). Printed PDFs in food banks are the worst-case stale vector and deserve explicit
   versioning/expiry stamping on the artifact itself.

6. **Non-partisan + chilling-effect tension is unaddressed.** "Describe programs as the law defines
   them" is right, but the *act of accurately describing* public-charge risk can itself chill eligible
   families — and inaccurately reassuring them is equally harmful. KFF reports **11% of immigrant
   adults (17% of parents) stopped participating in a program since January 2025 due to
   immigration-related worries**
   ([KFF](https://www.kff.org/medicaid/potential-chilling-effects-of-public-charge-and-other-immigration-policies-on-medicaid-and-chip-enrollment/)),
   and a new DHS public-charge NPRM (published Nov 17, 2025; comment period closed Dec 19, 2025) is
   pending with the 2022 rule still in effect
   ([National Immigration Forum](https://forumtogether.org/article/explainer-2025-proposed-rule-on-public-charge/),
   [NPR](https://www.npr.org/2025/11/18/g-s1-96806/trump-public-charge-rule)). The plan should add an
   explicit **"accurate-but-non-chilling" content standard for immigration-adjacent material**
   (state current rule, state that proposals are not law, avoid both false alarm and false
   reassurance, route to counsel) reviewed by the immigration attorney — this is a content-quality
   dimension distinct from the refusal layer.

7. **Accessibility/multilingual is well-specified but reading-level alone won't reach low-literacy +
   LEP users.** WCAG 2.2 AA + grade ≤6–8 + reviewed translations are right. Add **oral/visual
   modalities** (the brief's beneficiaries include low-literacy users for whom even grade-6 prose is a
   barrier): plain-language audio, iconography/flowcharts, and "what to bring" checklists. This is a
   completeness gap, not an error.

8. **Minor:** Success metrics omit a **comprehension/accuracy check with real beneficiaries** beyond
   readability formulas (readability scores are necessary, not sufficient — they don't measure whether
   people *understood*). The pilot should include moderated comprehension testing.

Net: the plan is approvable as a draft. The corrections above are refinements (effective-dating,
border-case calibration, county tier, source-conflict policy, errata runbook, non-chilling standard),
not foundational defects.

---

## 2. Competitive landscape

The space splits into four archetypes: **(a) eligibility screeners/application assisters**
(GetCalFresh, mRelief, Single Stop, Benefits.gov/USA.gov finder), **(b) resource directories /
referral networks** (findhelp, 211, Unite Us), **(c) benefit-management/fintech utilities** (Propel),
and **(d) official program sources** (USDA FNS, CMS, state portals). Crucially, **none of them is a
plain-language, openly-licensed, primary-source-cited, currency-tracked *explainer* corpus.** They
either screen, route, transact, or publish official-but-inaccessible text.

**Code for America — GetCalFresh / Social Safety Net.** The gold standard for human-centered SNAP
*application assistance*. GetCalFresh helped ~6.2M households access $12.8B in food assistance and cut
application time to <10 minutes; CA has now folded its principles into the state system BenefitsCal,
and the GetCalFresh homepage is now a guidance hub that hands off to BenefitsCal
([Code for America food benefits](https://codeforamerica.org/programs/social-safety-net/food-benefits/),
[10 years of GetCalFresh](https://codeforamerica.org/news/reflecting-on-10-years-of-getcalfresh/),
[CDSS transition](https://www.cdss.ca.gov/inforesources/cdss-programs/calfresh-outreach/getcalfresh-transition)).
*Strengths:* deep UX research, real outcomes, trust, the Benefits Enrollment Field Guide. *Weaknesses:*
**single-program, single-state (CalFresh/CA) in practice; it is an application funnel, not a
multi-program/multi-state explainer; its content is not an openly-licensed, citation-per-claim corpus
others can reuse; it screens/applies (which Benefits-Navigator deliberately does not).** This is the
sharpest comparison — and the gap is "national, multi-program, sourced, reusable explanation" vs.
"one program, one state, application flow."

**mRelief.** Nonprofit SNAP screener by web/text ("text FOOD to 74544"), 5-minute questionnaire,
operates across all 53 SNAP jurisdictions, has helped 2.7M+ people unlock $1B+
([mRelief](https://www.mrelief.com/),
[Digital Government Hub](https://digitalgovernmenthub.org/publications/mrelief/)). *Strengths:*
extreme simplicity, SMS reach to low-bandwidth users, national SNAP footprint, food-bank partnerships.
*Weaknesses:* **it is a screener (likely-eligible estimate) → an act Benefits-Navigator refuses; not a
plain-language explainer; SNAP-only; not an openly-licensed sourced corpus.** A natural *partner/
complement*, not a content competitor.

**Single Stop.** Nonprofit doing in-person benefits *screening + application + tax/legal* on community
college campuses; connected 269K+ students to $548M in benefits via a proprietary screening tool that
"incorporates thousands of pages of regulations into a single screening tool"
([Single Stop](https://singlestop.org/),
[Wikipedia](https://en.wikipedia.org/wiki/Single_Stop)). *Strengths:* wraparound human model, strong
outcomes, college reach. *Weaknesses:* **proprietary/closed tool; screening + case management (not an
open explainer); narrow setting (campuses); not multilingual-open or reusable.**

**Benefits.gov / USA.gov Benefit Finder.** The federal aggregator + anonymous pre-screen across
1,000+ federal/state programs; DOL/GSA centralized benefits info on USA.gov in 2024
([USA.gov benefit finder](https://www.usa.gov/benefit-finder),
[DOL release](https://www.dol.gov/newsroom/releases/oasam/oasam20240807)). *Strengths:* authoritative,
broad, anonymous, public-domain. *Weaknesses:* **written well above an accessible reading level,
fragmented, thin on "how to actually apply + get human help," limited languages, a questionnaire
rather than plain explanation.** This is precisely the official-but-inaccessible baseline the plan
targets — Benefits-Navigator should *cite and link to it*, not compete on authority.

**findhelp (formerly Aunt Bertha) + 211.** The dominant social-care *directory*: programs by ZIP in
every U.S. ZIP code, used by individuals and health/CBO partners, and it powers some 211 community
search; "Better Together" with United Way/211
([findhelp](https://www.findhelp.org/),
[findhelp + 211](https://company.findhelp.com/united-way-and-2-1-1/)). *Strengths:* unmatched breadth
of *local resources*, referral plumbing, partner network. *Weaknesses:* **it lists organizations/
programs; it does not explain *program rules* in plain, sourced language; quality/currency of listings
varies; closed data.** Benefits-Navigator is complementary: explain the program → hand to findhelp/211
for the local human.

**Unite Us (incl. Atlas).** Closed-loop referral + HRSN/Medicaid reimbursement infrastructure across
44 states, 1M+ services, Epic integration via Atlas
([Unite Us](https://uniteus.com/),
[closed-loop](https://uniteus.com/products/closed-loop-referral-system/)). *Strengths:* enterprise
healthcare/Medicaid integration, closed-loop tracking, scale. *Weaknesses:* **B2B/institutional, not a
consumer plain-language explainer; proprietary; oriented to referrals + reimbursement, not rule
explanation.** Not a content competitor.

**Propel (formerly Providers / Fresh EBT).** The #1 EBT-balance app, 5M+ users, EBT/WIC/SSI
management, theft-protection; during the late-2025 SNAP disruption it sent $50 payments to ~230K
high-need users
([Propel](https://www.propel.app/),
[NPR](https://www.npr.org/2025/11/04/nx-s1-5587728/snap-shutdown-propel-tech-startup-cash-donations)).
*Strengths:* enormous trusted reach into exactly the beneficiary population, fintech utility.
*Weaknesses:* **manages existing benefits, doesn't explain eligibility/how-to-apply in sourced plain
language; for-profit.** A potential *distribution* partner, not a content competitor.

**USDA FNS / CMS / state portals.** Authoritative primary sources (the corpus's raw material), public
domain at the federal level. *Weaknesses:* fragmented, jargon-heavy, rarely multilingual, no warm
hand-off. These are inputs, not competitors.

**Take-up context (validates the need):** USDA estimates ~88% of eligible people received SNAP in
FY2022, i.e., a ~12–18% "SNAP gap" — and SNAP is the *high*-take-up program; others (EITC, Lifeline,
TANF) are far worse
([USDA ERS](https://www.ers.usda.gov/topics/food-nutrition-assistance/supplemental-nutrition-assistance-program-snap/key-statistics-and-research),
[FRAC SNAP gap](https://frac.org/blog/the-snap-gap-a-state-by-state-glance)). The information gap the
plan targets is real and measurable.

---

## 3. Gaps we can fill

The landscape leaves a clear, unoccupied niche — **the explanation layer**:

1. **Plain-language, primary-source-*cited-per-claim* explanation.** Every incumbent either screens
   (mRelief, Single Stop, GetCalFresh), lists resources (findhelp, 211, Unite Us), transacts (Propel),
   or publishes inaccessible official text (Benefits.gov, FNS). **No one ships grade-6 prose with a
   citation and a verification date on each factual claim.**
2. **Open licensing / reuse.** GetCalFresh content, Single Stop's tool, findhelp/Unite Us data are all
   closed. A **CC-BY/CC0 corpus + structured data export** that other navigators, libraries, and even
   211/findhelp could embed is genuinely novel and force-multiplying.
3. **Currency as a guarantee.** In a period of historic churn (OBBBA, public-charge NPRM), an
   explicitly **effective-dated, expiry-gated** corpus beats static explainers that silently go stale.
4. **Multi-program + multi-jurisdiction explanation in one consistent structure** (vs. GetCalFresh's
   one-program/one-state depth).
5. **The warm hand-off as a measured guarantee** (official application + free human help on *every*
   artifact) — incumbents bury or omit this.
6. **Accurate, non-chilling immigrant-facing content** vetted by an immigration attorney — almost no
   consumer tool does this responsibly; most either ignore it or scare people off.
7. **Offline/printable + multilingual reviewed** artifacts for food banks/libraries — a distribution
   surface the screeners/apps don't serve.
8. **Privacy-by-construction (zero PII)** — a differentiator vs. screeners that necessarily collect
   income/household data.

---

## 4. Differentiators to win (vs. Code for America + findhelp)

**Versus Code for America (GetCalFresh):**

- **We explain, they apply.** GetCalFresh is a SNAP application funnel (now CA-handoff to
  BenefitsCal). Benefits-Navigator is the *upstream understanding layer* across many programs and
  jurisdictions — it can route *into* tools like GetCalFresh rather than replace them.
- **Open, reusable, cited corpus** vs. closed product UX. Our structured data + CC-BY licensing makes
  us infrastructure others build on; GetCalFresh's content is not reusable.
- **Currency guarantee** (effective-dating + expiry-gating) vs. content maintained at product pace.
- **No PII / no screening** — we are safe to consult anonymously (critical for immigrant families);
  GetCalFresh by design collects application data.
- **Multi-program breadth with depth-first discipline.** We do not try to out-UX CfA on SNAP
  applications; we win on *coverage + sourcing + reuse + currency*.

**Versus findhelp / 211:**

- **We explain the *program rules*; they list the *local orgs*.** Complementary, not competitive — and
  the explanation layer is exactly what their directory entries lack.
- **Cited, currency-tracked, plain-language** content vs. variable-quality, closed listings.
- **Integration play:** offer our structured explainers as an open layer findhelp/211 can embed beside
  their resource listings ("what is this program" next to "where to get it").

**The single strongest differentiator (overall):** **An openly-licensed, primary-source-cited,
currency-guaranteed plain-language explainer corpus with a measured route-to-human guarantee and zero
PII** — i.e., *trustworthy, reusable, always-current explanation* in a market where everyone else
screens, lists, transacts, or publishes inaccessible official text. The constraint (we never determine
eligibility) is the moat: it's what makes us safe, anonymous, non-chilling, and embeddable everywhere.

---

## 5. Claude API leverage — and the hard "must NOT decide" line

**Where Claude adds leverage (always human-verified, never the source of truth):**

1. **Drafting plain-language rule explainers from official sources.** Claude excels at compressing
   dense CFR/agency text into grade-6 prose with consistent structure (what it is / who it's generally
   for / what it provides / how to apply / documents / pitfalls / get help). This is the single highest
   ROI use — it turns "thousands of pages of regulations" into reviewable drafts, *which the
   credentialed reviewer then signs off.*
2. **Structuring state-variation and source provenance.** Claude can extract a program's federal floor
   vs. state options vs. local practice into the structured schema, attach candidate citations, and
   flag where a state portal diverges from federal rule — a triage layer for the reviewer.
3. **Plain-language transformation + readability iteration.** Rewriting to hit reading-grade targets,
   generating "what to bring" checklists, and producing translation drafts (for bilingual-reviewer
   sign-off, never machine-only publication).
4. **Adversarial red-team generation.** Claude can generate the ≥8-per-category misuse phrasings
   (determination, structuring/fraud, immigration, injection, euphemism, decomposition) to harden the
   refusal layer.
5. **Staleness/diff assistance.** Given a new poverty-guideline table or an OBBBA provision, Claude can
   draft the diff against existing guides and surface every claim that may be affected (a re-ver
   worklist for the reviewer) — high value given 2025–2027 churn.
6. **Corpus-only retrieval explainer** (if and only if the eval proves grounded+cited beats
   blank-slate and never invents numbers).

**Where Claude must NOT decide (hard boundaries — these are release gates, not guidelines):**

- **No individualized eligibility determination.** Claude must never output "you qualify / you don't /
  you'll get $X." Only the agency decides. Output screening blocks determination language independent
  of the classifier.
- **No legal/benefits/immigration advice.** Public-charge and status questions route to counsel;
  Claude does not opine on individual consequences.
- **No fabricated rules, thresholds, or amounts.** Corpus-only, no-source-no-claim; the eval hard-
  asserts zero invented eligibility numbers. Claude's parametric knowledge of benefit figures is stale
  and unsafe (it cannot know the 2026 COLA or OBBBA effective dates reliably) — **all program facts
  must come from the cited corpus, not the model.**
- **No "how to qualify" / structuring / concealment coaching** — hard refusal + redirect to lawful
  application and legal aid.
- **Flag-and-link to official screeners,** never substitute for them (route to mRelief/GetCalFresh/
  the state app + 211/legal aid on every answer).
- **No PII solicitation or retention;** remind users not to share SSNs/case numbers; stateless.
- **Currency/state-correctness is the model's blind spot:** because rules change mid-year and vary by
  state, the *most dangerous* Claude failure is a confident, plausible, outdated, or wrong-state
  answer. The corpus + provenance + staleness layer exists precisely to keep the model on a leash.

> Note on model/pricing specifics: defer to the project's Claude API skill for current model IDs,
> pricing, prompt-caching, and token-counting when implementing the LLM client and eval harness.

---

## 6. Ten concrete optimizations

1. **Add `effectiveDate` / `pendingChange` / `supersededBy` to the schema** so a guide can say "true
   today; changes on <date>" — essential for OBBBA's staggered 2026–2027 effective dates and the
   pending public-charge NPRM. (Currency.)
2. **Ship a borderline-case calibration corpus (~50 labeled phrasings)** separating allowed general
   conditional rules from forbidden individualized determinations; feed it to the classifier, the
   style guide, and reviewer training. (Eligibility-boundary precision.)
3. **Define a source-hierarchy + conflict-resolution rule** (statute/reg > federal guidance > state
   rule > state portal) recorded per claim when sources disagree. (Accuracy/sourcing.)
4. **Add a county/admin-region jurisdiction tier and a "federal-floor vs. state-option vs. local-
   practice" flag** on each fact. (State-specificity.)
5. **Stamp every PDF/print artifact with a version + "verify-after" date + a short URL to the live
   page,** and publish an **errata/retraction runbook** that flags superseded printed copies.
   (Harm-from-stale-info.)
6. **Add an "accurate-but-non-chilling" immigration content standard** (state current law, mark
   proposals as not-yet-law, avoid both false alarm and false reassurance, route to counsel),
   attorney-reviewed. (Chilling-effect harm + non-partisan accuracy.)
7. **Add moderated beneficiary comprehension testing to the pilot** (not just readability formulas) —
   measure whether people understood and could act. (Accessibility/efficacy.)
8. **Add oral/visual modalities** (audio plain-language, flowcharts, "what to bring" checklists) for
   low-literacy + LEP users beyond grade-level prose. (Accessibility/reach.)
9. **Publish the structured corpus as an embeddable open data layer + MCP server** so findhelp/211/
   libraries/CfA-style tools can surface "what is this program" beside their listings/flows.
   (Distribution/reuse — the moat.)
10. **Build a "monitored-sources" change-watch** (FNS/CMS/IRS/state-portal pages + Federal Register
    for rules like the public-charge NPRM) that opens re-verification tasks automatically when a
    watched source changes — turning currency from calendar-only to event-driven. (Currency + ops.)

---

## 7. Parallel & perpendicular spin-offs

**Parallel (same beneficiaries, adjacent content) — natural sibling projects:**

- **know-your-rights** explainers (tenant rights, due-process in benefits denials/appeals, workplace
  rights) — same plain-language + cited + non-advice + route-to-counsel pattern.
- **community-resource-maps / food-assistance-maps** — the *local-org* layer that complements our
  *program-rules* layer; explicitly designed to hand off to (and ingest from) findhelp/211 rather than
  rebuild their directory.
- **financial-literacy-open** — EITC/CTC, banking, debt, budgeting in the same sourced plain-language
  corpus; EITC already overlaps the benefits set.

**Perpendicular (reusable engine, different domains):**

- **A reusable "rules-explainer engine with currency-tracking"** — the schema (claim → source →
  `lastVerified`/`validUntil`/`effectiveDate`), the readability + accessibility + i18n pipeline, the
  not-advice/refusal policy layer, the source-change watcher, and the grounded-vs-blank-slate eval —
  generalizes to **any high-stakes, frequently-changing, jurisdiction-varying rule corpus**: immigration
  procedure, tax, housing code, disability/veterans benefits, even the sibling `public-official-guide`.
  This is the most valuable durable asset; the benefits corpus is its first instantiation.
- **An MCP server** exposing the vetted corpus (program explainers + structured eligibility-factor
  data + citations + currency metadata) as tools other agents can ground on — with the same not-advice
  guardrails enforced server-side. This is how the open corpus becomes infrastructure inside other
  assistants (and a clean Elyos agent-neutral-core fit).
- **A "currency-watch" service** (monitored official sources → change events → re-verification tasks)
  could itself be a standalone open utility other civic-info projects subscribe to.

---

## 8. Open questions

1. **Pilot jurisdiction + flagship program** (plan's own open Q): SNAP is the right tractable first
   pick, but which state, given OBBBA's state-option churn and reviewer availability? (Decided M0, due
   2026-08-31.)
2. **CC-BY vs CC0** for maximal reuse by findhelp/211/CfA-style embedders — CC0 likely maximizes the
   "infrastructure" play; weigh against attribution to reviewers/sources.
3. **How deep to go on public-charge** given the live NPRM and chilling stakes — full explainer
   (attorney-reviewed, non-chilling standard) vs. minimal "this is changing; talk to counsel" routing?
4. **"Find free help" without PII** — client-side, user-initiated location lookup; can we embed
   findhelp/211 results without collecting/storing location? Confirm their embed/API terms.
5. **Partner & distribution strategy:** are mRelief / Propel / findhelp / a library system the right
   *distribution* partners (not competitors) for an open explainer layer? A complement-not-compete
   posture could unlock reach we can't build alone.
6. **Event-driven vs. calendar currency:** is a Federal-Register / source-change watcher in scope for
   M-something, or deferred? (It materially reduces stale-content risk during 2025–2027.)
7. **Does the explainer ship at all** (plan's open Q) — gated on the eval; given the currency/
   state-correctness blind spots, the bar for shipping a generative answerer should stay high.
8. **Comprehension proof:** what beneficiary-comprehension instrument does the pilot use beyond
   readability formulas?

---

### Sources

- Code for America — [Food benefits](https://codeforamerica.org/programs/social-safety-net/food-benefits/),
  [10 years of GetCalFresh](https://codeforamerica.org/news/reflecting-on-10-years-of-getcalfresh/),
  [CDSS GetCalFresh→BenefitsCal transition](https://www.cdss.ca.gov/inforesources/cdss-programs/calfresh-outreach/getcalfresh-transition)
- [mRelief](https://www.mrelief.com/) · [Digital Government Hub: mRelief](https://digitalgovernmenthub.org/publications/mrelief/)
- [Single Stop](https://singlestop.org/) · [Single Stop — Wikipedia](https://en.wikipedia.org/wiki/Single_Stop)
- [USA.gov Benefit Finder](https://www.usa.gov/benefit-finder) · [DOL/GSA centralization release](https://www.dol.gov/newsroom/releases/oasam/oasam20240807)
- [findhelp](https://www.findhelp.org/) · [findhelp + United Way/211](https://company.findhelp.com/united-way-and-2-1-1/)
- [Unite Us](https://uniteus.com/) · [Unite Us closed-loop referrals](https://uniteus.com/products/closed-loop-referral-system/)
- [Propel](https://www.propel.app/) · [NPR — Propel SNAP-shutdown cash](https://www.npr.org/2025/11/04/nx-s1-5587728/snap-shutdown-propel-tech-startup-cash-donations)
- OBBBA / work requirements: [KFF](https://www.kff.org/medicaid/a-closer-look-at-the-work-requirement-provisions-in-the-2025-federal-budget-reconciliation-law/) · [CRS R48755](https://www.congress.gov/crs-product/R48755)
- Public charge 2025: [National Immigration Forum explainer](https://forumtogether.org/article/explainer-2025-proposed-rule-on-public-charge/) · [KFF chilling effects](https://www.kff.org/medicaid/potential-chilling-effects-of-public-charge-and-other-immigration-policies-on-medicaid-and-chip-enrollment/) · [NPR](https://www.npr.org/2025/11/18/g-s1-96806/trump-public-charge-rule)
- SNAP take-up: [USDA ERS key statistics](https://www.ers.usda.gov/topics/food-nutrition-assistance/supplemental-nutrition-assistance-program-snap/key-statistics-and-research) · [FRAC SNAP gap](https://frac.org/blog/the-snap-gap-a-state-by-state-glance)
