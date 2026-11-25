# PM Interview Coach

![PM Career Desk icon](assets/pm-career-desk-icon-512.png)

PM Interview Coach is a plugin for program and project managers, PMO leads and technical program managers (and close roles such as product manager, scrum master, delivery manager, business analyst and IT manager) who are preparing for a job interview in the US job market. It bundles six skills with the PM Career Desk connector. You paste your resume and, if you have one, the job posting. The tools read them with fixed rules written by practitioners and return the requirements of the posting with your own resume lines, the questions a hiring manager is likely to ask, and structure checks of your practice answers. Claude runs the conversation in your own session and gives feedback built only from facts you supplied.

The skills instruct Claude never to invent a figure, employer, date or outcome for you, to ask one question at a time, to let you answer first in your own words, and never to promise any result of an interview. Missing facts are asked for and marked as placeholders, not filled in.

## What is in this plugin

- Six skills, each in its own folder under `skills/`:
  - `interview-prep`: prepares you for an interview from your resume and the job posting (or a handoff code): the main requirement, a requirement table with your resume lines, 8 to 10 likely questions with what each answer must prove, inconsistencies, a day by day plan, a check of the written prep against your resume, then practice one question at a time and a scorecard.
  - `resume-job-match`: shows how your resume matches one posting, then helps you rework it for that job one missing requirement at a time, only from what you really did.
  - `resume-review`: reviews the whole resume line by line, or one bullet.
  - `linkedin-check`: checks your LinkedIn headline, About section and top experience entry for recruiters.
  - `mock-interview`: a mock interview with a scorecard, and practice progress across chats (signed-in accounts).
  - `pm-title-and-archetype`: which title fits your work (project manager, program manager or TPM) and the PM Archetype test, for reflection.
- `.mcp.json`: one remote MCP server, PM Career Desk, at `https://app.pmcareerdesk.com/mcp`.
- The assets folder: the PM Career Desk icon in SVG and PNG.

The plugin runs nothing on your computer: no scripts, no hooks, no package installs.

## The tools of the PM Career Desk connector

Ten free tools need no sign-in and are read-only:

- `prepare_interview_questions`: reads the resume and the optional posting with fixed rules and returns every resume line with its number, each requirement with a call (covered, partial, not_found, not_checked) and the resume lines found for it, the main requirement, inconsistencies of dates and figures, up to 10 likely questions with what each answer must prove, and a plan by the days left to the interview. The interview stage and the interviewer's title shift the mix of questions. It can also check a written prep draft against the resume, and it reads a handoff code.
- `check_interview_answer`: checks the structure of one practice answer (situation, your own action, result, a before and after figure or a named record, length, filler words, the balance of "we" and "I").
- `review_resume`: reads the whole resume and returns at most 12 flagged lines, each with the finding and the question a hiring manager may ask.
- `check_resume_line`: checks one resume bullet and returns one finding and one question a hiring manager may ask about it.
- `match_resume_to_job`: matches the posting requirements to your resume lines (covered, partial, gap), with the years and budget sizes the resume shows.
- `check_linkedin_profile`: checks a LinkedIn headline and About section and returns up to 10 findings, each with the question a recruiter may ask, plus a score per section.
- `get_pm_title_fit_questions` and `match_pm_title`: nine questions that compare project manager, program manager and technical program manager for your current work, and the closest title.
- `get_pm_archetype_test` and `score_pm_archetype`: the PM Archetype test, for reflection, not a psychometric or hiring assessment.

Nine tools work only after you sign in to a PM Career Desk account that has access:

- `prepare_interview_plan`: the full interview plan, every question by interview stage.
- `export_prep_pack`: the plan as a Word file, with a download link that works once.
- `build_story_bank`: 10 to 15 STAR stories built only from your resume lines, with the questions still open.
- `draft_30_60_90_plan`: a 30-60-90 day plan skeleton for one posting; you set the targets.
- `start_mock_interview`, `answer_mock_question` and `finish_mock_interview`: a mock interview of 5 to 10 questions for one stage, one question at a time, with follow-up questions picked from the structure of your answers, ending with a scorecard by competency. You write every answer.
- `save_practice` and `get_practice`: save a practice attempt when you ask, and read your progress in a later chat.

## The handoff code

On the PM Career Desk site or in its Chrome extension you can save your resume and a job posting and get a handoff code of the form PCD-XXXX-XXXX-XXXX-XXXX. Paste the request it gives you into Claude, and the tools read the resume and the posting from the code instead of the chat. The code holds them with personal details removed and encrypted, for up to 2 hours (and for 30 minutes after its first read); after that they are gone.

## Install

In Claude (web, desktop, Cowork), once the plugin is listed in the directory: open Customize, then Plugins, find PM Interview Coach and add it. Then connect the PM Career Desk connector from the plugin's Connectors tab (no account is needed for the free tools).

You can also add only the connector: Customize, then Connectors, then Add custom connector, with the URL `https://app.pmcareerdesk.com/mcp`.

In Claude Code:

```
claude plugin marketplace add DmitriiSelkov/pm-interview-coach
claude plugin install pm-interview-coach@pm-career-desk
```

Then ask, for example:

- "I have a program manager interview next week. Here is my resume and the job posting: prepare me."
- "Do I fit this TPM posting? What is missing from my resume?"
- "Review my whole resume for a PMO lead role and show me the lines a hiring manager is likely to question."
- "Check my LinkedIn headline and About section."
- "Interview me for the hiring manager round, one question at a time."
- "Am I a project manager or a program manager? Ask me the title fit questions."

## What is sent, and privacy

When a skill calls a tool, Claude sends the text the tool needs (the resume text, the job posting, the interviewer's title or profile text if you give them, a prep draft to check, a LinkedIn headline and About, or one practice answer) to `https://app.pmcareerdesk.com/mcp`. Nothing else is sent: not your other conversations, not your files, not Claude's memory. Contact details are removed before the rules read the text.

We do not store the text you send through the connector. We count which tool was used. The count uses an anonymous code: a salted hash of the Claude session or of your connector sign-in, or, when there is neither, of the network, changed every 30 days; never your IP address itself, and never your text.

A handoff code is made on the PM Career Desk site or in its Chrome extension, not in Claude: what you save there is held under the code with personal details removed and encrypted, for up to 2 hours, then deleted.

One exception, only with a signed-in account: practice you ask to save, the mock interview and a prep file. With a signed-in account, the tool and its outcome are also noted in your free Career file, without any text you sent. By default only the progress is saved (question id and type, structure checks met, word count, date). The text of an answer, together with the text of its question, is kept only when you ask, encrypted with your account key (in a mock interview, for an answer not in English, its English translation). Every saved item is deleted after 180 days or with your account. During a mock interview the session holds the questions (they quote lines of your resume), your answers and their structure checks, encrypted with your account key. When you finish, the progress of each answer is saved to your practice unless you ask to save nothing, the answers leave the session and only the scorecard stays; every session, finished or not, is deleted 24 hours after it started. A prep file is built in memory and kept in temporary memory on our server for its one download. The link stops working after 10 minutes; a file that was not downloaded is deleted at the next cleanup of that memory or when the server restarts.

Links in tool results go to pages of pmcareerdesk.com and carry `from=claude` and the tool name, so we can count visits that came from Claude. They carry nothing about you.

Your conversation with Claude is governed by Anthropic's terms and privacy policy. Our Privacy Notice: <https://pmcareerdesk.com/privacy/>. Terms: <https://pmcareerdesk.com/terms/>.

## AI disclosure

Reed (AI) is the PM Career Desk analyst named in the tool results. Reed is software, not a person. The questions and structure checks come from fixed rules written by the PM Career Desk team; no person reads what you send. The conversation and the feedback are written by Claude, an AI model, in your own Claude session. You decide what to say in an interview.

## Limits

- English resumes and postings; for a resume in another language the tools read its literal English translation. Resume up to 30,000 characters, posting up to 15,000, one answer up to 6,000.
- For some large US employers the questions include some built from the principles and hiring pages the company publishes, with links to those pages. They are our questions, not the company's.
- The checks read structure and wording. They do not judge whether a story is true, and a requirement the rules did not find on the resume is not proof that you lack it.

## Support

Email support@pmcareerdesk.com. Documentation: <https://pmcareerdesk.com/interview-coach/?from=claude>.

PM Career Desk is a service of PME Consulting, Inc. This plugin is not made or endorsed by Anthropic.

## License

All rights reserved; you may install and use the plugin, not copy or redistribute it. See the LICENSE file.
