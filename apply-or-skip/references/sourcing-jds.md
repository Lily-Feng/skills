# Sourcing the Full Job Description

Analysis quality is bounded by the input. A title, a summary, or a LinkedIn
teaser is not enough to classify gates and Core requirements — get the full
posting text or say the analysis is partial.

## The problem

Most enterprise career sites are JavaScript applications. A plain fetch returns
the page shell with no job content, and the posting silently reads as empty
rather than failing. Fetch the ATS API the page itself calls instead.

## ATS endpoints

Identify the ATS from the host or the URL shape, then request the JSON.

| ATS | Tell | Endpoint shape |
|---|---|---|
| Oracle Cloud (ORC) | `/hcmUI/CandidateExperience/`, host `*.oraclecloud.com` | `/hcmRestApi/resources/latest/recruitingCEJobRequisitionDetails?finder=ById;Id="<id>",siteNumber="CX_1001"` |
| Eightfold | `/careers?pid=`, host `*.eightfold.ai` | `/api/apply/v2/jobs/<pid>?domain=<domain>&pid=<pid>` |
| Greenhouse | `boards.greenhouse.io/<org>/jobs/<id>` | `https://boards-api.greenhouse.io/v1/boards/<org>/jobs/<id>` |
| Lever | `jobs.lever.co/<org>/<uuid>` | `https://api.lever.co/v0/postings/<org>/<uuid>` |
| Ashby | `jobs.ashbyhq.com/<org>/<uuid>` | Posting JSON is embedded in the page; the API is a POST to `/api/non-user-graphql` |
| Workday | `*.myworkdayjobs.com/<site>/job/...` | Append `?clientRequestID=` or request the same path with `Accept: application/json` |
| SmartRecruiters | `jobs.smartrecruiters.com/<org>/<id>` | `https://api.smartrecruiters.com/v1/companies/<org>/postings/<id>` |

The site number, domain, and org slug are visible in the browser URL or the
page's own network calls. Verify these shapes against the actual site before
relying on them — vendors change paths, and a 404 here is a normal outcome, not
a reason to guess at the JD's contents.

## Fallback order

1. ATS JSON endpoint above.
2. A browser tool, if one is available, on the rendered page.
3. Ask the user to paste the full text. This is fast and reliable — reach for it
   after one failed attempt, not five.

Never reconstruct a posting from the title, from a job board's summary, or from
what the company usually asks for. If only a partial JD is available, label the
report `based on partial posting` and name what is missing.

## Worth capturing alongside the text

- Req ID — the only stable handle for a posting; postings get pulled and reposted.
- Posted and last-updated dates — feeds the posting-quality signals.
- Location list and onsite policy — frequently a gate, and frequently buried
  below the fold or in a separate field from the description body.
- Published comp band — jurisdictions requiring disclosure put it in a distinct
  field that summaries drop.
- The raw JSON — keep it. It is the evidence for anything quoted later, and it
  outlives the live posting.
