[pull request]: https://help.github.com/articles/using-pull-requests
[pull request template]: https://help.github.com/articles/creating-a-pull-request-template-for-your-repository/
[name your feature branches by convention]: https://docs.microsoft.com/en-us/vsts/git/concepts/git-branching-guidance?view=vsts#name-your-feature-branches-by-convention

Git Protocol
============

A guide for programming within version control.

## Table of Contents

- [General Guidelines](#general-guidelines)
- [Writing a Feature](#writing-a-feature)
- [Reviewing Code](#reviewing-code)
- [Merging in General](#merging-in-general)
- [Pull Request Template](#pull-request-template)
- [Write Useful Commit Messages](#write-useful-commit-messages)


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

- `users/username/description`
- `users/username/workitem`
- `feature/feature-name`
- `feature/feature-area/feature-name`
- `bugfix/description`
- `hotfix/description`
- `cleanup/description`
- `chore/description`

When you [name your feature branches by convention] using slashes,
it provides a much nicer organization when viewing as directories
as well as within any Git GUI apps.

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

Be sure to [write a good commit message](#write-useful-commit-messages).

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

[Squash commits](./squash.md) like "Fix whitespace" into one or a small number
of valuable commit(s). Edit commit messages to reveal intent. Run tests.

```
git fetch origin
git rebase -i origin/master
```

- [How and Why to Squash Merge your Pull Request](./squash.md)

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

Please add a [Pull Request Template] to your repo,
to ensure that all pull requests follow our guide:

See our [Standard Pull Request Template](./pull_request_template.md) in this directory.

## Write Useful Commit Messages

Please ensure that you follow commit message best practices:

1. Separate subject from body with a blank line
1. Limit the subject line to 50 characters
1. Capitalize the first word of the subject line
1. Do not end the subject line with a period
1. Use the imperative mood in the subject line
   (e.g. "Fix the bug" not "Fixed the bug")
1. Wrap the body at 72 characters
1. Use the body to explain what and why vs. how

For example:

```
Present-tense summary under 50 characters

* More information about commit (under 72 characters).
* More information about commit (under 72 characters).

http://project.management-system.com/ticket/123
```

### Commit Message Best Practices
- [A Note About Git Commit Messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Commit Messages Guide](https://github.com/RomuloOliveira/commit-messages-guide)

### Commit Message Template

See our [Standard Commit Message Template](./commit_template.txt) in this directory.

To use the template, save it to your local machines and add it to your `.gitconfig`:

```
git config --global commit.template <.git-commit-template.txt file path>
```

For example, if you saved it to your home folder, try:

```
git config --global commit.template ~/.git-commit-template.txt
```
