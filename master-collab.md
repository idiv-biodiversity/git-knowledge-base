# Collaboration on master Branch

When many colleagues work with the **master** branch directly, conflicts can arise when pushing. **TL;DR:** Always **rebase** instead of **merge**! This creates a **clean, linear commit history**.

If you have made some changes directly on the **master** branch and want to **push** them, the push will either be *fast-forwarded* or git will tell you that other changes have been made to **master**:

```
$ git push
To /home/umcdev/projects/git-demo/pull-merge-vs-rebase.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to '/home/umcdev/projects/git-demo/pull-merge-vs-rebase.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

You will have to manually resolve this case and there are two choices:

1.  **merge origin/master** into your **master** and push

    ```console
    $ git lol
    * e82e9a2 (HEAD -> master) adds awesome feature from bob
    | * 1507845 (origin/master, origin/HEAD) adds awesome feature from alice
    |/
    * e6a4787 previous commit
    * 60019be ...

    $ git pull --no-edit
    Already up-to-date!
    Merge made by the 'recursive' strategy.

    $ git lol
    *   abfeda2 (HEAD -> master) Merge branch 'master' of /home/umcdev/projects/git-demo/pull-merge-vs-rebase
    |\
    | * 1507845 (origin/master, origin/HEAD) adds awesome feature from alice
    * | e82e9a2 adds awesome feature from bob
    |/
    * e6a4787 previous commit
    * 60019be ...
    ```

    Avoid this, because non-linear history is less readable!

2.  **rebase** your **master** on **origin/master** and push

    ```console
    $ git lol
    * e82e9a2 (HEAD -> master) adds awesome feature from bob
    | * 1507845 (origin/master, origin/HEAD) adds awesome feature from alice
    |/
    * e6a4787 previous commit
    * 60019be ...

    $ git pull --rebase
    First, rewinding head to replay your work on top of it...
    Applying: adds awesome feature from bob

    $ git lol
    * 519da48 (HEAD -> master) adds awesome feature from bob
    * 1507845 (origin/master, origin/HEAD) adds awesome feature from alice
    * e6a4787 previous commit
    * 60019be ...
    ```

    Much cleaner, this is the way to go!

**Note:** You can even make rebase'ing while pulling a default:

```
git config [--global] pull.rebase preserve
```

---

[back to index](index.html)
