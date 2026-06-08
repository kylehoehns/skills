---
name: catchup
description: Use when the user returns to an existing session after a break and says "/catchup" or "catch me up". Reconstructs context from the current session's history and delivers a brief summary of where things left off, key decisions made, and what's next.
---

# Catchup

Rebuild context for the current session, then deliver a crisp summary so the user can resume work immediately.

## Getting the history

Use the first source that works, in this order:

1. **In-context history.** If this conversation's earlier turns are still in your context, use them directly — no lookup needed.
2. **A session-query tool.** If your platform exposes one (e.g. a session store / SQL tool), query it for recent turns, milestones, and any referenced PRs/issues/commits.
3. **The on-disk transcript.** Otherwise locate this session's transcript file and read it. Agent CLIs store sessions under a per-user config dir, typically keyed by working directory and a session id. Discover it:
   - Check env vars for a session id and config/home path (names vary: `*SESSION_ID*`, `*_HOME`, `XDG_CONFIG_HOME`).
   - Look under `~/.<tool>/` or `~/.config/<tool>/` for a `sessions`, `projects`, or `history` directory; the current session is usually the most-recently-modified file there.
   - Transcripts are commonly JSONL (one event per line) or SQLite. Extract user/assistant turns plus any file-edit or tool-call records. Do **not** dump the whole file into context — pull just the recent turns and the list of files touched.

If none of these yield history, say so plainly and summarize only what's in context.

### Known platforms (shortcut for step 3)

- **Claude Code:** `~/.claude/projects/<cwd>/$CLAUDE_CODE_SESSION_ID.jsonl`, where `<cwd>` is the working directory with `/` and `.` replaced by `-` (e.g. `/Users/me/dev` → `-Users-me-dev`). JSONL; conversational turns have `type: "user"` / `type: "assistant"`, and file edits appear as `tool_use` blocks with `name` in `Edit`/`Write`. The file also contains non-conversational events (`attachment`, `file-history-snapshot`, `mode`, `system`, etc.) — ignore them. A record's `message.content` may be a plain string **or** an array of typed blocks (`text`, `tool_use`, `tool_result`); a `user` record is often a tool result or a large injected attachment, not a real prompt. Filter to genuine prompts and `text` blocks before summarizing.
- **GitHub Copilot CLI:** use the `session_store_sql` tool. Query checkpoints, recent turns, session refs, and session files.

## What to extract

- **Recent turns** (last ~15–20) — the freshest state of play. Filter to real conversational turns *first*, then take the last N. In transcript formats, tool calls, tool results, and attachments each occupy their own line, so a raw "last N lines" slice is **not** the last N exchanges.
- **Files / areas touched** — from edit or tool-call records; summarize by module or directory, not individual files.
- **Refs** — PRs, issues, or commits mentioned in the turns. Skip if none.

Ignore the `/catchup` request itself — it is usually the most recent entry. Summarize the work that came *before* it, not the act of asking for the summary.

## Output

Deliver exactly this format:

---
**Where we left off**

[1–2 sentence prose: what we were working on, the goal, and the current state]

**Key decisions**
- [decision or conclusion reached, with brief rationale if captured]

**What's next**
- [the next logical step or open item, if determinable]

**Areas touched**

[One sentence on modules/directories affected — skip if only one file or trivial]

---

Do not ask follow-up questions. Output the summary and stop.
