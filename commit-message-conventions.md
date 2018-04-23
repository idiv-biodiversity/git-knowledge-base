# Commit Message Conventions
{:.no_toc}

![https://xkcd.com/1296/](img/xkcd-1296-git-commit.png "https://xkcd.com/1296/")

The goal of good commit messages is to understand what happened in the project **years later**.

## contents
{:.no_toc}

* toc
{:toc}

## structural style

The following basic rules detail the **structural style** of a commit message. Everyone in every project should follow these rules.

1.  limit subject line to 50 characters
1.  separate subject line from body with a blank line
1.  wrap body at 72 characters
1.  avoid punctuation in subject line
1.  never enumerate in subject line
1.  put references to issue tracker ID's at the bottom of the body

This is an example that also contains some explanations of the rules above. You should read it!

```
this is a short subject line

This is the body. Notice that the subject line is short and to the
point. The commit message is often used in emails when notifying
collaborators of changes.

You can also have paragraphs in the body. Notice that the subject is
also separated from the body with a newline, just as paragraphs are.

You also can use enumerations in the body:

- an item
- another item

Do NOT enumerate in the subject! If you ever feel like doing that, you
should probably split the commit into two separate commits.

References to issue trackers should be in the very end.

fixes #42
```

## content

The **git diff** and **git log --patch** commands tell you **what** changed between commits and **how** it changed. The commit message **should** tell you **why** it changed. It should not repeat the *diff*, but should **provide context**. The context is often not easy to guess from the *diff*. That is why it is so important to provide the context in the commit message.

To provide a fast way to grasp the commits intent, follow these rules:

1.  use the subject line as a very short summary
1.  use the body to explain context

These rules are also very important:

1.  be concise
1.  be consistent

There are different preferences in terms of *how to write* the commit message, which tense to use, capitalization, etc. The most important rule is to figure out a way to do it and stick to it: **be consistent and follow project contribution guidelines!** Remember that it is all about being able to understand the projects history quickly.

### @cbeams

The full blog post is [here](https://chris.beams.io/posts/git-commit/). It closely resembles the rules git uses when automatically creating commit messages, e.g. for merge commits or when reverting.

The rules are:

1.  capitalize the subject line
1.  use the imperative mood in the subject line

Example:

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

My personal guideline is:

> Don't think: What have **I** done in this commit?
>
> Think: What **IS** this commit doing?

Your personal relation as the commit author is not important in the long run. What is important is what the commit does. Detach yourself. Think of the project history as a person. What is the project doing?

Especially when viewing the short summary, this helps a lot:

```console
$ git log --oneline
4fbb542 adds git fire meme
57e4655 corrects syntax highlighting
5dfe12a adds output of impossible push to master collab
d5c457e adds section about collaboration on master
8300e52 highlights to strive for linear history
13b2656 adds section about linear vs non-linear history
```

The following rules emerge:

1.  use present tense and third person in the subject line
1.  avoid caps in subject line

Example:

```
checks accounting file version in parsing

Parsing is now separated from Streaming. The new parser also checks the
version header of the accounting file to find out which version to use.
This boosts performance compared to the old exhaustive pattern match. On
a larger accounting file this improved the runtime from 92 minutes to 51
minutes.
```

---

[back to index](index.html)
