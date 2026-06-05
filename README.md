# Base Core Template (template-base)

This is the central, language-agnostic upstream parent template repository for the `itsjennyfiggy-platform` ecosystem.

---

## 🎯 Purpose

This repository contains the standard developer tooling configurations, agent safety rules, workflows, project planning templates, and testing standards that apply to **all** projects and source repositories across the platform.

Specialized child templates (such as cloud-native stack templates or homelab-specific service templates) inherit these base configurations to maintain uniform standards.

---

## 📂 Repository Structure

```
├── .agents/
│   ├── rules/
│   │   ├── git_safety.md          # Prevents credential leaks and wildcard commits
│   │   └── testing_standards.md   # Enforces test-driven development (TDD) and coverage
│   └── workflows/
│       └── git-workflow.md        # Standard multi-stage branch and PR process
├── docs/
│   └── templates/
│       └── PROJECT_PLANNING.md    # Reusable template for scoping project details and Why
├── .editorconfig                  # Code formatting guidelines (indents, line-endings)
├── .gitignore                     # Default system and local credential ignores
└── LICENSE                        # CC0 1.0 Universal (Public Domain) Dedication
```

---

## ⚖️ Licensing

This template is dedicated to the public domain under the **CC0 1.0 Universal** waiver. 

Downstream repositories scaffolded from this template have no legal requirement to carry copyright notices or attributions for the boilerplate files, allowing them to be closed-source, proprietary, or open-source under any choice of license.
