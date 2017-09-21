# How to Resolve Feature Branches
{:.no_toc}

It is considered good practice to commit everything to feature branches before integrating these changes in the branch it forked off from (usually **master**). Some [branching models](branching-models.md) even require it. There are a few different ways how to resolve a feature branch and integrate the changes in the originating branch.

In the following examples we will always use **master** for the *originating branch* and **topic/feature** for the *feature branch*.

* toc
{:toc}

## rewrite feature branch history

`git rebase` is **the** method to keep your history **linear**. It is recommended to **rebase before every merge** on top of the latest **master**. You should also not hesitate to rewrite **topic/feature** history before you merge so the resulting **master** history will look good.

## resolving methods

### merge with fast-forward

The goal of this method is to have the resulting history look like as if the **topic/feature** branch commits were created directly on **master**.

History before the merge:

```
* 4d5448f (HEAD -> master) blah blah
* c684920 blah
| * 12aabcd (topic/feature) fixes issue with feature
| * 49cd955 adds blah to feature
| * 667d1c4 adds feature foo
|/
* 2d9d186 previous commit
* ...
```

Resolving such a feature branch:

```
# rebase the feature branch on top of master
# (you may need to resolve conflicts here)
$ git checkout topic/feature
Switched to branch 'topic/feature'
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: adds feature foo
Applying: adds blah to feature
Applying: fixes issue with feature

# merge the cleaned-up changes
$ git checkout master
Switched to branch 'master'
$ git merge --ff-only topic/feature
Updating 2985b6b..6760407
Fast-forward
 foo | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 foo
```

History after the merge:

```
* 6760407 (HEAD -> master, topic/feature) fixes issue with feature
* 0794238 adds blah to feature
* f223d30 adds feature foo
* 2985b6b blah blah
* ebe0262 blah
* 03f4f8d previous commit
* 62a0ee9 ...
```

### merge with merge commit

The relevant difference to the other methods is that you preserve **topic/feature** history.

History before the merge:

```
* 4d5448f (HEAD -> master) blah blah
* c684920 blah
| * 12aabcd (topic/feature) fixes issue with feature
| * 49cd955 adds blah to feature
| * 667d1c4 adds feature foo
|/
* 2d9d186 previous commit
* ...
```

Resolving such a feature branch:

```console
# rebase the feature branch on top of master
# (you may need to resolve conflicts here)
$ git checkout topic/feature
Switched to branch 'topic/feature'
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: adds feature foo
Applying: adds blah to feature
Applying: fixes issue with feature

# merge the cleaned-up changes
$ git checkout master
Switched to branch 'master'
$ git merge --no-ff --no-edit topic/feature
Merge made by the 'recursive' strategy.
 feature | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 feature
```

History after the merge:

```
*   40018ef (HEAD -> master) Merge branch 'topic/feature'
|\
| * 982cc34 (topic/feature) fixes issue with feature
| * 94756b4 adds blah to feature
| * e532769 adds feature foo
|/
* 4d5448f blah blah
* c684920 blah
* 2d9d186 previous commit
* ...
```

The history is still considered linear because all commits reside on one side of the branch, that is also why it is important to rebase first.

### squash merge

This creates a single commit on top of **master**. All history of **topic/feature** gets condensed into a single commit. This way to resolve a feature branch should be used if the resulting diff is relatively small.

History before the merge:

```
* 5082481 (topic/feature) fixes issue with feature
* 2ed5553 adds blah to feature
* 9c339f9 adds feature foo
* 2d9d186 (HEAD -> master) previous commit
* 04159ab ...
```

Resolving such a feature branch:

```bash
# perform the squash
git checkout master
git merge --squash topic/feature
git commit -v
```

History after the merge:

```
* 6db1876 (HEAD -> master) adds feature foo
* 2d9d186 previous commit
* ...
```

## cleaning up feature branches

In most cases you want to remove **topic/feature** after the merge took place, both locally and on the remotes.

Remove local branch:

```console
$ git branch -D topic/feature
```

Remove remote branch:

```console
$ git push remote :topic/feature
```

---

[back to index](index.html)
