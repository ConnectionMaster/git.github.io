---
title: Git Rev News Edition 104 (October 31st, 2023)
layout: default
date: 2023-10-31 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 104 (October 31st, 2023)

Welcome to the 104th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of September 2023 and October 2023.

## Discussions

### General

+ [Git Virtual Contributor’s Summit 2023](https://docs.google.com/document/d/1GKoYtVhpdr_N2BAonYsxVTpPToP1CgCS9um0K7Gx9gQ)

  A virtual summit happened on September 26th and 27th, where the
  contributors discussed
  [topics that they had previously voted on](https://docs.google.com/spreadsheets/d/1EnhmTeEqRBlEI2pMAO3oZ4rO1xEwBzYp2vS4CMtvge8).
  Taylor Blau, who organized the summit, polished and then sent
  [the notes that were taken during the summit](https://lore.kernel.org/git/ZRregi3JJXFs4Msb@nand.local/#r)
  to the mailing list.


### Reviews

+ [[PATCH] diff --stat: add config option to limit filename width](https://lore.kernel.org/git/87badb12f040d1c66cd9b89074d3de5015a45983.1694446743.git.dsimic@manjaro.org/)

  Dragan Simic sent a patch to the mailing list that added a new
  `diff.statNameWidth=<width>` configuration option. The goal with
  this option was to make it possible to limit the width of the
  filepath part of the "stat" output of `git diff` commands.

  For example, the "stat" output of a `git diff` command contains lines like this:

  ```
  path/to/file.txt                         | 11 +++++++--
  ```

  where the "filepath" part, also called "name" or "filename" part, of
  that output is `path/to/file.txt` and the "graph" part is
  `11 +++++++--`.

  There were already a `diff.statGraphWidth=<width>` configuration
  option to limit the width of the graph part, and also
  `--stat-name-width=<width>` and `--stat-graph-width=<width>` command
  line options to limit the width of the name and graph part,
  respectively. So it was logical to add the missing configuration
  option.

  These options are especially useful for people using very large
  terminals, to prevent "stat" output from using a lot of columns.

  The new `diff.statNameWidth=<width>` was designed to be ignored by
  `git format-patch` in the same way as
  `diff.statGraphWidth=<width>`, because that command already respects
  the traditional 80-column standard.

  Before sending this patch, Dragan had sent
  [an RFC email](https://lore.kernel.org/git/eb8f524eca3975f086715ec32a8a1fbb@manjaro.org/)
  asking if such a patch would be accepted, which led to an interesting
  discussion between him and Junio Hamano, the Git maintainer, about
  the fact that we often cannot promise anything about a hypothetical
  patch before actually seeing it on the mailing list.

  Junio reviewed the actual patch and wondered if it would be possible
  to specify contradictory values for the whole width on one side and
  the "name" and "graph" width on the other side. He also suggested
  creating a helper function to initialize all the variables that
  contain the values of the configuration options for the different
  parts, as the code initializing those variables was duplicated in
  the code of many Git commands.

  Dragan replied that the diff code already performed "a reasonable
  amount of sanity checks and value adjustments". He wondered if
  warnings should be emitted in case of contradictory settings though.

  Dragan then agreed that refactoring the code that initialized the
  variables would be nice, but he proposed to do it after the current
  patch would have been merged.

  Junio and Dragan agreed with doing the refactoring later and
  discussed a bit deeper if more changes were needed in this patch, but
  it appeared that it could be merged as is, and so it was.

  A few days later Dragan sent
  [a patch to refactor the code that initialized the variables](https://lore.kernel.org/git/166396f0a98e248fc3d1236757632c5d648ddc0b.1695364961.git.dsimic@manjaro.org/).
  Junio reviewed it and suggested some improvements, which Dragan
  implemented in [a second version of the patch](https://lore.kernel.org/git/d45d1dac1a20699e370905b88b6fd0ec296751e7.1695441501.git.dsimic@manjaro.org/).

  This second version was also reviewed by Junio and then merged.

<!---
### Support
-->

<!---
## Developer Spotlight:
-->

## Other News

__Various__
* [New book “Boost Your Git DX”](https://adamchainz.gumroad.com/l/bygdx) by Git contributor Adam Johnson, covering tools and configurations to improve your command line workflow.
* [Git 2.42 release: Here are four of our contributions in detail](https://about.gitlab.com/blog/2023/10/12/contributions-to-git-2-42-release/)
  by Christian Couder on GitLab Blog.
    * [Highlights from Git 2.42](https://github.blog/2023-08-21-highlights-from-git-2-42/)
      link can be found in [Git Rev News Edition #102](https://git.github.io/rev_news/2023/08/31/edition-102/).

__Light reading__
+ [Some miscellaneous git facts](https://jvns.ca/blog/2023/10/20/some-miscellaneous-git-facts/)
  by Julia Evans on her blog.  The facts are:
    + the “index”, “staging area” and “`--cached`” are all the same thing
    + the stash is a bunch of commits
    + not all references are branches or tags
    + merge commits aren’t empty
+ [Why Git is hard](https://roadrunnertwice.dreamwidth.org/596185.html)
  by Nick Eff on his Roadrunner Twice Dreamwidth's journal,
  in response to Julia Evans ending her StrangeLoop 2023 keynote talk with
  “I still don’t know why Git is hard.”
    + There is some discussion on the [programming.dev Lemmy instance](https://programming.dev/post/4051745)
      about this post.
    + Various attempts to make Git or version control easier include
      [Gitless](http://gitless.com/) - first mentioned in [Git Rev News Edition #20](https://git.github.io/rev_news/2016/10/19/edition-20/),
      [Jujutsu](https://github.com/martinvonz/jj) - mentioned in [#85](https://git.github.io/rev_news/2022/03/31/edition-85/),
      and [EasyGit (eg)](https://github.com/dfabulich/easygit) - seems not to be actively developed.
+ [Investigating Git History](https://www.git-tower.com/blog/investigating-git-history/)
  by Kristian Lumme on Tower’s blog.
+ [Measuring Git performance with OpenTelemetry](https://github.blog/2023-10-16-measuring-git-performance-with-opentelemetry/)
  by Jeff Hostetler on GitHub Blog.  It describes how to use open source
  [Trace2](https://github.com/git/git/blob/master/Documentation/technical/api-trace2.txt)
  [receiver component (trace2receiver)](https://github.com/git-ecosystem/trace2receiver)
  and [OpenTelemetry](https://opentelemetry.io/docs/what-is-opentelemetry/)
  to capture and visualize telemetry from your Git commands.
+ [What is in that `.git` directory?](https://blog.meain.io/2023/what-is-in-dot-git/)
  by Abin Simon on meain/blog.
+ [Versioning data in Postgres? Testing a git like approach](https://www.specfy.io/blog/7-git-like-versioning-in-postgres)
  by Samuel Bodin on his Specfy Blog.
+ [Organizing multiple Git identities](https://garrit.xyz/posts/2023-10-13-organizing-multiple-git-identities)
  using `.gitconfig` includes,
  by Garrit Franke on Garrit's Notes blog.
+ [Linux Fu: Deep Git Rebasing](https://hackaday.com/2023/10/17/linux-fu-deep-git-rebasing/)
  by Al Williams on Hackaday.
+ [Git: Rewriting History 101](https://matheustavares.gitlab.io/posts/rewriting-history-101)
  by Matheus Tavares (2022).
+ [How to split off an older copy of a file while preserving git line history](https://devblogs.microsoft.com/oldnewthing/20230728-00/?p=108498)
  by Raymond Chen on Microsoft's The Old New Thing DevBlog.
    + His older article on [how to duplicate a file while preserving git line history](https://devblogs.microsoft.com/oldnewthing/20190919-00/?p=102904)
      was mentioned in [Git Rev News Edition #51](https://git.github.io/rev_news/2019/05/22/edition-51/).
+ [Embracing Database Deployments in CI/CD Practices with Git](https://thenewstack.io/embracing-database-deployments-in-ci-cd-practices-with-git/)
  by Vanessa Fox from PlanetScale on TheNewStack.
    + [An article](https://planetscale.com/blog/database-branching-three-way-merge-schema-changes)
      about [PlanetScale branching support for MySQL](https://planetscale.com/docs/concepts/branching)
      was mentioned in [Git Rev News Edition #99](https://git.github.io/rev_news/2023/05/31/edition-99/),
      while PlanetScale as solution was mentioned in set of article about databases and versioning
      in [Git Rev News Edition #82](https://git.github.io/rev_news/2021/12/30/edition-82/).
+ [TypeScript Monorepo with NPM workspaces](https://www.yieldcode.blog/post/npm-workspaces/)
  by Dmitry Kudryavtsev on yield code(); blog.
+ [The "Schrödinger's tree object": is it there or not?](https://matheustavares.gitlab.io/posts/empty-tree):
  Matheus Tavares finds about the hard-coded empty tree object (2022).

<!---
__Easy watching__
-->

__Git tools and sites__
+ [gittuf](https://gittuf.dev/) provides a security layer for Git
  using some concepts introduced by [The Update Framework (TUF)](https://theupdateframework.io/).
  Among other features it handles key management for all developers on the repository,
  allows you to set permissions for repository branches, tags, files, etc.<br>
  gittuf is a sandbox project at the [Open Source Security Foundation (OpenSSF)](https://openssf.org/)
  as part of the [Supply Chain Integrity Working Group](https://github.com/ossf/wg-supply-chain-integrity).
  It is currently in _alpha_.  Written in Go.
+ [trace2receiver](https://github.com/git-ecosystem/trace2receiver) project
  is a [trace receiver](https://opentelemetry.io/docs/collector/trace-receiver/) component library
  for an [OpenTelemetry Custom Collector](https://opentelemetry.io/docs/collector/) daemon.
  It receives [Git Trace2](https://git-scm.com/docs/api-trace2#_the_event_format_target) telemetry
  from local Git commands, translates it into an OpenTelemetry format, and forwards it
  to other OpenTelemetry components.  Written in Go as a static library component
  that must be linked into an OpenTelemetry Custom Collector.
+ [git-bundle-server](https://github.com/git-ecosystem/git-bundle-server)
  is a web server & management CLI to host Git bundles for use with Git's
  ["bundle URIs" feature](https://git-scm.com/docs/bundle-uri).
  By running this software, you can self-host a bundle server.
  Written in Go, under active development.  Installation on Windows is currently unsupported.
+ [Awesome GitHub Alternatives](https://github.com/ianchanning/awesome-github-alternatives)
  is a list of alternatives to GitHub that by default offer Git management in some way.
  All self-hosted options are free and open source, with GPL-compatibile licenses.
  Not exhaustive.
+ [src (Simple Revision Control)](http://www.catb.org/esr/src/)
  is RCS/SCCS reloaded with a modern UI, designed to manage single-file solo projects
  kept more than one to a directory. Use it for FAQs, `~/bin` directories, config files,
  and the like.  Written in Python.
    + Mentioned in passing in [Git Rev News Edition #46](https://git.github.io/rev_news/2018/12/19/edition-46/).


## Releases

+ GitHub Enterprise [3.10.3](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.3),
[3.9.6](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.6),
[3.8.11](https://help.github.com/enterprise-server@3.8/admin/release-notes#3.8.11),
[3.7.18](https://help.github.com/enterprise-server@3.7/admin/release-notes#3.7.18)
+ GitLab [16.5](https://about.gitlab.com/releases/2023/10/22/gitlab-16-5-released/)
+ Bitbucket Server [8.15](https://confluence.atlassian.com/bitbucketserver/bitbucket-server-release-notes-872139866.html)
+ GitKraken [9.9.2](https://help.gitkraken.com/gitkraken-client/current/),
[9.9.1](https://help.gitkraken.com/gitkraken-client/current/),
[9.9.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.3.4](https://desktop.github.com/release-notes/)
+ TortoiseGit [2.15.0](https://tortoisegit.org/download/)
+ git-credential-oauth [0.11.0](https://github.com/hickford/git-credential-oauth/releases/tag/v0.11.0)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Bruno Brito, Adam Johnson and Sven Strickroth.
