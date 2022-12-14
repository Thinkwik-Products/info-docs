# Git Rules

## General rules

- Make sure to fetch from main every morning (Explained in Branching strategy)
- Make sure to push at EOD every day. If the task is not complete, add a [wip] prefix
- Any stale branches should be deleted after a predefined time period

## Branching strategy

Following is the branching strategy that we use:

### Branches

- `main` - This is the default branch
- `feature/1110` - This is the feature branch where active development will be done.
- `staging` - This is the branch pointing to staging environment. Pushing/Merging to this branch will trigger automatic deployment for staging environment
- `production` - This is the branch pointing to production environment. Pushing/Merging to this branch will trigger automatic deployment for production environment
- `hotfix/1111` - This is the hotfix branch where any urgent fixes will be done.

#### Work flow

John is assigned a task #1110. This is the workflow he should be following:

- Create a new branch from `main` named `feature/1110`
- Checkout `feature/1110` in local
- Make code changes and commits in `feature/1110` branch
- John goes to home
- John comes to office next morning
- Take latest in `main` branch using below commands

```bash
git checkout main
git pull
```

- Rebase `main` branch to `feature/1110` branch using below commands

```bash
git checkout feature/1110
git rebase main
```

- Resolve conflicts if any
- Once all changes are done, create a pull request from `feature/1110` to `main`
- Team leader will review the commit and merge using `Rebase and Merge`

#### Hotfix workflow

There is some major issue in production, that needs to be fixed immediately. But we don't want all other changes to get pushed. This is the workflow we should follow:

- Create a new branch from `production` named `hotfix/1111`
- Checkout `hotfix/1111` in local
- Make code changes and commits in `hotfix/1111` branch
- Once tested and issue is fixed, create pull request from `hotfix/1111` to `production`
- Create another pull request from `hotfix/1111` to `main`

## Commit messages

Commit message should be simply an answer to the following question: `If merged, this commit will.....`

So if John implemented 2fa, then the above statement will become `If merged, this commit will implement 2FA`. So the commit message should be `implement 2FA`

If a commit message is for a specific task, then it should start with the task number. For example:

```txt
1110 - Implement 2FA
```

Each commit message should start with one of the following prefixes:

- `feat` ??? a new feature is introduced with the changes
- `fix` ??? a bug fix has occurred
- `chore` ??? changes that do not relate to a fix or feature and don't modify src or test files (for example updating dependencies)
- `refactor` ??? refactored code that neither fixes a bug nor adds a feature
- `docs` ??? updates to documentation such as a the README or other markdown files
- `style` ??? changes that do not affect the meaning of the code, likely related to code formatting such as white-space, missing semi-colons, and so on.
- `test` ??? including new or correcting previous tests
- `perf` ??? performance improvements
- `ci` ??? continuous integration related
- `build` ??? changes that affect the build system or external dependencies
- `revert` ??? reverts a previous commit

## .gitignore

Every repository should have a `.gitignore` file. This file should list all the files that are not needed to be pushed to git. Any file that can be generated by running some command should not be pushed to git (There are some exceptions though).

> Important: Adding a file to git and then adding to gitignore has no effect as it is already tracked in git history. So this should be taken care of from initial commit itself.

## README

Each repository should have a `README.md` file. Readme file should contain following points:

- Introduction: A short introduction of what is the Project/Repository for
- Technical Stack: List of technologies required in order to run the project
- Getting Started: Steps for setting up local environment
- Deployment: How to deploy project on a live environment
- Branching Strategy: What is the branching strategy used for this repository
