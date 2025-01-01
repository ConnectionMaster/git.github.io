---
title: Git Rev News Edition 118 (December 31st, 2024)
layout: default
date: 2024-12-31 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 118 (December 31st, 2024)

Welcome to the 118th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of November and December 2024.

## Discussions

### General

- Git participates in [Outreachy's December 2024 to March 2025 round](https://www.outreachy.org/alums/2024-12/):

  - Seyi Kuforiji is working on the "Convert unit tests to use the
    clar testing framework" project. He is mentored by Patrick
    Steinhardt and Phillip Wood and posting updates [on his gitlab.io blog](https://seyi-kuforiji-902b48.gitlab.io/posts/index.html)
	while his work is on [his GitHub repository](https://github.com/Seyi007/git).

  - Usman Akinyemi is working on the "Finish adding a 'os-version'
    capability to Git protocol v2" project. He is mentored by
    Christian Couder and posting updates [on his hashnode.dev blog](https://uniqueusman.hashnode.dev/)
	while his work is on [his GitLab repository](https://gitlab.com/Unique-Usman/git/-/branches).

  Congratulations to Usman and Seyi for being selected!

  We are still looking for corporate sponsors to fund these two
  Outreachy internship. Thank you in advance for contacting the Git
  PLC (git@sfconservancy.org) if you are interested.

  Many thanks also to the other contributors who applied and worked on
  micro-projects, but couldn’t be selected! We hope to continue to see
  you in the community!

<!---
### Reviews
-->

### Support

+ [./configure fails to link test program due to missing dependencies](https://lore.kernel.org/git/GV1PR02MB848925A79A9DD733848182D58D662@GV1PR02MB8489.eurprd02.prod.outlook.com/)

  Last September Henrik Holst reported an issue when trying to compile
  Git 2.44.0 with HTTPS/curl support on LFS 12.1. The 'configure' script
  failed to detect libcurl's dependencies properly when trying to link
  statically.

  The issue occurred because the 'configure' script only used the
  `-lcurl` build flag without running `pkg-config --libs libcurl` to
  add build flags for dependencies like `zstd` that libcurl
  needs. Henrik found that manually setting the LDFLAGS environment
  variable to include build flags for all dependencies (like `-lcurl
  -lssl -lcrypto -lzstd -lbrotlidec -lz`) allowed the build to
  succeed. This sparked a broader discussion about Git's build system
  situation.

  Looking at 'configure.ac', Junio Hamano, the Git maintainer, noted
  that `pkg-config` isn't used at all, instead `curl-config --libs` is
  used to detect curl's flags. Even if the 'configure' script was
  added early in the history of the Git project, Junio said it was an
  afterthought and nobody has considered "upgrading" from
  `curl-config` to `pkg-config` for dependency detection.

  In fact, our own Jakub Narębski
  [initially added the 'configure' script](https://lore.kernel.org/git/200607030156.50455.jnareb@gmail.com/)
  back in 2006 to make it much easier to create RPM spec file for Git.
  Creating `*.spec` file is especially easy when the
  compilation follows traditional `configure && make && make install`
  steps.

  brian m. carlson replied to Junio that users shouldn't statically
  link libcurl or OpenSSL at all, as this creates security issues.
  With static linking, security updates to these libraries would
  require recompiling Git to take effect. In contrast, dynamic linking
  allows security updates to be applied as soon as a new Git process
  is spawned.

  Patrick Steinhardt replied to Junio suggesting it might be time to
  reconsider Git's three build systems
  ([GNU Make](https://www.gnu.org/software/make/),
  [Autoconf](https://www.gnu.org/software/autoconf/), and
  [CMake](https://cmake.org/)). He proposed potentially dropping
  Autoconf and making CMake officially supported, or switching to
  [Meson](https://mesonbuild.com/) as an alternative.

  CMake was [added more recently in 2020](https://lore.kernel.org/git/pull.614.git.1587700897.gitgitgadget@gmail.com/)
  by Sibi Siddharthan as a third build system with the main goal of
  improving the build experience for developers on Windows.

  Soon after Patrick's reply, the Git Contributors' Summit happened
  and the
  ["Modern Build System" topic](https://lore.kernel.org/git/Zu2E3vIcTzywWOx3@nand.local/)
  was discussed there. Patrick Steinhardt raised concerns about
  maintaining three different build systems while others were
  concerned about having good platform support and good Windows
  developer experience. This led to an extensive discussion about
  the merits of different build systems in the thread started by
  Henrik.

  Eli Schwartz, the Meson maintainer, made a detailed case for
  preferring Meson over CMake, citing various CMake pain points and
  limitations. Phillip Wood agreed with Patrick about getting rid of
  Autoconf, but raised the importance of Visual Studio integration,
  since CMake was originally added to improve the Windows developer
  experience. Johannes Schindelin, alias Dscho, emphasized that
  CMake's deep Visual Studio integration was crucial for Windows
  developers and cautioned against switching to alternatives that
  would make the Windows experience worse. It appeared that Visual
  Studio has Meson support via plugins though, which alleviated some
  concerns.

  Paul Smith, the GNU Make maintainer, noted that requiring additional
  build tools like Meson, which are not yet often used and require
  some other dependencies, like Python3 for Meson, adds friction,
  though he acknowledged that for Git specifically this may be less of
  a concern given its existing dependencies.

  Junio seemed to agree that adding support for a fourth build system
  would be worth it if it would allow the project to drop all other
  three build systems eventually. He said the new build system would
  have "to be something available widely and easy to learn".

  Patrick came up later in October with a
  [21 patch long RFC series](https://lore.kernel.org/git/cover.1727881164.git.ps@pks.im/)
  to add support for the Meson build system with the goal of
  eventually replacing the current three build systems.

  There were a number of iterations on that series. Among the many
  comments, Taylor Blau asked about the eventual goals of the series
  and plans for CMake support. He noted that CMake support in contrib/
  was in an awkward position, neither fully supported nor properly
  maintained out-of-tree. He was concerned about having to maintain
  three build systems simultaneously during any transition period.

  David Aguilar expressed concerns about Python being a dependency
  through Meson. Eli replied that [muon](https://github.com/muon-build/muon),
  a C99 implementation of Meson,
  could be used instead and demonstrated it working with Git's build.

  Jeff King, alias Peff, asked about reliability for bisecting and
  whether out-of-source builds would work correctly when moving
  between commits. He also requested better documentation of common
  developer workflows with Meson compared to Make.

  Junio discussed the need to maintain build system compatibility
  during any transition period. He noted that many of the Makefile
  options were added over time for good reasons and dropping support
  for them would need careful consideration.

  A number of other developers participated in the reviews. Ramsay
  Jones tested the patches on various platforms including
  Cygwin. Phillip Wood reviewed CMake-related changes and provided
  technical feedback. Johannes Sixt commented on changes to the
  gitk-git subtree. Eric Sunshine provided technical feedback. Your
  own Christian Couder provided feedback on the documentation.

  Over the iterations, Patrick updated the series to improve
  documentation, fix conflicts with in-flight patches, and address the
  various technical concerns raised during review.

  Eventually the
  [version 11 of the patch series](https://lore.kernel.org/git/20241206-pks-meson-v11-0-525ed4792b88@pks.im/)
  was merged and will be part of Git v2.48.0 that should be released
  in the next few weeks. It should be a properly supported modern
  build system that can be faster and more easily configurable than
  the three existing ones which will hopefully get deprecated over
  time.

  The merged patch series especially adds
  [some documentation](https://lore.kernel.org/git/20241206-pks-meson-v11-24-525ed4792b88@pks.im/#Z31meson.build)
  (via comments in [`meson.build`](https://git.kernel.org/pub/scm/git/git.git/tree/meson.build))
  to help build Git with Meson and
  [a build system comparison](https://lore.kernel.org/git/20241206-pks-meson-v11-23-525ed4792b88@pks.im/#Z31Documentation:technical:build-systems.txt)
  (in [`Documentation/technical/build-systems.txt`](https://git.kernel.org/pub/scm/git/git.git/tree/Documentation/technical/build-systems.txt))
  that might be interesting to read.


<!---
## Developer Spotlight:
-->

## Other News

__Various__

+ [Git 2.48-rc0 Released With git-fsck Warning Over "Curiously Formatted" Ref Contents](https://www.phoronix.com/news/Git-2.48-rc0)
  by Michael Larabel on Phoronix.
+ [Git Merge 2024 Talks are Up (on YouTube)](https://blog.gitbutler.com/git-merge-2024-talks/)
  by Scott Chacon on GitButler Blog.  The article includes a quick summary
  of each of the talks.
+ [Forgejo makes a full break from Gitea](https://lwn.net/Articles/963095/)
  by Joe Brockmeier on LWN\.net (from February 23, 2024).
    + [Gitea](https://about.gitea.com/), which is Go-based software forge, a fork of [Gogs](https://gogs.io/),
      was first mentioned in [Git Rev News Edition #23](https://git.github.io/rev_news/2017/01/25/edition-23/);<br>
      [Forgejo](https://forgejo.org/), which started as a "soft" fork of Gitea,
      was first mentioned in passing in [Git Rev News Edition #103](https://git.github.io/rev_news/2023/09/30/edition-103/),
      and again in [Edition #114](https://git.github.io/rev_news/2024/08/31/edition-114/).
+ [EMERALDWHALE exploits vulnerable Git configuration files](https://www.developer-tech.com/news/emeraldwhale-exploits-vulnerable-git-configuration-files/)
  by Ryan Daws on Developer Tech News, about a global operation known as EMERALDWHALE,
  which has stolen over 15000 cloud service credentials by exploiting exposed Git configuration files
  (via misconfigured web services, which were exposing `.git` directory of a private repository).
+ [Abusing Git branch names to compromise a PyPI package](https://lwn.net/Articles/1001215/)
  (caused by project automatically processing pull requests with a flawed script),
  short post by daroc on LWN\.net.


__Light reading__

+ [NonStop discussion around adding Rust to Git](https://lwn.net/Articles/998115/)
  by Daroc Alden on LWN\.net.  The Git project discussed the prospect in January 2024,
  and then again at the Git Contributor's Summit in September 2024.
    + Git Contributor's Summit 2024 was mentioned in
      [Git Rev News Edition #115](https://git.github.io/rev_news/2024/09/30/edition-115/),
      with link to notes as posts to git mailing list (also available in read-only Google Docs),
      and repo with notes from breakout unconference sessions.
+ [Vigilante Justice on GitHub: GitHub Graffiti](https://trufflesecurity.com/blog/vigilante-justice-on-github)
  by Dylan Ayrey on The Dig (Truffle Security Co. blog), about
  how you can paint funny pixel art (graffiti) with fake commit Git histories 
  on spammer/phisher's GitHub profiles (on their activity heatmap plot) -
  which is [only] possible because of spammer attempts to leverage GitHub issues for phishing,
  on a repo one has push access to.
+ [Facing the Git commit-ID collision catastrophe](https://lwn.net/Articles/1001526/)
  (in Linux kernel repository) by  Jonathan Corbet on LWN\.net,
  about the concern that, given the growth of the kernel repository, soon 12 digits will not be enough;
  on the other hand, commits only make up about 1/8 of the total objects in the repository,
  and abbreviated hashes should be accompanied by the short-form version of the changelog
  (`--format=reference`).
+ [Optimizing Your Repository for Speed and Efficiency](https://dev.to/this-is-learning/optimizing-your-repository-for-speed-and-efficiency-5co2) and
  [Using Git Maintenance in GitHub Actions: Optimize Your Repositories Automatically](https://dev.to/this-is-learning/using-git-maintenance-in-github-actions-optimize-your-repositories-automatically-39ka)
  by Emanuele Bartolesi for This is Learning on DEV\.to create 2 part series
  [Streamline Your Workflow with the Git Maintenance Command](https://dev.to/kasuken/series/29808).
    + The [`git maintenance`](https://git-scm.com/docs/git-maintenance) command
      was mentioned in [Git Tips 2: Some Subtle New Things](https://blog.gitbutler.com/git-tips-2-new-stuff-in-git/)
      article on GitButler Blog by Scott Chacon, which in turn was mentioned in
      [Git Rev News Edition #108](https://git.github.io/rev_news/2024/02/29/edition-108/).
+ [Demystifying git submodules](https://www.cyberdemon.org/2024/03/20/submodules.html)
  by Dmitry Mazin on his blog.
+ [Fearless Rebasing](https://blog.gitbutler.com/fearless-rebasing/) by Scott Chacon on GitButler Blog
  is about "first class" conflict support in GitButler, based on Jujutsu concept of
  "[first class conflicts](https://martinvonz.github.io/jj/latest/conflicts/)".
    + The article does not mention the built-in (but optional) [git rerere](https://git-scm.com/docs/git-rerere)
      mechanism of reusing recorded resolution of conflicted merges
      (described for example in [Git Tools - Rerere](https://git-scm.com/book/en/v2/Git-Tools-Rerere)
      section in "Pro Git" 2nd Edition), that can help when repeatedly rebasing.
    + In order to reduce the pain of resolving merge conflicts,
      and allow a merge or a rebase to be saved, tested, interrupted, published,
      and collaborated on while it is in progress, one can also use
      [git-imerge](https://github.com/mhagger/git-imerge) tool
      (see also [git-imerge: A Practical Introduction](https://softwareswirl.blogspot.com/2013/05/git-imerge-practical-introduction.html) article).<br>
      `git-imerge` was first mentioned in passing in [Git Rev News Edition #17](https://git.github.io/rev_news/2016/07/20/edition-17/),
      while Edition #34 includes [Developer Spotlight: Michael Haggerty](https://git.github.io/rev_news/2017/12/20/edition-34/#developer-spotlight-michael-haggerty),
      an interview with the author of this tool.
    + [Jujutsu (`jj`)](https://jj-vcs.github.io/jj/), a Git-compatible version control system,
      written in Rust, was first mentioned in
      [Git Rev News Edition #85](https://git.github.io/rev_news/2022/03/31/edition-85/).
+ [Stacked Branches with GitButler](https://blog.gitbutler.com/stacked-branches-with-gitbutler/)
  by Scott Chacon on GitButler Blog.
  With 0.14 release GitButler can now manage dependent branches that are stacked,
  including managing stacked GitHub PRs (Pull Requests).
    + See also [Understanding the Stacked Pull Requests Workflow](https://www.git-tower.com/blog/stacked-prs/) by Bruno Brito on Tower's blog,
      mentioned in [Git Rev News Edition #111](https://git.github.io/rev_news/2024/05/31/edition-111/)
      together with various other articles and tools about stacked diffs, stacked PRs, and stacked branches.
    + See also [Rethinking code reviews with stacked PRs](https://www.aviator.co/blog/rethinking-code-reviews-with-stacked-prs/#)
      by Ankit Jain on Aviator blog,
      mentioned in [Git Rev News Edition #115](https://git.github.io/rev_news/2024/09/30/edition-115/)
      with links to more sites and tools related to stacked PRs, etc.
+ [~~Enforcing~~ Git Branch Naming Standards: ~~Tools and~~ Tips for Developers](https://dev.to/oj_redifined/enforcing-git-branch-naming-standards-tools-and-tips-for-developers-1p27)
  by Ojay on DEV\.to (despite the title, the article does not include any technical way of
  helping to enforce or even remind about branch naming conventions).
+ [9 ways to manage large creative projects with version control tools](https://www.xda-developers.com/manage-large-creative-projects-with-version-control-tools/)
  by Ruby Helyer on XDA Developers.  Mentions CI/CD, Git LFS, commit message and file naming conventions.
+ Adam Ruka posted a series of articles on working with the Git source control system:
    1. [GitFlow considered harmful](https://www.endoflineblog.com/gitflow-considered-harmful) (2015)
    2. [Follow-up to 'GitFlow considered harmful'](https://www.endoflineblog.com/follow-up-to-gitflow-considered-harmful) (2015)
    3. [OneFlow – a Git branching model and workflow](https://www.endoflineblog.com/oneflow-a-git-branching-model-and-workflow) (2017)
    4. [Implementing OneFlow on GitHub, BitBucket and GitLab](https://www.endoflineblog.com/implementing-oneflow-on-github-bitbucket-and-gitlab) (2021)
  [GitFlow: A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
  was a blog post by Vincent Driessen from 2010, with note of reflection from 2020;
  the original author now suggest to adopt a much simpler workflow (like 
  [GitHub flow](https://guides.github.com/introduction/flow/)) if the team is doing
  continuous delivery of software, and use GitFlow only when necessary,
  for explicitly versioned software - with multiple versions of it in the wild to be supported.<br>
  See also [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html)
  by Martin Fowler, mentioned in [Git Rev News Edition #63](https://git.github.io/rev_news/2020/05/28/edition-63/).


<!---
__Easy watching__
-->

__Git tools and sites__

+ [bus-factor-explorer](https://github.com/JetBrains-Research/bus-factor-explorer)
  by JetBrains Research is a web app for exploring Bus Factor of GitHub projects
  by analyzing the commit history.  Available as to install as a Docker image.
  The repository includes evaluation results for 935 popular repositories on GitHub.
  There is also a short video about the tool on YouTube: <https://youtu.be/uIoV79N14z8>.
  Written in Kotlin (with evaluation done with Jupyter notebooks), under MIT license.
    + See [The Bus Factor](https://mclare.blog/posts/the-bus-factor/) and
      [The github plugin my coworkers asked me not to write](https://scannedinavian.com/the-github-plugin-my-coworkers-asked-me-not-to-write.html)
      articles mentioned in [Git Rev News Edition #117](https://git.github.io/rev_news/2024/11/30/edition-117/)
      (the previous edition), together with accompanying links.
+ [Anonymous GitHub](https://anonymous.4open.science/) is a service
  that allows you to anonymize your GitHub repository for double-blind scientific review
  (of scientific article where source code is to be made available for open science reasons).
  Several anonymization options are available to ensure that you do not break the double-anonymize,
  such as removing links, images or specific terms.
  The goal is to make is as easy as possible for the reviewer to explore and review the repository.
+ [Git.News](https://git.news/) is a website which provides infinite newsfeed of
  trending repositories from GitHub, HackerNews & Reddit
  (which you can then filter by programming language).
+ [Octobox](https://octobox.io/) is a service to help manage GitHub notifications.
  Includes optional GitHub app to add live information on issue, PR, and CI status, labels, authors, etc.
  Octobox is free for open source projects with basic notifications for private projects.
+ [Filestash](https://www.filestash.app/) is Dropbox-like enterprise-grade file manager,
  connecting your storage with your identity provider and authorisations.
  It adds a web interface to storage solutions like S3 buckets, SFTP/FTPS server, Git repositories, etc.
  Self-hosted solution is free; it can be done using Docker image.
  Written in Go and JavaScript, under AGPLv3 license.
  Demo available at <https://demo.filestash.app/>,
  source code at <https://github.com/mickael-kerjean/filestash>.
+ [DistGit (Distribution Git)](https://github.com/release-engineering/dist-git)
  is Git with additional data storage, designed to hold content of source RPMs
  (Linux distribution packages).  Written in Python, under the MIT license,
  but with scripts/httpd/upload.cgi under GPLv1,
  and dist-git-client sub-directory under GPLv2+.
+ [wikmd](https://linbreux.github.io/wikmd/) is a file-based wiki, with
  documents written in Markdown, and which uses Git for version control.
  It is possible to connect Wikmd with an online repo.
  Written in Python, under MIT license.
+ [Mycorrhiza Wiki](https://mycorrhiza.wiki/) is a free and open-source wiki engine,
  with data stored as simple files, and changes [stored in Git](https://mycorrhiza.wiki/hypha/git).
  It uses [Mycomarkup](https://mycorrhiza.wiki/hypha/mycomarkup), a custom-made markup language,
  with support for transcluding units of contents.
  Written in Go, under AGPLv3 license.
+ [Gitit](https://github.com/jgm/gitit) is a wiki engine written in Haskell,
  that uses [Happstack](http://happstack.com/) (HAppS) for the web server
  and [pandoc](http://pandoc.org/) for markup processing (with extended Markdown format as default).
  Pages and uploaded files are stored in a git, darcs, or mercurial repository
  and may be modified through the wiki's web interface.
  Under GPLv2 license.
+ [Xandikos](https://www.xandikos.org/) is a lightweight CardDAV/CalDAV server
  that backs onto a Git repository.
  It allows to share calendars (events, todo items, journal entries) via CalDAV
  and contacts (vCard) via CardDAV.
  Written in Python using Dulwich, Jinja2, icalendar, and defusedxml,
  licensed under GPLv3+.
+ [Opengist](https://github.com/thomiceli/opengist) is a self-hosted pastebin powered by Git,
  similar to [GitHub Gist](https://gist.github.com/).
  Demo available at <https://demo.opengist.io/>.
  Written in Go, under AGPLv3 license.
+ [rgit](https://github.com/w4/rgit) is a gitweb/cgit-like fast web frontend for git repositories.
  You can see it in action at <https://git.inept.dev/>.
  Written in Rust using Axum, gitoxide, Askama and RocksDB.
  Under WTFPL license
  (which is not on the list of [OSI approved Licenses](https://opensource.org/licenses),
  but is on the list of [licenses that meet Debian Free Software Guidelines](https://wiki.debian.org/DFSGLicenses#DO_WHAT_THE_FUCK_YOU_WANT_TO_PUBLIC_LICENSE)).
+ [klaus](https://github.com/jonashaag/klaus) is a simple, easy-to-set-up Git web viewer.
  Supports syntax highlighting, Markdown + RestructuredText (reST) rendering support,
  and code navigation using Exuberant ctags.  Can be installed as Docker image of via `pip`.
  You can see its demo at <http://klausdemo.lophus.org/>.
  Written in Python, under unamed custom permissive license.
+ [git-activity](https://git-activity.olets.dev/) is a tool
  to record your Git activity across multiple (or all) repos,
  and read it optionally filtered by date,
  activity type (e.g. commit, branch creation, etc) regex pattern,
  repo name regex pattern, branch name regex pattern, commit message regex pattern,
  and/or commit SHA (first seven characters) regex pattern.
  Useful for retroactively filling out a time sheet (or correcting a time sheet),
  finding that time you solved a problem similar to the one you're working on now, etc.
  The log is stored in a plain text file.  Source code [on GitHub](https://github.com/olets/git-activity).
  Written as bash shell script using AWK, licensed under (custom)
  CC BY-NC-SA 4.0 with Hippocratic License v3 ethical requirements.
+ [git-branches-script](https://github.com/conorsheppard/git-branches-script)
  is a convenience script that prints a menu of recent git branches
  and allows you to switch to a new branch by selecting its corresponding number.
  Written as bash shell script, no license provided.


## Releases

+ Git [2.48.0-rc1](https://public-inbox.org/git/xmqqjzbhxeho.fsf@gitster.g/),
[2.48.0-rc0](https://public-inbox.org/git/xmqqfrmn4hr9.fsf@gitster.g/)
+ Git for Windows [2.48.0-rc0(1)](https://github.com/git-for-windows/git/releases/tag/v2.48.0-rc0.windows.1)
+ libgit2 [1.9.0](https://github.com/libgit2/libgit2/releases/tag/v1.9.0)
+ GitHub Enterprise [3.15.1](https://help.github.com/enterprise-server@3.15/admin/release-notes#3.15.1),
[3.14.6](https://help.github.com/enterprise-server@3.14/admin/release-notes#3.14.6),
[3.13.9](https://help.github.com/enterprise-server@3.13/admin/release-notes#3.13.9),
[3.12.13](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.13),
[3.11.19](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.19),
[3.15.0](https://help.github.com/enterprise-server@3.15/admin/release-notes#3.15.0),
[3.14.5](https://help.github.com/enterprise-server@3.14/admin/release-notes#3.14.5),
[3.13.8](https://help.github.com/enterprise-server@3.13/admin/release-notes#3.13.8),
[3.12.12](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.12),
[3.11.18](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.18)
+ GitLab [17.7](https://about.gitlab.com/releases/2024/12/19/gitlab-17-7-released/),
[17.6.2, 17.5.4, 17.4.6](https://about.gitlab.com/releases/2024/12/11/patch-release-gitlab-17-6-2-released/)
+ Gerrit Code Review [3.11.0](https://www.gerritcodereview.com/3.11.html#3110)
+ GitKraken [10.6.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.4.12](https://desktop.github.com/release-notes/),
[3.4.11](https://desktop.github.com/release-notes/),
[3.4.10](https://desktop.github.com/release-notes/)
+ Garden [1.10.0](https://github.com/garden-rs/garden/releases/tag/v1.10.0)
+ Git Cola [4.10.1](https://github.com/git-cola/git-cola/releases/tag/v4.10.1),
[4.10.0](https://github.com/git-cola/git-cola/releases/tag/v4.10.0)
+ GitButler [0.14.4](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.14.4),
[0.14.3](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.14.3)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from XXX.
