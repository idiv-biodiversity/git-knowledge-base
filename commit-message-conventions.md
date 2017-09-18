# Commit Message Conventions
{:.no_toc}

![https://xkcd.com/1296/](img/xkcd-1296-git-commit.png "https://xkcd.com/1296/")

The goal of good commit messages is to understand what happened in the project **years later**.

## contents
{:.no_toc}

* toc
{:toc}

## basic rules

Everyone in every project should follow these rules:

1.  limit subject line to 50 characters
1.  separate subject line from body with a blank line
1.  wrap body at 72 characters
1.  avoid punctuation in subject line
1.  do not enumerate in subject line
1.  put references to issue tracker ID's at the bottom of the body

The *diff* tells you **what** changed and **how** it changed, while the commit message tells you **why** it changed, it provides **context**. The context is hard to guess from the *diff*, that's why it is so important to provide the context in the commit message.

1.  use the subject as summary
1.  use the body to explain context

These are really important, too:

1.  be concise
1.  be consistent

## additional rules

There are different preferences. Just remember: be consistent and follow project contribution guidelines!

### @cbeams

full blog post: https://chris.beams.io/posts/git-commit/

1.  capitalize the subject line
1.  use the imperative mood in the subject line

example:

```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

### @wookietreiber

1.  avoid caps in subject line
1.  use the third person in the subject line

example:

```
parsing checks accounting file version

Parsing is now separated from Streaming. The new parser also checks the
version header of the accounting file to find out which version to use.
This boosts performance compared to the old exhaustive pattern match. On
a larger accounting file this improved the runtime from 92 minutes to 51
minutes.
```
