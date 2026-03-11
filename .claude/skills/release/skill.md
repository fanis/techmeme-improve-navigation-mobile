---
name: release
description: Release workflow - bump version, verify docs, commit, tag
disable-model-invocation: true
argument-hint: "[patch|minor|major]"
---

# Release Workflow

Execute a complete release cycle for this project.

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
- `README.md` - update the "Latest Version" line in the header to the new version number

If missing, update them. Ask user to confirm changes look correct.

### 4. Git Commit

- Run `git status` and `git diff --stat`
- Propose a commit message summarizing changes
- Ask user to approve or edit the message
- Once approved, stage all changes and commit

### 5. Create Tag

```bash
git tag X.Y.Z
```

### 6. Push Reminder

Tell the user to manually run:
```bash
git push
git push origin X.Y.Z
```

(Manual push required for authentication)

## Notes

- Always wait for user approval before committing
- The user must push manually due to authentication requirements
