---
name: git-backup
version: 1.0
description: Manual git operations for workspace backup and sync between OpenClaw and Kimi Code
type: procedural
keywords: ["push to git", "pull from git", "git status", "backup", "sync"]
---

# Git Backup Skill

**Version:** 1.0  
**Type:** Procedural  
**Scope:** Single workspace repo (Kimi-Claw-WorkSpace)  
**Auth:** HTTPS with embedded token  

---

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `push to git` | Stage, commit with timestamp, push to GitHub |
| `pull from git` | Pull latest changes from GitHub |
| `git status` | Show what's changed vs. remote |

---

## Configuration (Both Systems)

**Remote URL:**
```
https://ghp_<YOUR_TOKEN_HERE>@github.com/spencer-n1/Kimi-Claw-WorkSpace.git
```

**Verify setup:**
```bash
git remote -v
```

Should output:
```
origin  https://ghp_...TOKEN...@github.com/spencer-n1/Kimi-Claw-WorkSpace.git (fetch)
origin  https://ghp_...TOKEN...@github.com/spencer-n1/Kimi-Claw-WorkSpace.git (push)
```

---

## Operations

### 1. Push to Git

**OpenClaw:**
```bash
cd /root/.openclaw/workspace
git add .
git commit -m "Backup: $(date '+%Y-%m-%d at %H:%M')"
git push origin master
```

**Kimi Code:**
```bash
cd /path/to/your/workspace
git add .
git commit -m "Backup: $(date '+%Y-%m-%d at %H:%M')"
git push origin master
```

**What happens:**
- All new/modified files staged
- Commit with timestamp: `"Backup: 2025-04-12 at 14:30"`
- Pushed to `master` branch on GitHub

---

### 2. Pull from Git

**OpenClaw:**
```bash
cd /root/.openclaw/workspace
git pull origin master
```

**Kimi Code:**
```bash
cd /path/to/your/workspace
git pull origin master
```

**What happens:**
- Downloads latest commits from GitHub
- Merges into local workspace
- Reports any merge conflicts (rare)

---

### 3. Git Status

**OpenClaw:**
```bash
cd /root/.openclaw/workspace
git status
```

**Kimi Code:**
```bash
cd /path/to/your/workspace
git status
```

**Shows:**
- Modified files (red)
- Staged files (green)
- Untracked files
- Branch status vs. remote

---

## Conflict Resolution

If `git pull` shows merge conflicts:

```bash
# Check which files are conflicted
git status

# Option 1: Keep local version (your changes)
git checkout --ours <filename>

# Option 2: Keep remote version (GitHub version)
git checkout --theirs <filename>

# After resolving:
git add .
git commit -m "Resolved merge conflicts"
git push origin master
```

**To avoid conflicts:** Always pull before making changes if you switch between systems.

---

## File Exclusions (.gitignore)

**Location:** `.gitignore` file lives in the **workspace root folder** (same level as `skills/`, `prompts/`, etc.)

**Purpose:** Tells git which files/folders to skip. Large files (apps, builds, downloads) stay local — only your important work gets backed up.

### Minimal Exclusions

Only exclude bulky app builds. Everything else is backed up.

Copy this into your workspace root `.gitignore` file:

```
# Skip bulky app exports
Kimi Code Apps/
```

### How to Apply

**Check current exclusions:**
```bash
cat .gitignore
```

**Add new exclusions:**
```bash
echo "base44-builds/" >> .gitignore
echo "*.zip" >> .gitignore
```

**Verify what's being ignored:**
```bash
git status --ignored
```

### Common Exclusions by Use Case

| What You're Doing | Add This |
|-------------------|----------|
| Kimi Code app builds | `Kimi Code Apps/` |
| Large media files | `*.mp4`, `assets/videos/` |
| Python cache | `__pycache__/` |

---

## When to Use

| Situation | Action |
|-----------|--------|
| Finished a work session | `push to git` |
| Switching to other system | `push to git` → `pull from git` on other system |
| Before major changes | `push to git` (safety backup) |
| After being away | `git status` to see what's different |

---

## Token Management

If the token stops working:

1. Generate new token at https://github.com/settings/tokens
2. Update remote URL on both systems:
   ```bash
   git remote set-url origin https://NEW_TOKEN@github.com/spencer-n1/Kimi-Claw-WorkSpace.git
   ```

---

## Legacy Files

Old backup system lives in `/root/.openclaw/workspace/git/`:
- `BACKUP.md` — Original documentation
- `backup.sh` — Bash script (deprecated, use skill commands instead)

---

*Unified skill for OpenClaw + Kimi Code — HTTPS auth, manual triggers only*
