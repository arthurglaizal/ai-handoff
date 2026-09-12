Install three reusable AI Handoff commands in this AI coding assistant:

- `handoff-md`: create a concise handoff from the available conversation and verified repository state, then save it as `.ai/<project>-handoff-<YYYYMMDD-HHmm>.md`;
- `handoff-copy`: generate the same handoff and copy it to the clipboard without writing a project file;
- `handoff-both`: generate the handoff once, save it, and copy the exact same content.

Ask first whether I want a personal/global installation or a project-only installation. Then consult this assistant's current official documentation and inspect the local environment to find its supported user-invocable extension format and exact destination. Show every destination path and wait for confirmation before writing.

Keep the three commands separate and explicitly invoked. Start each handoff with its local generation time and source assistant. When Git is available, add the branch, short commit, and whether the working tree is clean. Each handoff must contain `Goal`, `Current state`, `Relevant files`, and `Next steps`. Add `Key context` only for decisions, constraints, rationale, or failed approaches that affect continuation. Add `Open issues` only for real blockers or unresolved questions.

Aim for 300 to 700 words and stay under 1,000 unless more detail is genuinely necessary. Inspect only the relevant repository state with lightweight, read-only checks. Do not scan the full architecture, run tests, install dependencies, or inspect broad history solely to create the handoff. Distinguish verified facts from discussion, mention material uncommitted work, avoid secrets, use the user's language, and never overwrite an existing handoff.

Use the host's safe clipboard mechanism. If clipboard access is unavailable, return the full Markdown in one fenced block. Do not install deprecated formats by default, overwrite existing commands without permission, add dependencies, or change unrelated configuration.
