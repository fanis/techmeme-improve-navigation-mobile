---
name: push
description: Bump version, verify docs, commit (no tag/release)
disable-model-invocation: true
argument-hint: "[patch|minor|major]"
---

# Push Workflow

Bump version, verify, and commit - without creating a git tag or GitHub release.

## Steps

### 1. Determine Version

- Read current version from the `@version` line in `src/techmeme-improve-navigation.js`
- Based on `$ARGUMENTS` (patch/minor/major), calculate new version
- If no argument, suggest based on changes (features = minor, fixes = patch)
- Show: "Version bump: X.Y.Z -> A.B.C"

### 2. Bump Version

Update the `@version` line in `src/techmeme-improve-navigation.js`.

### 3. Verify Documentation

Check that these reflect the new version and changes:
- `CHANGELOG.md` - has section for new version with changes
- `README.md` - version number updated

If missing, update them. Ask user to confirm changes look correct.

### 4. Git Commit

- Run `git status` and `git diff --stat`
- Propose a commit message summarizing changes
- Ask user to approve or edit the message
- Once approved, stage all changes and commit

### 5. Push

```bash
git push
```

No tag is created - use `/release` when ready to tag and trigger a GitHub release.

## Notes

- Always wait for user approval before committing
