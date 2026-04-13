# Claude Second Brain

A template for building a persistent "second brain" that gives Claude (or any LLM) continuity across sessions — so you don't have to re-explain yourself every time context is lost or a new conversation starts.

## The Problem

Claude loses context when:
- A conversation gets too long and is compacted
- You start a new session
- You switch between devices (mobile, web, desktop)

This repo solves that by giving you a structured set of markdown files that Claude can read at the start of any session to get back up to speed.

## How It Works

1. **Fork or copy this template** into a private repo
2. **Fill in the context files** with your own information
3. **Create a GitHub PAT** scoped to that repo (Settings > Developer Settings > Fine-grained tokens > Contents read/write)
4. **Save a bootstrap snippet** in your password manager (see below)
5. **Paste the snippet** at the start of any Claude session to load your context

### Bootstrap Snippet (save in your password manager)

```
Fetch and read these files from my GitHub repo using the API:
- https://api.github.com/repos/YOUR_USERNAME/YOUR_REPO/contents/BOOTSTRAP.md
- https://api.github.com/repos/YOUR_USERNAME/YOUR_REPO/contents/ACTIVE.md
Use header: Authorization: Bearer YOUR_PAT_HERE
```

### For Claude Code users

If you use Claude Code, the repo can be cloned locally and read directly from disk — no PAT needed for local sessions.

To get started, paste this prompt into Claude Code:

```
I have a "second brain" template repo at github.com/YOUR_USERNAME/YOUR_REPO (private).
Clone it locally, read BOOTSTRAP.md for instructions, then help me fill in the context
files (profile.md, work.md, projects.md, etc.) with my information. After we're done,
commit and push the changes. Also, save a memory note so you remember this repo exists
and where to find it in future sessions.
```

Claude Code will clone the repo, walk you through populating each file, and set up persistent memory so future sessions know where your second brain lives.

## Repo Structure

```
second-brain/
  ACTIVE.md              # What matters this week (load every session)
  BOOTSTRAP.md           # Instructions Claude gets on load
  context/
    profile.md           # Stable personal context
    work.md              # Job, career, active priorities
    projects.md          # Active builds and side projects
    finances.md          # High-level financial context (no sensitive specifics)
    health.md            # Training, nutrition, wellness
  sessions/
    YYYY-MM-DD.md        # Per-session snapshots when important context needs preserving
```

## Tips

- **ACTIVE.md is the key file.** Keep it under ~500 lines. It should answer: what's in flight, what decisions are pending, what you shouldn't have to re-explain.
- **Rotate ACTIVE.md weekly** or when major things resolve.
- **Don't put sensitive specifics in GitHub** — no account numbers, exact comp figures, or credentials. Keep financial/work files high-level and paste specifics directly into conversations when needed.
- **Use session snapshots** when a conversation is getting long. Ask Claude to write a state snapshot before context is lost, save it to `sessions/YYYY-MM-DD.md`, and load it in the next session.
- **Let Claude update the files.** At the end of productive sessions, ask Claude to write updates back to the relevant files.

## Security Notes

- Always use a **private repo**
- Scope your PAT to **only this repo** with **Contents read/write** only
- Your PAT will be visible in Claude conversation logs (Anthropic's data retention) — use a tightly scoped token and rotate periodically
- Never store credentials, account numbers, or sensitive financial details in these files

## License

MIT — use however you like.
