---
name: handoff-md
description: Create a concise AI handoff from the current conversation and the repository's actual state, then save it as a timestamped Markdown file in .ai. Use only when the user explicitly invokes `/handoff-md` or asks to create and save an AI handoff.
---

# Handoff MD

Create an operational handoff for the next AI agent and save it to the current project.

## Gather only what matters

Use the conversation context currently available and the repository's actual state. Start with lightweight, read-only checks: repository root, current branch, `git status`, and diff summaries when Git is available. Read only the diffs and files that are relevant to the active work.

Do not scan the full repository, reconstruct its architecture, run tests, install dependencies, or inspect broad history solely to create the handoff. Record test results or commits already available in the conversation or repository when they matter.

Never claim that discussed work exists unless it is verified. If the conversation conflicts with the repository, use the repository as the current state and mention the discrepancy only when it affects continuation. Do not reconstruct conversation content that is no longer available.

## Handoff content

Aim for 300 to 700 words. Stay under 1,000 words unless more detail is genuinely required to continue safely. Prefer file paths and precise pointers over explanations the receiving agent can retrieve from the project.

Use the user's language and this structure:

```markdown
# AI Handoff: <project name>

Generated: <local timestamp with timezone>
Source: Claude Code
Git: <branch> @ <short commit>, <clean or uncommitted changes>

## Objective

## Current state

## Key context

## Relevant files

## Next steps

## Open issues
```

`Goal`, `Current state`, `Relevant files`, and `Next steps` are required. Include `Key context` only for decisions, constraints, rationale, or failed approaches that change how the work should continue. Include `Open issues` only when real blockers or unresolved questions remain. Omit optional sections when empty.

Include the `Git` line only when Git information is available. If the repository is in detached HEAD state, say so instead of inventing a branch. The source is the assistant creating the handoff, not the model name or the intended destination.

Keep `Current state` focused on what is done, what is in progress, material uncommitted changes, and known validation results. List only the files the receiving agent is likely to open first, with a short reason for each. Use repository-relative paths for project files. Make the first next step concrete and directly actionable.

Omit trivial commands, exhaustive change logs, general architecture, information already obvious from the code, and abandoned exploration with no impact.

Do not include secrets, credentials, tokens, private keys, `.env` values, or credential-looking literals. Refer to their file or variable name only when necessary.

## File output

1. Determine the project name from the Git repository root directory. If the current directory is not in a Git repository, use the current directory name.
2. Normalize it to lowercase kebab-case using only `a-z`, `0-9`, and `-`.
3. Obtain the real local time at execution. Use `YYYYMMDD-HHmm` in the filename and include the UTC offset in the document's `Generated` line. Do not infer it from the conversation.
4. Create `.ai/` at the project root if needed.
5. Write the handoff to `.ai/<project>-handoff-<YYYYMMDD-HHmm>.md` using UTF-8.
6. Do not overwrite an existing file. If the minute-level filename exists, append seconds as `YYYYMMDD-HHmmss`; if it still exists, add a numeric suffix.

After writing, reply with the exact file path and one brief sentence describing the handoff's scope. Do not paste the full handoff unless the user asks.

## Constraints

Only create the handoff file and its `.ai/` directory. Do not modify project code, configuration, `.gitignore`, or any other file. Do not commit or push.
