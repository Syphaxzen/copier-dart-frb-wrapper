---
name: release-template
description: Create a new release of the Copier template. Use when user wants to release a new version, create a tag, or publish the template.
---

# Release Template

Guide for releasing new versions of copier-dart-frb-wrapper.

## Quick Release Checklist

```bash
# 1. Ensure all changes are committed
git status

# 2. Update CHANGELOG.md (move [Unreleased] to new version)
# 3. Commit changelog
git add CHANGELOG.md
git commit -m "chore: prepare release v1.x.x"

# 4. Create and push tag
git tag v1.x.x
git push origin main
git push origin v1.x.x

# 5. Create GitHub Release (optional)
gh release create v1.x.x --title "v1.x.x" --notes-file <(sed -n '/## \[1.x.x\]/,/## \[/p' CHANGELOG.md | head -n -1)
```

## Versioning Rules

Use [Semantic Versioning](https://semver.org/): `vMAJOR.MINOR.PATCH`

| Change Type | Version Bump | Examples |
|-------------|--------------|----------|
| Breaking changes | MAJOR | Renamed/removed variables, changed defaults that break existing projects |
| New features | MINOR | New variables, new template files, new conditionals |
| Bug fixes | PATCH | Typo fixes, documentation updates, minor corrections |

## CHANGELOG.md Format

```markdown
## [Unreleased]

## [1.1.0] - 2025-01-28

### Added
- New `my_variable` for custom configuration

### Changed
- Updated default `flutter_version` to 3.38.4

### Fixed
- Corrected WASM build configuration

### Removed
- Deprecated `old_variable`

[Unreleased]: https://github.com/djx-y-z/copier-dart-frb-wrapper/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/djx-y-z/copier-dart-frb-wrapper/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/djx-y-z/copier-dart-frb-wrapper/releases/tag/v1.0.0
```

## Pre-Release Verification

Before releasing, verify:

### 1. Test all configurations

```bash
# Basic
rm -rf /tmp/test && copier copy . /tmp/test --trust --defaults \
  --data package_name=test \
  --data description="Test" \
  --data native_library_name=lib \
  --data github_repo=u/r \
  --data native_repo=o/lib
ls /tmp/test/test/

# Without web
rm -rf /tmp/test && copier copy . /tmp/test --trust --defaults \
  --data package_name=test \
  --data description="Test" \
  --data native_library_name=lib \
  --data github_repo=u/r \
  --data native_repo=o/lib \
  --data enable_web=false

# With upstream
rm -rf /tmp/test && copier copy . /tmp/test --trust --defaults \
  --data package_name=test \
  --data description="Test" \
  --data native_library_name=lib \
  --data github_repo=u/r \
  --data native_repo=o/lib \
  --data upstream_crate=some_crate \
  --data upstream_version=v1.0.0
```

### 2. Check documentation is updated

- [ ] README.md - new variables documented
- [ ] CLAUDE.md - template variables table updated
- [ ] CONTRIBUTING.md - examples updated if needed
- [ ] CHANGELOG.md - all changes listed

### 3. Verify no uncommitted changes

```bash
git status
git diff
```

## Creating the Release

### Step 1: Update CHANGELOG.md

Move `[Unreleased]` items to new version section:

```markdown
## [Unreleased]

## [1.1.0] - 2025-01-28

### Added
- (items from Unreleased)
```

Update links at bottom:

```markdown
[Unreleased]: https://github.com/djx-y-z/copier-dart-frb-wrapper/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/djx-y-z/copier-dart-frb-wrapper/compare/v1.0.0...v1.1.0
```

### Step 2: Commit and Tag

```bash
git add CHANGELOG.md
git commit -m "chore: prepare release v1.1.0"
git tag v1.1.0
git push origin main
git push origin v1.1.0
```

### Step 3: Create GitHub Release (Optional)

```bash
# Using GitHub CLI
gh release create v1.1.0 \
  --title "v1.1.0" \
  --notes "See [CHANGELOG.md](CHANGELOG.md) for details."

# Or manually:
# 1. Go to https://github.com/djx-y-z/copier-dart-frb-wrapper/releases
# 2. Click "Draft a new release"
# 3. Select tag v1.1.0
# 4. Add release notes from CHANGELOG.md
```

## How Copier Uses Tags

- Copier lists available versions from git tags
- Users see versions when running `copier copy`
- `copier update` detects newer versions
- Without tags, Copier uses HEAD (development mode)

```bash
# User specifies version
copier copy https://github.com/djx-y-z/copier-dart-frb-wrapper project --vcs-ref v1.1.0

# User updates to latest
cd project && copier update

# User updates to specific version
copier update --vcs-ref v1.1.0
```

## Hotfix Release

For urgent fixes to a released version:

```bash
# Create hotfix branch from tag
git checkout -b hotfix/v1.0.1 v1.0.0

# Make fixes
# ...

# Update CHANGELOG.md
# Commit and tag
git add .
git commit -m "fix: critical bug fix"
git tag v1.0.1

# Push
git push origin hotfix/v1.0.1
git push origin v1.0.1

# Merge back to main if applicable
git checkout main
git merge hotfix/v1.0.1
git push origin main
```
