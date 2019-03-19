[pull request]: https://help.github.com/articles/using-pull-requests
[commit message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

Git Protocol
============

A guide for programming within version control.

General Guidelines
------------------

* Avoid including files that are specific to your own environment.
* Avoid committing directly to `master`.
* Perform all work in a feature branch.
* Rebase frequently to incorporate upstream changes.
* Use a [pull request] for code reviews.
* Delete your local and remote branches after merging.

Writing a Feature
-----------------

### Create a local feature branch based off master

```
git checkout master
git pull
git checkout -b <branch-name>
```

Prefix the branch name with something meaningful, for example:

- `feature/make-the-thing-better`
- `bugfix/735-sw-not-caching-images`
- `cleanup/rename-all-the-files`

Using slashes provides a much nicer organization when viewing as directories as well as within any Git GUI apps.

Another benefit is it lends itself to [this type of organization](https://docs.microsoft.com/en-us/vsts/git/concepts/git-branching-guidance?view=vsts#name-your-feature-branches-by-convention) as well, when/if needed:

> - `users/username/description`
> - `users/username/workitem`
> - `bugfix/description`
> - `feature/feature-name`
> - `feature/feature-area/feature-name`
> - `hotfix/description`

### Rebase frequently to incorporate upstream changes

```
git fetch origin
git rebase origin/master
```

Resolve conflicts. When feature is in a good state, stage the changes

```
git add --all
```

### Commit your changes

```
git status
git commit --verbose
```

Write a good [commit message]. Example format:

```
Present-tense summary under 50 characters

* More information about commit (under 72 characters).
* More information about commit (under 72 characters).

http://project.management-system.com/ticket/123
```

If you've created more than one commit, use a rebase to squash them into
cohesive commits with good messages:

```
git rebase -i origin/master
```

### Push your branch

```
git push origin <branch-name>
```

Submit a [pull request]. Ask for a code review.

Reviewing Code
--------------

### Fellow team members review the pull request

Your team members will follow code review guidelines to avoid miscommunication.
They make comments and ask questions directly on lines of code.
When satisfied, they'll approve your pull request and leave a comment:

> This is some excellent work, Ross. :thumbsup:

Merging in General
------------------

Once your PR has been approved, you are responsible for merging it.

### Rebasing

Squash commits like "Fix whitespace" into one or a small number of valuable
commit(s). Edit commit messages to reveal intent. Run tests.

```
git fetch origin
git rebase -i origin/master
```

### Force-Pushing

This allows GitHub to automatically close your pull
request and mark it as merged when your commit(s) are pushed to master. It also
makes it possible to find the pull request that brought in your changes.

```
git push --force origin <branch-name>
```

### The Big Green Button Method

Force-pushing may not always be appropriate for every project, depending on
other factors like hooks or continuous integration. Pull Requests may also be
merged into `master` (or whatever their target branch is) by simply
clicking the green "Merge Branch" button on the GitHub Pull Request page.

### Once merged, delete your branch

Delete the remote branch.

```
git push origin --delete <branch-name>
```

Delete your local feature branch.

```
git branch --delete <branch-name>
```

## Pull Request Template

Please add a [Pull Request Template](https://help.github.com/articles/creating-a-pull-request-template-for-your-repository/) to your repo, to ensure that all pull requests follow our guide:

```
## Overview

Please include a summary of the change and which issue is fixed.
Please also include relevant motivation and context.
List any dependencies that are required for this change.

## Screenshots

Visual changes should include a screenshot.

## Testing

1. instructions for reviewers
1. to test your changes

---

- Fixes # (issue)
- or [TrelloCard/Issue/Story](LINK_TO_STORY)

/CC @person
```
