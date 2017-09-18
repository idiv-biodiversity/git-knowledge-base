# how to integrate changes: from master to feature branch
{:.no_toc}

* toc
{:toc}

## situation

Imagine the following situation:

1.  You have worked on a feature branch **topic/feature** branched off of **master**:

    ```
    * cba1d40 (HEAD -> topic/feature) fixes issue with feature
    * 8b29f74 adds blah to feature
    * 7f295dd adds feature foo
    * 03f4f8d (master) previous commit
    * 62a0ee9 ...
    ```

2.  There are some changes to **master**:

    ```
    * 4dfe56f (master) blah blah blah
    * 2985b6b blah blah
    * ebe0262 blah
    | * cba1d40 (HEAD -> topic/feature) fixes issue with feature
    | * 8b29f74 adds blah to feature
    | * 7f295dd adds feature foo
    |/
    * 03f4f8d previous commit
    * 62a0ee9 ...
    ```

Now, you figure:

> Wow, these *blah blah blah* changes are really awesome and would help me implement my feature.

So, the question is:

> How do I integrate the changes from **master** into the **topic/feature** branch?

There are two ways to do this which are explained in the following sections.

## merge master into topic/feature

This workflow is recommended to be used when you work on that feature branch with other people, especially if they are not experienced git users.  The reason for this recommendation is that this workflow does not require **force pushing** and knowing how to deal with them.

So-called **merge commits** are created each time you merge **master** into the feature branch. This can make your commit history somewhat unreadable. At some point, though, you may want to clean up the commit history by removing all of these merge commits. This should be done when the feature branch is finally merged back into master with either a **squash and merge** or a **rebase and merge** (**TODO:** add links).

```console
$ git checkout topic/feature
Switched to branch 'topic/feature'

$ git merge --no-edit master
Merge made by the 'recursive' strategy.
blah | 3 +++
1 file changed, 3 insertions(+)
create mode 100644 blah
```

Resulting history:

```
*   7123a38 (HEAD -> topic/feature) Merge branch 'master' into topic/feature
|\
| * 4dfe56f (master) blah blah blah
| * 2985b6b blah blah
| * ebe0262 blah
* | cba1d40 fixes issue with feature
* | 8b29f74 adds blah to feature
* | 7f295dd adds feature foo
|/
* 03f4f8d previous commit
* 62a0ee9 ...
```

Publish these changes:

```console
$ git push origin topic/feature
```

## rebase topic/feature on master

This workflow keeps your commit history clean from the get-go. However, each time you rebase, you need to **force push** the changed history to your remotes. For this reason you should use this workflow **only if you work on that feature branch alone** or your colleagues know how to work with or recover from force pushes.

```console
$ git rebase master topic/feature
First, rewinding head to replay your work on top of it...
Applying: adds feature foo
Applying: adds blah to feature
Applying: fixes issue with feature
```

Resulting history:

```
* 8bdcaee (HEAD -> topic/feature) fixes issue with feature
* eefad50 adds blah to feature
* b4e1267 adds feature foo
* 4dfe56f (master) blah blah blah
* 2985b6b blah blah
* ebe0262 blah
* 03f4f8d previous commit
* 62a0ee9 ...
```

Publish these changes:

```console
$ git push --force[-with-lease] origin topic/feature
```

---

**TODO:** How and where are merge conflicts handled? I guess (not confirmed), that merging master will resolve the conflicts inside of the merge commit, while rebasing handles the conflicts immediately in the individual commits that are applied. How are these merge commits resolved/handled when **rebase and merge** is used to merge the feature branch back to master?
