---
title: Git Rev News Edition 110 (April 30th, 2024)
layout: default
date: 2024-04-30 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 110 (April 30th, 2024)

Welcome to the 110th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of March and April 2024.

## Discussions

### General

* [What's cooking in git.git (Mar 2024, #05; Tue, 19)](https://lore.kernel.org/git/xmqqil1iqi37.fsf@gitster.g/)

  In March, Junio Hamano, the Git maintainer, sent one of the usual
  "What's cooking in git.git" emails that describe the current state
  of the patch series that might be merged into the development
  branches (mostly "master", "next" and "seen").

  The patch series are listed in these emails along with some related
  information in a custom format, including the following elements:

    - a title line, for example:

    > * bl/cherry-pick-empty (2024-03-11) 7 commits

	where `bl` are the initials of the author, and `cherry-pick-empty`
    the series title,

	- a patch list, for example:

    >  - cherry-pick: add `--empty` for more robust redundant commit handling
    >  - cherry-pick: enforce `--keep-redundant-commits` incompatibility
    >  - sequencer: do not require `allow_empty` for redundant commit options
    >  - sequencer: treat error reading HEAD as unborn branch
    >  - rebase: update `--empty=ask` to `--empty=stop`
    >  - docs: clean up `--empty` formatting in git-rebase(1) and git-am (1)
    >  - docs: address inaccurate `--empty` default with `--exec`

	- a description, for example:

	>  "cherry-pick" told to keep redundant commits needs to be allowed to
    >  create empty commits to do its job, but it required the user to
    >  give the --allow-empty option, which was unnecessary.  Its UI has
    >  also been tweaked a bit.

    - a status, for example:

    >  Comments?

	- a source, for example:

    >  source: <20240119060721.3734775-2-brianmlyles@gmail.com>

  Some of the above elements, like the description, are also
  automatically used to create the release notes that Junio prepares
  and sends when he creates a new release.

  Brian Lyles replied to Junio that the description of the patch
  series used as an example above, which Brian had sent, was "a little
  out-of-date". He suggested a different wording for it, and said that
  he was going to send a version 4 of the series.

  Junio said that the wording suggestion for the description was
  very much appreciated, and wondered if the project could adopt a
  better workflow where contributors could write a short description
  at the top of the cover letter of their patch series and that
  description could be picked up automatically by some tools to appear
  in Junio's "What's cooking in git.git" emails.

  Brian Lyles agreed that improving the process could be a
  good idea. He mentioned a strategy used by other projects, namely
  adding an entry in a "CHANGELOG.NEXT.md" file in each
  important commit. At release time, all the entries in that
  file would be moved into a standard "CHANGELOG.md" file. He then
  showed how the entry in the "CHANGELOG.NEXT.md" file would look like
  for his series as an example.

  Junio replied by summarizing the current process related to these
  descriptions and pointing to the
  ["Documentation/howto/maintain-git.txt" file](https://github.com/git/git/blob/master/Documentation/howto/maintain-git.txt)
  which describes his workflow and says that maintaining these topic
  descriptions is his responsibility as the project maintainer. He
  then mentioned some downsides of giving that responsibility to the
  patch series authors.

  One downside is that the description might be harder to read because
  the authors "inevitably are biased by the importance of their own
  work ;-)". Another one is that the description might not be as
  consistent as when they are all written by the same person. Coming
  up with some description is also "a good opportunity" for the
  maintainer to find what is still unclear after reading the patches
  and cover letter. Junio agreed that "the distribution of burden is
  certainly attractive" though.

  Brian replied that he thought the author should still write
  something and that at least he was willing to do it. He also
  suggested having guidelines, like for commit messages, to help
  authors and reviewers standardize the style of these descriptions.

  In the meantime, in a separate email, Junio also pointed out that a
  "CHANGELOG.NEXT.md" file would make merges more difficult compared
  to having the description in the cover letter.

  To that Brian agreed, and proposed writing a patch to the
  "Documentation/SubmittingPatches" file to document that the
  description can be written in the cover letter.

  Junio replied by proposing a patch to that file himself. Brian
  commented that the description might need "some specific heading,
  phrase, or other structured text" to mark the description and make
  it easy to notice and extract.

  Dragan Simic joined the discussion saying that writing the
  description should not be a strict requirement and then agreed with
  Junio's patch. Max Gautier also chimed in, agreeing with Brian and
  Dragan about using a format to mark the description. Dragan replied
  that adding an example of such a formatted description in the patch
  Junio suggested would be good.

  Junio replied to Brian that he preferred starting "with a
  lightweight process that does not burden participants with too much
  red tape", so something like "When the first paragraph of the
  message looks like an entry in the Release Notes, it is used as
  such", as he thought that the Release Notes style was "distinct
  enough" as to "not require any further marking".

  As Junio's patch was then merged, it's now
  [officially possible to write a short description](https://github.com/git/git/blob/v2.45.0-rc1/Documentation/SubmittingPatches#L462-L472)
  in patches or cover letters. This description might then be used
  as-is in the "What's cooking in git.git" emails and in the release
  notes.

<!---
### Reviews
-->

<!---
### Support
-->

<!---
## Developer Spotlight:
-->

## Other News

__Various__

* [Highlights from Git 2.45](https://github.blog/2024-04-29-highlights-from-git-2-45/)
  by Taylor Blau on GitHub Blog.
* [What’s new in Git 2.45.0?](https://about.gitlab.com/blog/2024/04/30/whats-new-in-git-2-45-0/)
  by Patrick Steinhardt on GitLab Blog.
* Adam Johnson’s book “Boost Your Git DX”
  [has been updated](https://adamj.eu/tech/2024/04/04/bygdx-update/) with ten
  new pages of content. This book was mentioned in
  [Git Rev News Edition #104](https://git.github.io/rev_news/2023/10/31/edition-104/).

__Light reading__

* Julia Evans continues her series of blog posts about Git, preparing for a new Git zine,
  with [Notes on git's error messages](https://jvns.ca/blog/2024/04/10/notes-on-git-error-messages/).
  There is also [Some Git poll results](https://jvns.ca/blog/2024/03/28/git-poll-results/)
  (which are, as admitted by the author, highly unscientific, and might not be representative).
  The first entry in this series of blog posts can be found in [Git Rev News Edition #103](https://git.github.io/rev_news/2023/09/30/edition-103/),
  and it continues since, edition after edition so far.
* [Modern Git Commands and Features You Should Be Using](https://martinheinz.dev/blog/109)
  by Martin Heinz on his blog.  The list includes: `git switch`, `git restore`,
  `git sparse-checkout`, `git worktree`, and (not new) `git bisect`.
* [Learn Git Fundamentals – A Handbook on Day-to-Day Development Tasks](https://www.freecodecamp.org/news/learn-git-basics/)
  by Samyak Jain on freeCodeCamp.
* [Navigating the Stormy Waters of Git Merge Conflicts: A Guide for basic git conflicts](https://dev.to/kadea-academy/navigating-the-stormy-waters-of-git-merge-conflicts-a-complete-guide-38n9)
  by Jomagene for KADEA ACADEMY on DEV\.to.
* [The guide to Git I never had.](https://glasskube.dev/guides/git/)
  under Philip Miglinci byline, as Glasskube's guide to Git
  (also [on DEV\.to](https://dev.to/glasskube/the-guide-to-git-i-never-had-1450),
  by Jake Page for Glasskube).
* [How to get somebody fired using Git](https://dev.to/mauroaccorinti/how-to-get-somebody-fired-using-git-31if)
  (or: how to NOT use Git), by Mauro Accorinti on DEV\.to.
* [What Happens on GitLab When You do git push?](https://nanmu.me/en/posts/2022/what-happens-on-gitlab-when-you-do-git-push/)
  by Li Zhennan, on personal blog.
* [Radicle: peer-to-peer collaboration with Git](https://lwn.net/Articles/966869/)
  article by Lars Wirzenius on LWN\.net.
    * [Radicle](https://radicle.xyz/) was first mentioned in [Git Rev News Edition #49](https://git.github.io/rev_news/2019/03/20/edition-49/), then in [Edition #70](https://git.github.io/rev_news/2020/12/26/edition-70/).
      There was also an [article about Radicle from The New Stack](https://thenewstack.io/radicle-a-decentralized-alternative-to-github-for-web3/)
      in [Git Rev News Edition #86](https://git.github.io/rev_news/2022/04/30/edition-86/).
    * Compare with [ForgeFed](https://notabug.org/peers/forgefed) (formerly GitPub),
      a federation protocol for software forges, mentioned in [Git Rev News Edition #69](https://git.github.io/rev_news/2020/11/27/edition-69/).
    * There is also [Gitstr](https://github.com/fiatjaf/gitstr), a tool to send and receive Git patches
      over [Nostr](https://nostr.com/), using [NIP-34](https://github.com/nostr-protocol/nips/pull/997)
      (mentioned in [Git Rev News Edition #109](https://git.github.io/rev_news/2024/03/31/edition-109/)),
      and [git-ssb](https://scuttlebot.io/apis/community/git-ssb.html)
      (see the [git-ssb-intro](https://github.com/hackergrrl/git-ssb-intro) guide):
      decentralized Git repo hosting and issue tracking on [Secure-ScuttleButt (SSB)](https://www.scuttlebutt.nz/)
      (mentioned in [Git Rev News Edition #26](https://git.github.io/rev_news/2017/04/19/edition-26/)
      and [#40](https://git.github.io/rev_news/2018/06/20/edition-40/)).
* [Git as debugging tool](https://lucasoshiro.github.io/posts-en/2023-02-13-git-debug/)
  by Lucas Seiki Oshiro on his GitHub Pages-powered personal blog (2023).


__Easy watching__

* [re:bass](https://www.youtube.com/watch?v=S9Do2p4PwtE) by Dylan Beattie [4:34].
  If Git was music, what would it sound like? 
  An original composition inspired by the Git version control system.


__Git tools and sites__

* [git-bisect-find](https://gitlab.com/kevincox/git-bisect-find) is
  a simple command to find where to start your bisection.  Written in Rust.
    * See also [Announcing git bisect-find](https://kevincox.ca/2024/04/19/git-bisect-find/)
      by Kevin Cox on his blog.
* [git-cz](https://github.com/streamich/git-cz) is a command-line tool
  to help you make semantic Git commits.  Written in JavaScript for Node.js.
  Can be installed standalone, or with [Commitizen](https://commitizen-tools.github.io/commitizen/)
  (which was mentioned in [Git Rev News Edition #72](https://git.github.io/rev_news/2021/02/27/edition-72/)).
  Has non-interactive mode; is configurable (for example turning off emoji).
* [Ydiff](https://github.com/ymattw/ydiff) is a term based tool
  to view _colored, incremental diff_ in a version controlled workspace
  (supports Git, Mercurial, Perforce and Subversion so far)
  or from stdin, with _side by side_ (similar to `diff -y`) and _auto pager_ support.
  Written in Python.  (There also exists the outdated [cdiff](https://github.com/amigrave/cdiff) fork of it.)
* [gws](https://github.com/StreakyCobra/gws) is a text user-interface colorful helper
  to manage workspaces composed of Git repositories.  Written in bash.
* [Giftless](https://giftless.datopian.com/) ([GitHub repo](https://github.com/datopian/giftless))
  is a Python implementation of a [Git LFS](https://git-lfs.com/) Server.
  It is designed with flexibility in mind, to allow pluggable storage backends,
  transfer methods and authentication methods.
* [Gil](https://github.com/chronoxor/gil) (git links tool) is a tool to manage
  complex recursive repository dependencies with cross references and cycles.
  This tool provides a solution to the _git recursive submodules dependency_ problem.
  Written in Python.
* [git-subrepo](https://github.com/ingydotnet/git-subrepo) "clones" an external git repo
  into a subdirectory of your repo.  It is an alternative to `git submodule` and `git subtree`.
  The subrepo history is _squashed_ into a single commit that contains the reference information.
  Recommended as replacement for the (no longer maintained) [Git STree](https://deliciousinsights.github.io/git-stree/)
  project.
* [tomono](https://github.com/hraban/tomono): Multi- to Monorepo Migration,
  is a script that merges multiple independent tiny repositories into a single “[monorepo](https://monorepo.tools/)”.
  Every original repo is moved into its own subdirectory, branches with the same name are all merged.
    * Can be considered the reverse of [splitsh/lite](https://github.com/splitsh/lite) tool, whose goal is
      to make splitting a monolithic repository to read-only standalone repositories easy and fast
      (mentioned in [Git Rev News: Edition #16](https://git.github.io/rev_news/2016/06/15/edition-16/)).
* [Gitdm](https://github.com/npalix/gitdm) (the "git data miner")
  is the tool that Greg KH and Jonathan Corbet have used
  to create statistics on where kernel patches come from.
  Written in Python.  Original at git://git.lwn.net/gitdm.git
* [lolcommits](https://github.com/lolcommits/lolcommits): git-based selfies for software developers.
  lolcommits takes a snapshot with your webcam every time you git commit code,
  and archives a lolcat style image with it (image with embedded caption).
  Written in Ruby, requires a webcam and ImageMagick installed.
  See also [Lolcommits from around the world!](https://github.com/lolcommits/lolcommits/wiki/Lolcommits-from-around-the-world%21)
  page on the project Wiki.
* [Steve's Jujutsu Tutorial](https://steveklabnik.github.io/jujutsu-tutorial/introduction/introduction.html).
    * [Jujutsu (jj)](https://github.com/martinvonz/jj) is a version control system
      first mentioned in [Git Rev News Edition #85](https://git.github.io/rev_news/2022/03/31/edition-85/);
      additionally, links to the [LWN.net article]((https://lwn.net/Articles/958468/)
      and the [Jujutsu: A Git-Compatible VCS](https://www.youtube.com/watch?v=bx_LGilOuE4)
      talk about this version control system at Git Merge 2022 can be found in
      [Git Rev News Edition #107](https://git.github.io/rev_news/2024/01/31/edition-107/).
* [Awesome Git](https://github.com/dictcp/awesome-git)
  is a curated list of amazingly awesome Git tools, resources and shiny things.
* [Awesome Git Hooks](https://github.com/compscilauren/awesome-git-hooks)
  is a curated list of easy-to-use git hooks for automating tasks during git workflows.


## Releases

+ Git [2.45.0-rc1](https://public-inbox.org/git/xmqq4jbqzo3j.fsf@gitster.g/),
[2.45.0-rc0](https://public-inbox.org/git/xmqqcyqljmuu.fsf@gitster.g/)
+ Git for Windows [2.45.0-rc1(1)](https://github.com/git-for-windows/git/releases/tag/v2.45.0-rc1.windows.1),
[2.45.0-rc0(1)](https://github.com/git-for-windows/git/releases/tag/v2.45.0-rc0.windows.1)
+ GitHub Enterprise [3.12.2](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.2),
[3.11.8](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.8),
[3.10.10](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.10),
[3.9.13](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.13)
+ GitLab [16.11.1, 16.10.4, 16.9.6](https://about.gitlab.com/releases/2024/04/24/patch-release-gitlab-16-11-1-released/),
[16.11](https://about.gitlab.com/releases/2024/04/18/gitlab-16-11-released/),
[16.10.3, 16.9.5, 16.8.7](https://about.gitlab.com/releases/2024/04/15/gitlab-16-10-3-released/),
[16.10.2, 16.9.4, 16.8.6](https://about.gitlab.com/releases/2024/04/10/patch-release-gitlab-16-10-2-released/)
+ Gerrit Code Review [3.8.5](https://www.gerritcodereview.com/3.8.html#385),
[3.9.3](https://www.gerritcodereview.com/3.9.html#393),
[3.9.4](https://www.gerritcodereview.com/3.9.html#394)
+ GitHub Desktop [3.3.14](https://desktop.github.com/release-notes/),
[3.3.13](https://desktop.github.com/release-notes/)
+ tig [2.5.9](https://github.com/jonas/tig/releases/tag/tig-2.5.9)
+ git-credential-oauth [0.11.2](https://github.com/hickford/git-credential-oauth/releases/tag/v0.11.2)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Junio Hamano and Adam Johnson.
