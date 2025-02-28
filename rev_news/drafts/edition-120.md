---
title: Git Rev News Edition 120 (February 28th, 2025)
layout: default
date: 2025-02-28 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 120 (February 28th, 2025)

Welcome to the 120th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of January and February 2025.

## Discussions

<!---
### General
-->

### Reviews

+ [[PATCH] worktree: detect from secondary worktree if main worktree is bare](https://lore.kernel.org/git/pull.1829.git.1731653548549.gitgitgadget@gmail.com/)

  Last November, Olga Pilipenco sent a patch to the mailing list
  addressing an issue she encountered while working with multiple
  [worktrees](https://git-scm.com/docs/git-worktree).

  Git worktrees allow developers to check out multiple branches from
  the same repository simultaneously, each in its own working
  directory. Unlike creating separate clones, worktrees share the same
  object database and references, saving disk space and avoiding the
  need to push and fetch between copies of the repository. They can be
  very useful when working on multiple features in parallel or when
  needing to make a quick fix while in the middle of other development
  work.

  The issue happened when a repository had a main worktree that was
  bare with `core.bare = true` in `config.worktree`. If a new
  secondary worktree was created, then from that secondary worktree
  the main worktree appeared as non-bare. This prevented users from
  checking out or working with the default branch of the main worktree
  (typically "main" or "master") in the secondary worktree.

  When `extensions.worktreeConfig` is enabled, each worktree has its
  own configuration settings in a `config.worktree` file that can
  override repository-wide settings in the common `config` file. This
  allows different worktrees to have different configurations, but it
  also means that settings from one worktree aren't automatically
  visible to commands running in another worktree.

  Olga found that when inside the secondary worktree, the main
  worktree's configuration wasn't initialized, and her patch fixed
  that by loading the main worktree's `config.worktree` file only when
  required.

  Unfortunately Olga's email fell through the cracks, receiving no
  response. But last January she sent a
  [version 2](https://lore.kernel.org/git/pull.1829.v2.git.1737063335673.gitgitgadget@gmail.com/)
  of her patch. There was no code change compared to the first
  version, but she added people in "Cc:", and she had rebased the
  patch on top of the "maint" branch.

  This time Eric Sunshine replied. He acknowledged that this was a
  real problem and noted that it had been documented in a "NEEDSWORK"
  comment added in 2019 into the code that mentioned it. He then
  attempted to rewrite the commit message of the patch in a way that
  was "more idiomatic" to the project and that added more details to
  help understand the problem.

  The suggested commit message especially mentioned that when
  `extensions.worktreeConfig` is true, commands run in a secondary
  worktree only consulted `$commondir/config` and
  `$commondir/worktrees/<id>/config.worktree`. Thus they never saw
  that the main worktree's `core.bare` setting was true in
  `$commondir/config.worktree`.

  Eric also suggested removing some parts of Olga's commit message
  that talked about other solutions she had considered, or that
  repeated in which circumstances the problem appeared. Then there
  were a number of small comments on the code part of the patch.

  Olga replied to Eric saying that the commit message he proposed was
  "so much better" than the original one. She agreed with most of
  Eric's suggestions and answered the few questions he asked.

  Eric replied explaining some technical details and making a few more
  suggestions.

  Junio Hamano, the Git maintainer then replied to Eric thanking him
  "for an easy-to-read review" and thanking Olga for working on this
  issue.

  Eric and Olga further discussed technical improvements to the
  patch. In the course of that discussion, Eric explained the
  historical context related to using the "bare main worktree"
  expression:

  > It's a historic "accident" that when worktree support was designed,
  > the idea of linking worktrees to a bare repository was not considered.
  > Support for using worktrees with a bare repository was added later.
  > However, by that time, the term "main worktree" was already well
  > established, with the very unfortunate result that even when there is
  > no actual "main worktree" but only a bare repository with "linked
  > worktrees" hanging off it, the repository itself is usually referred
  > to as the "bare main worktree", which is an obvious misnomer; the
  > repository is just a repository (i.e. the object database and other
  > meta-information) and there is no actual main worktree.

  Olga then sent a
  [version 3](https://lore.kernel.org/git/pull.1829.v3.git.1738346881907.gitgitgadget@gmail.com/)
  of her patch. It used the commit message suggested by Eric, and
  implemented his suggestions.

  Junio reviewed this new version of the patch and had a single
  question about the code that decided when it was necessary to read
  the main worktree's `config.worktree` file. Olga and Junio further
  discussed how to make it clearer what that code was doing, and
  eventually agreed on adding a four line long comment on top of it.

  Olga then sent a
  [version 4](https://lore.kernel.org/git/pull.1829.v4.git.1738737014194.gitgitgadget@gmail.com/)
  of her patch which only added that four line long comment.

  The patch was later merged into the 'master' branch, so the next
  2.49 version of Git that should be released in a few weeks will
  finally resolve a long-standing issue and significantly enhance the
  usability of Git worktrees for developers working with bare
  repositories.

<!---
### Support
-->


## Community Spotlight: Chris Torek

_[Chris Torek](https://stackoverflow.com/users/1256452/torek) has been a prolific
contributor to the Git topic on Stack Overflow. This edition features an interview
with him. This a continuation of our initiative to interview community contributors
ouitside of our mailing list. Our first interview was [with VonC in edition 106](https://git.github.io/rev_news/2023/12/31/edition-106/#community-spotlight-vonc)_.


* **Who are you and what do you do?**

  "Who am I" is way too complicated! 🙂 What I do ... well, I'm now
  retired, and you'd think that would give me more time to answer things
  like this.

  I used to do a lot of embedded systems programming, and a lot of
  internal company education at times (about programming languages,
  various hardware functions and limitations, software tools, and such).
  That's what led me to [answering StackOverflow questions](https://stackoverflow.com/users/1256452/torek?tab=summary).

* **What would you name your most important contribution to Git?**

  I haven't put much into Git itself. I fixed a minor issue with
  case-insensitive rename once, and something that was annoying me about
  `git diff` applied to merge commits [[ref](https://public-inbox.org/git/pull.804.v4.git.git.1591978801.gitgitgadget@gmail.com/)].

* **What was your motivation behind answering questions about Git on
  Stack Overflow?**

  Here, well, I got roped into explaining Git to a group that was moving
  from Mercurial. I found existing descriptions to be lacking.
  Eventually that particular job went away but the question-answering
  persisted, until I got sufficiently annoyed at StackOverflow itself
  (for various reasons) to take a break that continues to this day.

* **If you could get a team of expert developers to work full time on
  something in Git for a full year, what would it be?**

  I'm not entirely sure.  There are a few big issues today, such as
  dealing with OS irregularities (the fact that Windows can't name a
  file `aux.h` for instance is a trivial example of the overall problem;
  very long file names, case and UTF-8 encoding sensitivities are
  another example of the same underlying issue); the ongoing
  [transition from SHA-1 to SHA-256](https://git-scm.com/docs/hash-function-transition)
  (which works now but there's no cross-compatibility); a number
  of minor but sometimes important niggles with merging; support
  for extremely large code bases, including submodules and other
  ideas (Microsoft's Git VFS). I have no ideas for *how* to
  achieve this but a better way to "see" history would,
  I think, be a huge improvement.

  One other thing that might be particularly good is an equivalent of
  [Mercurial's `evolve` extension](https://www.mercurial-scm.org/doc/evolution/).
  But even Mercurial's was never mainstreamed; this is very hard to
  get right (whatever "right" means).

* **If you could remove something from Git without worrying about backwards
  compatibility, what would it be?**

  I'm not convinced anything needs to be _removed_, but it would
  simplify things a lot if we didn't need SHA-1 compatibility, if
  SHA-256 magically just worked and everything were converted over. (And
  looking at [VonC's reply](https://git.github.io/rev_news/2023/12/31/edition-106/#community-spotlight-vonc)
  I agree that `switch`+`restore` is a much better
  split than the old `checkout`.) And, although people like it for
  convenience, it might be OK if we all had to use separate
  `fetch`-then-(whatever is needed) steps: see below.

* **What is your favorite Git-related tool/library, outside of Git itself?**

  I don't think I have one. I've used [gitk](https://git-scm.com/docs/gitk)
  for history browsing, and if it were somehow improved (see the list of
  items above) it might be particularly useful.

* **What is one of your most favourite features of Git?**

  Speed. Having used the previous generations of version control (and
  waited, and waited...), there's nothing quite like doing an update and
  having it take only seconds. The distributed nature is also pretty
  crucial, though it has its pluses and minuses.

* **Could you brief a bit about one of your most memorable experience with Git?**

  Hah, the most memorable one was probably one of the worst, back in the
  days of Git 1.5 or so. Back then, an initial `git pull` wasn't always
  careful about a pre-populated working tree. I had it destroy a week's
  worth of code once. Ever since then I've separated pull into fetch
  followed by merge-or-rebase. This is long since fixed, but it's
  instructive to new users to know that `pull` is really two separate
  steps. When I started, I didn't know that: the tutorial I read just
  said to run `git pull`.

* **What is your advice for people who want to start using Git? Where
  and how should they start?**

  I'm not entirely fond of any of the introductions I've seen. I started
  on a book once (between jobs) but stalled out when I went to work for
  another startup. One of these days I plan to get back to it.

* **There's a common conception that "Git is confusing". What are your
  thoughts about the same?**

  There *are* confusing parts, but they are inherent to the issues that
  occur with distributed repositories and independent development. The
  only way to really understand this is to get a good grounding—hence
  the idea of writing a book.

* **If there’s one tip you would like to share with other Git
  developers, what would it be?**

  For *developers* in particular, they should probably have a look at
  what surprises Git users. If something didn't work the way someone
  expected it to, why? Was it an incorrect expectation (it probably was)
  and if so, why did the user *have* that expectation in the first
  place?


## Other News

__Various__

- The Git project has been accepted as a [Mentor Organization](https://summerofcode.withgoogle.com/programs/2025/organizations/git)
  for Google Summer of Code (GSoC) 2025. We can still add project ideas to our
  [idea page](https://git.github.io/SoC-2025-Ideas/), and volunteers to (co-)mentor
  are still welcome. Feel free to join the discussion in the [corresponding thread](http://public-inbox.org/git/6C29409D-691B-471F-B08C-83E14D35EE13@gmail.com/T/#mb087c1b0ed06fcbd56d4ffa320efbeb42fd4983f).
  Also, feel free to spread the word about Git’s participation.

__Light reading__

<!---
__Easy watching__
-->

__Git tools and sites__


## Releases

+ Git [2.49.0-rc0](https://public-inbox.org/git/xmqqzfi8bljk.fsf@gitster.g/)
+ Git for Windows [2.49.0-rc0(1)](https://github.com/git-for-windows/git/releases/tag/v2.49.0-rc0.windows.1),
[2.48.1(1)](https://github.com/git-for-windows/git/releases/tag/v2.48.1.windows.1)
+ GitHub Enterprise [3.16.0](https://help.github.com/enterprise-server@3.16/admin/release-notes#3.16.0),
[3.15.3](https://help.github.com/enterprise-server@3.15/admin/release-notes#3.15.3),
[3.14.8](https://help.github.com/enterprise-server@3.14/admin/release-notes#3.14.8),
[3.13.11](https://help.github.com/enterprise-server@3.13/admin/release-notes#3.13.11),
[3.12.15](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.15)
+ GitLab [17.9.1, 17.8.4, 17.7.6](https://about.gitlab.com/releases/2025/02/26/patch-release-gitlab-17-9-1-released/),
[17.9](https://about.gitlab.com/releases/2025/02/20/gitlab-17-9-released/),
[17.8.2, 17.7.4, 17.6.5](https://about.gitlab.com/releases/2025/02/12/patch-release-gitlab-17-8-2-released/)
+ GitKraken [10.7.0](https://help.gitkraken.com/gitkraken-client/current/),
[10.6.3](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.4.17](https://desktop.github.com/release-notes/),
[3.4.16](https://desktop.github.com/release-notes/)
+ Sourcetree [4.2.11](https://product-downloads.atlassian.com/software/sourcetree/ReleaseNotes/Sourcetree_4.2.11.html)
+ tig [2.5.12](https://github.com/jonas/tig/releases/tag/tig-2.5.12),
[2.5.11](https://github.com/jonas/tig/releases/tag/tig-2.5.11)
+ Garden [2.1.0](https://github.com/garden-rs/garden/releases/tag/v2.1.0)
+ Git Cola [4.12.0](https://github.com/git-cola/git-cola/releases/tag/v4.12.0)
+ GitButler [0.14.8](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.14.8),
[0.14.7](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.14.7)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from XXX.
