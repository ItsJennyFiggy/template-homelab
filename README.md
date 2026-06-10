# template-homelab

A scaffolding template for single-purpose homelab applications deployed on a Mac Mini host. Use this template as the starting point for any new homelab service in the `ItsJennyFiggy` platform.

---

## Purpose

This template establishes the standard structure, agent rules, and workflow conventions for homelab apps. It enforces strict environment parameterization (no hardcoded config) and is designed for services that run as containers on the Mac Mini.

## Docker CD

Multi-arch container images (targeting `linux/amd64` and `linux/arm64`) are published automatically to `ghcr.io/itsjennyfiggy/<repo-name>` on every release tag created by release-please.

**Pull the image:**

```bash
# Pin to a specific release
docker pull ghcr.io/<owner>/<repo>:v1.2.3

# Or use the latest tag (always points to the most recent release)
docker pull ghcr.io/<owner>/<repo>:latest
```

The `.github/workflows/docker-buildx.yml` workflow triggers on any `v*` tag push. When release-please opens and merges a Release PR, it creates the tag automatically, which in turn triggers the Docker build and push.

---

## Repository structure

```
├── .agents/
│   ├── rules/                  # Shared agent safety, testing, and dependency rules
│   │   ├── dependency_management.md
│   │   ├── environment_bootstrapping.md
│   │   ├── subagent_orchestration.md
│   │   └── testing_standards.md
│   ├── skills/
│   │   └── dependency-auditor/ # Dependency audit skill and license checker
│   └── workflows/
│       └── bootstrap.md        # Local environment bootstrapping workflow
├── docs/
│   └── templates/
│       └── PROJECT_PLANNING.md # Project scoping template
├── .editorconfig               # Indentation and line-ending standards
├── CLAUDE.md                   # Agent rules index for this repo
├── LICENSE                     # MIT License
├── README.md                   # This file
└── README.template.md          # Blank README template for child repos scaffolded from this one
```

---

## Creating a new homelab service from this template

1. Create a new repository using this template on GitHub.
2. Rename `README.template.md` to replace `README.md` (or rewrite `README.md` to describe your service).
3. Add your application code, `Dockerfile`, and `.env.example` at the repository root.
4. Set all environment-specific values as environment variables — no hardcoded config in the image.
5. Follow `.agents/workflows/bootstrap.md` for local environment setup.

---

## Agent guidelines

If you are an AI coding agent working in this repository:

1. Read `.agents/rules/` before making any changes.
2. Follow `.agents/rules/git_safety.md` strictly — never stage secrets or `.env` files.
3. Run the full test suite and verify coverage gates before opening a PR (see `.agents/rules/testing_standards.md`).
4. Follow the branch and PR lifecycle in `.agents/workflows/git-workflow.md`.

---

## Licensing

Licensed under the MIT License. See [LICENSE](LICENSE).
