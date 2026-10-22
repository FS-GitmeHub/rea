# FS — REA GitHub setup

**Location:** [FS-GitmeHub/rea](https://github.com/FS-GitmeHub/rea)  
**Upstream project:** [morluto/rea](https://github.com/morluto/rea)  
**Pinned REA package:** `rea-agents@6.7.0`

## Status and purpose

REA source already exists in this GitHub repository. The extra, **manual** workflow
`.github/workflows/fs-rea-readiness.yml` installs the REA package onto a
temporary GitHub runner and attempts an isolated static JavaScript-analysis
self-test of a generated test fixture. It stores a JSON artifact for review.

This is **not** a permanent GitHub App installation and **not** an activated
Codex/AI agent. A workflow file alone does not establish a passing run.
REA needs to be separately registered with an authorized coding agent on the
environment where the agent will actually work.

## Manual readiness test

1. Open [Actions](https://github.com/FS-GitmeHub/rea/actions).
2. Choose **FS REA - Manual Readiness**.
3. Choose **Run workflow** on the default branch.
4. Check that the run passes and inspect `rea-isolated-readiness`.

Runs are not automatically scheduled. The workflow has read-only GitHub
permissions and accesses no other project repository.

## Later: configure an authorized coding agent

REA requires Node.js 22.19+, Node.js 24.11+, or Node.js 26+.
On an isolated computer, Codespace or approved agent host, preview changes first:

```bash
npx -y rea-agents@6.7.0 setup --client codex --dry-run --json
```

When the owner authorizes Codex activation and agrees to the previewed changes:

```bash
npx -y rea-agents@6.7.0 setup --client codex
```

Restart the chosen client and confirm REA's MCP tools appear.
The registration is host- and agent-specific: installing REA in a disposable
GitHub Actions runner does not register tools for ChatGPT or all repositories.
Native-binary analysis may need separately approved Ghidra, Hopper, or IDA.
See [official installation guide](https://github.com/morluto/rea/blob/main/docs/installation.md).

## Safeguards

- Do not access, test, modify, or benchmark the owner's personal application
  repositories during this installation. In particular, they are not CoPE labs.
- Require explicit target authorization for any subsequent inspection.
- Research findings must disclose technical limitations and retain citations,
  licenses, code provenance, and independent evaluation of any borrowed ideas.
- Future changes to owner project source require a clearly scoped branch,
  pull request, tests, and human review. Do not automatically merge or deploy.
- Do not activate Codex, expose credentials, or grant broader permissions by default.
- AI may generate incorrect, unsafe, or incomplete results. Expert review and
  human responsibility are required before publication, deployment, or delivery.
- REA is a reverse-engineering toolkit; a project-roadmap/stage management
  framework would be a separate installation and evaluation.
