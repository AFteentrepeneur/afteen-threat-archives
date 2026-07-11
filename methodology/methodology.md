# Methodology

How we research, verify, and write every ÄFteeñ Threat Archives case file.

## 1. Source Selection

We only draw from public, verifiable sources:
- Law enforcement / government advisories (e.g., CISA, FBI, Europol, INTERPOL)
- Court documents and indictments
- Established security research and journalism (e.g., Krebs on Security, vendor threat intel reports)
- Official statements from affected organizations

We do not use unverified forum posts, leaked data dumps, or dark web content directly as sources. Where a claim originates from a leak, we cite the *reporting on* that leak, not the leak itself.

## 2. Research Process

1. **Scoping** — Define the case or pattern, identify the core question the video will answer.
2. **Source gathering** — Pull primary sources first (court docs, official advisories), then cross-reference with secondary reporting.
3. **Timeline construction** — Build a chronological record of events, each entry tied to a source.
4. **Pattern extraction** — Identify what's repeatable/generalizable (the "lesson"), separate from case-specific detail.
5. **Fact-check pass** — Every factual claim in the case file must trace to a cited source before it's considered final.
6. **PII/sensitivity review** — Redact any personal data, victim identifiers, or live malicious links that appear in source material, even if the original source didn't redact them.

## 3. Case File Standard

Every case file in `/cases/` uses the same structure — see [case-template.md](./case-template.md):
- Summary
- Timeline
- Techniques used
- Patterns identified
- Defensive lessons
- Sources

## 4. Verification Standard

A claim goes in a case file only if it's corroborated by at least one credible public source, and ideally two. Where sources conflict, we note the discrepancy rather than picking one silently.

## 5. Tools Used in Research

- Perplexity / ChatGPT for initial source discovery (never as a primary source itself)
- Direct review of primary documents (court filings, advisories) where available
- TubeBuddy/vidIQ for topic/SEO research (production stage, not factual research)

## 6. Corrections Policy

If an error is identified after publication, the case file is updated and a note is added at the bottom logging the correction and date.
