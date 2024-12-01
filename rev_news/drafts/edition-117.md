---
title: Git Rev News Edition 117 (November 30th, 2024)
layout: default
date: 2024-11-30 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 117 (November 30th, 2024)

Welcome to the 117th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of October and November 2024.

## Discussions

<!---
### General
-->

<!---
### Reviews
-->

### Support

+ [Bug report: v2.47.0 cannot fetch version 1 pack indexes](https://lore.kernel.org/git/BA07EFA0-0793-420D-BED9-ACD7CEBE0112@townlong-yak.com/)

  Someone called 'fox' reported that when upgrading Git to v2.47.0
  from v2.46.2 or a previous version, cloning from their website,
  which uses the old "dumb HTTP" protocol, stopped working. With
  v2.47.0 there is an error message indicating that some index files
  "differ in contents".

  Using `git bisect`, fox found the commit that introduced the
  issue. That commit implemented a check that verified that the index
  file downloaded from the remote was byte-for-byte identical with the
  index file generated locally from the Git objects downloaded as part
  of the clone.

  That check failed because the remote had an index in the version 1
  format, while the locally generated index was in a more recent
  format. And fox wondered if this was intentional.

  Eric Sunshine replied to fox that he could reproduce the problem.

  Jeff King, alias Peff, also replied to fox saying that the breakage
  was not intended. He thought that it was better to rely on the
  locally generated index, but that there should be no guarantee for
  it to be identical to the downloaded one.

  Peff proposed a draft patch that discarded the downloaded version
  before generating an index, but said it was hacky and didn't check
  that the content was the same. So he suggested a better solution.

  He then proposed an improved draft patch, which implemented the
  better solution he had suggested by marking the downloaded index as
  temporary and then discarding it after a new one is generated.

  Taylor Blau, who was the temporary Git maintainer while Junio
  Hamano, the usual maintainer, had some time off, replied to Eric and
  fox in the meantime confirming it was an unintentional breakage, and
  saying he was going to look at Peff's patches.

  Taylor then discussed with Peff the first draft patch and agreed
  with Peff that the solution implemented in the improved draft patch
  was better.

  So Taylor reviewed Peff's improved draft patch. He made some
  comments but found it good, and asked Peff to add a test and to
  propose it as a regular patch.

  Peff replied to Taylor's comments, proposed a draft test, and said
  he was going to work on a proper patch as well as some cleanups and
  refactors in the dumb HTTP code.

  Taylor found Peff's draft test "beautifully written".

  Peff then sent
  [a series made of 11 patches](https://lore.kernel.org/git/20241025064148.GA2110169@coredump.intra.peff.net/)
  to fix the issue, clean up the dumb HTTP code and fix a couple of
  other bugs or potential bugs he found in the process.

  Taylor reviewed the patch series and discussed a few technical
  details with Peff. Overall he found the series good to go and
  eventually merged it.


## Developer Spotlight: Ghanshyam Thakkar

* Who are you and what do you do?

  I am Ghanshyam Thakkar. I was an undergrad student in Electronics
  when I started contributing to Git. I am now a Software Engineer at a
  startup. I sometimes contribute to open source projects in my free time,
  and explore/learn new technologies.

* How did you initially become interested in contributing to Git,
  and what motivated you to choose it as your GSoC project?

  Before GSoC, I was quite familiar with the Linux ecosystem and it had
  been my primary OS for the majority of my college years. And during
  those times I felt Git was the most impactful project enabling the vastly
  collaborative Linux Desktop Ecosystem. So, I felt like contributing
  to Git would be a great opportunity to learn and contribute to a
  project that had been so crucial to my everyday workflow.

* How do you feel your contribution has impacted the Git community
  or the broader open source ecosystem?

  Before my GSoC project, I had contributed some small patches, which
  could be considered as bug fix, general code cleanup, expanding test
  coverage, etc. Some of which can be observed in user-space. But my GSoC
  project was about migrating Git's test suite to a purely C-based
  test framework, which was not user-facing, however, was a step in the
  right direction for the project as a whole.

* Is there any aspect of Git that you now see differently after
  having contributed to it?

  The mailing list workflow. Although, I was skeptical about it at first
  because I had never used mailing lists before, I now see it as a very
  effective way to communicate and collaborate on a project of such
  massive scale. Although, I still am not a big fan of the all or nothing
  nature of the mailing lists. Subscribing to mails of a specific area
  would have been great. Although, I do understand that it can
  probably be done with filtering using a script.

* How do you balance your contributions with other responsibilities
  like work or school?

  When I was contributing to Git as part of GSoC, I was a student and I
  also had summer vacation, so it was quite easy for me to balance my
  contributions with my personal life. However, now that I am quite busy with my
  $DAYJOB, I don't have much bandwidth to contribute to open
  source in the short term. But I am planning to start contributing again
  after some time.

* Can you share how GSoC helped enhance your technical and
  non-technical skills (like communication, project management, etc.)?

  I would say it helped me improve my technical communication skills immensely.
  Going back and forth with the reviewers on the list, I learned quite a
  bit about how to communicate effectively. Also, this was my first time
  working in a C based project, so I learned some C hacks as well!

* What was your biggest takeaway or learning from GSoC that you now
  apply regularly in your work?

  Technical communication and effective code review. Also more effective
  Git usage.

* What was the biggest challenge you faced during your contributions
  to Git, and how did you overcome it?

  More than the technical challenges solving a problem, I would say it was
  more challenging finding the relevant work to do, as there is no
  official issue tracker. I would search for #leftoverbits on the mailing
  list and #TODOs in the codebase to find things to do. However,
  most of them seemed quite out of reach in terms of difficulty. However,
  I attempted them anyway and learned a lot in the process. The mailing
  list folks were quite helpful in guiding me in the right direction.

* Have you thought about mentoring new GSoC students?

  Yes, although I don't have the bandwidth to become a primary mentor,
  I would love to be a co-mentor.

* If you could get a team of expert developers to work full time on
  something in Git for a full year, what would it be?

  Honestly, I find Git to be quite mature and complete. I can't
  think of anything, off the top of my head, that I would like
  people to work on for a full year.

* What upcoming features or changes in Git are you particularly
  excited about?

  Rust adoption.

* What is your favorite Git-related tool/library, outside of Git
  itself?

  I quite frequently find myself using [`lazygit`](https://github.com/jesseduffield/lazygit)
  on the command line for some quick and dirty git operations.

* What is your toolbox for interacting with the mailing list and for
  development of Git?

  I use [aerc](https://aerc-mail.org/) and `send-email`/`format-patch`
  for email interactions. And for development, I use [Neovim](https://neovim.io/)
  and [clang LSP](https://gist.github.com/Strus/042a92a00070a943053006bf46912ae9)
  with `GENERATE_COMPILATION_DATABASE` build flag.

* How do you envision your own involvement with Git or other open
  source projects in the future?

  I think I will continue to be a part of the open source community in some
  way or the other. My perspective towards open source has always been
  very positive and I would like to continue contributing to it.

* What is your advice for people who want to start Git development?
  Where and how should they start?

  I would suggest to start from reading the docs, particularly
  [MyFirstContribution](https://git-scm.com/docs/MyFirstContribution)
  and [SubmittingPatches](https://git-scm.com/docs/SubmittingPatches).
  And then start with some [#leftoverbits](https://lore.kernel.org/git/?q=%23leftoverbits)
  or if you are particularly interested in a specific area, you can
  even reach out to people working on those areas to ask for guidance.

* Would you recommend other students or contributors to participate in
  the GSoC, or other mentoring programs, working on Git? Why? Do you
  have advice for them?

  Absolutely! GSoC is a great opportunity to learn and contribute to open
  source projects. It is a great way to learn how a project of such
  massive scale is managed and developed.


## Other News

__Various__


__Light reading__

+ [The Bus Factor](https://mclare.blog/posts/the-bus-factor/)
  by Maryanne Wachter (also known as &lt;mclare&gt; or m-clare) on her blog
  (with visualizations built with Observable), and
  [The github plugin my coworkers asked me not to write.](https://scannedinavian.com/the-github-plugin-my-coworkers-asked-me-not-to-write.html)
  by Shae Erisson on Shae Erisson's Blog.
    + The _bus factor_ is a measurement of the risk resulting from information and capabilities
      not being shared among team members, derived from the phrase "in case they get hit by a bus".
      It is also known as the bus problem, truck factor, bus/truck number or circus factor.
      The "bus factor" is the minimum number of team members that have to suddenly disappear
      from a project before the project stalls due to lack of knowledgeable or competent personnel.
      (From [Wikipedia](https://en.wikipedia.org/wiki/Bus_factor)).
    + Based on the ["A Novel Approach for Estimating Truck Factors"](https://arxiv.org/abs/1604.06766)
      paper from 2016 by Guilherme Avelino, Leonardo Passos, Andre Hora, and Marco Tulio Valente,
      with many citations since.
      Original implementation available at <https://github.com/aserg-ufmg/Truck-Factor>.
+ [How we shrunk our Javascript monorepo git size by 94%](https://www.jonathancreamer.com/how-we-shrunk-our-git-repo-size-by-94-percent/)
  Mentions using the [git-sizer](https://github.com/github/git-sizer) tool
  which was mentioned in passing in [Git Rev News Edition #37](https://git.github.io/rev_news/2018/03/21/edition-37/).
  The work described in the article also led to adding the `--path-walk` option to `git repack`
  and the `pack.usePathWalk` config option to Git,
  and to the new experimental [`git survey`](https://github.com/microsoft/git/pull/667) command
  (that for now is present in Microsoft's fork of Git),
+ [Deleted your fork. Is it gone? Not really…](https://ygreky.com/2024/07/deleted-your-fork-is-it-gone-not-really/)
  Marta Rybczynska on Ygreky Blog.  Provides some recommendations for best practices
  when using public forges.
    + References [Anyone can Access Deleted and Private Repository Data on GitHub](https://trufflesecurity.com/blog/anyone-can-access-deleted-and-private-repo-data-github)
      blog post by Truffle Security, mentioned in [Git Rev News Edition #113](https://git.github.io/rev_news/2024/07/31/edition-113/).
    + See also [Demystifying GitHub Private Forks - The Hidden Danger of Cached View](https://blog.gitguardian.com/demystifying-github-cached-views-the-hidden-danger/)
      by Guillaume Valadon on GitGuardian Blog.
+ [How I configure my Git identities](https://www.benji.dog/articles/git-config/)
  with the help of `git config` features: `includeIf` with `gitdir:` and with `hasconfig:`,
  and with `~/.ssh/config` (and `insteadOf`, where needed).
  Written by Benji Encalada Mora on their blog
  (with a comment of "This may be overkill, but it works on my machine").
+ [When to rewrite Git history?](https://drewdeponte.com/blog/when-to-rewrite-git-history/)
  (beside "Don't rewrite history once it is shared.").  Written by Drew De Ponte on his blog.
+ [[The Ultimate Guide to] Git Commit Creation](https://drewdeponte.com/blog/git-commit-creation/)
  by Drew De Ponte on his blog.
+ [How to Use Git Stash to Efficiently Manage Your Code](https://www.freecodecamp.org/news/how-to-use-git-stash-to-manage-code)
  by Okoro Emmanuel Nzube on freeCodeCamp.
+ [Finding when a bug was fixed with git bisect](https://jvns.ca/til/finding-when-a-bug-was-fixed-with-git-bisect/)
  in Julia Evans [TILs](https://jvns.ca/til/) (<b>T</b>oday <b>I</b> <b>L</b>earned).
    + Julia Evans has written a series of articles on Git, which were referenced in
      Git Rev News from [Edition #103](https://git.github.io/rev_news/2023/09/30/edition-103/)
      to [#111](https://git.github.io/rev_news/2024/05/31/edition-111/).
    + She has also published two [zines](https://wizardzines.com/) about Git:
      _[Oh shit, git!](https://wizardzines.com/zines/oh-shit-git/)_ and
      _[How Git Works](https://wizardzines.com/zines/git/)_
+ [Quick tip: Ignore commits in Git blame using a file](https://marijkeluttekes.dev/blog/articles/2024/11/17/quick-tip-ignore-commits-in-git-blame-using-a-file/)
  (recommended name is `.git-blame-ignore-revs`)
  by Marijke Luttekes on her blog.
+ [4 reasons you should use Git for productivity, even if you aren't a developer](https://www.xda-developers.com/reasons-should-use-git-productivity/)
  by Adam Conway on XDA Developers blog.

<!-- tangentially related to Git -->

+ [Doomed Keys and Hidden Threats: The Scariest Secrets in Your Repositories](https://blog.gitguardian.com/scary-secrets-2024/)
  by Gaetan Ferry and
  [The Extent of Hardcoded Secrets: From Development to Production](https://blog.gitguardian.com/the-extent-of-hardcoded-secrets-from-development-to-production/)
  by Guillaume Valadon on GitGuardian Blog.


<!---
__Easy watching__
-->

__Git tools and sites__

+ [GitFourchette](https://gitfourchette.org/) - The comfortable Git UI for Linux.
  Under development; you can currently install it [with AppImage or from source](https://github.com/jorio/gitfourchette/releases).
  Written in Python, using the Qt UI (via PyQt6/PySide6) and pygit2.  Under GPLv3 license.
+ [Changesets](https://github.com/changesets/changesets) is a tool
  to manage versioning and changelogs with a focus on multi-package repositories (monorepos).
  Written in TypeScript, under MIT license.
    + For an explanation of the "monorepo" concept see
      [What is a Monorepo?](https://monorepo.tools/#what-is-a-monorepo)
      on <monorepo.tools> (this site was mentioned first in
      [Git Rev News Edition #84](https://git.github.io/rev_news/2022/02/28/edition-84/)).
+ [Beachball](https://microsoft.github.io/beachball/): The Sunniest Semantic Version Bumper.
  Tool for automating npm publishing.
  Written in TypeScript, under MIT license.
+ [git-sizer](https://github.com/github/git-sizer) is a tool that computes various size metrics
  for a Git repository, flagging those that might cause problems.
  Written in Go, under MIT license.
    + This tool was mentioned in passing in
      [Git Rev News Edition #37](https://git.github.io/rev_news/2018/03/21/edition-37/).
+ [git-remote-s3](https://github.com/awslabs/git-remote-s3) is a library
  that enables you to use Amazon S3 as a git remote and as an LFS server.<br>
  It provides an implementation of a [git remote-helper](https://github.com/awslabs/git-remote-s3)
  to use S3 (Amazon Simple Storage Service) as a serverless Git server, and
  of the [git-lfs custom transfer](https://github.com/git-lfs/git-lfs/blob/main/docs/custom-transfers.md)
  to enable pushing LFS managed files to the same S3 bucket used as remote.
  Written in Python, under Apache 2.0 license.
+ [PatchScope](https://github.com/ncusi/PatchScope) is a tool that
  annotates files and lines of diffs (patches) with their purpose and type,
  and performs statistical analysis on diffs and on the generated annotation data.
  It also includes a web app, displaying various data visualizations.
  Written in Python, under MIT license.
    + Its README includes a [list of similar tools and sites](https://github.com/ncusi/PatchScope/blob/main/README.md#related-projects),
      many of which were mentioned here on Git Rev News.
+ [Mergiraf](https://mergiraf.org/) is a syntax-aware [git merge driver](https://git-scm.com/docs/gitattributes#_performing_a_three_way_merge)
  (and a `mergiraf` command line tool that helps solving merge conflicts)
  for a growing collection of programming languages and file formats.
  Adding a new language to Mergiraf is done in a declarative way.
  Written in Rust, under GPLv3 license.
    + The author recommends using Mergiraf together with [Difftastic](https://difftastic.wilfred.me.uk/),
      a structural diff tool that understands syntax, mentioned in
      [Git Rev News Edition #86](https://git.github.io/rev_news/2022/04/30/edition-86/).
+ [Diffdiff.net](https://diffdiff.net/) (formerly diff.so) is a web application
  that provides a fast, [private](https://diffdiff.net/privacy) way to compare two pieces of text
  in a "split diff"/"side diff" view, side by side with highlighting the text that is different
  from the text on the other side.

<!-- proprietary tools -->

+ [DiffLens](https://www.difflens.com/) - The Developer's Diff Tool.
  Provides language-aware semantic diffs for GitHub Pull Requests,
  adding them as a comment to the pull request.
  Available as a [GitHub app](https://github.com/marketplace/difflens)
  or a [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=DiffLens.difflens).
  Proprietary tool, with 14 days free trial, and [demo](https://www.difflensapp.com/difflensDemo2_849ca26f9ee09faa084cbdcdc90b6f90f8ce8495).
  See above for possible alternatives.


## Releases

+ Git [2.47.1](https://public-inbox.org/git/xmqq5xob6coo.fsf@gitster.g/)
+ Git for Windows [2.47.1(1)](https://github.com/git-for-windows/git/releases/tag/v2.47.1.windows.1)
+ libgit2 [1.8.4](https://github.com/libgit2/libgit2/releases/tag/v1.8.4)
+ Gerrit Code Review [3.10.3](https://www.gerritcodereview.com/3.10.html#3103),
[3.8.10](https://www.gerritcodereview.com/3.8.html#3810),
[3.9.8](https://www.gerritcodereview.com/3.9.html#398)
+ GitHub Enterprise [3.15.0](https://help.github.com/enterprise-server@3.15/admin/release-notes#3.15.0)
+ GitLab [17.6.1](https://about.gitlab.com/releases/2024/11/26/patch-release-gitlab-17-6-1-released/),
[17.6](https://about.gitlab.com/releases/2024/11/21/gitlab-17-6-released/),
[17.5.2](https://about.gitlab.com/releases/2024/11/13/patch-release-gitlab-17-5-2-released/)
+ GitKraken [10.5.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.4.9](https://desktop.github.com/release-notes/)
+ Sourcetree [4.2.10](https://product-downloads.atlassian.com/software/sourcetree/ReleaseNotes/Sourcetree_4.2.10.html),
[4.2.9](https://product-downloads.atlassian.com/software/sourcetree/ReleaseNotes/Sourcetree_4.2.9.html)
+ Garden [1.9.1](https://github.com/garden-rs/garden/releases/tag/v1.9.1)
+ Git Cola [4.9.0](https://github.com/git-cola/git-cola/releases/tag/v4.9.0)
+ git-credential-oauth [0.13.4](https://github.com/hickford/git-credential-oauth/releases/tag/v0.13.4)
+ GitButler [0.14.0](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.14.0),
[0.13.17](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.13.17)
+ Tower for Windows [8.0](https://www.git-tower.com/release-notes/windows?show_tab=release-notes), [8.1](https://www.git-tower.com/release-notes/windows?show_tab=release-notes) ([Release blog post](https://www.git-tower.com/blog/tower-windows-8/))
+ Tower for Mac [12.3](https://www.git-tower.com/release-notes/mac?show_tab=release-notes)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Bruno Brito.
