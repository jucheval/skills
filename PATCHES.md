# Local patches

This file documents intentional divergences from upstream.

- **Upstream:** <https://github.com/mattpocock/skills>
- **Sync strategy:** Merge `upstream/main` into `main`
- **Policy:** Preserve local requirements while incorporating compatible upstream improvements.

## Patch inventory

| ID | File or path | Change type | Rationale | Sync considerations |
| --- | --- | --- | --- | --- |
| P001 | `skills\productivity\grilling\SKILL.md` | Modified | Use `vscode.askQuestions` for round formatting | Check if upstream comes with a better UI |
| P002 | several files | Modified | Replace "leading word" by "high-signal word" | Check if upstream comes with a better wording |

## Patch details

### P001 — Use `vscode.askQuestions` for round formatting

- **Files:** `skills\productivity\grilling\SKILL.md`
- **Reason:** Simplify the UX reducing friction with hand-written responses.
- **Upstream behavior:** Questions and answers are formatted as plain text with emojis. The user must manually number questions and provide answers in a separate message.
- **Local behavior:** Questions and answers are formatted as a single message using `vscode.askQuestions`. The user can provide answers by clicking buttons.
- **Sync checks:**
  - Check if upstream improves the UX.
- **Introduced after commit:** `2539c23989c06cbb9370faaaffc8fe667e6ed28b`

### P002 — Replace "leading word" by "high-signal word"

- **Files:** `.agents/writing-docs.md`, `docs/engineering/ask-matt.md`, `docs/productivity/wait-what.md`, `docs/productivity/writing-for-agents.md`, `skills/in-progress/writing-fragments/SKILL.md`, `skills/productivity/writing-for-agents/SKILL-MECHANICS.md`, `skills/productivity/writing-for-agents/SKILL.md`
- **Reason:** "high-signal word" is better than "leading word" for the intended meaning ("leading word" may be confused with the first word in a sentence).
- **Upstream behavior:** Use "leading word".
- **Local behavior:** Use "high-signal word".
- **Sync checks:**
  - Check if upstream improves the wording.
- **Introduced after commit:** `e815c83b5fdb062aab0e770eb5c01c816f5bb4ae`

## Sync checklist

- [ ] Review upstream commits since the last sync.
- [ ] Resolve conflicts while preserving intended local behavior.
- [ ] Review every patch listed above.
- [ ] Check for upstream changes that affect local additions, even without conflicts.
- [ ] Update this document if the patch inventory changes.
