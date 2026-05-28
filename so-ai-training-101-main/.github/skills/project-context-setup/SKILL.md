---
name: project-context-setup
description: Interactive, conversational workflow for turning raw onboarding
  materials (meeting notes, transcripts, briefings, decks) into a structured
  set of project-context reference files — typically People, Organization,
  Systems, and Opportunities. Supports one or more input source files in
  varied formats (.docx, .pdf, .md, .txt, .eml/.msg, .vtt/.srt), non-linear
  section completion, save-and-resume, and lightweight check-ins to validate
  uncertain or conflicting facts. Use when a user joins a new project, team,
  or engagement and needs to convert messy raw notes into trustworthy
  reference documents that capture the people, org structure, systems
  landscape, and opportunities.
---

# Project Context Setup

This skill guides building a set of structured project-context reference
files from raw onboarding materials. It mirrors how an analyst actually
works: extract → structure → spot-check the uncertain parts → produce
trustworthy reference docs.

## Default Output Structure

Unless the user adjusts during the initial check-in, produce these four
files in a project-named output folder (e.g., `Acme Output/`):

1. **People.md** — Roster of people mentioned, with role, team, and
   reporting context. Separate tables for internal staff vs. external
   vendors/contacts.
2. **Organization.md** — How the org is structured: departments, teams,
   vendors, dynamics, plus a Mermaid org chart.
3. **Systems.md** — Inventory of systems/tools, grouped by functional
   category, with purpose, owner, vendor, and status.
4. **Opportunities.md** — Identified opportunities/initiatives grouped
   by theme, with description, potential value, potential cost, systems
   involved, and departments involved.

The structure is a strong default but not mandatory. Confirm or adjust
during the initial check-in (see Workflow §1).

**Templates** — Use these as the starting structure for each default file:
- [references/template-people.md](references/template-people.md)
- [references/template-organization.md](references/template-organization.md)
- [references/template-systems.md](references/template-systems.md)
- [references/template-opportunities.md](references/template-opportunities.md)

**Alternative outputs** — If the user requests a file beyond the four
defaults (e.g., Processes, Glossary, Risks, Decisions, Timeline,
Metrics), follow
[references/alternative-outputs-guide.md](references/alternative-outputs-guide.md)
to keep structure consistent with the defaults.

## Workflow Pattern

### 1. Initial Scan & Structure Check-in (always first)

When the user provides one or more source files:

**DO:**
- Inventory the sources: list every file by name and format.
- Read each source. For binary formats use the extraction notes in
  [references/input-formats.md](references/input-formats.md).
- Build a quick mental model: what kind of project is this? What kinds
  of entities show up (people, systems, processes, opportunities)? What
  themes recur?
- Present a brief summary (~5 bullets) of what was found.
- Propose the output structure (default 4 files, or adjusted if the
  material clearly calls for different sections — e.g., a heavily
  process-focused source might warrant a `Processes.md`).
- **Check in with the user** on:
  - Project name (used for the output folder)
  - Output structure (confirm defaults, or add/remove/rename sections)
  - Anything in the source that looks ambiguous about scope (e.g., "this
    covers two business units — do you want them combined or split?")

**DON'T:**
- Start producing files before confirming structure.
- Ask more than ~3 questions in one batch. Pick the highest-leverage ones.

**Example opening:**
```
I've read the 3 source files (intro-call.docx, org-chart.pdf,
ops-notes.md). Quick summary:
• ~40 people referenced, mostly internal; one external vendor (Alphonse)
• Two distinct business areas discussed (AR retail + e-commerce)
• ~50 systems mentioned, several with unclear identity (EP, PIMDAM)
• ~80 opportunities, mostly informal and unsized

Default output is People / Organization / Systems / Opportunities
in a new folder. A couple of quick checks before I start:

1. Project/folder name? (suggesting "TPC Output/")
2. The AR and e-commerce areas are intertwined — combine in one set
   of files, or split?
3. Anything else you want as its own file (e.g., Processes, Glossary)?
```

### 2. File-by-File Building (core loop)

For each output file, run this loop. The order is user-directed —
default suggestion is People → Organization → Systems → Opportunities,
but the user may start anywhere or jump around.

#### Generation Phase

- Generate ONLY the file the user picked.
- Pull facts directly from the source(s). Quote or paraphrase faithfully.
- Use "unknown" as the placeholder when a field isn't in the source.
  Never fabricate.
- Apply the Uncertainty Tagging rules (see §4) as you go.
- Write the file to the output folder.

#### Targeted Check-in Phase

For certain files, do a focused check-in with the user — not on
everything, just on items most likely to be wrong or contentious.
Surface conflicts and inferences, NOT trivia.

Built-in check-in moments:

- **After People.md** — Validate:
  - Names written with ambiguity in source (e.g., "Bryan?" with a
    question mark)
  - Inferred reporting lines or team placements
  - Any name that appears with conflicting roles in the source
- **After Systems.md** — Validate:
  - Inferred system identities (acronyms whose meaning isn't spelled out)
  - Inferred system owners (especially when one name appears across many
    systems)
  - Status guesses (live / planned / deprecated)
- **Before Opportunities.md** — Confirm:
  - Top themes to emphasize
  - Whether to include speculative items raised once vs. only
    well-supported items
- **After each file** — Quick "looks good / refine X" prompt before
  moving on.

**Check-in budget:** Aim for ≤ 5 questions per check-in. Bundle related
questions. Skip a check-in if the file genuinely has no uncertainty.

#### Refinement Phase

When the user pushes back, common edits:
- **Correct a fact** — fix and re-verify against source.
- **Re-attribute** — change owner, team, or department.
- **Merge / split** — combine duplicate entries; split conflated ones.
- **Add missing item** — search source again to confirm or note as
  user-provided (cite the user in the source column).

After refinement, ask once: "Anything else, or shall we move on?"

#### Transition Phase

- Mark file complete in the progress tracker.
- Offer the logical next file, but allow non-linear choice:
  ```
  ✓ People.md complete
  ✓ Saved to TPC Output/People.md

  Progress:
  ✓ People
  ○ Organization
  ○ Systems
  ○ Opportunities

  Next up logically would be Organization (uses People as input).
  Or pick:
  [1] Organization  [2] Systems  [3] Opportunities  [4] Pause
  ```

### 3. State Management & Resume

**Primary state store:** the output files themselves, plus a small
`_progress.md` file inside the output folder.

`_progress.md` format:
```markdown
<!-- Project context setup — progress tracker -->

## Sources
- raw/intro-call.docx
- raw/org-chart.pdf

## Files
- [x] People.md — complete (last refined: 2026-05-28)
- [ ] Organization.md — not started
- [ ] Systems.md — not started
- [ ] Opportunities.md — not started

## Open check-in items
- (none)
```

**Resume:** When the user returns and asks to continue, look for an
existing output folder and `_progress.md`. Read it, summarize state, and
offer next steps. Do not regenerate completed files unless asked.

**Non-linear work:** The user can revisit any completed file. When they
do, read the current version from disk, make edits, write back.

### 4. Uncertainty Tagging Rules

Strong, accurate "I don't know" handling is the highest-value behavior of
this skill. Apply these rules during generation:

1. **Missing field** → write `unknown`. Never guess.
2. **Source says "X?" or hedges** → carry the uncertainty into the
   output (e.g., a "Notes" column saying "Name written as 'Bryan?' in
   source — confirm spelling").
3. **Conflicting source statements** → record the conflict explicitly;
   do not silently pick one side.
4. **Inferred fact** (you connected dots the source didn't connect) →
   the fact may appear in the table, but it MUST also appear in the
   file's **Validation Recommended** section.
5. **Question the source doesn't answer at all** but that a reader will
   ask → list in the file's **Open Questions** section.

#### Open Questions and Validation Recommended sections

Add these sections to the **top** of any output file that contains
material uncertainty. If a file is fully grounded in source with no
inferences, omit them — don't pad. Most non-trivial files will have at
least one of these.

- **Open Questions** — things the source genuinely doesn't answer that
  a reader will want to know. Group by sub-theme if there are many.
- **Validation Recommended** — items present in the file that were
  inferred, were stated by a single interviewee, are directional rather
  than measured, or were carried over with caveats. Use a table:
  `| Item | Field(s) to Validate | Why |`

When you re-visit a file later, move Open Questions / Validation
Recommended to the top if they're not already there, and expand them
based on what you've learned.

### 5. Source Fidelity Rules

- **Never invent names, numbers, or relationships.** If you can't point
  to a line in a source for a claim, it's an inference — tag it.
- **Quote sparingly but quote.** When a claim is contentious, include a
  short verbatim quote in a Notes column or footnote.
- **Preserve speaker attribution** when the source has it ("Joe said
  ~$2.1M/yr in parts"). It's evidence the reader can act on.
- **Treat informal source language with care.** Casual notes often use
  shorthand; verify before promoting shorthand to fact.

## Input Format Handling

The skill supports multiple source formats and multi-file projects.
For format-specific extraction notes (especially for binary formats
like .docx, .pdf, .msg), see
[references/input-formats.md](references/input-formats.md).

General rules:
- Read every source before generating any output file.
- If a binary format can't be read, ask the user for a plain-text
  export rather than guessing at content.
- When sources conflict, treat the conflict as data — surface it in
  Open Questions.

## Anti-patterns

- **Generating all four files at once.** Overwhelms review; degrades
  accuracy. Always one file at a time.
- **Polling the user with 15 questions.** Pick the few that matter.
- **Filling unknowns with plausible guesses.** Use `unknown` and tag
  it. The reader's trust is the deliverable.
- **Dropping the Open Questions / Validation Recommended sections
  to "tidy up" the file.** Those sections are the value-add.
- **Locking in structure too early.** Confirm structure in the initial
  check-in; don't reverse-engineer it from the first generated file.
