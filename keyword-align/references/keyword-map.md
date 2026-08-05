# VOLO Health — target search terms

Within every list below, terms are ordered **most important first**. The priority label
tells you how hard to chase each one.

| Priority | Meaning | Use in swaps |
|---|---|---|
| **First** | Real demand, winnable now | Prefer these |
| **Next** | Real demand, needs genuinely good content to win | Use when the copy is squarely about this |
| **Later** | Entrenched incumbents hold these | Only if the page is already on this exact subject |
| **Own** | Our terms to define. No outside demand yet | Always normalise to canonical form |
| **Skip** | Not worth an edit | Never swap toward these |

---

## Consumer

### C1 — Long-term & proactive health · Homepage

| Target term | Priority |
|---|---|
| health risk assessment | **First** — the head term for this cluster |
| what is a health risk assessment | **First** |
| online health risk assessment | **First** |
| health risk assessment with scoring | **First** — echoes our own scoring model |
| proactive health monitoring | **First** |
| how do you measure long-term health | Unverified — demand unconfirmed, do not swap toward it yet |
| how to predict future health risk | Unverified — same |
| how to know if you're aging well | Skip |

### C2 — Longevity & healthspan · Individuals

| Target term | Priority |
|---|---|
| healthspan vs lifespan | **First** |
| how to increase healthspan | **First** |
| longevity test | **Next** — contested by review and listicle sites |
| how to live longer and healthier | **Next** |

### C3 — Biological age & health scores · VOLO Scores

| Target term | Priority |
|---|---|
| what is my biological age | **First** — best return in the cluster |
| biological age test | **Next** — the largest audience of any term we track, and correspondingly contested |
| how healthy am I for my age | **Next** |
| health score calculator | **Next** |
| how accurate are biological age tests | **Next** |

### C4 — Biomarker interpretation · Resources

| Target term | Priority |
|---|---|
| lab test reference ranges | **First** |
| lab reference ranges | **Next** |
| how to read blood test results | **Next** — large audience, worth real content |
| what is a good LDL level | **Later** — WebMD and Mayo are entrenched here |
| what does high A1c mean | Skip |

### C5 — Early detection & risk · Resources

| Target term | Priority |
|---|---|
| how to prevent chronic diseases | **First** — strong demand, easy to win |
| chronic disease prevention | **Next** |
| how to lower my A1c | **Next** — large audience |
| risk score for heart disease | **Next** — cardiovascular is a VOLO Score domain |
| cardiovascular disease risk score | **Next** — same rationale |
| risk factors for type 2 diabetes | **Later** — medical publishers entrenched |
| how to lower cardiovascular risk | **Later** |

### C6 — The science · Research

| Target term | Priority |
|---|---|
| predictive biomarker | **First** |
| predictive biomarkers | **First** — plural variant, worth carrying both |
| how are VOLO Scores calculated | **Own** |
| what is a predictive health model | Skip — confirmed dead end |

---

## Clinician

### B1 — Value-based care · Clinicians

| Target term | Priority |
|---|---|
| population health management software | **First** — strongest clinician term we have, and buyers here are actively purchasing |
| value-based care software | **First** |
| best population health management software | **First** — easiest in the cluster, and buying intent |
| value-based care platform | **First** |
| population health risk stratification tools | Skip |

### B2 — Functional & longevity-medicine tech · Clinicians

| Target term | Priority |
|---|---|
| functional medicine software | **First** — smaller audience, but the most commercially valuable term on the whole list |
| longevity clinic software | Skip — confirmed dead end |
| longevity medicine practice software | Skip — confirmed dead end |

### B3 — Patient risk & trajectory · Clinicians

The whole cluster is currently unwinnable. Every term tested was either a dead end or
carries the retrieval problem described under Guardrails. Do not swap toward any of it.

| Target term | Priority |
|---|---|
| calculate patient risk score | Skip |
| clinical risk prediction tools | Skip — confirmed dead end |
| track patient health trajectory | Skip — confirmed dead end |

### B4 — Clinician biomarker education · Clinicians / Resources

| Target term | Priority |
|---|---|
| functional medicine lab tests | **First** — the easiest term on the entire list |
| functional medicine lab testing | **First** |
| functional medicine lab reference ranges | Skip |

---

## Branded terms — canonical forms

Normalise **capitalisation and spelling only**. Trademark symbols are a brand-legal
decision: never add, move or remove a ™. If a page uses ™ inconsistently, note it and
leave it.

| Canonical | Not | Notes |
|---|---|---|
| **VOLO Score** | Volo score, volo Score, Volo Health Score | Singular when naming the metric |
| **VOLO Scores** | — | Plural only for the set across domains |
| **VOLO Age** | Volo age, biological age score | Ours to win outright |
| **VOLO Modeled Range** | Volo modelled range, VMR on first use | Spell in full on first use, VMR acceptable after |
| **Biomarker Strength** | biomarker strength score | Capitalised as a defined term |
| **VOLO Health** | Volo Health, VoloHealth, Voloridge Health | One spelling sitewide. Voloridge Health is the parent, not a synonym |

Branded terms are exempt from the density limit. Normalising the same term five times in
a page is consistency, not stuffing, and it feeds entity resolution. Log them as one
grouped row rather than five.

---

## Near-miss mappings

The left column is phrasing that already appears in VOLO copy. Swap only when the meaning
is genuinely the same.

### Consumer

| If the copy says | Consider | Cluster |
|---|---|---|
| health assessment, health evaluation, wellness assessment | health risk assessment | C1 |
| assess your health online, digital health check | online health risk assessment | C1 |
| staying ahead of your health, preventive tracking | proactive health monitoring | C1 |
| years of healthy life, quality years, health span | healthspan | C2 |
| living longer versus living well | healthspan vs lifespan | C2 |
| longevity panel, longevity screening | longevity test | C2 |
| how old your body is, physiological age, internal age | biological age | C3 |
| biological age assessment, age test | biological age test | C3 |
| find out your biological age | what is my biological age | C3 |
| understand your bloodwork, interpret your labs, make sense of lab results | how to read blood test results | C4 |
| normative data, normal ranges, standard ranges, reference intervals | lab reference ranges | C4 |
| reduce disease risk, avoid chronic illness, disease prevention | how to prevent chronic diseases · chronic disease prevention | C5 |
| heart disease risk, cardiac risk | cardiovascular disease risk score | C5 |
| blood sugar control, lowering A1c | how to lower my A1c | C5 |
| predictive marker, forward-looking biomarker, leading indicator | predictive biomarker | C6 |

### Clinician

| If the copy says | Consider | Cluster |
|---|---|---|
| population health tools, panel management | population health management software | B1 |
| value-based care solution, VBC tooling | value-based care software · value-based care platform | B1 |
| functional medicine platform, practice technology | functional medicine software | B2 |
| lab panels for functional medicine, functional testing | functional medicine lab tests | B4 |

---

## Guardrails

**"Risk score" is contested on clinician-facing pages.** Live testing showed queries
containing that phrase return risk-adjustment and HCC/RAF coding vendors — Arcadia,
Optum, Innovaccer, Inovalon — because the phrase is dominated by reimbursement software.
Two consequences:

- On clinician pages, do **not** swap toward "risk score" phrasing. Prefer the B1 and B2
  terms, which retrieve cleanly.
- If the copy already uses "risk score" on a clinician page, leave it and flag in Notes
  that the page needs an explicit "this is not risk adjustment or RAF coding"
  disambiguation. That is a content decision, not a term swap.

**Consumer terms containing "risk score" are safe.** "Cardiovascular disease risk score"
and "risk score for heart disease" retrieve clinical and consumer health content, not
billing software. The collision is specific to clinician software queries.

**Never cross audiences.** Clinician terms in consumer copy read as jargon and retrieve
the wrong intent. Consumer terms on clinician pages undercut credibility.

**Subjects missing from this list.** If a page's core subject appears nowhere above, say
so in Notes rather than forcing swaps. Some good content sits outside the current
strategy, and that is a decision for a human — either add the cluster, or treat the page
as supporting content that links into a page which is on the list.
