---
name: worklog-daily
description: Record a coding session (today by default) into a daily worklog.
argument-hint: "[today | yesterday | YYYY-MM-DD — defaults to today]"
disable-model-invocation: true
---

Maintain one persistent daily record across ALL SESSIONS active today, across any nested project repos. 
The goal is to capture the technical details that allows the user to reproduce the work done independently and record lessons learned that can improve future work for agents.

## Steps

1. Resolve the **effective date**: the user's named date or keyword ("today"/"yesterday"/`YYYY-MM-DD`). With nothing named, default to yesterday. Then apply the 04:00 rule: if the resolved date is today and the current local time is in between 00:00 and 04:00, shift it back one day — work from midnight to 04:00 belongs to the prior day.
2. Open `~/worklogs/daily/<effective-date>.md` (create `~/worklogs/daily/` if absent). 
3. An existing file should be updated, not replaced — read it in full first to avoid overlaps and identify points to update.
3. Across all sessions active today, record technical details of:
  - Resolved problems with their fix.
  - Decisions made with their tradeoffs. 
  - User input and intervention. What did the user steer the agent to do, and what was the agent doing wrong or differently? 
  - Debugging commands that diagnosed something and the reasoning behind the troubleshooting steps.
  - Operation commands with real effect like builds, deploys, migrations, test runs.
  - Copy commands verbatim from tool calls or shell history, never from memory.
  - Skip commands that led nowhere or are insignificant, unless they led to a troublesome debugging session that produced a lesson worth recording. In that case, record the learning points and the commands that led to it.
  - Attach commit IDs within the time range of the worklog, if any.
4. For each resolved problem, ask the user what the takeaway was, never invent it. The log's value is the user's own lesson, in their own words.
5. Confirm with the user which drafted entries earn a line. 
6. If a project has a `.changelog-id` and has major architectural changes or added features, flag that a `worklog-changelog` entry may be necessary and offer to run it.
7. Never overwrite existing content. Update existing content if changes overlap with prior entries. 
8. Append the confirmed entries under the effective date's heading, using the template below. The format is flexible to allow for different problem types, but the following fields are recommended for each entry:

# [<>] <short title>
- Task: <problem/goal>                     (omit for a pure decision)
- Process: <solution/steps>               (omit for a pure decision)
- Commands: <verbatim, only the crucial ones>
- Decision / tradeoff: <what was chosen, what was given up, and why>
- Lesson: <the user's own takeaway>
```

## Reference

- One file per day, `~/worklogs/daily/<date>.md` — read then merge or update, never overwrite.
- Enough details should be captured to reproduce and debug the work independently, but not so much that it becomes a transcript of every keystroke.
