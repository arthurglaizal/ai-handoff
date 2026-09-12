Install the three reusable AI Handoff skills in Claude Code: `handoff-md`, `handoff-copy`, and `handoff-both`.

Their behavior must match the source files in this repository's `.claude/skills/` directory. Do not merge them into one command with arguments.

Follow these steps:

1. Ask whether I want a personal/global installation (recommended) or a project-only installation, then stop and wait for my answer.
2. Consult the current official Claude Code documentation and inspect my installed version. Determine the current recommended skill format, required files, and exact location for the selected scope. Treat remembered paths as hypotheses, not facts.
3. Show the fully expanded destination paths before writing. If they are outside the workspace, state that approval may be required. Wait for confirmation.
4. Check for existing files and symbolic links in the resolved current location and any documented deprecated locations. Never overwrite an existing installation without showing the differences and asking.
5. Install all three source skill folders, adapting only metadata fields required by the current documented format. Preserve their names, explicit-only invocation policy, behavior, and separate triggers.
6. Validate that all three skills are discoverable and report their exact invocations plus whether Claude Code needs a restart or a new conversation.

Do not install deprecated formats by default, change Claude Code configuration, add dependencies, or modify unrelated files.

