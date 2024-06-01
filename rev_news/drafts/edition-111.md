---
title: Git Rev News Edition 111 (May 31st, 2024)
layout: default
date: 2024-05-31 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 111 (May 31st, 2024)

Welcome to the 111th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of April and May 2024.

## Discussions

### General

* [[GSoC] Welcoming our 2024 contributors and thanking our applicants](https://public-inbox.org/git/406aa31f-4ea0-496c-aeb6-443be86385c0@gmail.com/)

  The Git project was accepted in the
  [Google Summer of Code (GSoC)](https://summerofcode.withgoogle.com/)
  this year again, and 3 applicants were selected:

  - Jialuo She will work on the
    ["Implement consistency check for refs" project](https://summerofcode.withgoogle.com/programs/2024/projects/ukm4PTEF)
    mentored by Karthik Nayak and Patrick Steinhardt. He already
    started posting on [his blog](https://luolibrary.com/categories/GSoC-2024/),
    and will push his work to his [Git repo](https://github.com/shejialuo/git).

  - Ghanshyam Thakkar will work on the
    ["Move existing tests to a unit testing framework" project](https://summerofcode.withgoogle.com/programs/2024/projects/e9C4rhrv)
    mentored by Kaartic Sivaraam and Christian Couder. He already
    started posting on [his blog](https://spectre10.github.io/posts/),
    and will push his work to his [Git repo](https://github.com/spectre10/git).

  - Chandra Pratap will work on the
    ["Move and improve reftable tests in the unit testing framework" project](https://summerofcode.withgoogle.com/programs/2024/projects/tlh611d7)
    mentored by Patrick Steinhardt and Christian Couder. He already
    started posting on [his blog](https://chand-ra.github.io/),
    and will push his work to his [Git repo](https://github.com/Chand-ra/git).

  Congratulations to them, and thanks a lot to all the applicants who
  worked on Git and submitted proposals! It was tough to choose from
  multiple potential contributors, all of them good in their own
  respect.

* [Git Merge conference](https://public-inbox.org/git/Zj0JyL1b+g1G3zWx@nand.local/) and Contributor's Summit

  Taylor Blau from GitHub announced that Git Merge 2024 is happening
  in-person on September 19th and 20th in Berlin. It is being co-hosted
  by GitHub and [GitButler](https://gitbutler.com/).

  The talks are scheduled on September 19th and the birds of a feather
  are scheduled on September 20th. Registration is yet to open.

  The announcement welcomes calls for proposals, ideas on the format,
  topics for discussions, venue setup, and applications for financial
  assistance.

### Reviews

+ [[PATCH 0/3] color: add support for 12-bit RGB colors](https://lore.kernel.org/git/20240429164849.78509-1-dev+git@drbeat.li/)

  Beat Bolli sent a patch series consisting of 3 patches to add 12 bit RGB
  color support to the color parsing code. That code is used
  especially when parsing configuration files, as
  [a lot of configuration options](https://git-scm.com/docs/git-config#Documentation/git-config.txt-coloradvice)
  allow users to customize how Git colorizes its output.

  Before Beat's patch series, the code supported the following:
    - fixed strings, like `normal`, `blue`, `red`, etc,
	- 256-color-modes from the terminal, like `[1;38;5;254;48;5;255m` , and
	- 24-bit color values in the form `#RRGGBB`.

  With Beat's patch, it also supports 12-bit colors in the form
  `#RGB`, where in both the 24-bit and 12-bit forms, `R`, `G` and `B`
  are hexadecimal digits for the red, green and blue components of the
  color respectively.

  The first patch in the series fixed a typo. The second patch added
  tests for invalid non-hexadecimal characters in `#RRGGBB`
  values.

  The last patch added support for the `#RGB` form and mentioned in
  its commit message that such a shortened 12 bit form is already
  supported in Cascading Style Sheets (CSS). When used in CSS, each of
  the hexadecimal digits in this form is duplicated to convert the
  color to 24 bits, and the same duplication is performed in Beat's
  patch. For example `#f1b` specifies the same color as `#ff11bb`.

  Junio Hamano, the Git maintainer, replied to Beat's third patch
  saying that it looked good. Junio noticed that a wrong `#0xFF0000`
  value in a code comment was converted to the right `#FF0000` value
  by removing `Ox`. He wondered if there were instances of the same
  mistake in our documentation. Beat replied that it was the only
  place he found such a mistake.

  Taylor Blau then reviewed the patch series and said it looked "very
  nice". Jeff King, alias Peff, also reviewed Beat's series and
  commented on the third patch. Looking at the tests that checked the
  rejection of invalid values, Peff wondered what would happen if
  values like "#1", "#12", "#1234" were passed. Junio replied to Peff
  that such values would be worth covering in the tests but doing that
  in a separate cleanup patch outside this series would be fine.

  Then Junio replied to himself and suggested adding such tests in the
  second patch of the series which already added tests for invalid
  values. Junio even sent a 'fixup!' patch to add these tests to the
  second patch. Peff replied that this 'fixup!' patch looked good.

  Beat then sent a
  [version 2 of his series](https://lore.kernel.org/git/20240502110331.6347-1-dev+git@drbeat.li/)
  that incorporated Junio's patch. Both Junio and Peff approved of it,
  so it was later merged into the 'master' branch.

<!---
### Support
-->

## Developer Spotlight: Beat Bolli

* Who are you and what do you do?

  I'm a software engineer currently working in an Integration Engineer role
  for the Swiss government. When I'm not coding, I read, ride any of my three
  bikes or play the guitar or electric bass.

* What would you name your most important contribution to Git?

  I'm more a drive-by contributor. There are no big issues that I work on.
  For example, my very first commit was "just" a spelling correction.

  The biggest contribution in terms of the number of commits was a cleanup of
  the test scripts that eliminated redundant processes in long pipelines.

  Other topics that come to mind are the strict ISO date format, the
  "copy commit reference" menu item in [gitk](https://git-scm.com/docs/gitk),
  and some cleanups to get a warning-free compile with `-pedantic`.

* What are you doing on the Git project these days, and why?

  As explained in the previous answer, I mostly see small things that I try
  to improve, like [recently adding the 12-bit RGB color format](#reviews).

* If you could get a team of expert developers to work full time on
  something in Git for a full year, what would it be?

  Honestly, I'm pretty content with the state of Git. I've been using Git since
  2009 and I guess I got used to its idiosyncrasies (but see the next question!).

* If you could remove something from Git without worrying about
  backwards compatibility, what would it be?

  There are too many different options and/or subcommands to remove things.
  Compare `git remote remove`, `git branch (-d/-D)`, `git rm` (for files).
  I understand that these are different situations but from time to time I
  have to really think about which is the right syntax in a given case.

* What is your favorite Git-related tool/library, outside of
  Git itself?

  First, I'm a fan of the command line, so Git itself does over 80% of what
  I need. Next up are [tig](https://jonas.github.io/tig/) and [vim-fugitive](https://github.com/tpope/vim-fugitive).
  I also use a comprehensive set of Git-related shell aliases that improve
  my efficiency.

* Do you happen to have any memorable experience w.r.t. contributing to
  the Git project? If yes, could you share it with us?

  Nothing out of the ordinary, but then I'm old-school and have no problems
  with an email-based workflow. My first commits were accepted without much
  fanfare, and this encouraged me to continue to submit things.

* What is your toolbox for interacting with the mailing list and for
  development of Git?

  I follow the mailing list on [lore.kernel.org](https://lore.kernel.org/git/), and
  have also subscribed to the NNTP feed in Thunderbird. For submitting patches I
  have configured a few send-email options, probably like everyone else who
  contributes. I do most of my development on a Mac mini in [iTerm2](https://iterm2.com/)
  and Vim.

* What is your advice for people who want to start Git development?
  Where and how should they start?

  First, don't think you're not good enough. By following [SubmittingPatches](https://git-scm.com/docs/SubmittingPatches)
  and the rest of the [beginner's documentation](https://git-scm.com/docs/MyFirstContribution),
  everyone can contribute. I experience the "mood" on the mailing list as very
  supportive and helpful.

* If there's one tip you would like to share with other Git
  developers, what would it be?

  Just a tiny pet peeve of mine: `sizeof` is not a function 😉


## Other News

__Various__

+ [Securing Git: Addressing 5 new vulnerabilities](https://github.blog/2024-05-14-securing-git-addressing-5-new-vulnerabilities/)
  fixed in v2.45.1, by Johannes Schindelin on GitHub Blog.
  The main theme of fixes in v2.45.1 is to improve the security of cloning Git repositories.


__Light reading__

+ [A beginner's guide to the Git reftable format](https://about.gitlab.com/blog/2024/05/30/a-beginners-guide-to-the-git-reftable-format/)
  (available since the [release of Git 2.45.0](https://about.gitlab.com/blog/2024/04/30/whats-new-in-git-2-45-0/)).
  Article by Patrick Steinhardt on GitLab Blog.
+ Julia Evans has just published her new Git zine, “[How Git Works](https://wizardzines.com/zines/git/)”.
  She [counted](https://fosstodon.org/@b0rk@jvns.ca/112519150131306917)
  that she apparently wrote 28,000 words of blog posts while writing the zine.
  These posts were covered here, starting from [Git Rev News Edition #103](https://git.github.io/rev_news/2023/09/30/edition-103/),
  and continuing, edition after edition, until [the previous edition #110](https://git.github.io/rev_news/2024/04/30/edition-110/).<br>
  As a companion to this zine, there is a little [git cheat sheet](https://wizardzines.com/git-cheat-sheet.pdf) (PDF) freely available.
    + Julia Evans had also published the “[Oh Shit, Git](https://wizardzines.com/zines/oh-shit-git/)” zine in 2018;
      as she [describes](https://fosstodon.org/@b0rk@jvns.ca/112338598244430472):
      “Oh Shit, Git” is about how to get out of Git messes, while
      “How Git Works” explains why those messes happen in the first place.
    + The [Oh Shit, Git!?!](http://ohshitgit.com/) website by Katie Sylor-Miller
      was first mentioned in [Git Rev News Edition #19](https://git.github.io/rev_news/2016/09/14/edition-19/).
+ [Securing Git repositories with gittuf](https://lwn.net/Articles/972467/)
  by Joe Brockmeier on LWN\.net is a report of a talk by Aditya Sirish A Yelgundhalli and Billy Lynch
  at Open Source Summit North America (OSSNA).
  The video of the talk [is available on YouTube](https://www.youtube.com/watch?v=eCSeIEdMbCw).
  [Gittuf](https://gittuf.dev/) was mentioned
  in [Git Rev News Edition #104](https://git.github.io/rev_news/2023/10/31/edition-104/).
+ [Clone arbitrary single Git commit](https://blog.hartwork.org/posts/clone-arbitrary-single-git-commit/)
  by Sebastian Pipping on Hartwork Blog.  Inspired by GitHub Action [`actions/checkout`](https://github.com/actions/checkout).
+ [Reverting File Changes in Git: A Comprehensive Guide](https://dev.to/mochafreddo/reverting-file-changes-in-git-a-comprehensive-guide-80i)
  by Geoffrey Kim on DEV\.to.
+ [What is Git? GitHub beginner’s guide to version control](https://github.blog/2024-05-27-what-is-git-our-beginners-guide-to-version-control/)
  by Kedasha Kerr on GitHub Blog.
+ [Signed Git commits with Sigstore, Gitsign and OpenID Connect (OIDC)](https://buildkite.com/blog/securing-your-software-supply-chain-signed-git-commits-with-oidc-and-sigstore)
  by James Healy on Buildkite Blog.
  [Sigstore](https://www.sigstore.dev/) and [Gitsign](https://github.com/sigstore/gitsign)
  tools for keyless Git signing were both mentioned
  in [Git Rev News Edition #91](https://git.github.io/rev_news/2022/09/30/edition-91/).
+ [Understanding the Stacked Pull Requests Workflow](https://www.git-tower.com/blog/stacked-prs/) by Bruno Brito on Tower's blog.
    There have been various approaches to adding stacks to Git workflows:
    + [Stacked Git](https://stacked-git.github.io/) (aka StGit) was mentioned in
      [Git Rev News Edition #17](https://git.github.io/rev_news/2016/07/20/edition-17/),
      [#21](https://git.github.io/rev_news/2016/11/16/edition-21/),
      and [#74](https://git.github.io/rev_news/2021/04/30/edition-74/),
      and finally presented as a tool in [#93](https://git.github.io/rev_news/2022/11/30/edition-93/).
    + Stacked diffs were discussed in [Stacked Diffs Versus Pull Requests](https://jg.gg/2018/09/29/stacked-diffs-versus-pull-requests/)
      (mentioned in [Git Rev News Edition #44](https://git.github.io/rev_news/2018/10/24/edition-44/))
      and [Stacked Diffs (and why you should know about them)](https://newsletter.pragmaticengineer.com/p/stacked-diffs) (mentioned
      in [#105](https://git.github.io/rev_news/2023/11/30/edition-105/)).
    + [Working with stacked branches](https://andrewlock.net/working-with-stacked-branches-in-git-is-easier-with-update-refs/)
      was mentioned in [Git Rev News Edition #93](https://git.github.io/rev_news/2022/11/30/edition-93/).
+ [How short can Git abbreviate?](https://blog.cuviper.com/2013/11/10/how-short-can-git-abbreviate/)
  by Josh Stone on his WordPress-based blog (2013).


__Easy watching__

+ [Securing Git Repositories with Gittuf](https://www.youtube.com/watch?v=eCSeIEdMbCw) -
  Aditya Sirish A Yelgundhalli, New York University & Billy Lynch, Chainguard.
  A 30 minute long video on The Linux Foundation channel on YouTube.


__Git tools and sites__

+ [KSDB](https://lwn.net/ksdb/) is the LWN\.net kernel source database, a site
  which can answer a wide range of questions about the Linux kernel's development history.
+ The [Kernel.org Transparency Log Monitor](https://tlog.linderud.dev/)
  webpage is a monitor of the kernel.org transparency log for git-receive operations.
  Among others, it tracks signed pushes (compare with [gittuf](https://gittuf.dev/)).
  Runs [kernel.org-git-verifier](https://github.com/Foxboron/kernel.org-git-verifier).
    + There is also the [Gitolite transparency log](https://korg.docs.kernel.org/gitolite/transparency-log.html),
      with git-receive operations published at the [transparency-logs/gitolite/git](https://git.kernel.org/pub/scm/infra/transparency-logs/gitolite/git/)
      repositories in [the public-inbox v2 format](https://public-inbox.org/public-inbox-v2-format.html).
      [Gitolite](http://gitolite.com/gitolite/) was first mentioned in
      [Git Rev News Edition #17](https://git.github.io/rev_news/2016/07/20/edition-17/)
      and [#22](https://git.github.io/rev_news/2016/12/14/edition-22/).
+ [Sigstore Rekor](https://github.com/sigstore/rekor) is meant to
  provide an immutable tamper resistant ledger of metadata
  generated within a software project's supply chain.
  It enables software maintainers and build systems to record and query
  signed metadata.
  Can be run as part of [Sigstore](https://sigstore.dev/) or on its own.
+ [Quickhook](https://github.com/dirk/quickhook/) is a Git hook runner designed for speed.
  Written in Go.
+ [etckeeper](https://etckeeper.branchable.com/) is a collection of tools
  to let `/etc` be stored in a Git repository, and use Git
  to review or revert changes that were made to `/etc`.
  Written as shell scripts (with some plugins in Python).
+ [Dangit, Git!?!](https://dangitgit.com/en) has the same contents, only without swears,
  as the [Oh Shit, Git!?!](https://ohshitgit.com/) website
  (first mentioned in [Git Rev News Edition #19](https://git.github.io/rev_news/2016/09/14/edition-19/)).


## Releases

+ Git [2.45.1 and friends](https://public-inbox.org/git/xmqqv83g4937.fsf@gitster.g/)
  (2.44.1, 2.43.4, 2.42.2, 2.41.1, 2.40.2, and 2.39.4)
+ Git for Windows [2.45.1(1)](https://github.com/git-for-windows/git/releases/tag/v2.45.1.windows.1)
+ libgit2 [1.8.1](https://github.com/libgit2/libgit2/releases/tag/v1.8.1)
+ GitLab [17.0.1, 16.11.3, 16.10.6](https://about.gitlab.com/releases/2024/05/22/patch-release-gitlab-17-0-1-released/),
[17.0](https://about.gitlab.com/releases/2024/05/16/gitlab-17-0-released/),
[16.9.8](https://about.gitlab.com/releases/2024/05/09/gitlab-16-9-8-released/),
[16.11.2, 16.10.5, 16.9.7](https://about.gitlab.com/releases/2024/05/08/patch-release-gitlab-16-11-2-released/)
+ Gerrit Code Review [3.10.0](https://www.gerritcodereview.com/3.10.html#3100),
[3.7.9](https://www.gerritcodereview.com/3.7.html#379),
[3.8.6](https://www.gerritcodereview.com/3.8.html#386),
[3.9.5](https://www.gerritcodereview.com/3.9.html#395)
+ GitHub Enterprise [3.12.4](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.4),
[3.11.10](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.10),
[3.10.12](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.12),
[3.9.15](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.15),
[3.13.0](https://help.github.com/enterprise-server@3.13/admin/release-notes#3.13.0),
[3.12.3](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.3),
[3.11.9](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.9),
[3.10.11](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.11),
[3.9.14](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.14)
+ GitKraken [10.0.1](https://help.gitkraken.com/gitkraken-client/current/),
[10.0.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.4.0](https://desktop.github.com/release-notes/),
[3.3.18](https://desktop.github.com/release-notes/),
[3.3.17](https://desktop.github.com/release-notes/),
[3.3.16](https://desktop.github.com/release-notes/),
[3.3.15](https://desktop.github.com/release-notes/)
+ TortoiseGit [2.16.0](https://tortoisegit.org/download/)
+ Git Cola [4.7.1](https://github.com/git-cola/git-cola/releases/tag/v4.7.1)
+ Garden [1.5.0](https://github.com/garden-rs/garden/releases/tag/v1.5.0)
+ Tower for Mac [11.0](https://www.git-tower.com/release-notes/windows?show_tab=release-notes) ([blog post](https://www.git-tower.com/blog/tower-mac-11/))
+ Tower for Windows [7.0](https://www.git-tower.com/release-notes/windows?show_tab=release-notes)
+ tig [2.5.10](https://github.com/jonas/tig/releases/tag/tig-2.5.10)
+ git-credential-oauth [0.11.3](https://github.com/hickford/git-credential-oauth/releases/tag/v0.11.3)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Sven Strickroth, David Aguilar and
Bruno Brito.
