---
name: gh-default-repo-is-upstream
description: In this fork, bare gh commands resolve to upstream mc1arke repo; always pass --repo passionfactory-oss/sonarqube-community-branch-plugin
metadata:
  type: project
---

Without `gh repo set-default`, `gh repo view` in a checkout of this fork resolves to `mc1arke/sonarqube-community-branch-plugin` (upstream), so a bare `gh pr create` fails with "No commits between main and ..." / "Head ref must be a branch".

**Why:** the `upstream` remote makes gh pick the parent repo as default. `gh repo set-default passionfactory-oss/sonarqube-community-branch-plugin` fixes it, but only for that checkout (it writes `.git/config`), so a fresh clone or worktree starts on upstream again. Tools that call `gh repo view` ignore `GH_REPO`.
**How to apply:** pass `--repo passionfactory-oss/sonarqube-community-branch-plugin` to every `gh pr` call. The repo is under `passionfactory-oss`, not `chatbot-pf`/`pleaseai`, and has no PR template, so PRs are created ready unless asked otherwise.
