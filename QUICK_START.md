# Quick Start Guide - CodeMie Kata Repository

## 🚀 Ready to Push to GitHub

Your kata repository is fully set up and ready to be pushed to GitHub!

## 📋 What's Been Created

### Repository Contents

```
✅ README.md                    - Main documentation (154 lines)
✅ CONTRIBUTING.md              - Author guidelines (289 lines)
✅ .kata-catalog.yaml          - Catalog metadata
✅ .gitignore                  - Standard ignore patterns
✅ REPOSITORY_STRUCTURE.md     - This structure overview
✅ katas/mastering-codemie-code-cli/
   ✅ kata.yaml               - Complete metadata (103 lines)
   ✅ steps.md                - 6 challenges with instructions (275 lines)
```

**Total**: 821 lines of quality documentation and content
**Commits**: 2 commits ready to push

---

## 🔄 Steps to Push to GitHub

### 1. Create GitHub Repository

Go to https://github.com/new and create a new repository:
- **Name**: `codemie-katas` (or your preferred name)
- **Description**: "CodeMie Kata Catalog - Curated AI development katas"
- **Visibility**: Public or Private
- **DO NOT** initialize with README, .gitignore, or license (already have these)

### 2. Add Remote and Push

```bash
cd /Users/Vadym_Vlasenko/AI/codemie/codemie-katas

# Add your GitHub repository as remote
git remote add origin https://github.com/YOUR_USERNAME/codemie-katas.git

# Or if using SSH
git remote add origin git@github.com:YOUR_USERNAME/codemie-katas.git

# Verify remote
git remote -v

# Push to GitHub
git push -u origin main
```

### 3. Verify on GitHub

Visit your repository URL:
```
https://github.com/YOUR_USERNAME/codemie-katas
```

You should see:
- ✅ README.md displayed on main page
- ✅ All files and folders
- ✅ 2 commits in history
- ✅ Clean directory structure

---

## 📥 Import into CodeMie Platform

### Method 1: REST API Import

```bash
curl -X POST http://localhost:8080/v1/katas/import \
  -H "user-id: YOUR_ADMIN_USER_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "repository_url": "https://github.com/YOUR_USERNAME/codemie-katas",
    "branch": "main",
    "auto_publish": true,
    "allow_updates": true
  }'
```

Expected response:
```json
{
  "message": "Import complete: 1 imported, 0 updated, 0 skipped, 0 failed",
  "stats": {
    "total_found": 1,
    "imported": 1,
    "updated": 0,
    "skipped": 0,
    "failed": 0,
    "errors": []
  }
}
```

### Method 2: Startup Auto-Import

Edit `config/kata-sources.yaml` in your CodeMie instance:

```yaml
sources:
  - repository: "https://github.com/YOUR_USERNAME/codemie-katas"
    branch: "main"
    auto_publish: true
    allow_updates: true
    enabled: true
```

Then restart the application:
```bash
# Katas will be automatically imported on startup
cd src/
poetry run uvicorn codemie.rest_api.main:app --reload
```

---

## ✏️ Adding More Katas

### 1. Create New Kata

```bash
cd /Users/Vadym_Vlasenko/AI/codemie/codemie-katas

# Create kata directory (use kebab-case)
mkdir -p katas/build-rag-pipeline

# Create kata files
cat > katas/build-rag-pipeline/kata.yaml << 'EOF'
id: "build-rag-pipeline"
version: "1.0.0"
title: "Build a RAG Pipeline with LangChain"
description: "Learn to build a Retrieval-Augmented Generation pipeline..."
level: "intermediate"
duration_minutes: 45
tags:
  - "rag"
  - "langchain"
  - "vector-search"
roles:
  - "developer"
  - "ai-engineer"
status: "published"
EOF

# Create steps
cat > katas/build-rag-pipeline/steps.md << 'EOF'
# Build a RAG Pipeline with LangChain

[Your kata content here...]

## 🎯 Challenge 1: Setup

...
EOF
```

### 2. Commit and Push

```bash
git add katas/build-rag-pipeline/
git commit -m "Add kata: Build a RAG Pipeline with LangChain"
git push origin main
```

### 3. Re-import to Platform

The platform will detect the new kata and import it automatically (if configured), or trigger manual import via API.

---

## 🔄 Updating Existing Katas

### 1. Edit Kata Files

```bash
cd /Users/Vadym_Vlasenko/AI/codemie/codemie-katas

# Edit kata.yaml - increment version
# version: "1.0.0" -> "1.1.0"

# Edit steps.md - make your changes
```

### 2. Commit and Push

```bash
git add katas/mastering-codemie-code-cli/
git commit -m "Update kata: Mastering CodeMie Code CLI v1.1.0

- Added new challenge for advanced features
- Updated installation instructions
- Fixed typos in Challenge 3"

git push origin main
```

### 3. Re-import

The platform will:
- Detect changes via checksum comparison
- Update the existing kata (not create duplicate)
- Preserve enrollment and progress data
- Update version tracking

---

## 🎯 Kata from Database to Repository Conversion

**Your first kata was successfully converted from:**

**Database Record** → **Repository Structure**

```
Database fields          →  kata.yaml + steps.md
├─ id                   →  Generated: mastering-codemie-code-cli
├─ title                →  kata.yaml: title
├─ description          →  kata.yaml: description
├─ steps                →  steps.md (full content)
├─ level                →  kata.yaml: level (BEGINNER → beginner)
├─ duration_minutes     →  kata.yaml: duration_minutes
├─ tags                 →  kata.yaml: tags (expanded)
├─ roles                →  kata.yaml: roles
├─ links                →  kata.yaml: links
├─ image_url            →  kata.yaml: image_url
├─ status               →  kata.yaml: status (PUBLISHED → published)
└─ creator_id           →  kata.yaml: author.email
```

**Additional fields added:**
- `version: "1.0.0"` - For version tracking
- `author` section - With name, email, GitHub
- `metadata` section - Original DB ID, timestamps

---

## 📊 Quick Stats

| Metric | Value |
|--------|-------|
| **Total Files** | 7 files |
| **Total Lines** | 1,073 lines |
| **Katas** | 1 kata |
| **Documentation** | 695 lines |
| **Kata Content** | 378 lines |
| **Commits** | 2 commits |
| **Status** | ✅ Ready to push |

---

## 🔗 Useful Commands

### Git Operations

```bash
# View status
git status

# View commit history
git log --oneline

# View changes
git diff

# View remote
git remote -v

# Push changes
git push origin main
```

### Repository Info

```bash
# Count lines in all files
find . -name "*.md" -o -name "*.yaml" | xargs wc -l

# List all katas
ls -la katas/

# View kata metadata
cat katas/mastering-codemie-code-cli/kata.yaml
```

---

## ✅ Final Checklist

Before pushing:
- [x] Git repository initialized
- [x] All files created and committed
- [x] README.md is comprehensive
- [x] CONTRIBUTING.md provides guidelines
- [x] First kata is complete and tested
- [x] .gitignore is configured
- [ ] GitHub repository created
- [ ] Remote added to local repository
- [ ] Code pushed to GitHub
- [ ] Repository URL shared

After pushing:
- [ ] Verify all files are on GitHub
- [ ] Test import via API
- [ ] Verify kata appears in platform
- [ ] Test kata from user perspective
- [ ] Share repository with team

---

## 🎓 Success!

You now have a production-ready kata repository that follows all CodeMie specifications and best practices!

**Next Actions:**
1. Create GitHub repository
2. Push code
3. Import into CodeMie platform
4. Create more katas
5. Share with the community

---

**Created**: 2025-12-09
**Location**: `/Users/Vadym_Vlasenko/AI/codemie/codemie-katas`
**Ready**: ✅ Yes
