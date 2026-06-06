# unikong-public — session bootstrap

**On session start, read [`HANDOFF.md`](./HANDOFF.md) first, then resume the
re-alignment from there.** It has the full context — what this repo is, the open
decisions, the pending `whim-releases → unikong-public` rename refs, and the
auto-update state. You do not need a typed prompt; `HANDOFF.md` is the brief.

## What this repo is

`UniKongAI/unikong-public` (PUBLIC) — the **org-level public distribution channel**
for UniKong products (renamed from `whim-releases` 2026-06-06; old name redirects).
Holds the Whim desktop (Windows) installers, the WinSparkle EdDSA appcast, and a
multilingual download README.

## Rules

- **NOT an auto-push repo** — commit *and* push only with Steven's explicit
  approval (only `whim-doc` + `unikong-bridge` auto-push).
- Cross-repo ref edits (esp. `whim-app`'s WinSparkle feed URL — Morgan's shipped
  code) need approval + a sync with Morgan before pushing.
- Re-alignment session: settle the `HANDOFF.md` Open decisions with Steven before
  mass edits; one question at a time.
