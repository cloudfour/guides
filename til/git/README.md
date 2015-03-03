## Linking to Multiple Lines

I learned today that you can link to a multiple-line selection, not just a single line, e.g. https://github.com/hexojs/hexo/blob/master/lib/plugins/console/generate.js#L89-L101

Add `CONTRIBUTING.md` at the top of your repo and it will get linked to with a "read the guidelines for contributing..." automatically!

## --ours vs. --theirs

Recently I learned about

`git checkout --ours [file...]`

and

`git checkout --theirs [file...]`

Which is a quick way to resolve a conflict on something in an intuitive way. Then commit the results.

## git rev-parse

The [`git rev-parse` command](http://git-scm.com/docs/git-rev-parse) is a "porcelainish" interface to some lower-level git internals. 

Kinda handy:

* `git rev-parse --is-inside-work-tree` returns a Boolean as to whether you are, well, currently inside of a working git tree
* `git rev-parse --short HEAD` Gits you the short SHA hash for the most recent commit on HEAD


## git symbolic-ref

`git symbolic-ref --quiet --short HEAD` is a programattic way to ask what your working branch is at the moment.

