---
title: Git Rev News Edition 121 (March 31st, 2025)
layout: default
date: 2025-03-31 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 121 (March 31st, 2025)

Welcome to the 121st edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of February and March 2025.

## Discussions

### General

* [10 years of Git Rev News](https://git.github.io/rev_news/archive/)

  Git Rev News started 10 years ago with
  [edition 1 published on March 25, 2015](https://git.github.io/rev_news/2015/03/25/edition-1/),
  and then one edition per month.

  To celebrate, let's look at some stats that we have gathered about
  these first 120 editions.

  + First we would like to thank all those who helped us so far.

    This includes those who helped with ideas, links, PRs, small
    corrections, letting us know about a Git related software release,
    and even sometimes full articles without being part of our editor
    team. Here is the top 12 along with the number of editions they
    helped us with, according to our "Credits" section, and the number
    of commits they contributed:

    - Johannes Schindelin: 29 editions and 71 commits
    - Bruno Brito: 25 editions and 36 commits
    - Luca Milanesio: 19 editions and 23 commits
    - Štěpán Němec: 18 editions and 22 commits
    - Junio Hamano: 13 editions and 22 commits
    - Philip Oakley: 10 editions and 10 commits
    - Elijah Newren: 10 editions and 9 commits
    - Andrew Ardill: 8 editions and 15 commits
    - David Pursehouse: 8 editions and 12 commits
    - Jeff King: 8 editions and 5 commits
    - Matthieu Moy: 6 editions and 14 commits
    - Lars Schneider: 6 editions and 14 commits

    In total, more than 125 people helped this way.

    Former members of the editor team helped a lot, too:

    - Thomas Ferris Nicolaisen: 33 editions and 135 commits
    - Gabriel Alcaras: 22 editions and 7 commits
    - Nicola Paolucci: 16 editions and 5 commits

    A small number of people have also helped us by contributing to
    [our scripts](https://github.com/chriscool/getreleases/) to
    automate parts of the edition and publication process:

    - Gabriel Alcaras: 9 commits
    - David Aguilar: 3 commits
    - Mirth Hickford: 2 commits

  + A number of people helped by accepting to be interviewed in our
    "Developer Spotlight" or "Community Spotlight" sections. Thanks to
    them, too:

    - Total interviews: 72
    - Unique interviewees: 70
    - Repeat interviews: 2 (David Aguilar and Eric Sunshine have been interviewed twice)
    - Developer interviews: 70
    - Community interviews: 2

  + Most of the long articles are in a "Discussions" section and in
    one of its subsections: "General", "Reviews" or "Support". Here
    are some related stats:

    Total over all the editions:

    - Discussions articles: 254
    - General articles: 106
    - Reviews articles: 79
    - Support articles: 69

    Average per edition:

    - Discussions: 2.12
    - General: 0.88
    - Reviews: 0.66
    - Support: 0.57

  + Among those long articles, 16 articles were written by people
    outside the editor team. Big thanks to them! The top 3 is:

    - Junio Hamano: 4
    - Matthieu Moy: 3
    - Jacob Keller: 2

    The following people wrote one article each:

    Andrew Ardill, Elijah Newren, Eric S. Raymond, Eric Sunshine,
    Jiang Xin, Lars Schneider.

    One article was also written collaboratively by the following
    students:

    François Beutin, Jordan De Gea, William Duclot, Samuel Groot,
    Erwan Mathonière, Antoine Queru, Simon Rabourg and Tom Russello.

    These articles were mostly written towards the first years of Git
    Rev News:

    - 2015: 8 articles
    - 2016: 2 articles
    - 2018: 2 articles
    - 2019: 1 article
    - 2020: 3 articles

  + There were 2298 entries in the "Other News" section,
    which gathers links to various news, articles, sites, tools,
    and sometimes media about Git (or related to Git).

    Those entries include:

    - 1090 entries in "Light reading" over 114 editions
      with 1777 links; around 13.76% of entries mention previous editions.
    - 691 entries in "Git tools and sites" over 118 editions
      with 1270 links; around 11.72% of entries mention previous editions.
    - 411 entries in "Various" over 110 editions
      with 635 links; around 7.06% of entries mention previous editions.
    - 20 entries in "Events" over 12 editions
      with 39 links
    - 15 entries in "Light reading" over 12 editions
      with 31 links; of those, 3 entries mention previous editions.

    There were quite a few one-off names of sub-lists, like
    "Slightly heavier reading", "April Fool's", "Listening and watching".
    The template with standardized names was not present in the 1st edition,
    but was created later.


* [Git participated in the December 2024 Outreachy round](https://www.outreachy.org/alums/2024-12/)

  All the Outreachy interns have successfully completed their
  internship:

  - Seyi Kuforiji worked on the "Convert unit tests to use the clar
    testing framework" project, mentored by Patrick Steinhardt and
    Phillip Wood. See
    [his completion email](https://lore.kernel.org/git/CAGedMtcLRjr0GVNYmUU_tacrA0aRvOCYFGyOy0FACTBL=X3cwA@mail.gmail.com/)
    and
    [his retrospect blog post](https://seyi-kuforiji-902b48.gitlab.io/posts/a-retrospect-on-new-test-conversions).

  - Usman Akinyemi worked on the "Finish adding a 'os-version'
    capability to Git protocol v2" project, mentored by Christian
    Couder. See
    [his completion blog post](https://uniqueusman.hashnode.dev/my-outreachy-internship-experience-at-git).

<!---
### Reviews
-->

<!---
### Support
-->

## Developer Spotlight: Peter Krefting

* **Who are you and what do you do?**

  My name is Peter Krefting and I am a software engineer. Hailing from Sweden,
  I moved to Norway for my first job, at Opera Software, mostly working on
  internals such as Unicode support and internal libraries. I ended up staying
  in Norway and am currently working for a small company providing monitoring
  equipment for digital TV.

* **What are you doing on the Git project these days, and why?**

  My answers to these two are the same, I am the maintainer of the
  [Swedish translation of Git](https://github.com/git-l10n/git-po/blob/master/po/sv.po).
  I like having software running in my own language, and sometimes
  you have to take matters in your own hands.

* **If you could get a team of expert developers to work full time on
  something in Git for a full year, what would it be?**

  I think [`git gui`](https://git-scm.com/docs/git-gui) and
  [`gitk`](https://git-scm.com/docs/gitk) could need some extra love,
  these are my daily drivers, in addition to the command line.

* **Is there something that developers could do to ease the life of
  translators?**

  My main gripe is using library function names as verbs,
  like `cannot fsync`. That's hard to read even in the original
  language, even for a C developer like myself.

* **What is your favorite Git-related tool/library, outside of
  Git itself?**

  I like simple and clean interfaces, so using [cgit](https://wiki.archlinux.org/title/Cgit)
  to visualize history on a web server is very nice.

* **What is your toolbox for interacting with the mailing list and for
  development of Git?**

  I mostly just read the mailing list, and only a small percentage of the
  posts to it; the localization is handled through [GitHub pull requests](https://github.com/git-l10n/git-po/pulls?q=is%3Apr),
  so that's where that work happens. The few patches I have sent to the
  mailing list have been very manual, using `git format-patch` and
  the [Alpine mail client](https://alpineapp.email/).

* **What is your advice for people who want to start Git development?
  Where and how should they start?**

  Find some small part you want to improve, and work on that. Git is a
  fairly complex piece of software, implemented in several different
  languages, making it hard to get an overview. I most definitely do not have that,
  even after having read (and translated) most of the user-visible strings.


## Other News

__Various__

+ [What's new in Git 2.49.0?](https://about.gitlab.com/blog/2025/03/14/whats-new-in-git-2-49-0/)
  by Toon Claes on GitLab Blog.  This blog post mentions, among other things,
  improved performance thanks to zlib-ng, a new name-hashing algorithm, and git-backfill.
+ [Highlights from Git 2.49](https://github.blog/open-source/git/highlights-from-git-2-49/)
  by Taylor Blau on GitHub Blog.  Mentioned items include faster packing with name-hash v2,
  backfilling historical blobs in partial clones, building Git with zlib-ng,
  and libgit-sys and libgit Rust crates.


__Light reading__

+ [Going down the rabbit hole of Git's new bundle-uri](https://blog.gitbutler.com/going-down-the-rabbit-hole-of-gits-new-bundle-uri/)
  by Scott Chacon on GitButler blog.<br>
  The [`bundle-uri`](https://git-scm.com/docs/bundle-uri) was mentioned in passing in [Git Rev News Edition #95](https://git.github.io/rev_news/2023/01/31/edition-95/)
  (in _"Developer Spotlight"_), and in [Edition #104](https://git.github.io/rev_news/2023/10/31/edition-104/)
  (in _"Git tools and sites"_, when mentioning [git-bundle-server](https://github.com/git-ecosystem/git-bundle-server)).
+ [No Longer My Favorite Git Commit](https://mtlynch.io/no-longer-my-favorite-git-commit/)
  by Michael Lynch on his blog, talks about how one could _improve_ the commit message
  described in David Thompson's [“My favourite Git commit”](https://dhwthompson.com/2019/my-favourite-git-commit) - which
  was mentioned in [Git Rev News Edition #57](https://git.github.io/rev_news/2019/11/20/edition-57/)
  and [#108](https://git.github.io/rev_news/2024/02/29/edition-108/).
    + The article mentions the [How to Write Useful Commit Messages](https://refactoringenglish.com/chapters/commit-messages/)
      guide by Michael Lynch, one of the sample chapters for his prospective book,
      _"Refactoring English: Effective writing for software developers"_.
    + Another post by Michael Lunch, [How to Make Your Code Reviewer Fall in Love with You](https://mtlynch.io/code-review-love/),
      was mentioned in [Git Rev News Edition #70](https://git.github.io/rev_news/2020/12/26/edition-70/).
+ [19000 curl commits](https://daniel.haxx.se/blog/2025/03/14/19000-curl-commits/)
  by Daniel Stenberg on his blog, presenting some statistics about those commits.
+ [Why fastDOOM is fast](https://fabiensanglard.net/fastdoom/index.html)
  by Fabien Sanglard, examines FastDOOM performance evolution over time,
  doing some nice Git archeology.
+ [Personal Agency With Git Time Logging](https://doocot.sh/blog/2025/03/28/time-tracking-with-git)
  by Doug Bridgens on doocot blog.  The `commit-msg` and `pre-push` hooks from
  [git-time-hooks](https://github.com/thisdougb/git-time-hooks) are used to measure time spans
  from creating a new branch to merging that branch.
+ [git bisect …](https://theweeklychallenge.org/blog/git-bisect/)
  by Mohammad Sajid Anwar (MANWAR) on The Weekly Challenge blog.
  The blog post shows how to use `git bisect` on a detailed example (in Perl).
+ [Python monorepo with uv and pex](https://chrismati.cz/posts/uv-pex-monorepo/)
  by Christoph Pröschel on his blog.  The solution of using regular Python tooling
  over, for example, the [Pants](https://www.pantsbuild.org/) build tool,
  because it was easier to justify its adoption for the rest of the team.
    + You can find a definition of "monorepo" and a list of various tools on the [Monorepo.tools](https://monorepo.tools/) site,
      which was first mentioned in [Git Rev News Edition #84](https://git.github.io/rev_news/2022/02/28/edition-84/).
+ [TIL: Hugo's GitInfo](https://blog.erethon.com/log/2025-03-03-hugo-git-info/)
  by Dionysis Grigoropoulos, about the [GitInfo](https://gohugo.io/methods/page/gitinfo/) method
  of [Hugo](https://gohugo.io/), the static site generator
  in Go. The method returns Git information related to the
  last commit of the given page.
+ [GitHub meets GitLab](https://theweeklychallenge.org/blog/github-meets-gitlab/)
  by Mohammad Sajid Anwar (MANWAR) on The Weekly Challenge blog,
  about the terminology differences between GitHub and GitLab
  (part of the learning process to pick up GitLab).
+ [Comparing Git Mirror Options](https://www.lloydatkinson.net/posts/2025/comparing-git-mirror-options/):
  by Lloyd Atkinson on his blog.
  The tools considered include gitweb, cgit, and Forgejo;
  the last option (Forgejo) was ultimately selected.
+ [Migrating git.adyxax.org from gitolite and cgit to Forgejo](https://www.adyxax.org/blog/2025/03/25/migrating-git.adyxax.org-from-gitolite-and-cgit-to-forgejo/):
  How I am deploying [Forgejo](https://forgejo.org/) with [Ansible](https://www.ansible.com/).
  By Julien (Adyxax) Dessaux on his blog.
+ [Learn Git through Gamification – A Visual Guide to Key Version Control Concepts](https://www.freecodecamp.org/news/learn-git-through-gamification)
  by Jacob Stopak on freeCodeCamp.
+ [4 reasons you need to run a Git server on your NAS (even if you're not a developer)](https://www.xda-developers.com/reasons-run-git-server-nas/)
  by Adam Conway on XDA Developers.
+ [Manage DNS Records with GitHub Actions and DNSControl](https://runtimeterror.dev/manage-dns-records-github-actions-dnscontrol)
  by John Wq on [runtimeerror] blog.
+ [WSL SSH agent and Git](https://www.patriktrefil.com/posts/wsl_ssh_agent_and_git/)
  by Patrik Trefil (2024) on his blog.
  This article describes how you can avoid the hassle of copying and pasting your SSH passphrase
  every time you want to connect to a machine via ssh.
+ [Accessing git Servers Over Another Port When 22 is Blocked and Cloning Hangs Waiting for Connection](https://jdsalaro.com/howto/fix-git-hang-connection-blocked-port-22-github-gitlab-bitbucket/)
  by Jayson Salazar Rodriguez (2024) on his site.
+ [Automatic Versioning with Xcode and Git](https://blog.reiterate.app/software/2024/07/09/automatic-versioning-with-xcode-and-git/)
  by Rat Troupe on Reiterations blog (2024).
+ [Version controlling Jenkins config](https://scripter.co/version-controlling-jenkins-config)
  by Kaushal Modi (2022) on A Scripter's Notes;
  mentions `jenkins-plugin-cli` from [Plugin Installation Manager Tool for Jenkins](https://github.com/jenkinsci/plugin-installation-manager-tool).
    + Compare [How to use the Jenkins Git Plugin: Tips and tricks](https://www.theserverside.com/video/Tips-and-tricks-on-how-to-use-Jenkins-Git-Plugin)
      by Cameron McKenzie from [Git Rev News Edition #44](https://git.github.io/rev_news/2018/10/24/edition-44/),
      about [Git | Jenkins Plugin](https://plugins.jenkins.io/git/).
+ [Using Git Delta with Magit](https://scripter.co/using-git-delta-with-magit/)
  by Kaushal Modi (2022) on A Scripter's Notes.
    + [Delta](https://github.com/dandavison/delta) is a highly configurable command line utility
      that makes the git diffs look better, while also syntax-highlighting the code in the diffs.
      First mentioned in [Git Rev News Edition #86](https://git.github.io/rev_news/2022/04/30/edition-86/).
    + [Magit](https://magit.vc/) is a popular Emacs interface to Git,
      first mentioned (in passing) in [Git Rev News Edition #6](https://git.github.io/rev_news/2015/08/05/edition-6/).
+ [How to Proxy Git Connections: using socat to ...Git... through a corporate firewall](https://bryanbrattlof.com/how-to-proxy-git-connections/)
  by Bryan Brattlof (2022) on his blog.
+ [Git aliases supporting main and master: How to make your aliases agnostic to the default branch](https://phili.pe/posts/git-aliases-supporting-main-and-master/)
  by Philipe Fatio (2022) on his blog.
+ [Keeping ‘live‘ dotfiles in a Git repo](https://probablerobot.net/2021/05/keeping-'live'-dotfiles-in-a-git-repo/)
  by creating a repository directory named `.dotfiles/` rather than `.git/` via the `--git-dir` Git wrapper option.
  From <https://probablerobot.net/> (2021).
+ [On mainline merges and fast forwards](https://vcscompare.blogspot.com/2008/06/on-mainline-merges-and-fast-forwards.html)
  by aoeuo (2008) on the Blogger-based DVCS Comparison blog.
  Compares Bazaar with Git and Mercurial.

+ [GPLv2 is not impressed by git](https://www.thomas-huehn.com/gplv2-is-not-impressed-by-git/)
  by Thomas Huehn on his Bear-powered blog, a short musing about the following phrase from the license:
  > You must cause the modified files to carry prominent notices stating that you changed the files and the date of any change.
+ [I found commit 0](https://programming.dev/post/27187038)
  (or rather a commit whose SHA-1 identifier begins with 0000000),
  by Kissaki on the programming\.dev Lemmy instance.<br>
  [Lemmy](https://join-lemmy.org/docs/index.html) is a self-hosted, federated social link aggregation and discussion forum,
  somewhat similar to Reddit.
    + Note that there are tools like [git-vain](https://git.anna.lgbt/anna/git-vain)
      and [git-vanity-sha](https://github.com/mattbaker/git-vanity-sha),
      most recently listed in [Git Rev News Edition #103](https://git.github.io/rev_news/2023/09/30/edition-103/),
      which can be used to make the SHA-1 hash of a commit start with a specific pattern, like `000000`,
      by manipulating the commit date or message.


<!---
__Easy watching__
-->

__Git tools and sites__

+ [git-who](https://github.com/sinclairtarget/git-who) is a command-line tool for finding
  the people responsible for entire components or subsystems in a codebase.
  You can think of `git-who` as a sort of `git blame` but for file trees rather than individual files.
  Written in Go under MIT license.
+ [chrondb](https://chrondb.moclojer.com/) ([repo](https://github.com/moclojer/chrondb))
  is a chronological key/value database,
  where storing data is based on database-shaped `git` (core) architecture and Lucene for indexing.
  Written in Clojure, uses MIT license.
+ [Calendar.txt](https://terokarvinen.com/2021/calendar-txt/) is a solution
  to keep your calendar in a plain text file.
  One of its advantages is that it is versionable: because it's plain text, you can keep it in Git.
  You can also easily take diffs of calendar files, as it's one day one line.
    + See also [Todo.txt](http://todotxt.org/) to keep your TODO list in a plain text file,
      and tools like [Taskwarrior](https://taskwarrior.org/), and
      [Plain Text Accounting (PTA)](https://plaintextaccounting.org/).
+ [YSK there are open-source (gamified) tutorials to learn git](https://programming.dev/post/26285997)
  provides a list of some tutorials and interactive learning tools, including:
    + [Oh My Git!](https://ohmygit.org/), an open source game about learning Git,
      first mentioned in [Git Rev News Edition #72](https://git.github.io/rev_news/2021/02/27/edition-72/).
    + [Learn Git Branching](http://learngitbranching.js.org/), visual and interactive way to learn Git on the web,
      first mentioned in [Git Rev News Edition #30](https://git.github.io/rev_news/2017/08/16/edition-30/).
    + [Git Gud: Master Git Through Play](https://www.gitmastery.me/), a modern website
      to learn Git commands and concepts through an interactive game.
    + [Git+ Coach](https://github.com/vishal2376/git-coach), a free education app
      designed to help users learn Git and its commands.  Written in Kotlin, for Android.
    + [Git-it](https://github.com/jlord/git-it-electron) is a desktop (Mac, Windows and Linux) Electron app
      that teaches you how to use Git and GitHub on the command line.
      First mentioned in [Git Rev News Edition #7](https://git.github.io/rev_news/2015/09/09/edition-7/)
+ [BeanHub](https://beanhub.io/) is a modern accounting book app
  based on the most popular open source version control system Git
  and the text-based double entry accounting book software [Beancount](https://beancount.github.io/docs/index.html).
  [Mostly open-sourced](https://beanhub.io/open-source/).  See also the following posts by Fang-Pen Lin:
    + [My Beancount books are 95% automatic after 3 years](https://fangpenlin.com/posts/2024/12/30/my-beancount-books-are-95-percent-automatic/).
    + [How BeanHub works part 1: the danger of processing Beancount data with sandbox](https://beanhub.io/blog/2024/04/23/how-beanhub-works-part1-sandboxing/).
    + [How BeanHub works part 2: large-scale auditable Git repository system based on container layers](https://beanhub.io/blog/2024/06/26/how-beanhub-works-part2-layer-based-git-repos/).
      


## Releases

+ Git [2.49.0](https://public-inbox.org/git/xmqqfrjfilc8.fsf@gitster.g/),
[2.49.0-rc2](https://public-inbox.org/git/xmqq34fk958s.fsf@gitster.g/),
[2.49.0-rc1](https://public-inbox.org/git/xmqqjz94r8p0.fsf@gitster.g/)
+ Git for Windows [2.49.0(1)](https://github.com/git-for-windows/git/releases/tag/v2.49.0.windows.1),
[2.49.0-rc2(1)](https://github.com/git-for-windows/git/releases/tag/v2.49.0-rc2.windows.1),
[2.49.0-rc1(1)](https://github.com/git-for-windows/git/releases/tag/v2.49.0-rc1.windows.1)
+ Gerrit Code Review [3.10.5](https://www.gerritcodereview.com/3.10.html#3105),
[3.11.2](https://www.gerritcodereview.com/3.11.html#3112),
[3.9.10](https://www.gerritcodereview.com/3.9.html#3910)
+ GitLab [17.10.1, 17.9.3, 17.8.6](https://about.gitlab.com/releases/2025/03/26/patch-release-gitlab-17-10-1-released/),
[17.10](https://about.gitlab.com/releases/2025/03/20/gitlab-17-10-released/),
[17.9.2, 17.8.5, 17.7.7](https://about.gitlab.com/releases/2025/03/12/patch-release-gitlab-17-9-2-released/)
+ GitHub Enterprise [3.16.1](https://help.github.com/enterprise-server@3.16/admin/release-notes#3.16.1),
[3.15.5](https://help.github.com/enterprise-server@3.15/admin/release-notes#3.15.5),
[3.14.10](https://help.github.com/enterprise-server@3.14/admin/release-notes#3.14.10),
[3.13.13](https://help.github.com/enterprise-server@3.13/admin/release-notes#3.13.13),
[3.12.17](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.17),
[3.16.0](https://help.github.com/enterprise-server@3.16/admin/release-notes#3.16.0),
[3.15.4](https://help.github.com/enterprise-server@3.15/admin/release-notes#3.15.4),
[3.14.9](https://help.github.com/enterprise-server@3.14/admin/release-notes#3.14.9),
[3.13.12](https://help.github.com/enterprise-server@3.13/admin/release-notes#3.13.12),
[3.12.16](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.16)
+ GitKraken [11.0.0](https://help.gitkraken.com/gitkraken-client/current/),
[10.8.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.4.18](https://desktop.github.com/release-notes/)
+ GitButler [0.14.14](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.14.14),
[0.14.13](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.14.13)
+ git-credential-azure [0.3.1](https://github.com/hickford/git-credential-azure/releases/tag/v0.3.1)
+ git-credential-oauth [0.15.0](https://github.com/hickford/git-credential-oauth/releases/tag/v0.15.0)
+ Tower for Mac [12.6](https://www.git-tower.com/release-notes/mac?show_tab=release-notes)
+ Tower for Windows [9.0](https://www.git-tower.com/release-notes/windows) ([Release blog post](https://www.git-tower.com/blog/tower-windows-9/))

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Peter Krefting and Štěpán Němec.
