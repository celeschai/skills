---
name: worklog-daily
description: Record a coding session (today by default) into a daily worklog.
argument-hint: "[today | yesterday | YYYY-MM-DD — defaults to today]"
disable-model-invocation: true
---

Maintain one persistent daily record across ALL SESSIONS active today, across any nested project repos. 
The goal is to capture the technical details that allows the user to reproduce the work done independently and record lessons learned that can improve future work for agents.

## Steps

1. Use a low cost subagent to find all sessions (including nested repo sessions) for the provided timerange ("today"/"yesterday"/`YYYY-MM-DD`). Work from 0000h to 0400h belongs to the prior day. 
2. Open `~/worklogs/daily/<effective-date>.md` (create `~/worklogs/daily/` if absent). 
3. An existing file should be updated, not replaced, read it in full first to avoid overlaps and identify points to update. Keep metadata for the latest seen message or timestamp for each session processed so update runs know where to resume.
4. Across all sessions active today, identify and number the main tasks completed. For each task, spin a mid cost subagent on low effort to record technical details of:
    - Resolved problems with their fix.
    - Decisions made with their tradeoffs. 
    - User input and intervention that steered the agent's action. What did the user steer the agent to do, and what was the agent doing wrong or differently? 
    - Debugging commands that diagnosed something. Reasoning behind any troubleshooting steps taken (files checked, data compared, memory managed, etc). Include code snippets if buggy code was fixed and explain why was that change the key.
    - Operation commands with real effect like builds, deploys, migrations, test runs.
    - Copy commands verbatim from tool calls or shell history, never from memory.
    - Skip commands that led nowhere or are insignificant, unless they led to a troublesome debugging session that produced a lesson worth recording. In that case, record the learning points and the commands that led to it.
    - Check with `git log` first. Attach commits within the time range of the worklog, if any.
5. Confirm with the user which drafted entries should be included.
6. Ask the user what are some takeaways or lesson learnt was, never invent it, the point is for the user to recap in their own words. Add details if the user requests for it in the point they bring up in the takeway.
7. Never overwrite existing content. Update existing content if changes overlap with prior entries. 
8. Append the confirmed entries. The format is flexible to allow for different problem types, but the fields provided in `template.md` are recommended for each entry.
9. Be concise, factual, and technical. Avoid paragraphs. Break into bullet points if many sentences are needed for one section of an entry.
10. If a project has a `.changelog-id` and has major architectural changes or added features, flag that a `worklog-changelog` entry may be necessary and ask user if the skill should be invoked.


## Reference

- One file per day, `~/worklogs/daily/<date>.md` — read then merge or update, never overwrite.
- Refer to `template.md` for the recommended format of each entry.
- Refer to latest past worklog for examples.

