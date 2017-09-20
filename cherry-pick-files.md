# Cherry-Pick Files

Suppose you work on *feature branch*, e.g. `wip/topic/feature`, forked off of a *source branch*, e.g. `master`. Now, you have made some changes you want to immediately make available in *source branch* without waiting for *feature branch* to be finished - everyone should benefit from these changes as soon as possible.

**Note:** We are using `wip/topic/feature` here on purpose to highlight that the use case for cherry-picking files usually occurs when working heavily on such a work-in-progress *feature branch*.

**Note:** For the workflow below we assume that all of these changes are in a single file. This simplifies the workflow visually. You could apply the workflow to multiple files, too.

**Note:** This is analogous to the `git cherry-pick` command, even though we don't actually use it.

```bash
# checkout source branch
git checkout master

# get all changes to `file` and apply them
git diff-tree --patch master wip/topic/feature -- file | git apply
git stage file
git commit
```

Finally, you also want to rebase the *feature branch* on top of the new *source branch* to remove the changes from *feature branch* we now already have in *source branch*. Most likely, there will be merge conflicts because *feature branch* iteratively introduces the changes, while *source branch* (**HEAD**) already has everything. Thus, you should almost always pick **HEAD** from the conflicts to remove the changes from the feature branch, which is, after all, what we want to achieve with the rebase.

```bash
git rebase master wip/topic/feature
```

---

[back to index](index.html)
