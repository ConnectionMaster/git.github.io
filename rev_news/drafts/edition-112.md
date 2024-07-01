---
title: Git Rev News Edition 112 (June 30th, 2024)
layout: default
date: 2024-06-30 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 112 (June 30th, 2024)

Welcome to the 112th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of May and June 2024.

## Discussions

<!---
### General
-->

### Reviews

* [[RFC PATCH] docs: document upcoming breaking changes](https://lore.kernel.org/git/fc1a9fa03de7330f79dc56b0f2712834cb236b5a.1715070296.git.ps@pks.im/)

  Patrick Steinhardt sent an RFC patch to the mailing list that
  created a new "UpcomingBreakingChanges.md" document. The goal of the
  document was to inform users and developers of deprecations and
  breaking changes, and to encourage discussion of the direction of
  the project regarding these topics in advance.

  Patrick noted that the changes listed in the document, along with
  links to mailing list threads where they had been discussed, were a
  work in progress with controversial and missing items, and that he
  didn't want to push for a Git 3.0 release with the listed changes
  soon.

  The idea for that new document had been discussed previously
  [in a thread about a patch series from Patrick](https://lore.kernel.org/git/ZjiL7vu5kCVwpsLd@tanuki/)
  that introduced subcommands like `get`, `set`, etc, in `git config`.
  In that thread, after Patrick asked if we wanted to introduce a
  document to keep track of upcoming removals for a potential Git 3.0
  release, Junio Hamano, the Git maintainer, replied to Patrick that
  in a few of his ["What's cooking" emails](https://lore.kernel.org/git/?q=s%3A%22What%27s+cooking+in+git.git%22)
  before the Git 2.44.0 release, he wrote:

  > It may not be a bad idea to reflect on what technical debt and UI
  > warts we have accumulated so far to see if we have enough of them to
  > start planning for a breaking Git 3.0 release (or, of course, keep
  > incrementally improve the system, which is much more preferable --
  > continuity and stability is good).

  So Junio was happy that "somebody has bit it ;-)" and suggested a
  number of topics that could be added to the document Patrick wanted
  to create. This started a discussion about the possibility of
  deprecating some features, such as the `restore`, `switch`,
  `submodules` and `worktrees` subcommands.

  In the RFC patch to add the document, Patrick mentioned some of the
  topics suggested by Junio, but not others that seemed controversial
  in the previous discussion.

  Johannes Schindelin, alias Dscho, replied to Patrick's RFC patch
  saying he loved it. Dscho also gave his opinion about the topics,
  and suggested to deprecate or remove additional rarely used
  features.

  Junio replied to Patrick's patch suggesting to add features that we
  don't want to drop and why, and to mention that we deprecate but,
  for backward compatibility, rarely remove old ways to do things.
  Patrick agreed to Junio's suggestion and proposed a "superseded"
  section for the features we don't want to drop.

  Dragan Simic, who participated in the previous discussions in the
  `git config` thread, repeated that he didn't want to see any of
  `git restore`, `git switch` or `git checkout` deprecated, which
  Patrick agreed shouldn't be done.

  Phillip Wood, replying to Patrick's patch, asked if the document
  should track the progress of some unfinished work, like the config
  based hooks implementation, but Patrick said he was planning on
  creating a separate document for long running projects, projects
  already discussed and perhaps also small or micro projects to help
  newcomers looking for something to work on too.

  Justin Tobler also replied to Patrick's patch suggesting adding the
  removal of double dot and triple dot syntax (".." and "...") from
  `git diff` to the document. This was discussed by Junio and Patrick
  but, as it would need a lot more work, Patrick decided to not add it
  to the document for now.

  Patrick then sent a
  [version 2 of his patch](https://lore.kernel.org/git/2ef53ff98b12fe9373a15ec3a795235f040d9049.1715667067.git.ps@pks.im/)
  adding a section about features "that are _not_ to be
  deprecated" and proposing some further deprecations, while withdrawing
  the $GITDIR/hooks directory deprecation proposal.

  Karthik Nayak replied to the version 2 patch, listing a number of
  commands not mentioned in the document that do similar things, which
  might indicate that some of them could be deprecated too. Patrick,
  Junio and Dragan discussed these commands, but decided that only
  `git pickaxe`, which is an alias for `git blame`, could be removed
  for now.

  So Patrick sent a
  [version 3 of his patch](https://lore.kernel.org/git/84c01f1b0a2d24d7de912606f548623601c0d715.1716555034.git.ps@pks.im/)
  which only added the removal of `git pickaxe`.

  Junio replied to this version 3 with a lot of comments to discuss
  how each item was justified and how we could improve on justifying
  items in general. Patrick then agreed on ways to improve the
  document.

  Patrick sent a
  [version 4](https://lore.kernel.org/git/cover.1717141598.git.ps@pks.im/)
  where the single patch had been broken down into 4 patches. In the
  process a lot of the proposed deprecations from the previous version
  were removed and the document name was changed from
  "UpcomingBreakingChanges.md" to "BreakingChanges.md" as some changes
  listed in the "Superseded features that will not be deprecated"
  section should not be considered upcoming.

  The goal was to introduce the document in a skeletal form in the
  first patch and then add only one item to each of the three sections
  in the following patches. This way each of the last 3 patches should
  be an example of how other items should later be added to the
  document.

  Junio, Patrick and Todd Zullinger then discussed relatively small
  improvements to the form and content of the document.

  Patrick sent a
  [version 5 of the patch series](https://lore.kernel.org/git/cover.1717402497.git.ps@pks.im/)
  where the main change was that the document was converted to
  AsciiDoc instead of Markdown and renamed from "BreakingChanges.md"
  to "BreakingChanges.txt" for format compatibility with most other
  documents in the codebase.

  Junio, Phillip Wood and Patrick discussed other small improvements
  which Patrick integrated into the
  [version 6 of the patch series](https://lore.kernel.org/git/cover.1717504292.git.ps@pks.im/).

  Junio then suggested a few more small improvements which Patrick
  integrated into the
  [version 7 of the patch series](https://lore.kernel.org/git/cover.1718345026.git.ps@pks.im/)
  which was later merged into the 'master' branch.

<!---
### Support
-->

<!---
## Developer Spotlight:
-->

## Other News

__Various__


__Light reading__

* [BitKeeper, Linux, and licensing disputes: How Linus wrote Git in 14 days](https://graphite.dev/blog/bitkeeper-linux-story-of-git-creation)
  by Nicholas Yan on Graphite Blog.
  See also, among others, [GitHistory page in the archives of Git SCM Wiki](https://archive.kernel.org/oldwiki/git.wiki.kernel.org/index.php/GitHistory.html),
  which was mentioned in [Git Rev News Edition #105](https://git.github.io/rev_news/2023/11/30/edition-105/),
  and other links that were mentioned in that edition.
* [Git Workflows for API Technical Writers](https://bump.sh/blog/git-workflows-for-api-technical-writers)
  by James Higginbotham on Bump\.sh.
  Mentions [Bump.sh](https://bump.sh/), an API doc platform for tech writers and engineers,
  at the end of the article.
* [What is Git? Our beginner’s guide to version control](https://github.blog/2024-05-27-what-is-git-our-beginners-guide-to-version-control/) and
  [Top 12 Git commands every developer must know](https://github.blog/2024-06-10-top-12-git-commands-every-developer-must-know/)
  by Kedasha Kerr on GitHub Blog.  This blog post accompanies the
  [GitHub for Beginners](https://youtube.com/playlist?list=PL0lo9MOBetEFcp4SCWinBdpml9B2U25-f&feature=shared)
  series (YouTube playlist).
* [Pull Request vs. Merge Request: Essential Differences](https://www.codium.ai/blog/pull-request-vs-merge-request-essential-differences/)
  by CodiumAI Team (with some promotion of their AI tool at the end of the article).
* [Stop Wasting Hours! Git Bisect: Your Ultimate Bug Hunting Tool](https://ionixjunior.dev/en/stop-wasting-hours-git-bisect-your-ultimate-bug-hunting-tool/)
  by Ione Souza Junior on his blog; also available [on DEV.to](https://dev.to/ionixjunior/stop-wasting-hours-git-bisect-your-ultimate-bug-hunting-tool-4ebc)
  as a part of [mastering-git series](https://dev.to/ionixjunior/series/26070).
* [The Magic of Git Stash: How It Saved My Day](https://dev.to/waqaryounis7564/the-magic-of-git-stash-how-it-saved-my-day-119k)
  by waqaryounis7564 on DEV\.to.
* [Prevent Hidden Merge Conflicts](https://dev.to/shinigami92/prevent-hidden-merge-conflicts-2lem)
  by Shinnigami on DEV\.to; but note that the described solutions might warrant some more thought
  (linearizing history by requiring rebase instead of merge to integrate changes
  versus requiring branch to be up to date before merging), and are not the only possible
  solutions (for example: post-merge checks).
* [“Good Commit” vs “Your Commit”: How to Write a Perfect Git Commit Message](https://dev.to/safdarali/good-commit-vs-your-commit-how-to-write-a-perfect-git-commit-message-59ol)
  by Safdar Ali on DEV\.to.
    * Compare the [Conventional Commits](https://www.conventionalcommits.org/) specification,
      first mentioned in [Git Rev News Edition #52](https://git.github.io/rev_news/2019/06/28/edition-52/),
      and [Gitmoji](https://gitmoji.dev/), first mentioned in [Git Rev News Edition #47](https://git.github.io/rev_news/2019/01/23/edition-47/).
* [Ten Things You Didn’t Know Git And GitHub Could Do](https://owenou.com/ten-things-you-didnt-know-git-and-github-could-do/)
  by Owen Ou on Owen Ou's blog (2012).
* [Versioning FreeCAD files with git](https://blog.lambda.cx/posts/freecad-and-git/)
  (FreeCAD files are zip archives containing text documents) by Dante Catalfamo on lambda.cx blog (2021).
* [Programming in Unison](https://lwn.net/Articles/978955/)
  by Daroc Alden on LWN\.net ([free subscriber link](https://lwn.net/SubscriberLink/978955/cd8dffc792b86313/)).
  [Unison](https://www.unison-lang.org/) is an MIT-licensed programming language,
  where programs are stored in an append-only, content-addressed database
  (though still displayed to the user for editing as text, using the editor of their choice)...
  just like information about project versions is stored in Git.

<!---
__Easy watching__
-->

__Git tools and sites__

* [setuptools-scm](https://github.com/pypa/setuptools_scm)
  is a tool that extracts Python package versions from `git` or `hg` metadata
  instead of declaring them as the version argument or in an SCM managed file.
  Additionally, it provides setuptools with a list of files that are managed by the SCM
  (i.e. it automatically adds all of the SCM-managed files to the sdist).
  Unwanted files must be excluded via `MANIFEST.in`.
  The preferred way to configure setuptools-scm is via `pyproject.toml`.<br>
  The [latest version](https://setuptools-scm.readthedocs.io/en/latest/)
  and the [stable version documentation](https://setuptools-scm.readthedocs.io/en/stable/)
  are available on Read the Docs).
* [`piku`](https://piku.github.io/), which was inspired by [`dokku`](https://dokku.com/),
  allows you to do `git push` deployments to your own servers, no matter how small they are.
  An open source PaaS (Platform as a Service) alternative to services such as Heroku.
  Written in Python.
* [gitchangelog](https://github.com/vaab/gitchangelog) is a tool that
  creates a changelog from git log history.  Written in Python;
  no longer actively developed (version 3.0.4 is from 2018).
    * Compare with for example [git-cliff](https://git-cliff.org/) changelog generator,
      mentioned in [Git Rev News Edition #108](https://git.github.io/rev_news/2024/02/29/edition-108/).
* [git-open-remote](https://github.com/masukomi/masuconfigs/blob/master/bin/git-scripts/git-open-remote)
  is a shell script by [masukomi](https://masukomi.org) to open the web page for the repo's remote(s).
  With this script you can simply cd into a git repo and type `git open-remote`.
  Requires [`open`](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/open.1.html)
  or [`xdg-open`](https://linux.die.net/man/1/xdg-open)
  (aliased or linked to `open`) to open the web browser,
  and [charm gum](https://github.com/charmbracelet/gum)
  to implement the selection UI when the git repo has more than one remote.
* [Git EOL Conversion Diagram](https://gist.github.com/DecimalTurn/3f99a3903366bf9fb2c1f513bd3c5a83) for checkout
  as Gist providing [SVG version](https://raw.githubusercontent.com/gist/DecimalTurn/3f99a3903366bf9fb2c1f513bd3c5a83/raw/d54d0e842c1f22e0b04d7a044dde1489993d87bf/Git-EOL-Conversion-Diagram.svg)
  and [editable version on Mindmup](https://app.mindmup.com/map/_free/2024/06/982eaeb032cf11ef93d0a9d7af4d6195),
  by Martin Leduc (@DecimalTurn).

## Releases

+ Git [2.45.2 and friends to unbreak "git lfs" and others](https://public-inbox.org/git/xmqqr0dheuw5.fsf@gitster.g/)
+ Git for Windows [2.45.2(1)](https://github.com/git-for-windows/git/releases/tag/v2.45.2.windows.1)
+ GitHub Enterprise [3.13.0](https://help.github.com/enterprise-server@3.13/admin/release-notes#3.13.0),
[3.12.5](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.5),
[3.11.11](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.11),
[3.10.13](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.13),
[3.9.16](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.16)
+ GitLab [17.1.1, 17.0.3, 16.11.5](https://about.gitlab.com/releases/2024/06/26/patch-release-gitlab-17-1-1-released/),
[17.1](https://about.gitlab.com/releases/2024/06/20/gitlab-17-1-released/),
[17.0.2, 16.11.4, 16.10.7](https://about.gitlab.com/releases/2024/06/12/patch-release-gitlab-17-0-2-released/)
+ GitKraken [10.0.2](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.4.2](https://desktop.github.com/release-notes/),
[3.4.1](https://desktop.github.com/release-notes/)
+ Tower for Mac 12.0 (BETA) — [Release blog post](https://www.git-tower.com/blog/tower-mac-12/)
+ garden [1.7.0](https://github.com/garden-rs/garden/releases/tag/v1.7.0),
[1.6.0](https://github.com/garden-rs/garden/releases/tag/v1.6.0)
+ git-cola [4.8.0](https://github.com/git-cola/git-cola/releases/tag/v4.8.0)
+ git-credential-oauth [0.12.1](https://github.com/hickford/git-credential-oauth/releases/tag/v0.12.1),
[0.12.0](https://github.com/hickford/git-credential-oauth/releases/tag/v0.12.0)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Bruno Brito, David Aguilar and Dragan Simic.
