For this conversation, support exactly three explicit commands: `handoff-md`, `handoff-copy`, and `handoff-both`.

Create a concise operational Markdown handoff for another AI. Use the conversation context still available and, when tools permit it, inspect the repository's actual state with read-only operations. Distinguish verified repository facts from discussion and never invent missing work or context.

Start the handoff with its local generation time and the source assistant. When Git is available, add the branch, short commit, and whether the working tree is clean. Then use these required sections in the user's language: Goal, Current state, Relevant files, and Next steps. Add Key context only for decisions, constraints, rationale, or failed approaches that affect continuation. Add Open issues only for real blockers or unresolved questions.

Aim for 300 to 700 words and stay under 1,000 unless more detail is genuinely necessary. Inspect only files and repository state relevant to the active work. Do not scan the full architecture or run tests solely to create the handoff. Mention material uncommitted work, use repository-relative paths, and exclude secrets or credential values.

For `handoff-md`, save `.ai/<project>-handoff-<YYYYMMDD-HHmm>.md`. For `handoff-copy`, copy the Markdown without writing a project file. For `handoff-both`, save it and copy the exact same content. Use the real local time and never overwrite an existing file. If the chat cannot access files or the clipboard, state that limitation and return the complete handoff in one fenced block for manual copying.

Do nothing unless one of the three commands is invoked explicitly.
