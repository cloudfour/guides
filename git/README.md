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

They follow code review guidelines to avoid miscommunication. They make comments
and ask questions directly on lines of code. For changes which they can make
themselves, they `checkout` the branch:

```
git checkout <branch-name>
```

If needed, they make small changes right in the branch, test the feature on
their machine, `commit`, and `push`.

```
git commit -m "Fix the stuff that so-and-so missed"
git push origin <branch-name>
```

### When satisfied, they comment on the pull request

> This is some excellent work, Ross. :thumbsup:

Merging in General
------------------

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
