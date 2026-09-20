<p align="center">
  <img src="assets/ai-handoff-demo.gif" alt="AI Handoff demo: move an active coding session from Claude Code to Codex without losing context" width="960">
</p>

# AI Handoff

> **Continue your work in another AI without starting over.**


AI Handoff packages the context and current project state needed to pick up the same work in Claude Code, Codex, or another AI agent.

## Commands

| Output | Claude Code | Codex |
| --- | --- | --- |
| Timestamped Markdown file | `/handoff-md` | `$handoff-md` |
| Clipboard only | `/handoff-copy` | `$handoff-copy` |
| File and clipboard | `/handoff-both` | `$handoff-both` |

`handoff-md` and `handoff-both` save the document as:

```txt
.ai/<project>-handoff-<YYYYMMDD-HHmm>.md
```

Example:

```txt
.ai/ios-todo-list-handoff-20260912-1646.md
```

## Example output

Here is a realistic example generated while moving an unfinished iOS project to another AI: [iOS Todo List handoff](examples/ios-todo-list-handoff-20260912-1646.md).

Every handoff records when it was generated, which assistant created it, and a compact Git reference when available. The exact model and destination are intentionally omitted so the handoff stays portable.

## Why?

When you move from one AI to another, the files come with you but the working context usually does not. The new agent can see the code, but not necessarily the goal, the decisions already made, what was tried, or what should happen next.

A raw transcript is too long. A conversation-only summary can contradict the repository. AI Handoff combines the useful context from the conversation with the work that actually exists in the project.

AI Handoff checks both sources and gives the next agent what it needs to continue:

- the objective and current state;
- important decisions and completed work;
- problems, open questions, and constraints;
- relevant files and recommended next steps;
- useful conversation context that the repository cannot show.

## What it does

The command reads the conversation context still available to the agent and checks only the repository state relevant to the active work. It does not scan the full architecture or run tests just to create a handoff. It distinguishes verified repository facts from discussion, mentions material uncommitted work, and avoids including secrets.

The generated handoff normally stays between 300 and 700 words, with a soft limit of 1,000 words for unusually complex work. It is not a transcript, a full project history, or a replacement for Git documentation.

## Continue in another AI

Start a new conversation in the other AI and give it the generated Markdown file or paste the clipboard content. The handoff is written so the new agent can verify the current state and continue from the recommended next step without needing the original conversation.

## File naming

The project name is detected from the Git repository root, normalized to lowercase kebab-case, and followed by the real local timestamp. Existing files are never overwritten: seconds or a numeric suffix are added if necessary.

Multiple handoffs can coexist in `.ai/`, making it possible to retain previous transfer points when that is useful. Remove old ones whenever they are no longer relevant.

## Install in Claude Code

### Assisted installation

Paste [install-handoff-for-claude-code.md](prompts-for-installation/install-handoff-for-claude-code.md) into Claude Code. It checks the current official format and lets you choose a personal or project installation before writing anything.

### Manual installation

Clone this repository, enter it, then link the three skills into your personal skills folder:

```sh
mkdir -p "$HOME/.claude/skills"
ln -s "$PWD/.claude/skills/handoff-md" "$HOME/.claude/skills/handoff-md"
ln -s "$PWD/.claude/skills/handoff-copy" "$HOME/.claude/skills/handoff-copy"
ln -s "$PWD/.claude/skills/handoff-both" "$HOME/.claude/skills/handoff-both"
```

For a project-only install, copy the three folders from `.claude/skills/` into the project's `.claude/skills/` folder. Confirm the current locations in the [Claude Code skills documentation](https://code.claude.com/docs/en/skills) if they change.

## Install in Codex

### Assisted installation

Paste [install-handoff-for-codex.md](prompts-for-installation/install-handoff-for-codex.md) into Codex. It checks the current official format and lets you choose a personal or project installation before writing anything.

### Manual installation

Clone this repository, enter it, then link the three skills into your personal skills folder:

```sh
mkdir -p "$HOME/.agents/skills"
ln -s "$PWD/.agents/skills/handoff-md" "$HOME/.agents/skills/handoff-md"
ln -s "$PWD/.agents/skills/handoff-copy" "$HOME/.agents/skills/handoff-copy"
ln -s "$PWD/.agents/skills/handoff-both" "$HOME/.agents/skills/handoff-both"
```

For a project-only install, copy the three folders from `.agents/skills/` into the project's `.agents/skills/` folder. Confirm the current locations in the [Codex skills documentation](https://learn.chatgpt.com/docs/build-skills) if they change.

Codex uses `$handoff-md`, `$handoff-copy`, and `$handoff-both`, not custom root slash commands.

## Other AI assistants and regular chats

- For another coding assistant, paste [install-handoff-for-any-ai.md](prompts-for-installation/install-handoff-for-any-ai.md).
- For ChatGPT, Claude, Gemini, or another regular chat, paste [handoff-ai-chat-version.md](prompts-for-ai-chat/handoff-ai-chat-version.md).

Clipboard access depends on the host. If it is unavailable, the command returns the Markdown in a copyable code block.

## Repository structure

```txt
ai-handoff/
├── README.md
├── LICENSE
├── .agents/skills/
│   ├── handoff-md/
│   ├── handoff-copy/
│   └── handoff-both/
├── .claude/skills/
│   ├── handoff-md/
│   ├── handoff-copy/
│   └── handoff-both/
├── examples/
│   └── ios-todo-list-handoff-20260912-1646.md
├── prompts-for-installation/
│   ├── install-handoff-for-claude-code.md
│   ├── install-handoff-for-codex.md
│   └── install-handoff-for-any-ai.md
└── prompts-for-ai-chat/
    └── handoff-ai-chat-version.md
```

## More AI workflow commands

| Command | What it does |
| --- | --- |
| [WaitGo](https://github.com/arthurglaizal/wait-go) | Batches your instructions, then executes only when you say go. |
| [Session Recap](https://github.com/arthurglaizal/session-recap) | Recaps what you did in the current session and what to pick up next. |
| [Noob Command](https://github.com/arthurglaizal/noob-command) | Rewrites the last AI answer in simple, concise language. |
| [Ask Mode](https://github.com/arthurglaizal/ask-mode) | Lets you question your codebase without the assistant changing anything. |
| [FYI](https://github.com/arthurglaizal/fyi-command) | Gives your assistant context without giving it a task. |

## Support

If you find my work useful, you can [buy me a coffee](https://ko-fi.com/arturo_ux) ☕️

## License

MIT. See [LICENSE](LICENSE).
