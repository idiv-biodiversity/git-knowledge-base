## Branch Naming Conventions

Independent of the used **branching model** (TODO link) these are generally useful guidelines:

1.  use dashes to separate words in branch names

    this gives you the best readability

    examples:

    - **prepare-for-paper-x**
    - **issue-426**
    - **ui-cli-output**

1.  use grouping tokens as prefixes separated with a slash

    - **topic/*** feature or feature set
    - **release/*** prepare release
    - **hotfix/*** bugs fix
    - **wip/*** work in progress

    examples:

    - **topic/feature-name**
    - **hotfix/42687**
    - **release/1.6.0**
    - **wip/trying-feature-name**

    you can also combine these prefixes:

    - **hotfix/42687/buggy-thing**
    - **topic/ui/cli/feature-name**
    - **wip/topic/feature-name**

    having these slash-separated prefixes helps with some git commands, e.g.:

    ```console
    $ git branch --list 'topic/*'
    topic/feature-foo
    topic/feature-bar
    ```

1.  be consistent

1.  don't fear renaming

    Most branches are essentially temporary names attached to commits. Don't fear renaming them.
