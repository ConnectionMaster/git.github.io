---
title: Git Rev News Edition 108 (February 28th, 2024)
layout: default
date: 2024-02-28 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 108 (February 28th, 2024)

Welcome to the 108th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of January 2024 and February 2024.

## Discussions

<!---
### General
-->

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

- The Git project has been accepted as a [Mentor Organization](https://summerofcode.withgoogle.com/programs/2024/organizations/git) for Google Summer of Code (GSoC) 2024. We could still add project ideas to our [idea page](https://git.github.io/SoC-2024-Ideas/) and volunteers to (co-)mentor are still welcome. Feel free to chime in [the corresponding thread](https://public-inbox.org/git/1de82b27-116a-450e-98c0-52eb65a8f608@gmail.com/). Also, feel free to spread the word about Git's participation.


__Light reading__

+ [Git Tips and Tricks: a 3 part series](https://blog.gitbutler.com/git-tips-and-tricks/)
  by Scott Chacon on [GitButler]() blog,
  accompanying the video from the talk
  [So You Think You Know Git - FOSDEM 2024](https://www.youtube.com/watch?v=aolI_Rz0ZqY)
  (available on YouTube)
    + [Git Tips 1: Oldies but Goodies](https://blog.gitbutler.com/git-tips-1-theres-a-git-config-for-that/):
      conditional configs, git blame and log with line ranges (`-L`),
      git blame with following, word diff, resolution reuse (`git rerere`).
    + [Git Tips 2: Some Subtle New Things](https://blog.gitbutler.com/git-tips-2-new-stuff-in-git/):
      git branch stuff (`--sort`, `--column`), safe force pushing (`--force-with-lease`),
      SSH commit signing, push signing, `git maintenance`.
    + [Git Tips 3: Really Large Repositories and Monorepos](https://blog.gitbutler.com/git-tips-3-really-large-repositories/):
      prefetching, commit graph, filesystem monitor, partial cloning, sparse checkouts,
      [scalar](https://git-scm.com/docs/scalar) tool.
+ [Git Trailers](https://alchemists.io/articles/git_trailers) by Brooke Kuhlmann. Learn how to
  leverage commit metadata for powerful automations and more human readable commit messages.
+ [More Expressive Commits with Gitmoji ☺️](https://www.git-tower.com/blog/gitmoji/)
  by Bruno Brito on Tower’s blog.
    + [Gitmoji](https://gitmoji.dev/) was first mentioned in [Git Rev News Edition #47](https://git.github.io/rev_news/2019/01/23/edition-47/),
      though then under [different URL](https://gitmoji.carloscuesta.me/)
      (which now redirects to the current one).
    + Similar [Emoji-Log](https://github.com/ahmadawais/Emoji-Log) commit log messages spec standard
      was mentioned in [Git Rev News Edition #101](https://git.github.io/rev_news/2023/07/31/edition-101/).
+ [My Git pre-commit hook contained a footgun](https://blog.plover.com/prog/git/hook-disaster.html)
  by Mark Dominus (陶敏修) on his The Universe of Discourse blog.
+ Julia Evans continues her series of blog posts about Git with
  [Dealing with diverged git branches](https://jvns.ca/blog/2024/02/01/dealing-with-diverged-git-branches/)
  and [Popular git config options](https://jvns.ca/blog/2024/02/16/popular-git-config-options/).
  First entry in this series can be found in [Git Rev News Edition #103](https://git.github.io/rev_news/2023/09/30/edition-103/).
+ [Git Battle: YOLO Mode vs. Clean History](https://hankadev.com/git-battle-yolo-mode-vs-clean-history/)
  by Hana Klingová on her blog (and also [on DEV.to](https://dev.to/hankadev/git-battle-yolo-mode-vs-clean-history-594d)):
  about usefulness of `git commit --fixup` and `rebase.autosquash`.
+ [Restore deleted/lost files with git](https://dev.to/this-is-learning/restore-deletedlost-files-with-git-3lf7)
  by Leonardo Montini for This is Learning, a part 6 of
  [git better - Improve your git skills (6 Part Series)](https://dev.to/balastrong/series/21372).
  Originally published [at leonardomontini.dev](https://leonardomontini.dev/git-restore-deleted-file/)
  (includes [video version](https://youtu.be/TL_t3aOXumo)).
+ [My favourite Git commit](https://dhwthompson.com/2019/my-favourite-git-commit) (2019)
  by David Thompson on his blog,
  about the benefits of good commit messages (the example is one character change).<br>
  Includes links to the following recommended articles on the same topic:
    + [Telling stories through your commits](https://blog.mocoso.co.uk/posts/talks/telling-stories-through-your-commits/) by Joel Chippindale (2016)
    + [A branch in time](https://tekin.co.uk/2019/02/a-talk-about-revision-histories) by Tekin Süleyman (2019)
    
+ [Contribution experience report: Git](https://antonin.delpeuch.eu/posts/contribution-experience-report-git/)
  by Antonin Delpeuch on his blog.


__Easy watching__

+ [So You Think You Know Git - FOSDEM 2024](https://www.youtube.com/watch?v=aolI_Rz0ZqY)
  on YouTube, 47 minutes long.


__Git tools and sites__

+ [Milestoner](https://alchemists.io/projects/milestoner) by Brooke Kuhlmann. Significant updates
  have been made where you can build release notes from your commit messages based on Git notes and
  trailers in multiple formats: Text, ASCII Doc, Markdown, and HTML. Includes automatic calculation
  of your next version and automatic tagging too.
+ [git-cliff](https://git-cliff.org/) is a highly customizable changelog generator
  using regex-powered custom parsers, that can generate changelog files for any Git repository
  that follows the [conventional commits](https://www.conventionalcommits.org/) specification.
  Written in Rust as a command-line application.
+ [pg-diff](https://michaelsogos.github.io/pg-diff/) is a PostgreSQL schema and data comparing tool.
  Written in JavaScript by Michael Sogos.
+ [Another trivial utility: git-q](https://blog.plover.com/prog/git-q.html) by Mark Dominus
  available from [mjdominus personal git-util repository](https://github.com/mjdominus/git-util)
  as [git-q](https://github.com/mjdominus/git-util).
+ [Aho](https://github.com/djanderson/aho) is a Git implementation in AWK.
  It is a _toy project_ to explore some of the internals of Git and newer features of GNU AWK.


## Releases

+ Git [2.44.0](https://public-inbox.org/git/xmqqbk87w164.fsf@gitster.g/),
[2.43.3](https://public-inbox.org/git/xmqqil2fw16c.fsf@gitster.g/),
[2.44.0-rc2](https://public-inbox.org/git/xmqqbk8brrj3.fsf@gitster.g/),
[2.43.2](https://public-inbox.org/git/xmqqo7cjvuht.fsf@gitster.g/),
[2.44.0-rc1](https://public-inbox.org/git/xmqqttmbvuyh.fsf@gitster.g/),
[2.44.0-rc0](https://public-inbox.org/git/xmqqo7cph7ov.fsf@gitster.g/),
[2.43.1](https://public-inbox.org/git/xmqqttmhh7ow.fsf@gitster.g/)
+ Git for Windows [2.44.0(1)](https://github.com/git-for-windows/git/releases/tag/v2.44.0.windows.1),
[2.44.0-rc2(1)](https://github.com/git-for-windows/git/releases/tag/v2.44.0-rc2.windows.1),
[2.44.0-rc1(1)](https://github.com/git-for-windows/git/releases/tag/v2.44.0-rc1.windows.1),
[2.44.0-rc0(1)](https://github.com/git-for-windows/git/releases/tag/v2.44.0-rc0.windows.1)
+ GitLab [16.9.1, 16.8.3, 16.7.6](https://about.gitlab.com/releases/2024/02/21/security-release-gitlab-16-9-1-released/)
[16.9](https://about.gitlab.com/releases/2024/02/15/gitlab-16-9-released/),
[16.8.2, 16.7.5, 16.6.7](https://about.gitlab.com/releases/2024/02/07/security-release-gitlab-16-8-2-released/)
+ Gerrit Code Review [3.7.7](https://www.gerritcodereview.com/3.7.html#377),
[3.8.4](https://www.gerritcodereview.com/3.8.html#384)
+ GitHub Enterprise [3.12.0](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.0),
[3.11.5](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.5),
[3.10.7](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.7),
[3.9.10](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.10),
[3.8.15](https://help.github.com/enterprise-server@3.8/admin/release-notes#3.8.15),
[3.11.4](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.4),
[3.10.6](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.6),
[3.9.9](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.9),
[3.8.14](https://help.github.com/enterprise-server@3.8/admin/release-notes#3.8.14)
+ GitKraken [9.12.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.3.9](https://desktop.github.com/release-notes/)
+ Sourcetree [4.2.7](https://product-downloads.atlassian.com/software/sourcetree/ReleaseNotes/Sourcetree_4.2.7.html)
+ Tower for Mac [10.4](https://www.git-tower.com/release-notes/mac?show_tab=release-notes)
+ git-credential-oauth [0.11.1](https://github.com/hickford/git-credential-oauth/releases/tag/v0.11.1)
  
## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Brooke Kuhlmann and Bruno Brito.
