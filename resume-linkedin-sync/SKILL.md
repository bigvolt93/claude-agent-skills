---
name: profile-sync-audit
description: Cross-check a resume against a LinkedIn profile, report every inconsistency with severity, and generate copy-paste-ready per-section LinkedIn updates aligned to the resume, with a public/private filter that excludes confidential details from public copy. Triggers on requests like "check my resume against LinkedIn", "is my LinkedIn up to date", "sync my profile", or "audit my resume vs my profile".
---

# Profile Sync Audit

You audit consistency between two documents that describe the same career: the user's resume and their LinkedIn profile. You report drift and produce ready-to-paste fixes. **You never edit anything directly. Output files only.**

## Inputs

- **Resume:** a file the user provides (PDF, DOCX, or markdown).
- **LinkedIn profile:** pasted text from the user, or read via browser if a browser tool is connected. If neither is available, ask the user to paste their profile sections.

## Workflow

### 1. Build a fact table from each source

Extract from BOTH documents, independently:
- Roles: company, title, start date, end date (or "present")
- Education entries
- Headline / summary claims
- Quantified metrics and achievements (revenue figures, growth %, team sizes, etc.)
- Skills and certifications

Keep the two tables separate at this stage. Do not "helpfully" merge or assume.

### 2. Diff and report inconsistencies

Compare the tables and produce an audit report listing every mismatch, each with a severity:

- **High:** missing current role, wrong/accidental end dates (anything that misrepresents employment status), contradictory titles, metrics that conflict between the two documents.
- **Medium:** date mismatches of a month or more, achievements present in one but absent in the other, outdated headline.
- **Low:** wording drift, skills listed in one but not the other, formatting gaps.

For each item: what the resume says, what LinkedIn says, why it matters. No vague "consider reviewing". State the exact discrepancy.

### 3. Generate per-section LinkedIn updates

For each LinkedIn section that needs a change, write a separate, copy-paste-ready markdown block:
- Headline
- About / summary
- Each experience entry (title, dates, description)
- Skills (if changes are needed)

Rules:
- Treat the resume as the source of truth for facts (dates, titles, metrics) unless the user says otherwise. If LinkedIn appears MORE current than the resume for some item, flag it and ask rather than assuming.
- Write in LinkedIn's register (first person, public-facing), not resume bullet-speak, but keep the facts identical.
- Match the user's existing voice where visible.

### 4. Apply the public/private filter

Before finalizing the LinkedIn copy, scan for content that is acceptable in a privately shared resume but NOT on a public profile:
- Internal/confidential company financials and revenue figures
- Client names under NDA or clearly sensitive customer details
- Unannounced products, internal project codenames
- Personal data (phone, address, salary)

**Exclude these from the public copy** and replace with directionally true, non-confidential phrasing (e.g. "drove significant revenue growth" instead of an internal figure). List everything you excluded and why, so the user can override deliberately if they wish.

### 5. Output, never apply

- Write the audit report and the per-section update files to an output folder.
- **Never auto-edit the LinkedIn profile or the resume**, even if a browser tool is connected and could. The user pastes the changes themselves.
- End with a short checklist: which sections to update, in what order, estimated time.

## Guardrails

- Facts only. Never invent achievements, inflate metrics, or "improve" numbers. If a metric exists in neither document, it doesn't exist.
- If the two documents conflict and the truth is unclear, ask the user; do not pick silently.
- Treat both documents as sensitive personal data; do not quote them anywhere beyond the output files.
