---
title: Git Rev News Edition 105 (November 30th, 2023)
layout: default
date: 2023-11-30 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 105 (November 30th, 2023)

Welcome to the 105th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of October 2023 and November 2023.

## Discussions

### General

- Git participates in [Outreachy's December 2023 to March 2024 round](https://www.outreachy.org/alums/2023-12/)

  Achu Luma will work on the "Move existing tests to a unit testing
  framework" project. They will be mentored by Christian Couder.

  Congratulations to Luma for being selected!

  Thanks also to the other contributors who applied and worked on
  micro-projects, but couldn’t be selected! We hope to continue to see
  you in the community!


### Reviews

+ [[PATCH v2 0/2] Prevent re-reading 4 GiB files on every status](https://lore.kernel.org/git/20231012160930.330618-1-sandals@crustytoothpaste.net/)

  In May 2022 Jason Hatton sent
  [an email to the mailing list](https://lore.kernel.org/git/CY4PR16MB1655A1F7DD8B2FABCC30C9DAAFC39@CY4PR16MB1655.namprd16.prod.outlook.com/)
  about the fact any file with a size that is an exact multiple of
  8GBi makes Git extremely slow on the repository.

  He said that he had already opened
  [an issue about this on the Git for Windows issue tracker](https://github.com/git-for-windows/git/issues/3833#issuecomment-1116544918)
  where Jason, Philip Oakley, brian m. carlson and Dscho, alias
  Johannes Schindelin had already discussed the issue.

  Git uses an `uint32_t` type, a 32 bit long unsigned integer, for
  storing the file size in the index. This rolls over if the value is
  greater than 2 to the power 32, so with file sizes over 4GB. When
  the size is exactly 4GBi or a multiple of it, like 8GBi, the roll
  over makes it zero.

  A zero file size in the index has a special meaning for Git
  though. It tells Git that the file needs to be hashed again. Hashing
  a file is supposed to reset its file size in the index to a non zero
  value, but with a 4GBi file size the roll over happens and the file
  size is still zero. So the hashing will be performed again and again
  by many different Git commands which will make Git very slow.

  Jason proposed, as a solution to this problem, to detect when the
  roll over would happen, and in that case set the size to 1 instead
  of zero.

  Junio C Hamano, the Git maintainer, replied to Jason confirming the
  issue and explaining it a bit more in detail. Jason and Junio then
  discussed the issue a bit more, while Jason tested locally his
  suggested fix and proposed to send a real patch to fix the issue.

  René Scharfe then chimed into the discussion asking if a value other
  than one would be better and would avoid other possible issues.
  Philip Oakley replied to René suggesting using 0x80000000 instead of
  1 when the roll over is detected. This would make it easier to
  detect "almost all incremental and decremental changes in file
  sizes", as the file size in the index helps detecting file changes.

  Jason and Philip discussed the issue a bit more and agreed that
  using 0x80000000 only for exact multiples of 4GiB would likely be
  the best solution.

  Philip and Carlo Marcelo Arenas Belón also tried to help Jason
  properly submit a patch to the mailing list.

  Jason then sent
  [a patch to the mailing list](https://lore.kernel.org/git/CY4PR16MB16552D74E064638BEC11ECB1AFC59@CY4PR16MB1655.namprd16.prod.outlook.com/)
  with the changes and explanation that had been discussed. Torsten
  Bögershausen, Philip and Junio reviewed it, and suggested some
  improvements. Junio especially requested some tests to be added.

  After some discussions with Jason to clarify what should be
  improved, Jason sent
  [another version of his patch](https://lore.kernel.org/git/20220507185813.1403802-1-jhatton@globalfinishing.com/).

  It looked like Jason found an issue with the patch due to using
  0x80000000 instead of 1. René and Philip discussed it with Jason,
  but there was no clear conclusion. It wasn't even clear if there was
  an issue at all. But anyway the work on this stopped for more than
  one year.

  Fortunately a few weeks ago, brian m. carlson sent
  [a new version of Jason's patch](https://lore.kernel.org/git/20231012160930.330618-1-sandals@crustytoothpaste.net/)
  along with another patch adding tests.

  These patches were reviewed by Eric Sunshine, Peff, alias Jeff King,
  Junio and Jason. After some discussions it appeared that the patches
  were good enough for Junio so that he decided to make a small change
  in them and then merge them. This issue is therefore fixed in the
  Git 2.43.0 version released on November 20.

<!---
### Support
-->

## Developer Spotlight: Alexander Shopov

* Who are you and what do you do?

  I am Alexander Shopov - a backend engineer in the Amsterdam office of
  Uber working on money related systems. I am a long time translator of
  FOSS software in Bulgarian - I am coordinating translations of GNOME,
  Translation Project and many GNU modules. Bulgarian is an Eastern
  South Slavic language written in the Cyrillic alphabet.

* What would you name your most important contribution to Git?

  I made and now maintain the Bulgarian translation of the text
  interface of Git, Gitk and Git Gui.

* What is the typical workflow of a contributor contributor engaged
  in translation for Git?

  There are 19 translations of the text interface of Git and only 13 of
  them are above 80% so I am not sure about "typical". It is a fairly
  standard workflow for a FOSS project.

  Generally one needs to do the following:

  1. Read the translator-targeted README.md in the po directory
  2. Sync pace with the [calendar of git releases](https://tinyurl.com/gitcal)
  3. Use the [l10n coordinator repository](https://github.com/git-l10n/git-po)
     maintained by Jiang Xin who makes sure translations get integrated upstream.

  Currently the translation is a bit above 5500 messages which is about
  40k words, 250k of characters or about 150 pages of text. It can be
  intimidating for a new translator. But you can definitely make it: be
  patient and translate some messages every release, merge, publish and
  repeat. Even better though harder is getting more than one person
  translating.

* Do you contribute to Git in ways other than providing translation?
  If so, could you elaborate about them?

  Sadly not that much. On rare occasions I improve messages and mark
  strings for translations. Perhaps that will be the way I contribute
  unless I find a mentor and something that I find particularly
  interesting and important for me. So if anyone is willing to mentor
  me, especially in making large repos faster - [ping me](mailto:ash@kambanaria.org).
  I can be a competent tester at least.

* If you could get a team of expert developers to work full time on
  something in Git for a full year, what would it be?

  Due to its enormous success, Git is being used on humongous code bases
  with a crazy number of files, directories, commits and branches.
  Working with repos larger than 10GB can be a bit slow. Improving the
  experience will be a great thing.

* If you could remove something from Git without worrying about
  backwards compatibility, what would it be?

  Backwards compatibility is massively important and I am thankful
  developers and users are all invested in this.

  If we treat this as a hypothetical question: there are 3 things to Git:
  - The command-line interface;
  - The wire protocol;
  - The storage format;

  The command-line interface is gradually being improved. The wire
  protocol is also a place where there are workarounds for versioning.
  The storage format however is another (quite conservative and public)
  API. I would remove the old versions and try to design it targeting
  projects that are 10-100 times larger than the linux kernel first. In
  for a penny, in for a pound. If we break things, let us break them so
  hard that bards will sing songs about us!

* What is your favorite Git-related tool/library, outside of Git itself?

  I mainly use commandline git plus gitk and git-gui. I do like using
  the meld diff tool when I work on translations.

* Do you happen to have any memorable experience w.r.t contributing
  to the Git project? If yes, could you share it with us?

  The initial getting to 100% translated messages was a challenge. I
  decided that I should translate Git around December 2013. That was
  around 2200 messages at that time and it took me about 3 releases of
  Git to reach 100%. Getting to 100% was immensely hard, rewarding and
  memorable. Afterwards keeping the translation at 100% was much easier.

* Is there something you feel that could be done to ease the life of
  translators?

  The terminology glossary of Git is much larger than 7 years ago and we
  (the translators) should actually update git://repo.or.cz/git-gui.git::po/glossary
  and merge it in Git.

* What is your advice for people who want to start Git development?
  Where and how should they start?

  I don't know to be honest. If I knew I may have started already.

* If there's one tip you would like to share with other Git
  developers, what would it be?

  That would be the tip of master two years in the future. On a more
  serious note - perhaps more tools for migration out of the still
  existing proprietary version control systems will be helpful.


## Other News

__Various__

+ [Highlights from Git 2.43](https://github.blog/2023-11-20-highlights-from-git-2-43/)
  by Taylor Blau on GitHub Blog.  Those include new `git repack` tricks
  (including adjusting sparse clone filters), nicer looking reverts of reverts
  with `git revert`, fixed interaction between `--subject-prefix` and `--rfc`
  in `git format-patch`, custom log format options that simulate the decorations, etc.
+ [Gitea Cloud: A brand new platform for managed Gitea Instances](https://blog.gitea.com/gitea-cloud/),
  designed for enterprise organizations to set up and run
  their own Gitea instances more easily and efficiently.
+ [Announcing DoltgreSQL](https://www.dolthub.com/blog/2023-11-01-announcing-doltgresql/)
  by Daylon Wilkins on DoltHub Blog.
    + [Git-for-Data, Version-Controlled Database Dolt Gets PostgreSQL-Flavor](https://www.infoq.com/news/2023/11/DoltgreSQL-git-for-data-postgres/)
      by Sergio De Simone on InfoQ.
    + [Dolt](https://github.com/dolthub/dolt), a version-controlled database,
      was first mentioned in [Git Rev News Edition #62](https://git.github.io/rev_news/2020/04/23/edition-62/).
+ [An Interesting CMS With Version Control is Now Open-Source!](https://news.itsfoss.com/tinacms-open-source/)
  by Sourav Rudra on It's FOSS News (it's [TinaCMS](https://tina.io/)).
+ [Introducing the Space Git Subtree](https://blog.jetbrains.com/space/2023/11/21/space-git-subtree/)
  by Ilia Afanasiev on The Space Blog (where Space is JetBrains' code collaboration platform).
+ [Developers can’t seem to stop exposing credentials in publicly accessible code](https://arstechnica.com/security/2023/11/developers-cant-seem-to-stop-exposing-credentials-in-publicly-accessible-code/)
  by Dan Goodin on Ars Technica, and<br>
  [Uncovering thousands of unique secrets in PyPI packages](https://blog.gitguardian.com/uncovering-thousands-of-unique-secrets-in-pypi-packages/)
  by Tom Forbes on GitGuardian Blog.


__Light reading__
    
+ [How I (kind of) killed Mercurial at Mozilla](https://glandium.org/blog/?p=4346)
  by Mike Hommey (author of [git-cinnabar](https://github.com/glandium/git-cinnabar),
  Git remote helper to interact with Mercurial repositories).
+ Julia Evans continues the series of articles about Git (started in
  [Git Rev News #103](https://git.github.io/rev_news/2023/09/30/edition-103/)
  with [In a git repository, where do your files live?](https://jvns.ca/blog/2023/09/14/in-a-git-repository--where-do-your-files-live-/)
  and
  [Git Rev News #104](https://git.github.io/rev_news/2023/10/31/edition-104/)
  with [Some miscellaneous git facts](https://jvns.ca/blog/2023/10/20/some-miscellaneous-git-facts/));
  currently there are available the following additional posts:
  [Confusing git terminology](https://jvns.ca/blog/2023/11/01/confusing-git-terminology/),
  [git rebase: what can go wrong?](https://jvns.ca/blog/2023/11/06/rebasing-what-can-go-wrong-/),
  [How git cherry-pick and revert use 3-way merge](https://jvns.ca/blog/2023/11/10/how-cherry-pick-and-revert-work/),
  and [git branches: intuition & reality](https://jvns.ca/blog/2023/11/23/branches-intuition-reality/)
  (so far).
    + Julia Evans (@b0rk@jvns.ca) asked about read-only FUSE filesystem for a git repository
      where every commit is a folder and the folder contains all the files in that commit
      [on Mastodon](https://fosstodon.org/@b0rk@jvns.ca/111462737333140668), so this series may continue
      (so far it led to very experimental [git-commit-folders](https://github.com/jvns/git-commit-folders)
      tool from her, and [GitMounter](https://belkadan.com/blog/2023/11/GitMounter/) from
      Jordan Rose being made public).
    + See also [Pain in the dots](https://matthew-brett.github.io/pydagogue/pain_in_dots.html)
      by Matthew Brett (part of [Notes and tutorials on git](https://matthew-brett.github.io/pydagogue/git.html)),
      about confusing difference in how two-dot and three-dot notation
      behaves in `git log` and in `git diff`, as an adition to the Julia Evans' article
      about confusing git terminology, the [.. and ... section](https://jvns.ca/blog/2023/11/01/confusing-git-terminology/#and).
+ [How I teach Git](https://blog.ltgt.net/teaching-git/) by Thomas Broyer
  on his blog (also [on DEV.to](https://dev.to/tbroyer/how-i-teach-git-3nj3)).
  inspired to write it down by Julia Evans' (renewed) interest in Git,
  and her questions on social networks.
+ [Stacked Diffs (and why you should know about them)](https://newsletter.pragmaticengineer.com/p/stacked-diffs)
  by Gergely Orosz in The Pragmatic Engineer blog.  Another article about Stacked Diffs
  can be found in [Git Rev News Edition #44](https://git.github.io/rev_news/2018/10/24/edition-44/).
    + Compare and contrast  [Ship / Show / Ask: A modern branching strategy](https://martinfowler.com/articles/ship-show-ask.html)
      mentioned in [Edition #79](https://git.github.io/rev_news/2021/09/30/edition-79/).
+ [Why I Prefer Trunk-Based Development](https://koenvangilst.nl/blog/trunkbased-development)
  by Koen van Gilst on his blog.
    + See also [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html)
      in [Git Rev News Edition #73](https://git.github.io/rev_news/2021/03/27/edition-73/).
+ A bit controversial [Dependencies Belong in Version Control](https://www.forrestthewoods.com/blog/dependencies-belong-in-version-control/)
  (even if it's not practical today due to Git's limitations)
  by Forrest Smith on his blog.
+ [Managing My Resume with Git: A Version Control Approach](https://dev.to/dunkbing/managing-my-resume-with-git-a-version-control-approach-7hk)
  by Bui Dang Binh (dunkbing) on DEV\.to.
+ [See the History of a Method with `git log -L`](https://calebhearth.com/git-method-history)
  by Caleb Hearth on his blog; the post lists also a few his other articles about Git:
    + [Stash only what `git commit` wouldn't commit](https://calebhearth.com/stash-what-git-wouldnt-commit).
    + [Ignore refactoring commits in `git blame`](https://calebhearth.com/rubocop-git-blame).
    + [Use your SSH key to sign commits](https://calebhearth.com/sign-git-with-ssh).
        + See also for example
          [Signing Git Commits with SSH Keys](https://blog.dbrgn.ch/2021/11/16/git-ssh-signatures/)
          from [Git Rev News Edition #83](https://git.github.io/rev_news/2022/01/31/edition-83/).
+ [Why Git blame sucks for understanding WTF code (and what to use instead)](https://tekin.co.uk/2020/11/patterns-for-searching-git-revision-histories)
  by Tekin Süleyman (2020); the author recommend "pickaxe" search with `git log -S` and
  `git log -G`, or searching commit messages with `git log --grep`.
+ [How to Resolve Merge Conflicts Using the Merge Editor Feature on VS Code](https://adiati.com/how-to-resolve-merge-conflicts-using-the-merge-editor-feature-on-vs-code)
  by Ayu Adiati on Ayu's Notes On Blog (also [on DEV\.to](https://dev.to/adiatiayu/how-to-resolve-merge-conflicts-using-the-merge-editor-feature-on-vs-code-pic),
  as part of larger [Open-Source Series' Articles](https://dev.to/adiatiayu/series/15234)).
+ [The Ultimate "git nah" Alias](https://laravel-news.com/the-ultimate-git-nah-alias)
  for abort their current changes and any possible operation in progress,
  by Paul Redmond on Laravel News.
+ [Understanding Git: The history and internals](https://graphite.dev/blog/understanding-git)
  by Kenneth DuMez on the Graphite Blog (more about history and internals than about
  understanding Git).  See also:
    + [GitHistory page in the archives of Git SCM Wiki](https://archive.kernel.org/oldwiki/git.wiki.kernel.org/index.php/GitHistory.html),
    + [The Git Parable](http://tom.preston-werner.com/2009/05/19/the-git-parable.html),
      by Tom Preston-Werner (2009) - the ideas behind the architecture of Git;
      covered in [Git Rev News #30](https://git.github.io/rev_news/2017/08/16/edition-30/),
    + Will Hay Jr.’s [The Architecture and History of Git: A Distributed Version Control System](https://medium.com/@willhayjr/the-architecture-and-history-of-git-a-distributed-version-control-system-62b17dd37742),
      mentioned in [Git Rev News #46](https://git.github.io/rev_news/2018/12/19/edition-46/),
    + [The History of Git: The Road to Domination in Software Version Control](https://git.github.io/rev_news/2020/02/19/edition-60/)
      referenced in [Git Rev News #60](https://git.github.io/rev_news/2020/02/19/edition-60/).
+ [Tracking SQLite Database Changes in Git](https://garrit.xyz/posts/2023-11-01-tracking-sqlite-database-changes-in-git)
  with appropriate `textconv` gitattribute, by Garrit Franke on Garrit's Notes.
+ [GitHub’s all-in bet on AI may overlook Git](https://www.infoworld.com/article/3710428/githubs-all-in-bet-on-ai-may-overlook-git.html)
  by Matt Asay on InfoWorld.
+ [🙏 Please Add .gitattributes To Your Git Repository](https://dev.to/deadlybyte/please-add-gitattributes-to-your-git-repository-1jld)
  by Carl Saunders on DEV\.to (2020).
    + A `.gitattributes` file [can be used to improve](https://github.com/github-linguist/linguist/blob/master/docs/overrides.md#using-gitattributes)
     language detection on GitHub, which is using
     [Linguist](https://github.com/github-linguist/linguist) library.


__Easy watching and listening__

+ [Git Training](https://www.youtube.com/playlist?list=PL1gv5yv3DoZNIPVAlZRGPEB0fBvflO-xN)
  playlist of 45 short YouTube videos by Joost De Cock
  provides git training materials for people who would like to understand
  how Git works rather than try to memorize all of its commands
  without knowing what they do.
+ The Real Python Podcast:
  [Episode 179: Improving Your Git Developer Experience in Python](https://realpython.com/podcasts/rpp/179/)



__Git tools and sites__

+ [gitattributes.io](https://gitattributes.io/) is a service to generate 
  [`.gitattributes`](https://git-scm.com/docs/gitattributes) file,
  similar to [gitignore.io](https://www.toptal.com/developers/gitignore/).
+ [githistory.xyz](https://githistory.xyz/) is a service that allows to
  quickly browse the history of files in any git repo (from GitHub, GitLab, Bitbucket).
  Also available as Chrome, Firefox, and Visual Studio extensions,
  and as `git-file-history` command line tool (in Node.js).
  Mentioned in passing in [Git Rev News Edition #48]().
+ Josh Branchaud (jbranchaud) list of
  [Today I Learned (TIL) tips about Git](https://github.com/jbranchaud/til#git).
+ [lei](https://public-inbox.org/lei.html) is a command-line tool
  for importing and searching email, regardless of whether it is from a personal mailbox
  or a public-inbox instance, like [public-inbox.org](https://public-inbox.org/README.html)
  or [lore.kernel.org](https://lore.kernel.org/).<br>
  Warning: lei is still in its early stages and may destroy mail.
    + See also [lore+lei: part 1, getting started](https://people.kernel.org/monsieuricon/lore-lei-part-1-getting-started)
      article by Konstantin Ryabitsev (2021).
+ [git-fame](https://github.com/casperdcl/git-fame): Pretty-print
  git repository collaborators sorted by contributions (includes computing
  code survival).  Written in Python.
+ [git-fame-rb](https://github.com/oleander/git-fame-rb) is a command-line tool
  that helps you summarize and pretty-print collaborators, based on the number of contributions.
  The statistics are mostly based on the output of `git blame` (counting surviving lines).
  Written in Ruby.
+ [GQL (Git Query Language)](https://amrdeveloper.github.io/GQL/)
  [[repo](https://github.com/AmrDeveloper/GQL)]
  is a SQL like language to perform queries on .git files,
  with supports of most of SQL features
  such as grouping, ordering and aggregations functions.<br>
  You can find more in [How I Created a SQL-like Language to Run Queries on Local Git Repositories](https://www.freecodecamp.org/news/gql-design-and-implementation/)
  article by Amr Hesham on freeCodeCamp.<br>
  See also the following tools:
   + [Gitana](https://github.com/SOM-Research/Gitana): SQL-based Project Activity Inspector
     (repo archived in 2022),
     first mentioned in [Git Rev News Edition #7](https://git.github.io/rev_news/2015/09/09/edition-7/)
   + [gitbase](https://github.com/src-d/gitbase): SQL interface to git repositories, written in Go;
     (last release from 2019, [homepage](https://docs.sourced.tech/gitbase) is not working),
     first mentioned in [Git Rev News Edition #48](https://git.github.io/rev_news/2019/02/27/edition-48/)
   + [git-history](https://datasette.io/tools/git-history) is a tool
     for analyzing Git history using SQLite (last release in 2021),
     first mentioned in [Git Rev News Edition #82](https://git.github.io/rev_news/2021/12/30/edition-82/)
   + [MergeStat](https://github.com/mergestat/mergestat) enables SQL queries
     for data in git repositories (and related sources, such as the GitHub API).
     There is also [mergestat-lite](https://github.com/mergestat/mergestat-lite)
     command line tool, which runs SQL queries against local git repositories.
     First mentioned in [Git Rev News Edition #82](https://git.github.io/rev_news/2021/12/30/edition-82/).
     Actively developed, mergestat-lite is written in Go.
+ [GibleFS](https://github.com/fanzeyi/giblefs) is a toy project
  that maps a Git repository to a virtual filesystem, which then can be used
  to access the repository at any given commit.  Written in Rust, does not seem
  to be actively developed.
+ `Git/fs` binary in [Git9](https://orib.dev/git9.html)
  (Git client for Plan 9 non-POSIX filesystem)
  serves repository history as a file system.
+ [gitfs](https://github.com/presslabs/gitfs) is a FUSE file system
  that fully integrates with git. You can mount a remote repository's branch locally,
  and any subsequent changes made to the files will be automatically committed to the remote.
  Written in Python, last release in 2019.
    + Note: that is not the only project named gitfs or git-fs.
+ [SlothFS](https://github.com/google/slothfs) is a FUSE filesystem
  that provides light-weight, lazily downloaded, read-only checkouts
  of manifest-based Git projects. It is intended for use with Android.
  Written in Go, repository archived in 2022.
+ [GitMounter](https://belkadan.com/source/GitMounter/) is
  a toy FUSE browser for Git repos based on [Suffusion](https://belkadan.com/source/Suffusion/).
  Requires FUSE, libgit2, pkg-config, and Swift installed.
  Written in Swift.


## Releases

+ Git [2.43.0](https://public-inbox.org/git/xmqqzfz8l5or.fsf@gitster.g/),
[2.43.0-rc2](https://public-inbox.org/git/xmqqo7fwxn4s.fsf@gitster.g/),
[2.43.0-rc1](https://public-inbox.org/git/xmqq8r785ev1.fsf@gitster.g/),
[2.43.0-rc0](https://public-inbox.org/git/xmqqy1fgkqg1.fsf@gitster.g/),
[2.42.1](https://public-inbox.org/git/xmqq4ji4m50l.fsf@gitster.g/)
+ Git for Windows [2.43.0(1)](https://github.com/git-for-windows/git/releases/tag/v2.43.0.windows.1),
[2.43.0-rc2(1)](https://github.com/git-for-windows/git/releases/tag/v2.43.0-rc2.windows.1),
[2.43.0-rc1(1)](https://github.com/git-for-windows/git/releases/tag/v2.43.0-rc1.windows.1),
[2.43.0-rc0(1)](https://github.com/git-for-windows/git/releases/tag/v2.43.0-rc0.windows.1)
+ GitLab [16.6](https://about.gitlab.com/releases/2023/11/16/gitlab-16-6-released/)
[16.5.2](https://about.gitlab.com/releases/2023/11/14/gitlab-16-5-2-released/),
[16.5.1, 16.4.2, 16.3.6](https://about.gitlab.com/releases/2023/10/31/security-release-gitlab-16-5-1-16-4-2-16-3-6-released/)
+ Gerrit Code Review [3.6.8](https://www.gerritcodereview.com/3.6.html#368),
[3.7.6](https://www.gerritcodereview.com/3.7.html#376),
[3.8.3](https://www.gerritcodereview.com/3.8.html#383),
[3.9.0](https://www.gerritcodereview.com/3.9.html#390)
+ GitHub Enterprise [3.11.0](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.0)
+ GitKraken [9.10.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.3.5](https://desktop.github.com/release-notes/)
+ Tower for Windows [5.2](https://www.git-tower.com/blog/tower-windows-52/)
+ Tower for Mac [10.2](https://www.git-tower.com/blog/tower-mac-102/)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Alexander Shopov and Bruno Brito.
