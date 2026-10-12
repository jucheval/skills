# Update instructions

## 1. Fetch

Run the following commands regularly in the repository's root directory to keep your fork in sync with upstream:

```bash
git fetch upstream
git log --oneline main..upstream/main
git merge --no-ff upstream/main
```

The `--no-ff` option explicitly preserves a merge commit, even when Git could fast-forward. This makes synchronization events easier to identify in history.

## 2. Merge

Follow [`PATCHES.md` Sync checklist](PATCHES.md#sync-checklist). Then push the validated result:

```bash
git push origin main
```
