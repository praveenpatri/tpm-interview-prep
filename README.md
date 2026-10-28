##Blog on my experience: https://praveenpatri.medium.com/what-if-ai-could-personalize-your-interview-prep-165e38791b89 

# TPM Interview Prep Skill for Claude

A Claude skill that turns a company name (or job posting URL) plus your resume into a
**company-specific TPM interview prep guide**: round-by-round breakdowns, likely questions,
and full answers written from your own experience, plus an honest list of your gaps.

No setup files to edit. Install it, point it at your resume, and go.

## What you get

- Interview process overview (rounds, format, who interviews you, timeline)
- What the company looks for in a TPM, based on their culture and public interview reports
- For each round: what is being tested, what a strong answer looks like, recommended frameworks
- 5-6 questions per round with first-person answers grounded in **your** resume
- A mandatory **Gaps & Coaching Notes** section with bridging strategies
- Company-tailored prep action items
- Output as a downloadable markdown file

## Install

**Claude.ai / Claude Desktop**
1. Download `tpm-interview-prep.zip` from the latest release (or zip the `tpm-interview-prep/` folder yourself).
2. Open Claude's Settings, find the Skills section (under Capabilities), and upload the zip.
3. Make sure Web search is on. Connect Google Drive if you want Claude to read your resume from there.

**Claude Code**
```bash
git clone https://github.com/praveenpatri/tpm-interview-prep.git
cp -r tpm-interview-prep ~/.claude/skills/
```

## First run: what Claude will ask you

There is no setup step. The first time you use the skill, Claude asks for three things in one message:

1. **The company or job posting URL.**
2. **Your background:** a Google Drive folder or file, an uploaded resume, or pasted text.
3. **Anything beyond your resume** (optional): stories and experiences that aren't on your resume, questions
   you've been asked, notes from past interviews, or company research. You can say "skip."

**You don't need to format anything.** Drop your resume and any stories or notes into the same Drive folder,
in whatever form they exist: Google Docs, Word files, PDFs, rough bullet points, even interview transcripts.
Claude reads them, organizes your stories itself, and uses them as facts in the guide.

Claude doesn't remember anything between chats on its own. To avoid re-sharing, keep everything in one
Drive folder and name it each time (for example, "my Job Search folder").

## Use: step by step

1. **Prepare your background.** Save your resume, plus any stories and notes (any format), in Google Drive, ideally in one folder such as "Job Search". No Drive? Keep your resume PDF handy, or have the text ready to paste.
2. **Turn on the tools.** In Claude, enable Web search. If you're using Drive, connect Google Drive.
3. **Start a new chat and ask.** Examples:

   > I have a TPM interview at Stripe next week. My resume is in my Google Drive folder "Job Search".

   > /tpm-interview-prep https://jobs.example.com/technical-program-manager-12345 (resume attached)

4. **Answer Claude's questions.** If you didn't give the company or your background, Claude will ask. It may also ask for your target level or which rounds you've already done.
5. **Wait for the research.** Claude searches for the company's real TPM interview process, reads the job posting, and reads your resume.
6. **Download your guide.** You get a markdown file named `[Company]-TPM-Interview-Prep.md` with round-by-round Q&As written from your experience, plus Gaps & Coaching Notes.
7. **Practice.** Ask Claude to run a mock interview for any round, or to rework any answer that doesn't sound like you. Fill in every `[add: ...]` tag with your real numbers, and keep each `[verify: ...]` detail only if it's true.

Claude accepts your background three ways:

| Option | How |
|--------|-----|
| **Google Drive** (recommended) | Give a folder name, file name, or Drive link. Claude finds your resume and any notes or STAR stories in it. |
| **Upload** | Attach your resume (PDF, DOCX, or text) to the chat. |
| **Paste** | Paste resume text or a short background summary. |

### Reading your guide: the two tags
- `[add: ...]` marks a number or detail your resume doesn't state. Fill it in.
- `[verify: ...]` marks a scenario detail the guide drafted as a scaffold. Keep it only if it's true.

The guide never presents an invented detail as fact, so complete every tag before you practice.

### Tips for the best output
- If your Drive has several resume versions, name the folder or file you want used.
- Put your resume **and** your stories, past interview notes, and company research in one Drive folder, then name that folder in your first message.
- Include stories that are **not** on your resume. They make the best answers.
- Rough is fine. Claude organizes your notes, so you don't need to write them as polished stories.
- Mention your target level (e.g. Senior TPM, L6) if the posting doesn't state it.
- Tell Claude which rounds you've already finished so it can focus the guide.

## Requirements

| Capability | Required? |
|-----------|-----------|
| Web search and web fetch | Yes |
| Google Drive connector | Optional (upload or paste works too) |

## Privacy

The skill contains no personal data. Your resume is read at run time, only to write your guide,
and contact details are kept out of the output. Interview reports from the web are anonymous
and unverified, so treat them as signal, not fact.

## Repo layout

```
tpm-interview-prep/
├── SKILL.md                              # Instructions Claude follows
├── README.md
├── LICENSE
└── references/
    ├── output-template.md                # Structure of the generated guide
    ├── candidate-profile-template.md     # What to extract from a resume
    └── frameworks.md                     # STAR, SPADE, DACI, RICE, and more
```

## Customize

- Change the guide structure in `references/output-template.md`.
- Add or swap frameworks in `references/frameworks.md`.
- Change default question counts in the Output Notes section of `SKILL.md`.

## Contributing

Issues and PRs welcome, especially for better round templates for specific companies and
improvements to the answer quality bar.

## License

MIT. See `LICENSE`.
