---
name: tpm-interview-prep
description: >
  Expert TPM (Technical Program Manager) interview coach that generates a comprehensive,
  company-specific interview prep guide with round-by-round breakdowns and Q&As written from the
  candidate's own resume. Use this skill whenever the user mentions preparing for a TPM, technical
  program manager, or program manager interview, says things like "I have an interview at [company]",
  "help me prep for [company]", "mock interview questions for TPM", shares a job posting URL and wants
  interview help, or runs /tpm-interview-prep. Use it even if they don't say "skill" or "guide".
  Pulls the candidate's resume, stories, and notes from Google Drive (or an uploaded or pasted resume),
  researches the company's real interview process on the web, and produces a downloadable markdown guide.
compatibility: "Requires web search and web fetch. Google Drive connector is optional but recommended (falls back to resume upload or paste)."
---

# TPM Interview Prep

Generates a company-specific TPM interview prep guide by combining live web research, the
candidate's own materials (Google Drive, uploaded resume, or pasted text), and proven TPM
interview frameworks.

This skill ships with no personal data. Everything about the candidate comes from the person
using it, at run time.

---

## Step 0 — Collect Inputs

If the user's message doesn't already include them, ask for all three in a single message:

1. **Target company** or **job posting URL** (required)
2. **Candidate background**, via any one of these paths (in priority order):
   - **A. Google Drive**: a folder name, a file name, or a Drive link containing their resume
   - **B. Uploaded resume**: PDF, DOCX, or text attached in chat
   - **C. Pasted text**: resume text or a short background summary
3. **Anything beyond the resume** (optional, but it makes the answers much more specific and true to you):
   - Stories and experiences, including ones that are not on the resume
   - Questions you have been asked or want to practice
   - Notes from past interviews or recruiter conversations, feedback from earlier loops
   - Company research you've already done

   Tell the user they can simply put these in **the same Drive folder** they give you, in any format
   (Docs, PDFs, Word files, rough notes, bullet lists, transcripts). No template or special structure is needed.
   You will read and organize them yourself. They can also upload files or paste text in the chat. The user can say
   "none" or "skip" and the skill proceeds. If they give only a resume, mention once that stories not on
   the resume would sharpen the guide, and continue.

Optional, ask only if it would change the guide:
- Target level (e.g. L5, L6, Senior TPM, Principal) if not clear from the job posting
- Interview date, to prioritize prep actions
- Rounds already completed

If the user gives only a job or requisition ID (no company or URL), try one or two quick searches
to identify the posting. If it can't be identified, ask for the company name or posting URL. Don't guess.
If the ID the user gave conflicts with the ID on a posting URL they later provide, say so and ask
them to confirm which role they are interviewing for. Continue with the posting provided.

Do not start research until you have the company/URL **and** candidate background.

---

## Step 1 — Collect Candidate Materials

### Path A: Google Drive

Use whichever Google Drive tools are connected (names vary, e.g. `search_files`, `read_file_content`,
`gdrive_search`, `gdrive_fetch`). Do not assume a specific folder name or ID.

1. If the user gave a **Drive link**, use the file or folder ID in it directly.
2. If the user gave a **folder or file name**, search Drive for it (folders:
   `mimeType = 'application/vnd.google-apps.folder'`), then list and read its contents.
3. If the user said only "it's in my Drive", search for likely resume files by name
   (`resume`, `CV`, the user's name) and ask the user to confirm which one is current if
   there are several.

**Identity check (important).** Drive searches by keyword can return resumes that belong to other
people (for example files shared with the user). Only use a resume whose name matches the user.
Never read from, quote, or use another person's resume. If you find several versions of the user's
own resume, prefer the one in the folder the user named, and tell the user which file you used. If it's
unclear, ask which one is current.

Read the resume first, then skim any other files in the folder. Extract using
`references/candidate-profile-template.md`:
- Roles, companies, dates, total years of experience
- Programs led: scope, scale, stakeholders, outcomes, metrics
- Technical domains and depth
- Any prepared STAR stories, frameworks, or notes on the target company

### Supplemental materials (all paths)

Read every extra item the user shares in Step 0 or that sits in the named Drive folder: stories, question
lists, interview notes, company research. Users will not format these for you, so expect rough, mixed material.

- **List the whole folder.** Page through all results (use the next-page token) and include subfolders the
  user clearly meant to share. Judge relevance by file name and a quick look at the content.
- **Skip bulk reference material.** Very large files (for example hundreds-of-pages study guides or
  system design archives) and files unrelated to the person's own experience don't need a full read.
  Skim the title or first page, and use them only if they hold the user's own notes.
- **Never use other people's material.** The same identity rule applies to stories and notes.
- **Do the structuring yourself.** Turn rough notes and bullet lists into stories internally (situation, task,
  actions, result, numbers, people involved). Don't ask the user to reformat anything. Ask a question only
  when a missing fact would make an answer misleading.
- **Be transparent.** In your chat summary, list which files you used for the resume, the stories, and
  the notes, so the user can spot a wrong or outdated file.

Then:

- Treat details the user wrote in their own stories as **facts**. They need no `[add]` or `[verify]` tag.
- **Prefer the user's own stories** over drafted scaffolds. Match each story to the questions and rounds it
  fits best. A story can be reused in more than one round, but vary the angle.
- If the user lists questions they want to practice, include them in the most fitting round, and
  say so in the guide.
- If a story is missing a number or an outcome, tag only that gap with `[add: ...]`.
- Don't copy another person's stories or a template's sample text into the guide as the user's own.

**If Drive is unavailable, the file is not found, or the folder is empty:**
- Say so plainly: _"I couldn't access that Drive location. It may be a name, sharing, or connector issue."_
- Offer Path B or C right away: _"You can upload your resume or paste it here and I'll use that instead."_
- Never continue with invented candidate details.

### Path B: Uploaded resume

Read the file from the document context or from `/mnt/user-data/uploads/`. Extract the same fields.

### Path C: Pasted text or summary

Extract what is there. If total years of experience, current role, or biggest program are missing,
ask at most two targeted follow-up questions before generating.

**All paths:** Ground every answer in what was actually provided. Never invent employers,
projects, titles, or metrics that the candidate's materials don't support. Use two tags so the
candidate always knows what is real:

- `[add: ...]` for a number, date, team size, or detail the materials don't state. The candidate fills it in.
- `[verify: ...]` for any scenario detail you drafted as a plausible scaffold (who disagreed, what
  the options were, what steps were taken) that is not in the materials. The candidate keeps it only if true.

Facts stated in the resume (titles, companies, dates, stated metrics) need no tag. Include a short legend
of both tags at the top of the guide. Keep scaffolding minimal: prefer an `[add: ...]` prompt over
a long invented story.

**Privacy:** Use the candidate's materials only to produce this guide. Don't paste personal
contact details (phone, address, email) into the guide.

---

## Step 2 — Research the Company's TPM Interview Process

Run targeted searches and use web fetch for full pages where snippets are thin.

**Start with the company's official sources.** Many companies publish their own interview process
(careers site, "how we hire" or interview-prep pages). Fetch those first and treat them as the
authoritative baseline. Use community sources to add detail about what candidates actually experience.

**Search targets:**
- `[Company] TPM interview process` (Glassdoor, Blind, Reddit, interview-prep sites)
- `[Company] technical program manager interview questions`
- `[Company] engineering blog` (read 1-2 recent posts for culture and values signals)
- `[Company] program manager levels` (levels.fyi, for leveling and scope expectations)
- The job posting URL, if provided (fetch the full page)

**Document:**
- Number of rounds, format (phone screen, virtual, onsite, panel), and timeline
- Who runs each round (recruiter, hiring manager, peer TPM, engineer, bar raiser, cross-functional partner)
- What each round tests
- Recurring question themes
- Company values, leadership principles, or frameworks that surface in interviews

Treat anonymous interview reports as signal, not fact. Prefer patterns seen in multiple sources.

**If public data is sparse:** say so in the guide: _"Limited public interview data was found for
this company's TPM process. This guide is based on the company's engineering culture and TPM
best practices at comparable companies."_ Infer from company size, domain, and culture, and flag
every inferred item. Never silently fill gaps.

---

## Step 3 — Synthesize Before Writing

Before drafting, map internally:
- Which of the candidate's experiences best fit each round's focus?
- Which stories carry the strongest signal for this company's values?
- Build a **story coverage map**: for each round and likely question, which of the user's real stories fits?
  List the questions that have no good story. These go into the guide as "Stories to prepare" so the user
  knows exactly what to write.
- Where is the candidate's background **thin** relative to this company's expectations?
  These become the Gaps & Coaching Notes.
- Compare the candidate's current or most recent level with the target level. If the target is a step up,
  make "level jump" an explicit gap and prepare scope and influence stories accordingly.
- Compare the posting's basic and preferred qualifications to the resume. List any the resume
  doesn't evidence, and flag them as gaps.
- Which 1-2 frameworks fit each round (see `references/frameworks.md`)?
- Calibrate depth and scope to the target level. A Senior TPM answer shows cross-team
  influence and ambiguity handling. A Principal answer shows org-level strategy and
  mechanism-building.

---

## Step 4 — Generate the Guide

Always deliver the guide as a **downloadable markdown file**, not inline in chat.

- Save to `/mnt/user-data/outputs/[Company]-TPM-Interview-Prep.md` (use the working directory
  if that path doesn't exist) and share it with `present_files` when available.
- Follow the structure in `references/output-template.md` exactly.
- In chat, add only a short summary: file link, number of rounds covered, and the top 2-3 gaps.

**Length and build.** A full guide can reach 8,000-10,000 words. Build the file in sections rather than
in one write. Default to 5 Q&As per round and include only the rounds the company actually uses or that
sources support. Label rounds you predicted rather than confirmed by an official source as
"(predicted)". If the user wants a shorter guide, offer a compact version (3 Q&As per round).

**Voice.** Write answers the way a person speaks: plain words, short sentences, and no em dashes.

**Quality bar for every Q&A:**
- Reads like a senior TPM with 8-10 years of experience wrote it
- Specific, with no filler like "I worked with stakeholders to align"
- Names the stakeholder tension, the decision, the mechanism, and the measurable outcome
- Metrics and scale consistent with the candidate's real background
- Frameworks applied correctly, not just name-dropped
- First person, in a natural spoken voice (not a written essay)

---

## Error Handling

| Situation | Action |
|-----------|--------|
| No company name or URL | Ask before doing anything else |
| Drive folder or file not found, or connector unavailable | Warn, then offer upload (B) or paste (C) |
| Drive file unreadable (format or permissions) | Warn for that file, continue with the rest |
| No resume found in the Drive location | Ask the user to upload or paste one |
| Multiple resume versions found | Ask which is current |
| Resume uploaded directly | Proceed without Drive |
| Resume text is thin | Ask at most two follow-ups, then proceed |
| Sparse public interview data | State it, infer from culture and comparable companies, flag inferences |
| Job posting URL won't load | Ask the user to paste the posting text |
| Drive search returns someone else's resume | Ignore it. Use only a resume that matches the user's name |
| User has stories or notes not on the resume | Ask for them in Step 0, use them as facts, prefer them over drafted scaffolds |
| User has no stories yet | Proceed with `[add]` and `[verify]` scaffolds, and list "Stories to prepare" in the guide |
| Job ID given with no company | Try one or two searches, then ask for the company or URL |
| Job ID conflicts with the posting URL | Tell the user and ask them to confirm the role |

---

## Output Notes

- Default to **5-6 Q&As per round**. Go up to 10 only if the user asks.
- Include every block defined in `references/output-template.md` for each round.
- The **Gaps & Coaching Notes** section is mandatory. Never omit it.
- After delivering, offer one next step: a mock interview for a specific round, or deeper
  work on a weak story.
