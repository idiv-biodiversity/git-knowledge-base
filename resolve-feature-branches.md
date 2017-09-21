# How to Resolve Feature Branches
{:.no_toc}

It is considered good practice to commit everything to feature branches before integrating these changes in the branch it forked off from (usually **master**). Some [branching models](branching-models.md) even require it. There are a few different ways how to resolve a feature branch and integrate the changes in the originating branch.

**Note:** In the following examples we will always use **master** for the *originating branch* and **topic/feature** for the *feature branch*.

* toc
{:toc}

## rewrite feature branch history

`git rebase` is **the** method to keep your history **linear**. It is recommended to **rebase before every merge** on top of the latest **master**. You should also not hesitate to rewrite **topic/feature** history before you merge so the resulting **master** history will look good.

```console
$ git lol
* 2985b6b (master) blah blah
* ebe0262 blah
| * cba1d40 (HEAD -> topic/feature) fixes issue with feature
| * 8b29f74 adds blah to feature
| * 7f295dd adds feature foo
|/
* 03f4f8d previous commit
* 62a0ee9 ...
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: adds feature foo
Applying: adds blah to feature
Applying: fixes issue with feature
$ git lol
* 76e29d1 (HEAD -> topic/feature) fixes issue with feature
* 5428f8d adds blah to feature
* 43d263e adds feature foo
* 2985b6b (master) blah blah
* ebe0262 blah
* 03f4f8d previous commit
* 62a0ee9 ...
```

Without the rebase, the history after a merge would be *non-linear*:

```console
$ git checkout master
Switched to branch 'master'
$ git merge topic/feature
Merge made by the 'recursive' strategy.
 foo | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 foo
$ git lol
*   f17ba26 (HEAD -> master) Merge branch 'topic/feature'
|\
| * cba1d40 (topic/feature) fixes issue with feature
| * 8b29f74 adds blah to feature
| * 7f295dd adds feature foo
* | 2985b6b blah blah
* | ebe0262 blah
|/
* 03f4f8d previous commit
* 62a0ee9 ...
```

**Note:** All histories *before the merge* below are already rebased like this!

## resolving methods

History before the merge:

```
* d2e7011 (HEAD -> topic/feature) fixes issue with feature
* f1a50c4 adds blah to feature
* 174ed5d adds feature foo
* 2985b6b (master) blah blah
* ebe0262 blah
* 03f4f8d previous commit
* 62a0ee9 ...
```

### merge with fast-forward

The goal of this method is to have the resulting history look like as if the **topic/feature** branch commits were created directly on **master**.

```console
$ git checkout master
Switched to branch 'master'
$ git merge --ff-only topic/feature
Updating 2985b6b..c6121fd
Fast-forward
 foo | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 foo
```

History after merge:

```
* c6121fd (HEAD -> master, topic/feature) fixes issue with feature
* fcbba2d adds blah to feature
* 2e09b2a adds feature foo
* 2985b6b blah blah
* ebe0262 blah
* 03f4f8d previous commit
* 62a0ee9 ...
```

### merge with merge commit

The relevant difference to the other methods is that you preserve **topic/feature** history.

```console
$ git checkout master
Switched to branch 'master'
$ git merge --no-ff --no-edit topic/feature
Merge made by the 'recursive' strategy.
 foo | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 foo
```

History after merge:

```
*   4ea0082 (HEAD -> master) Merge branch 'topic/feature'
|\
| * c6121fd (topic/feature) fixes issue with feature
| * fcbba2d adds blah to feature
| * 2e09b2a adds feature foo
|/
* 2985b6b blah blah
* ebe0262 blah
* 03f4f8d previous commit
* 62a0ee9 ...
```

The history is still considered linear because all commits reside on one side of the branch, that is also why it is important to **rebase first**.

### squash merge

This creates a single commit on top of **master**. All history of **topic/feature** gets condensed into a single commit. This way to resolve a feature branch should be used if the resulting diff is relatively small.

```console
$ git checkout master
Switched to branch 'master'
$ git merge --squash topic/feature
Updating 2985b6b..c6121fd
Fast-forward
Squash commit -- not updating HEAD
 foo | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 foo
$ git commit -v
[master 66fcf8b] adds feature foo
 1 file changed, 3 insertions(+)
 create mode 100644 foo
```

History after merge:

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
