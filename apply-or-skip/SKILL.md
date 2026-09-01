---
name: apply-or-skip
description: Decide whether a job posting is worth an application by matching a job description against a resume or story inventory, separating hard gates from noise, rating evidence strength rather than keyword overlap, and returning a verdict with the tailoring work required. Use when the user shares a JD and asks "should I apply", "am I a fit", "how do I stack up", wants a gap analysis against a posting, wants a JD-to-resume mapping, or is triaging a list of roles to decide where to spend application effort.
---

# Apply or Skip

Judge a posting against real evidence and return a decision the user can act on
in minutes. Application effort is the scarce resource; the verdict is always
relative to what tailoring would cost, never an absolute score.

## Operating contract

- Score **two things separately**: the odds of surviving a recruiter screen, and
  whether the user could actually do the job. These diverge constantly and the
  gap between them *is* the finding.
- Never invent, upgrade, or imply experience the user has not stated. A gap that
  cannot be closed honestly stays a gap.
- Keyword overlap is not fit. Rate evidence strength, not term frequency.
- Report reasons to skip with the same weight as reasons to apply.
- Do not write resume or cover-letter copy in this skill. It ends at the verdict
  and the tailoring brief.

## Workflow

### 1. Get both sides in full

**The posting.** Work from the complete text, not a summary or a title. Many
career sites render through JavaScript and return an empty shell to a fetch; see
[references/sourcing-jds.md](references/sourcing-jds.md) for the ATS endpoints
that return the real JSON, and ask the user to paste when that fails. Capture
the req ID, location and onsite policy, level, posted/updated date, and comp
band if published.

**The candidate.** Prefer, in order: a story inventory or evidence file, the
current resume, the user's LinkedIn/portfolio, then answers to questions. If a
story inventory exists with ownership levels recorded, use those levels verbatim
— they are the whole point.

Ask at most three questions, and only where the answer changes the verdict
(work authorization, willingness to relocate, comp floor). Otherwise state the
assumption and continue.

### 2. Decompose the posting

Classify every requirement into one of four buckets using
[references/fit-rubric.md](references/fit-rubric.md):

- **Gate** — disqualifying if unmet, and no narrative fixes it: work
  authorization, clearance, licensure, onsite/geography, a hard degree bar.
- **Core** — the job is this. Failing one is a real problem.
- **Signal** — screened on but learnable or narratable.
- **Noise** — boilerplate, the wish list, the "10+ years of a 6-year-old
  technology" line. Discount it explicitly.

Most postings are 60-70% noise. Say so, and say which lines you discarded — an
inflated requirement list is the most common reason a qualified person self-
rejects.

### 3. Rate the evidence, not the vocabulary

For each Gate and Core requirement, find the strongest supporting evidence and
place it on the ladder: **Owned → Co-led → Contributed → Exposure → Absent**.
Record where it comes from and how old it is. Recency matters more for tooling
than for judgment work.

Flag two failure modes in the user's own materials:

- **Buried strength** — evidence that clears a Core requirement but appears
  nowhere the screener will look. This is a tailoring instruction, not a gap.
- **Overreach** — a claim the resume makes that this JD would interrogate and
  the evidence would not survive. Name it now, before the interview does.

### 4. Score both axes

Produce two ratings with one sentence of reasoning each, per
[references/fit-rubric.md](references/fit-rubric.md):

- **Screen** (0-10): does a recruiter or parser scanning for 30 seconds see a
  match? Driven by titles, named tools, industry adjacency, level language, and
  whether required terms literally appear.
- **Substance** (0-10): could the user do the job well? Driven by owned
  outcomes, transferable depth, and demonstrated judgment.

Then name the divergence. `Screen << Substance` means the problem is
presentation and a referral or a rewrite is high-leverage. `Screen >> Substance`
means the application may succeed and the interview will not — flag it as an
expensive way to fail, and check the user actually wants the job.

### 5. Sanity-check the posting itself

Before recommending effort, weigh it against
[references/fit-rubric.md](references/fit-rubric.md#posting-quality-signals):
reposting age, evergreen/pipeline language, level-to-comp mismatch, a scope that
reads like three jobs, and whether the role is on the user's actual track. A
role that is easy to get and hard to leave — a track switch dressed as a step up
— deserves an explicit warning, not a high score.

### 6. Return the verdict

One of:

- **Apply now** — clears gates, Core evidence is present and findable. Tailoring
  is cosmetic.
- **Apply with tailoring** — the evidence exists but is buried or mis-framed.
  Name the specific rewrite and estimate the hours.
- **Apply only with a referral** — Screen score will not survive a parser or a
  cold pile, but Substance holds. State who or what would unblock it.
- **Close a gap first** — one or two Core gaps are days of study away, not
  years. Say exactly what to learn and what artifact would prove it.
- **Skip** — a gate fails, the Core gap is structural, or the effort is better
  spent on a role already in the pipeline. Give the reason in one line.

Write the output with [references/report-template.md](references/report-template.md).
End with the single highest-leverage action and, when the verdict is not Skip,
the three pieces of evidence to lead with.

## Triage mode

When the user hands over several postings at once, do not run the full workflow
on each. Run steps 2-4 shallowly, produce a ranked table (role, Screen,
Substance, verdict, tailoring hours), and offer the deep pass on the top two.
Sorting by expected value per hour of application effort is the entire job here.

## Quality rules

- Separate what the JD says, what it means, and what you are inferring.
- Quote the JD line when a gate or Core gap rests on it.
- Never soften a failed gate into "a stretch." Gates are binary.
- Never quote a comp band, headcount, or hiring signal from memory — cite the
  posting or mark it unverified.
- When the user's evidence is thin, say the evidence is thin. Do not compensate
  by inflating the transferability of what is there.
- A verdict with no downside listed is not finished.
