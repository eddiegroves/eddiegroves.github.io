---
layout: post
title:  Fixing Commit Message Typos in Git
date:   2013-06-05 00:00:00
---

Use these to quickly fix a typo that was just created, **before** pushing upstream.

    git commit --amend
    git commit --amend -m "Fixed commit message"

The first command opens the text editor with the last commit message ready to edit.

If the typo was not the latest commit, then **rebase** is used.

    git rebase -i HEAD~2

Change the `~2` to how many commits away the typo is and use `reword` during the rebase.

### Further information

* [Git Tools - Rewriting History][1]
* `git help commit`
* `git help rebase`

[1]: http://git-scm.com/book/ch6-4.html

