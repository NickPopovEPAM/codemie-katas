# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **CodeMie Kata Catalog** - a curated collection of AI development katas (hands-on coding challenges) that can be imported into the CodeMie platform. Each kata is a self-contained exercise with metadata and step-by-step instructions stored as static files in a Git repository.

## Architecture

### Kata Structure
Each kata consists of two files in a dedicated directory under `katas/`:
```
katas/
└── kata-name/                 # kebab-case directory name
    ├── kata.yaml              # Metadata (id, title, level, tags, etc.)
    └── steps.md               # Step-by-step instructions in Markdown
```

### Catalog Metadata
- `.kata-catalog.yaml` - Catalog-level configuration and statistics
  - `config` section: Import behavior (auto_publish, allow_updates, update_strategy)
  - `stats` section: Auto-generated statistics (total katas, counts by level/status)

### Automation Scripts
Located in `scripts/`:
- `update_catalog.py` - Python script to auto-update catalog statistics (requires PyYAML)
- `update_catalog_simple.sh` - Bash script for manual statistics calculation (no dependencies)
- `setup_hooks.sh` - Configures Git pre-commit hook for automatic updates

Git hooks in `.githooks/`:
- `pre-commit` - Automatically runs `update_catalog.py` before commits

## Common Tasks

### Creating a New Kata

When users request to create a new kata, follow these principles and steps:

#### Kata Design Principles
1. **Gamification First**: Design katas as engaging challenges with clear progression, achievements, and success milestones
2. **AI Adoption Focus**: Help users adopt AI tools and CodeMie platform through hands-on, practical experiences
3. **Time-Boxed**: Maximum 30 minutes completion time (aim for 15-25 minutes for better engagement)
4. **Tutorial Value**: Must provide genuine learning value, not just step-by-step instructions
5. **Challenge-Based**: Structure as progressive challenges with increasing difficulty
6. **Real-World Scenarios**: Use practical, relatable use cases that users will encounter

#### Available Metadata
- **Roles** (MAXIMUM 3): See `metadata/kata-roles.yaml` for complete list of available roles
  - Common: developer, ai-engineer, data-scientist, product-manager, devops, architect
- **Tags** (MAXIMUM 3): See `metadata/kata-tags.yaml` for complete list of available tags
  - Common: getting-started, ai-agents, langchain, rag, code-generation, claude-code, codemie-code

#### Step-by-Step Creation Process
1. **Create Directory**: `mkdir -p katas/kata-name` (use kebab-case, descriptive name)

2. **Design kata.yaml**:
   ```yaml
   id: "kata-name"                    # Must match directory name
   version: "1.0.0"                   # Start with 1.0.0
   title: "Engaging Challenge Title"
   description: >
     Clear, compelling description of what users will learn and achieve.
     Focus on outcomes and practical value.
   level: "beginner"                  # beginner | intermediate | advanced
   duration_minutes: 25               # Maximum 30, aim for 15-25
   tags:                              # MAXIMUM 3 tags - Reference: metadata/kata-tags.yaml
     - "getting-started"
     - "ai-agents"
     - "code-generation"
   roles:                             # MAXIMUM 3 roles - Reference: metadata/kata-roles.yaml
     - "developer"
     - "ai-engineer"
   status: "published"                # draft | published | archived
   author:                            # Recommended
     name: "Author Name"
     email: "author@example.com"
   ```

3. **Create steps.md with Gamification Structure**:
   ```markdown
   # [Kata Title]

   Engaging introduction that hooks the user and explains the practical value.

   ## 🎯 Challenge 1: [Action-Oriented Title] (5 min)

   **Goal:** Clear, specific objective for this challenge

   ### Instructions

   Step-by-step guidance with code examples and explanations.

   **✅ Success Criteria:**
   - [ ] Specific, measurable achievement
   - [ ] Another concrete milestone

   **🏆 Bonus:** (Optional)
   - Advanced challenge for power users

   ---

   ## 🎯 Challenge 2: [Next Challenge] (7 min)

   [Continue pattern...]

   ---

   ## 🎓 Kata Complete!

   ### What You've Accomplished

   ✅ List of achievements and skills gained

   ### Next Steps

   Suggestions for further learning and exploration
   ```

4. **Kata Content Guidelines**:
   - Start with quick wins (5-minute first challenge)
   - Build complexity progressively
   - Include real-world context and use cases
   - Use active voice and clear action verbs
   - Add code examples with syntax highlighting
   - Include troubleshooting tips for common issues
   - Make success criteria specific and verifiable
   - Add bonus challenges for advanced users

5. **Update Catalog Statistics**:
   ```bash
   ./scripts/update_catalog_simple.sh
   # Or: python3 scripts/update_catalog.py
   ```

6. **Commit Changes**:
   ```bash
   git add katas/kata-name/ .kata-catalog.yaml
   git commit -m "Add kata: [Kata Title]"
   ```

#### Quality Checklist Before Creating
- [ ] Duration is 30 minutes or less
- [ ] Includes 3-5 progressive challenges
- [ ] Has clear success criteria for each challenge
- [ ] Maximum 3 tags selected from metadata/kata-tags.yaml
- [ ] Maximum 3 roles selected from metadata/kata-roles.yaml
- [ ] Provides real learning value, not just instructions
- [ ] Uses gamification elements (challenges, achievements, progression)
- [ ] Includes practical, real-world scenarios
- [ ] Code examples are tested and working
- [ ] Success criteria are specific and measurable

### Adding a New Kata (Simple/Quick)
1. Create directory: `mkdir -p katas/kata-name` (use kebab-case)
2. Create `kata.yaml` with required fields (see format above)
3. Create `steps.md` with challenge structure (see format above)
4. Update catalog statistics: `./scripts/update_catalog_simple.sh` or `python3 scripts/update_catalog.py`
5. Commit both kata files and `.kata-catalog.yaml`

### Updating Existing Kata
1. Increment `version` in `kata.yaml` (follow semantic versioning)
2. Make changes to `kata.yaml` or `steps.md`
3. Update catalog statistics: `./scripts/update_catalog_simple.sh` or `python3 scripts/update_catalog.py`
4. Commit with clear description of changes

### Updating Catalog Statistics
Three methods available:
1. **Bash script** (recommended, no dependencies): `./scripts/update_catalog_simple.sh` - outputs YAML to copy-paste
2. **Python script** (auto-updates file): `python3 scripts/update_catalog.py` (requires: `pip install pyyaml`)
3. **Git hooks** (fully automatic): Run `./scripts/setup_hooks.sh` once to enable pre-commit auto-updates

The `stats` section in `.kata-catalog.yaml` should be updated whenever katas are added, removed, or modified.

## Kata YAML Format

### Required Fields
- `id`: Unique identifier (kebab-case, matches directory name)
- `version`: Semantic versioning (e.g., "1.0.0")
- `title`: Display title
- `description`: Brief description (can use YAML multi-line with `>`)
- `level`: "beginner" | "intermediate" | "advanced"
- `duration_minutes`: Integer (5-240, maximum 30 recommended)
- `tags`: Array of tag IDs (MAXIMUM 3 items, reference: metadata/kata-tags.yaml)
- `roles`: Array of role IDs (MAXIMUM 3 items, reference: metadata/kata-roles.yaml)
- `status`: "draft" | "published" | "archived"

### Optional Fields
- `image_url`: URL to card image (400x300px recommended)
- `links`: Array of external resources with `title`, `url`, `type` (documentation|guide|video|blog|tutorial)
- `references`: Array of strings for further reading
- `author`: Object with `name`, `email`, `github`
- `metadata`: Additional metadata (keywords, timestamps, etc.)

## Steps Markdown Format

Structure your `steps.md` files with:
- Brief introduction explaining the kata objectives
- `## 🎯 Challenge N: Title (X min)` headers for each main step
- `**Goal:**` statement for each challenge
- Clear instructions with code blocks (use language-specific syntax highlighting)
- `**✅ Success Criteria:**` section with checkboxes
- `**🏆 Bonus:**` section for optional advanced challenges (optional)
- `## 🎓 Kata Complete!` final section with accomplishments and next steps

## Integration with CodeMie Platform

The catalog is imported into CodeMie via:
1. **REST API**: `POST /v1/katas/import` with repository URL
2. **Startup auto-import**: Configure in `config/kata-sources.yaml`

Platform import behavior controlled by `.kata-catalog.yaml` config:
- `auto_publish: true` - Katas are published immediately (vs. draft)
- `allow_updates: true` - Existing katas can be updated
- `update_strategy: replace` - How updates are handled (replace|merge|skip)

## File Naming Conventions
- Directories: kebab-case (e.g., `mastering-codemie-code-cli`)
- Kata files: Always `kata.yaml` and `steps.md` (lowercase, no variations)
- Kata IDs: Must match directory name exactly

## Version Control Guidelines
- Increment `version` in `kata.yaml` for all kata updates:
  - Major (1.0.0 → 2.0.0): Breaking changes, significant restructuring
  - Minor (1.0.0 → 1.1.0): New content, additional challenges
  - Patch (1.0.0 → 1.0.1): Fixes, clarifications, minor updates
- Catalog version in `.kata-catalog.yaml` only changes for repository-wide restructuring
- Always update catalog statistics before committing kata changes
- Use descriptive commit messages: "Add kata: [title]" or "Update kata: [title] v[version]"

## Documentation Files
- `README.md` - Main documentation for users and platform administrators
- `CONTRIBUTING.md` - Guidelines for kata authors (detailed format specs)
- `QUICK_START.md` - Step-by-step guide for repository setup and GitHub push
- `CATALOG_MAINTENANCE.md` - Detailed guide for maintaining `.kata-catalog.yaml`
- `scripts/README.md` - Documentation for maintenance scripts

## Python Dependencies
Only required if using Python automation scripts:
```bash
pip install pyyaml
```

No other dependencies needed for basic kata authoring.
