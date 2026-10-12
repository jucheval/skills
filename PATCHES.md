# Local patches

This file documents intentional divergences from upstream.

- **Upstream:** <https://github.com/mattpocock/skills>
- **Sync strategy:** Merge `upstream/main` into `main`
- **Policy:** Preserve local requirements while incorporating compatible upstream improvements.

## Patch inventory

| ID | File or path | Change type | Rationale | Sync considerations |
| --- | --- | --- | --- | --- |
| P001 | `skills/example/SKILL.md` | Modified | Adapt instructions to my workflow | Recheck instructions against upstream changes |

## Patch details

### P001 — Adapt example skill

- **Files:** `skills/example/SKILL.md`
- **Reason:** Explain the specific local requirement.
- **Upstream behavior:** Describe the original behavior that matters.
- **Local behavior:** Describe the intended modification.
- **Sync checks:**
  - Check whether upstream changed the same instructions.
  - Verify the skill still follows the current skill format.
- **Introduced in:** `<commit hash or PR>`

## Sync checklist

- [ ] Review upstream commits since the last sync.
- [ ] Resolve conflicts while preserving intended local behavior.
- [ ] Review every patch listed above.
- [ ] Check for upstream changes that affect local additions, even without conflicts.
- [ ] Update this document if the patch inventory changes.
