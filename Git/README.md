# Git

## 1. Brief Introduction

Git is a distributed version control system used to track changes, create branches, review work and maintain project history.

Git is central to DevOps because application code, infrastructure code, CI/CD configuration and Kubernetes manifests can all be versioned in Git.

Git records project history as commits. A local repository contains the project history and object database, so many operations can be performed without a central server.

Hosting platforms such as GitHub, GitLab and Bitbucket add pull/merge requests, permissions and collaboration.

---

## 2. Git Architecture

A practical Git model is:

**Working Tree → Staging Area / Index → Git Repository**

Git stores content using objects such as blobs, trees and commits. Branches are lightweight movable references to commits.

| Component | Role |
|---|---|
| Working tree | Files currently checked out and edited |
| Staging area / index | Selects changes that will enter the next commit |
| `.git` directory | Repository metadata, refs and object database |
| Commit | Snapshot plus metadata and parent references |
| Branch | Movable pointer to a commit |
| Remote | Reference to another repository, usually a hosted repository |

---

## 3. Key Commands

| Command | Purpose | Example |
|---|---|---|
| `git init` | Create a repository | `git init` |
| `git clone` | Copy a remote repository | `git clone https://example.com/repo.git` |
| `git status` | Show working/staging state | `git status` |
| `git add` | Stage changes | `git add .` |
| `git commit` | Create a snapshot | `git commit -m "Add health check"` |
| `git log` | View history | `git log --oneline --graph` |
| `git branch` | List/create/delete branches | `git branch feature/login` |
| `git switch` | Switch branches | `git switch feature/login` |
| `git merge` | Merge another branch | `git merge feature/login` |
| `git rebase` | Replay commits on a new base | `git rebase main` |
| `git pull` | Fetch and integrate changes | `git pull --rebase` |
| `git push` | Upload commits | `git push origin feature/login` |
| `git diff` | Inspect changes | `git diff` |
| `git stash` | Temporarily save uncommitted work | `git stash` |
| `git tag` | Create release/version tags | `git tag v1.2.0` |

---

## 4. Real-Time Project Usage

A typical DevOps workflow using Git:

1. Create a repository for application and DevOps configuration.
2. Protect the main branch and require pull/merge requests.
3. Use short-lived feature branches.
4. Run CI checks before merge.
5. Tag releases for deployment traceability.
6. Keep Dockerfiles, Terraform and Kubernetes manifests under version control.

Git provides traceability across development, infrastructure and deployment workflows.

---

## 5. Practical Example: Feature-to-Deployment Workflow

```bash
git clone https://example.com/university-app.git
cd university-app

git switch -c feature/health-endpoint

# edit files

git add .
git commit -m "Add health endpoint"

git push -u origin feature/health-endpoint

# Open pull/merge request
# CI runs tests and security checks
# Merge to main and trigger release pipeline
```

Do not commit passwords, cloud credentials, private keys or generated secrets.

Use `.gitignore` and secret-management systems.

---

## 6. Alternatives & Comparison

| Tool | Strength | Typical Use |
|---|---|---|
| Git | Distributed model and dominant ecosystem | Application, infrastructure and configuration versioning |
| Mercurial | Distributed version control with a simpler command model | Projects that specifically choose Mercurial |
| Perforce Helix Core | Centralized, high-performance enterprise version control | Large binary-heavy or specialized enterprise workflows |
| Subversion (SVN) | Centralized version control | Legacy environments requiring centralized control |

---

## 7. Best Practices & Troubleshooting

- Use meaningful commit messages.
- Keep branches short-lived where practical.
- Use pull/merge requests and branch protection.
- Resolve conflicts carefully and run tests afterward.
- Use `.gitignore` for generated files and local secrets.
- Use `git reflog` when recovering from accidental resets/rebases.
- Use tags for releases.

---

## 8. Suggested Internship Mini-Project

Create a repository containing a small application, Dockerfile and CI workflow.

The project should:

1. Create a feature branch.
2. Submit a pull request.
3. Pass automated checks.
4. Merge to main.
5. Tag a release.
6. Document how a commit becomes a deployment artifact.

---

## Conclusion

Git provides traceability across the DevOps lifecycle.

Important skills include:

- Commits
- Branches
- Remotes
- Reviews
- Conflict resolution
- Recovery
- Release tagging

## References

- Git documentation  https://git-scm.com/docs/git
- Pro Git   https://git-scm.com/book/en/v2/Getting-Started-What-is-Git
- Git Objects   https://git-scm.com/book/en/v2/Git-Internals-Git-Objects.html
- Git Branches   https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell
