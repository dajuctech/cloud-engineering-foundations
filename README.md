# Cloud Engineering Foundations

A beginner-friendly Git and GitHub project that documents the workflow I use to manage changes safely in cloud engineering repositories.

This README is the main entry point for the project. It explains what I built, what I learned, how the repository is organized, and how to repeat the workflow from beginning to end.

## Table of Contents

- [Project Overview](#project-overview)
- [What This Project Demonstrates](#what-this-project-demonstrates)
- [Completed Work](#completed-work)
- [Core Concepts](#core-concepts)
- [Project Structure](#project-structure)
- [Complete Git and GitHub Workflow](#complete-git-and-github-workflow)
- [Using GitHub Issues](#using-github-issues)
- [Using `.gitignore` Safely](#using-gitignore-safely)
- [Validation](#validation)
- [Common Problems](#common-problems)
- [GitHub Actions Basics](#github-actions-basics)
- [Lessons Learned](#lessons-learned)
- [How I Would Explain This Project](#how-i-would-explain-this-project)

## Project Overview

I created this repository to practise the Git and GitHub skills that support almost every cloud engineering project. Infrastructure code, application code, architecture diagrams, and operational documentation all need a reliable way to record changes and support review.

The project follows a simple but complete workflow:

```text
Create or clone a repository
        |
        v
Create a feature branch
        |
        v
Make and review changes
        |
        v
Stage and commit the changes
        |
        v
Push the feature branch
        |
        v
Open and review a pull request
        |
        v
Merge into main
        |
        v
Synchronize the local repository
        |
        v
Delete the merged branch
```

This is a documentation project rather than a deployed application. Its value comes from showing a clean, traceable workflow and safe repository habits.

## What This Project Demonstrates

By completing this project, I demonstrated that I can:

- create and clone a GitHub repository
- initialize an existing local folder as a Git repository
- connect a local repository to a GitHub remote
- create an organized project structure
- create and switch between branches
- inspect working-tree and staged changes
- stage and commit selected files
- push local branches to GitHub
- open, review, and merge pull requests
- create GitHub Issues and link them to pull requests
- synchronize local `main` with `origin/main`
- remove merged branches safely
- use `.gitignore` to reduce the risk of publishing sensitive files
- document technical work clearly
- explain the purpose of GitHub Actions

## Completed Work

The repository history records the completed exercises:

| Work item | Evidence |
|---|---|
| Initial project structure | Pull request [#1](https://github.com/dajuctech/cloud-engineering-foundations/pull/1) |
| Git and GitHub learning notes | Pull request [#3](https://github.com/dajuctech/cloud-engineering-foundations/pull/3) |
| Architecture folder documentation | Issue [#2](https://github.com/dajuctech/cloud-engineering-foundations/issues/2) and pull request [#4](https://github.com/dajuctech/cloud-engineering-foundations/pull/4) |
| Markdown file cleanup | Issue [#5](https://github.com/dajuctech/cloud-engineering-foundations/issues/5) and pull request [#6](https://github.com/dajuctech/cloud-engineering-foundations/pull/6) |

This history shows that the repository was improved through branches and pull requests instead of making every change directly on `main`.

GitHub Issues and pull requests share the same number sequence. That is why this repository has pull request `#1`, issue `#2`, pull requests `#3` and `#4`, issue `#5`, and pull request `#6`.

## Core Concepts

| Term | Beginner-friendly meaning |
|---|---|
| Git | A tool that records changes to files on my computer |
| GitHub | An online platform that stores Git repositories and supports collaboration |
| Repository | A project folder and its Git history |
| Remote | The online repository connected to my local repository |
| `origin` | The conventional name for the main remote repository |
| Branch | An independent workspace for a change |
| Commit | A saved checkpoint with a message describing the change |
| Push | Upload local commits to a remote repository |
| Pull | Download and integrate remote changes into the current branch |
| Pull request | A request to review and merge one branch into another |
| Merge | Combine approved branch changes into the destination branch |
| Issue | A tracked task, problem, or improvement |
| `.gitignore` | Rules that tell Git which untracked files it should ignore |
| README | The main explanation and usage guide for a repository |

### Git and GitHub Are Different

Git works locally and records the history of the repository. GitHub hosts a copy of that Git repository online and adds collaboration features such as pull requests, issues, and Actions.

I can use Git without GitHub, but I use both together for this workflow.

### Why Branches Matter

A branch lets me work on one task without changing the stable `main` branch immediately. I can review the work first, then merge it when it is ready.

### Why Pull Requests Matter

A pull request creates a visible review point. It explains why a change was made, shows the exact file differences, records discussion, and can connect the work to an issue.

## Project Structure

```text
cloud-engineering-foundations/
|-- README.md
|-- .gitignore
|-- architecture/
|   `-- README.md
|-- notes/
|   `-- git-and-github.md
|-- scripts/
|   `-- README.md
`-- lessons-learned.md
```

| Path | Purpose |
|---|---|
| `README.md` | Complete public guide and main entry point |
| `.gitignore` | Prevents selected local and sensitive files from being tracked |
| `architecture/` | Location for sanitized diagrams and architecture notes |
| `notes/git-and-github.md` | Original short learning notes created during the Git workflow exercise |
| `scripts/` | Location for safe learning and automation scripts |
| `lessons-learned.md` | Original short reflection created during the exercise |

The smaller Markdown files remain because they were part of the hands-on branch, issue, and pull-request practice. They are supporting project artifacts, not separate guides that a visitor must read before using this README.

A detailed `steps-by-steps-process.md` file also exists locally as my private learning record. It includes mistakes, recovery steps, and the exact sequence I followed while building the repository. It is intentionally excluded from GitHub through `.gitignore`; this README contains everything a public visitor needs.

## Complete Git and GitHub Workflow

### 1. Check Git

```bash
git --version
git config --get user.name
git config --get user.email
```

Git attaches the configured name and email address to commits. A GitHub-provided `noreply` address can be used when a personal email should not appear in public commit history.

### 2. Prepare the Repository

For a repository that already exists on GitHub:

```bash
git clone https://github.com/<github-username>/cloud-engineering-foundations.git
cd cloud-engineering-foundations
git status
git remote -v
```

For an existing local folder connected to an empty GitHub repository:

```bash
cd cloud-engineering-foundations
git init -b main
git remote add origin https://github.com/<github-username>/cloud-engineering-foundations.git
git status
git remote -v
```

Only one of these two approaches is needed. Cloning already creates the local Git repository and configures `origin`.

### 3. Synchronize `main`

Before starting new work:

```bash
git switch main
git pull origin main
git status
```

This reduces the chance of building a feature branch from an outdated version of the project.

### 4. Create a Feature Branch

Use a short name that describes one task:

```bash
git switch -c improve-documentation
git branch --show-current
```

The output should show `improve-documentation`. I then make only the changes needed for that task.

### 5. Review the Changes

```bash
git status
git diff
git diff --check
```

- `git status` shows changed, untracked, and staged files.
- `git diff` shows unstaged content changes.
- `git diff --check` detects whitespace errors.

Reviewing changes before staging helps catch accidental edits and sensitive information.

### 6. Stage and Commit

Stage the intended files explicitly:

```bash
git add README.md
git status
git diff --cached
git commit -m "Improve project documentation"
```

`git add` prepares a snapshot. `git commit` records that snapshot locally. The commit message should state what the change accomplishes.

### 7. Push the Feature Branch

```bash
git push -u origin improve-documentation
```

The `-u` option connects the local feature branch to its remote branch. Later pushes from that branch can normally use `git push`.

### 8. Open a Pull Request

On GitHub:

1. Open the repository.
2. Select **Pull requests**.
3. Select **New pull request**.
4. Set the base branch to `main`.
5. Set the compare branch to the feature branch.
6. Review the **Files changed** tab.
7. Add a clear title and description.
8. Create the pull request.

Example description:

```md
## Summary

Improved the main project documentation.

## Changes

- Added the complete beginner workflow.
- Explained the repository structure.
- Added validation and troubleshooting guidance.

## Safety

- No credentials or sensitive account information were added.
```

The description belongs in the GitHub pull-request form, not inside a project file.

### 9. Review and Merge

Before merging:

- confirm the base branch is `main`
- read the pull-request description
- inspect every file under **Files changed**
- confirm no secrets or unrelated files are present
- wait for any required automated checks

After review, merge the pull request and delete the remote feature branch when GitHub offers that option.

### 10. Update the Local Repository

```bash
git switch main
git pull origin main
git branch -d improve-documentation
git fetch --prune
git status
```

Lowercase `-d` safely deletes a local branch only when Git considers it merged. `git fetch --prune` removes stale references to remote branches that have been deleted.

## Using GitHub Issues

Issues make work visible before implementation begins. A useful issue describes the task and defines how completion will be checked.

Example:

```md
## Task

Improve the main README so it provides one clear learning path.

## Acceptance Criteria

- Explain the purpose of the repository.
- Document the complete Git workflow.
- Include validation and troubleshooting guidance.
- Do not include secrets or private account information.
```

Create a feature branch for the issue, complete the work, and include the verified issue number in the pull-request description:

```text
Closes #<issue-number>
```

GitHub closes the linked issue automatically when that pull request is merged into the default branch.

## Using `.gitignore` Safely

This repository ignores common sensitive or generated files:

```gitignore
.env
.env.*
!.env.example
*.pem
*.key
.aws/
.terraform/
terraform.tfstate
terraform.tfstate.backup
.DS_Store
node_modules/
__pycache__/
/steps-by-steps-process.md
```

Important rules:

- `.env` and its variants can contain application secrets.
- `.env.example` may be committed only with safe placeholder values.
- `.pem` and `.key` files can contain private keys.
- `.aws/` can contain AWS credentials and configuration.
- Terraform state can contain infrastructure details and sensitive values.
- The local process guide is ignored because it is a personal learning record.

`.gitignore` does not remove a file that Git already tracks. If sensitive data is committed, removing the current file is not enough because the secret can remain in Git history. The credential must be revoked or rotated immediately.

Check why a file is ignored:

```bash
git check-ignore -v <file-name>
```

Never commit passwords, tokens, private keys, AWS access keys, credentials, account-specific data, or Terraform state.

## Validation

Run these commands from the repository root:

```bash
git status
git branch -avv
git remote -v
git log --oneline --decorate --graph --all -10
git ls-files
git check-ignore -v steps-by-steps-process.md
git diff --check
```

The expected result is:

- the intended branch is checked out
- the local branch tracks the correct remote branch
- `origin` points to the intended GitHub repository
- the commit graph shows the branch and merge history
- only intended public files are tracked
- the private process guide is ignored
- no whitespace errors are reported

Before every commit, use this shorter safety loop:

```bash
git status
git diff
git diff --cached
```

## Common Problems

### `fatal: not a git repository`

Confirm the current folder and look for `.git`:

```bash
pwd
ls -la
```

Move into the repository or initialize the correct existing folder with `git init -b main`.

### `remote origin already exists`

Inspect the existing remote:

```bash
git remote -v
```

If it is incorrect, update it:

```bash
git remote set-url origin https://github.com/<github-username>/cloud-engineering-foundations.git
```

### A Branch Already Exists

Switch to it without the create option:

```bash
git switch <branch-name>
```

### Nothing to Commit

Run `git status`. The file may be unchanged, already committed, or ignored by `.gitignore`.

### GitHub Shows Nothing to Compare

Confirm that `main` is the base, the feature branch is the compare branch, and the feature branch has a commit that is not already on `main`:

```bash
git log --oneline --decorate --graph --all
```

### A Push Is Rejected

For `main`, synchronize first:

```bash
git switch main
git pull origin main
```

For a feature branch that changed remotely:

```bash
git pull --rebase origin <branch-name>
git push
```

Do not force-push unless the effect on shared history is understood.

### A Merge Conflict Appears

Open the affected file and look for the three markers Git added: the line that starts with seven less-than signs, the separator made from seven equals signs, and the line that starts with seven greater-than signs. Decide which content should remain, then remove all three marker lines.

Then stage and commit the resolved file:

```bash
git add <file-name>
git commit
```

## GitHub Actions Basics

GitHub Actions can automatically run checks when code is pushed or a pull request is opened.

| Term | Meaning |
|---|---|
| Workflow | The complete automation definition |
| Event | The activity that starts a workflow |
| Job | A group of steps run on one runner |
| Step | One command or reusable action |
| Runner | The machine that executes the job |
| Action | A reusable automation component |

Workflow files use YAML and live in `.github/workflows/`. GitHub Actions was studied conceptually in this project, but no workflow was implemented because automation was not required for the original exercise.

For future workflows, I should grant only required permissions, store secrets in GitHub Actions secrets, review third-party actions, and avoid printing sensitive values in logs.

## Lessons Learned

The most important lesson was that Git work should follow a deliberate sequence. I first check my location and branch, then review changes, stage only what I intend to publish, inspect the staged diff, commit, and push.

I also learned that:

- a branch provides isolation, but it does not replace reviewing my work
- a commit should represent one understandable change
- pushing a branch does not merge it into `main`
- a pull request provides evidence of review and discussion
- issues define work, while pull requests deliver it
- local `main` must be updated after a pull request is merged on GitHub
- deleted remote branches can leave stale references until I prune them
- issue and pull-request numbers come from one shared sequence
- `.gitignore` helps prevent mistakes but is not a secret-management system
- credentials must never enter Git history
- clear documentation is part of the engineering work

## How I Would Explain This Project

> I created the `cloud-engineering-foundations` repository to practise a complete Git and GitHub workflow. I organized the repository, protected sensitive local files with `.gitignore`, completed changes on feature branches, committed and pushed the work, opened and merged pull requests, and tracked improvements with GitHub Issues. The project gave me practical experience with the version-control workflow I will use for cloud code, automation, architecture documentation, and infrastructure projects.

## References

- [Git documentation](https://git-scm.com/doc)
- [GitHub documentation](https://docs.github.com/)
- [GitHub pull request documentation](https://docs.github.com/en/pull-requests)
- [GitHub Issues documentation](https://docs.github.com/en/issues)
- [GitHub Actions documentation](https://docs.github.com/en/actions)
