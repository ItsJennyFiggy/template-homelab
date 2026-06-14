# Workflow: Dev Container Personas

Two dev container configurations exist in `.devcontainer/`. Choose the persona
that matches the operator — a human developer or an AI agent.

---

## Personas at a Glance

| | Human (`.devcontainer/`) | Agent (`.devcontainer/agent/`) |
|---|---|---|
| **Purpose** | Full interactive development | AI agent workloads (planning, analysis, code generation) |
| **AWS access** | `~/.aws` mounted read-write; full operator credentials | `~/.aws` mounted **read-only**; agent credentials configured externally |
| **terraform apply** | Permitted (subject to standard review gates) | Not applicable |
| **terraform plan** | Permitted | Permitted |
| **git auth** | `~/.gitconfig` mounted; uses host SSH/keychain | GitHub App token via `.agents/bin/git-auth`; no personal SSH keys mounted |

---

## Permission Matrix

### Human persona

| Resource | Permission |
|---|---|
| AWS (full operator role) | Read + Write + Destructive (scoped to operator IAM user/role) |
| terraform plan | Allowed |
| terraform apply / destroy | Allowed |
| git push to main | Blocked by branch protection; PR required |
| Personal SSH keys | Available via host keychain mount |

### Agent persona

| Resource | Permission |
|---|---|
| AWS (`itsjennyfiggy-agent-development` assumed role) | Configured externally |
| terraform plan | Allowed |
| terraform apply / destroy | Not applicable |
| git push to main | Blocked by branch protection; PR required |
| Personal SSH keys | Not mounted — use GitHub App token via `.agents/bin/git-auth` |

---

## Opening the Human Container

```bash
# In VS Code: "Dev Containers: Open Folder in Container"
# -> select .devcontainer/devcontainer.json  (the root, i.e. default)

# Or from the CLI:
devcontainer open .
```

The container mounts `~/.aws` (read-write) and `~/.gitconfig`, giving the
developer full credential access identical to their host workstation.

---

## Opening the Agent Container

```bash
# In VS Code: "Dev Containers: Open Folder in Container"
# -> select .devcontainer/agent/devcontainer.json

# Or target it explicitly:
devcontainer open --workspace-folder . --config .devcontainer/agent/devcontainer.json
```

On container start, the agent container is ready for use. Configure AWS
credentials externally before running Terraform or other AWS-dependent commands:

```bash
eval "$(aws configure export-credentials --format env)"
```

---

## GitHub App Git Authentication (Agent Persona)

Agents must not use personal SSH keys. Instead, configure the GitHub App token
before any `git push` or `gh` command:

```bash
# Inside the agent container, authenticate via the GitHub App wrapper:
PATH="$(pwd)/.agents/bin:$PATH" git push origin feat/my-branch
```

See `.agents/bin/git-auth` and `.agents/workflows/git-workflow.md` for the
full authentication setup.

---

## Updating the Base Image

Both personas use `mcr.microsoft.com/devcontainers/base:2.0.5-ubuntu-24.04`.

Before bumping the image tag, verify the latest stable release against the
primary source:

```
https://mcr.microsoft.com/v2/devcontainers/base/tags/list
```

Update both `devcontainer.json` files atomically and run the bats test suite
(`bats tests/`) to confirm the agent devcontainer JSON still validates.
