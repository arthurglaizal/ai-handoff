---
name: handoff-copy
description: Create a concise AI handoff from the current conversation and the repository's actual state, then copy it to the clipboard without creating a project file. Use only when the user explicitly invokes `/handoff-copy` or asks to copy an AI handoff.
---

# Handoff Copy

Create an operational handoff for the next AI agent and copy it to the clipboard.

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

Determine the project name from the Git repository root directory, or otherwise the current directory name. Obtain the real local timestamp at execution and include its UTC offset in the document's `Generated` line; do not infer it from the conversation.

## Clipboard output

Copy the complete Markdown exactly once using the clipboard facility available on the system (`pbcopy` on macOS, `wl-copy` or `xclip` on Linux, or PowerShell `Set-Clipboard` on Windows). Avoid passing the handoff as a shell argument; send it through standard input or an equivalent safe mechanism.

Do not create or modify any project file. If no clipboard facility is available or clipboard access is denied, explain the blocker and return the complete Markdown in one fenced block so the user can copy it manually.

After a successful copy, reply with a brief confirmation and do not paste the full handoff unless the user asks.
