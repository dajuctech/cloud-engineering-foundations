# Cloud Engineering Foundations

This project documents the Git and GitHub workflow used as a foundation for cloud engineering
projects.

Cloud engineering work is usually managed through files. Terraform files describe infrastructure,
YAML files define pipelines, Markdown files explain architecture, and scripts automate tasks. Git
and GitHub make those files easier to track, review, protect, and explain.

The goal of this repository is to demonstrate a clean foundational workflow for managing cloud project
files safely.

## What This Project Covers

This project covers:

- creating a GitHub repository
- preparing a local Git repository
- creating and switching branches
- editing files safely
- checking changes before committing
- staging selected files
- writing useful commit messages
- pushing branches to GitHub
- opening pull requests
- merging pull requests
- using GitHub Issues
- protecting sensitive files with `.gitignore`
- keeping local learning notes private
- writing clear documentation

## Project Structure

The public project is intentionally simple:

```text
cloud-engineering-foundations/
+-- README.md
+-- .gitignore
```

There is also a private local learning file:

```text
steps-by-steps-process.md
```

That file is ignored by Git and should not be published. It can be used as a personal step-by-step
practice guide, while this README remains the single public document for the project.

## Why Git Matters In Cloud Engineering

Git tracks changes to files over time. This matters in cloud engineering because infrastructure and
operations are often controlled by files.

Examples:

| File type | Cloud engineering use |
|---|---|
| Terraform files | Create and manage cloud infrastructure |
| YAML files | Define CI/CD pipelines or Kubernetes resources |
| Markdown files | Explain architecture, runbooks, and project steps |
| Shell scripts | Automate repeated tasks |
| Policy files | Define permissions or security rules |

Without Git, it becomes difficult to answer:

- What changed?
- Why did it change?
- When did it change?
- Which version worked before?
- Who made the change?

Git gives the project a history. GitHub gives that history a place to be reviewed, shared, and
presented.

## Git And GitHub In Plain English

Git and GitHub are related, but they are not the same.

| Tool | Meaning |
|---|---|
| Git | Tracks file changes locally |
| GitHub | Stores Git repositories online and adds collaboration features |

Simple flow:

```text
Local files
-> Git tracks changes
-> commits record checkpoints
-> GitHub stores the remote copy
-> pull requests review changes before merging
```

## Important Terms

| Term | Meaning |
|---|---|
| Repository | A project folder tracked by Git |
| Clone | Copy a GitHub repository to the local machine |
| Branch | A separate workspace for changes |
| Commit | A saved checkpoint |
| Stage | Select changes for the next commit |
| Push | Send local commits to GitHub |
| Pull | Download latest changes from GitHub |
| Pull request | Ask to merge branch changes into another branch |
| Merge | Combine approved changes |
| Issue | A GitHub task, bug, note, or reminder |
| `.gitignore` | Tells Git which files not to track |
| `main` | The stable branch for the project |
| `origin` | The local name for the GitHub remote repository |

## Basic Workflow

A safe Git and GitHub workflow looks like this:

```text
Create or clone repository
-> create a branch
-> edit files
-> check changes
-> stage files
-> commit
-> push
-> open pull request
-> review
-> merge
-> pull latest main
-> clean up branch
```

This workflow keeps the `main` branch stable while changes are reviewed.

## Example Commands

Check the repository state:

```bash
git status
```

Create and switch to a new branch:

```bash
git switch -c update-documentation
```

Review unstaged changes:

```bash
git diff
```

Stage a file:

```bash
git add README.md
```

Review staged changes:

```bash
git diff --cached
```

Commit the staged changes:

```bash
git commit -m "Update project documentation"
```

Push the branch to GitHub:

```bash
git push -u origin update-documentation
```

After a pull request is merged, update local `main`:

```bash
git switch main
git pull origin main
```

Remove stale remote branch references:

```bash
git fetch --prune
```

## Why Branches Matter

Branches allow work to happen without changing the stable version directly.

For example, instead of editing `main`, create a branch:

```bash
git switch -c improve-readme
```

The branch can be pushed to GitHub and reviewed through a pull request. If the work is correct, it
can be merged into `main`. If it is wrong, it can be changed or deleted without damaging the stable
branch.

This same habit is useful later for Terraform, CI/CD, Kubernetes, and AWS project changes.

## Why Pull Requests Matter

A pull request creates a review space before changes enter `main`.

It helps show:

- what changed
- why it changed
- which files were touched
- whether the change is ready
- whether feedback is needed

Even in a personal portfolio project, pull requests are useful because they show how the work was
managed, not only the final result.

## Why Issues Matter

GitHub Issues help track work before the file changes happen.

An issue can describe:

- a task
- a bug
- a documentation improvement
- a cleanup item
- a future idea

Example:

```text
Issue: Improve project README
```

A branch can then be created for that issue. When the pull request is opened, the description can
include:

```text
Closes #<issue-number>
```

When the pull request is merged, GitHub closes the issue automatically.

## Security Rules

This repository should not contain:

- passwords
- access keys
- secret tokens
- `.pem` private keys
- AWS credentials
- Terraform state files
- private environment files
- account IDs
- sensitive architecture details

The `.gitignore` file protects common unsafe files:

```gitignore
.env
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
.env.*
!.env.example
```

The rule:

```gitignore
/steps-by-steps-process.md
```

keeps the private learning guide local to the machine.

## Checking What Git Tracks

Do not assume every visible file is being tracked by Git.

To see tracked files:

```bash
git ls-files
```

To check why a file is ignored:

```bash
git check-ignore -v steps-by-steps-process.md
```

To check what will be committed:

```bash
git diff --cached
```

These commands help prevent accidental commits of private files.

## Architecture Notes

Architecture documentation should explain how services connect and why decisions were made.

In future cloud projects, architecture notes may include:

- diagrams
- service relationships
- traffic flow
- design decisions
- security notes
- cost considerations
- troubleshooting notes

Only sanitized architecture information should be published. Do not include private account
details, credentials, sensitive diagrams, or real internal environment data.

## Scripts Notes

Scripts are useful for automation, but they must be handled carefully.

Safe scripts should:

- avoid hardcoded secrets
- use clear names
- include comments where needed
- be tested before use
- explain what they change
- avoid destructive actions unless clearly documented

Do not store passwords, tokens, private keys, or AWS credentials inside scripts.

## Lessons Learned

This project demonstrates these core lessons:

- Git tracks file changes and preserves history.
- GitHub stores the repository online and supports review.
- Branches make changes safer.
- Commits should be focused and clearly named.
- Pull requests help review and explain work.
- Issues help track tasks.
- `.gitignore` helps keep unsafe files out of the repository.
- Documentation should be easy for another person to understand.
- Private learning notes do not always belong in a public repository.

## Common Mistakes To Avoid

- Editing `main` directly for every change.
- Forgetting to stage files before committing.
- Using vague commit messages such as `fix` or `update`.
- Running `git add .` without checking what will be staged.
- Forgetting to pull the latest `main` after merging on GitHub.
- Committing secrets, keys, `.env` files, or Terraform state.
- Leaving project documentation scattered across too many files.

## Final Checklist

Before pushing changes:

- [ ] `git status` has been checked.
- [ ] The active branch is correct.
- [ ] `git diff` has been reviewed.
- [ ] Only intended files are staged.
- [ ] `git diff --cached` has been reviewed.
- [ ] No secrets or private keys are staged.
- [ ] Commit message clearly explains the change.
- [ ] Pull request description explains the purpose.

## Project Outcome

The final project is intentionally simple so the workflow is easy to understand.

The public repository should mainly show:

- a clear README
- safe `.gitignore` rules
- a clean Git history
- pull request workflow
- issue tracking
- no committed secrets

The purpose is not to make the folder look complex. The purpose is to show clean engineering
practice before moving into larger cloud projects.
