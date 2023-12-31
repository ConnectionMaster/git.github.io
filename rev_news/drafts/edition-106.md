---
title: Git Rev News Edition 106 (December 31th, 2023)
layout: default
date: 2023-12-31 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 106 (December 31th, 2023)

Welcome to the 106th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of November and December 2023.

## Discussions

<!---
### General
-->

### Reviews

+ [[PATCH 0/4] Switch links to https](https://lore.kernel.org/git/pull.1589.git.1695392027.gitgitgadget@gmail.com/)

  In September, Josh Soref had posted a 4 patch long series on the
  mailing list to improve the URLs used throughout the documentation
  and the code base of the project.

  The main goal was to use HTTPS instead of HTTP in the URLs to
  improve user security, but along the way some patches replaced URLs
  that didn't work anymore with some new ones pointing to the same
  content.

  Eric Sunshine replied to Josh's patches asking why one URL was
  changed from `http://json.org/` to `https://www.json.org/` instead
  of just replacing `http` with `https`. Josh replied that it was
  because that website was self-identifying with the later URL using a
  [meta refresh](https://en.wikipedia.org/wiki/Meta_refresh).

  In the meantime, Junio Hamano, the Git maintainer, replied to some
  patches saying that it might not be worth updating some URLs, either
  because it was clear from the context that they were old, or because
  they were part of some code we borrowed from other projects. In some
  cases, they were an argument of a Git command and still just worked,
  while the meaning of the command changed a bit when `http` was
  replaced with `https`. Junio liked the fact that some broken links
  were fixed by the series though.

  Josh then sent a
  [version 2 of his patch series](https://lore.kernel.org/git/pull.1589.v2.git.1695553041.gitgitgadget@gmail.com/).
  This took into account Eric's comments as a commit message was
  improved to say that some changes were made to respect a site's
  self-identification. Junio's comments were also taken into account
  as a number of URLs that were previously changed were now left
  as-is.

  Elijah Newren and Junio commented on this new version. They both
  suggested improving commit messages or the cover letter of the
  series to better explain the reasons for the changes that were made.
  In one case, Elijah and Josh discussed replacing the URL of a
  website that seemed to be often down with a link to its content on
  the [Internet Archive](https://archive.org/).

  In November, Josh then sent a
  [version 3 of his patch series](https://lore.kernel.org/git/pull.1589.v3.git.1700796916.gitgitgadget@gmail.com/)
  where the first and second patches had been swapped to avoid some
  confusion for reviewers who would ask why some URLs weren't changed
  in the first patch overlooking that the second one would change them.

  The other significant change compared to version 2 was that Josh
  decided not to replace the URL of the website that was often down
  saying "we'll risk users getting hacked content from an arbitrary
  [MITM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)
  instead of taking archived authenticated content based on the last
  time their web site was properly maintained".

  Elijah replied that he would be fine with using the archived link if
  it was better justified in the commit message, but said that he also
  agreed with merging the whole series as-is, as he had checked all
  the links and they all looked good to him.

  Josh replied he could come back later to change the URL and preferred
  the series to be merged as-is. He thanked Elijah for taking the time
  to re-check every link, saying he knew exactly how tedious that is.

  Junio agreed with merging the series, which is now part of the
  'master' branch.

<!---
### Support
-->

## Community Spotlight: VonC

_[VonC](https://stackoverflow.com/users/6309/vonc) is a
prolific contributor to the Git topic on Stack Overflow. This edition features an
    interview with him. Thanks to our [survey respondents](https://git.github.io/rev_news/2023/06/30/edition-100#some-statistics-about-the-ongoing-first-git-rev-news-readers-survey)
for suggesting to interview, VonC!_

* **Who are you and what do you do?**

  By day, I am an information technology consultant working for a computer services
  company in France. By night, I am [VonC on Stack Overflow](https://stackoverflow.com/users/6309),
  and I have contributed to various topics since its early days (Sept. 2008).
  I do that [every single day](https://meta.stackexchange.com/q/122976/6309).
  It includes answering questions about Git: [almost 16K answer](https://stackoverflow.com/search?q=user:6309+[git])
  in 15 years.

* **What would you name your most important contribution to Git?**

  I do not contribute to Git directly, but I report on Stack Overflow
  any interesting [git/git commits](https://github.com/git/git/commits/master)
  which provides a new answer to old questions.

  I started in 2012 with questions like "[Squash the first two commits in Git?](https://stackoverflow.com/a/598788/6309)"
  and "[How do I remove a submodule?](https://stackoverflow.com/a/16162000/6309)".
  Then [1630](https://stackoverflow.com/search?page=33&tab=Newest&pagesize=50&q=user%3a6309%20%22see%20commit%22&searchOn=3)
  commits followed over the next decade.

* **Why answering questions about Git on Stack Overflow?**

  As I mentioned in "[**How to earn a million reputation on Stack Overflow: be of service to others**](https://stackoverflow.blog/2022/10/09/how-to-earn-a-million-reputation-on-stack-overflow-be-of-service-to-others/)",
  by **[Ryan Donovan](https://twitter.com/RThorDonovan)**, this is a way to
  give back to the community, and to learn in the process.

  I learnt Git itself even before installing it, by answering a few
  questions on Stack Overflow, as I detailed in "[How'd you get started?](https://meta.stackexchange.com/a/367773/6309)".

* **If you could get a team of expert developers to work full-time on something in Git for a full year, what would it be?**

  I mentioned in 2013/2016 the issue of [storing large files in Git repositories](https://stackoverflow.com/a/17897705/6309).

  But nowadays, I would work on the workflow side of Git, and how to make
  it easier to use for beginners. I follow [GitButler](https://docs.gitbutler.com/)
  and [Scott Chacon](https://twitter.com/chacon)'s work.

  > GitButler is rethinking everything between when you write code in your editor of choice and when you push that code to GitHub for review.
  > Why are you making 'wip' commits when your SCM should be recording everything for you?
  > Why are everyone's commit messages close to useless?
  > Why is `git blame` the best way to get context on the code your team has written?
  > Why can't you seamlessly transition work between computers?

* **If you could remove something from Git without worrying about backward compatibility, what would it be?**

  `git checkout`! It is time. As I [explained in 2020](https://stackoverflow.com/questions/58003030/what-is-the-git-restore-command-and-what-is-the-difference-between-git-restor#comment115524702_58003889),
  the `git switch`/`git restore` commands are "[experimental](https://github.com/git/git/commit/4e43b7ff1ea4b6f16b93a432b6718e9ab38749bd)"
  in name only, and are here to stay.


* **What is one of your most favorite features of Git?**

  Coming from CVS/SVN, one of my favorite features of Git is its powerful
  branching and merging capabilities. Branches in Git are lightweight and
  switching between them is fast, making it convenient to manage multiple
  streams of work simultaneously (and you have [`git worktree`](https://stackoverflow.com/a/30185564/6309)
  if you want to preserve your current working tree).

  I use those branches and merges with ["gitworkflow" (one word)](https://stackoverflow.com/a/57175304/6309),
  using long-lived integration branches (like "`master`/`main`/`release`"),
  and "ephemeral" integration branches (like "`public`/`next`/`devel`",
  created for a specific release cycle, then deleted and recreated for the
  next release cycle). See more at "[gitworkflow workflow](https://stackoverflow.com/a/53405887/6309)"
  and "[Handle Git branching for test and production](https://stackoverflow.com/a/44470240/6309)".

* **What is your favorite Git-related tool/library, outside of Git itself?**

  I often used [github.com/github/gitignore](https://github.com/github/gitignore)
  ("**A collection of .gitignore templates**"). I have also used and promoted
  [`git filter-repo`](https://github.com/newren/git-filter-repo), to
  [remove large files from a Git repository](https://stackoverflow.com/a/76300821/6309).

* **Could you brief a bit about one of your most memorable experiences with Git?**

  My first `git clone`.

  As mentioned in "[How to earn a million reputation on Stack Overflow: be of service to others](https://stackoverflow.blog/2022/10/09/how-to-earn-a-million-reputation-on-stack-overflow-be-of-service-to-others/)",
  at the time I stumbled upon Git (2008/2009), I was managing big Rational
  ClearCase repositories of terabytes of data. The idea of cloning a *full* (Git)
  repository on my laptop was... incongruous, to say the least!

  I am aware of the debate around monorepo vs. multirepo (which sometimes
  goes in hand with the debate around monolith vs. microservices), but I found
  in the subsequent years that working with multiple small Git repositories was
  much more manageable than working with a single large one, as I used to do
  before, using huge [ClearCase VOBs](https://www.ibm.com/docs/en/rational-clearcase/9.0.0?topic=clearcase-about-vobs-versioned-objects).

* **What is your advice for people who want to start using Git? Where and how should they start?**

  Start with understanding Git **branching**, and operations around branches
  (switch, merge, rebase, cherry-pick)

  For that, I always redirect people to "[Learn Git Branching](https://learngitbranching.js.org)"
  (`learngitbranching.js.org`): nothing to install, all exercises are done
  directly in the browser, and it is very visual.

  I also discourage people from blindly following the "[Git Branching Model](https://nvie.com/posts/a-successful-git-branching-model/)",
  where an integration branch like `develop` is merged to another integration
  one like `master`. See the links above for "gitworkflow" where I explain
  why one should merge to an integration branch, not from it: merging *from*
  it means you are merging *everything* currently integrated into that branch.
  If you want to "exclude" some of those integrated commits, that becomes a
  nightmare to manage.

* **There's a common conception that "Git is confusing". What are your thoughts about the same?**

  Right... you mean [XKCD 1597, Oct. 2015, "Git"](https://explainxkcd.com/wiki/index.php/1597:_Git).

  The level of integration of Git in IDEs (like Eclipse, IntelliJ, VSCode, ...)
  has made Git more accessible to beginners. I often redirect them to a combo
  VSCode + [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens),
  and that is enough to get them started.

  As long as the workflow is clearly defined, and the rebase is understood,
  for [managing pull request](https://stackoverflow.com/a/44672221/6309)
  (you rebase your local feature branch on top of the target branch,
  before force pushing it to the remote repository, [with lease](https://stackoverflow.com/a/52937476/6309)
  or [if-includes](https://stackoverflow.com/a/64627761/6309)), the users
  manage to get by. The bulk of my training is about the PR (Pull Request)
  workflow, which involves `git rebase` (`--onto`), and
  `git push --force-with-lease `or `--force-if-includes`.

  But clarifying *why* Git exists, and where it comes from (I have younglings
  who have no idea who [Linux Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds)
  is, and his role in the [creation of Git](https://en.wikipedia.org/wiki/Git#History))
  can help. Git comes with a certain vision of how a VCS should work, and
  it has a lot to do with the way the Linux kernel is developed.

* **If there’s one tip you would like to share with other users of Git, what would it be?**

  Stop using `git checkout`, start using `git switch`/`git restore` instead!

_Editor's note: We hope you enjoyed this interview. We'll explore if we could
interview other such contributors who don't directly participate in the mailing
list. If you have any suggestions, you're most welcome to share them with us through
[our issue tracker](https://github.com/git/git.github.io/issues) or by writing an
email to &lt;<kaartic.sivaraam@gmail.com>&gt;._

## Other News

__Various__

+ [Google Summer of Code 2024: Contribute to GitLab and Git to prepare](https://about.gitlab.com/blog/2023/12/20/google-summer-of-code-2024-contribute-to-gitlab-and-git-to-prepare/)
  by Christian Couder and Nick Veenhof on GitLab Blog.
+ [Upcoming changes to repository insights [on GitHub]](https://github.blog/changelog/2023-11-29-upcoming-changes-to-repository-insights/)
  on GitHub Blog.
+ [Git platform AllSpice now curries favor with enterprises](https://techcrunch.com/2023/12/05/git-allspice-enterprise-6m/)
  by Christine Hall on TechCrunch.
+ [GitLab Duo Code Suggestions is generally available](https://about.gitlab.com/blog/2023/12/22/gitlab-duo-code-suggestions-is-generally-available/)
  by David DeSanto on GitLab Blog.
  [GitLab Code Suggestions](https://about.gitlab.com/solutions/code-suggestions/)
  is an alternative to [GitHub Copilot](https://github.com/features/copilot)
  and [OpenAI ChatGPT](https://chat.openai.com/) (to a lesser extent).


__Light reading__

+ Julia Evans continues her streak of Git-related blog posts with
  [Mounting git commits as folders with NFS](https://jvns.ca/blog/2023/12/04/mounting-git-commits-as-folders-with-nfs/)
  (and FUSE), about the experimental [git-commit-folders](https://github.com/jvns/git-commit-folders)
  tool.  This tool was mentioned in [previous Git Rev News](https://git.github.io/rev_news/2023/11/30/edition-105/).
+ Julia Evans also published a few comics about Git at [Wizard Zines comics](https://wizardzines.com/comics/),
  for a zine on Git that she is currently writing
  (these are only the most recent ones; some of earlier ones made it into
  [Oh Shit, Git! Recipes for getting out of git mess](https://wizardzines.com/zines/oh-shit-git/) zine):
    + [every git jargon](https://wizardzines.com/comics/every-git-jargon/)
    + [git discussion bingo](https://wizardzines.com/comics/git-discussion-bingo/)
    + [every git command I use](https://wizardzines.com/comics/every-git-command/)
    + [meet the branch](https://wizardzines.com/comics/meet-the-branch/)
    + [branches have no rules](https://wizardzines.com/comics/branches-have-no-rules/)
      (at least no built-in ones, though you can try to enforce some with [git hooks](https://githooks.com/))
    + [`HEAD` and heads](https://wizardzines.com/comics/head-and-heads/)
    + [my rules for rebasing](https://wizardzines.com/comics/rules-for-rebasing/)
+ [Every engineer should understand git reflog](https://graphite.dev/blog/every-engineer-should-understand-git-reflog)
  by Harsh Siriah on Graphite Blog.
+ [Fine-grained file differences](https://www.johndcook.com/blog/2023/12/13/fine-grained-file-differences/)
  by John D. Cook on his blog.
+ [DiffDebugging](https://martinfowler.com/bliki/DiffDebugging.html)
  by Martin Fowler on his blog/wiki.  Page created in 2004, rewritten in 2013.
+ [Monorepo, Poly-repo, or No Repo at all?
   Using Bit to make “irreversible decisions” easy to make and change.](https://blog.bitsrc.io/monorepo-poly-repo-or-no-repo-at-all-830328c7a546)
  by Eden Ella on Bits and Pieces blog.
    + [Bit](https://bit.dev/), a build system for composable software,
      was first mentioned in [Git Rev News Edition #45](https://git.github.io/rev_news/2018/11/21/edition-45/),
      (then at old bitsrc.io URL, instead of current bit.dev URL).
    + It was mentioned again in [Git Rev News Edition #77](https://git.github.io/rev_news/2021/07/31/edition-77/)
      in [How to Collaborate on Components across Projects with Bit](https://dev.to/giteden/how-to-collaborate-on-components-across-projects-with-bit-29c3) by Eden Ella on DEV\.to.
+ [Recovering Deleted Files From Your Git Working Tree](https://www.smashingmagazine.com/2023/12/recovering-deleted-files-git-working-tree/)
  by Oluwasanmi Akande on Smashing Magazine.
+ [Git Grep Like a Pro: The Complete Guide](https://www.kosli.com/blog/git-grep-like-a-pro-the-complete-guide/)
  by Bruce Johnston on Kosli Blog (2022).
+ [Flexible Identities in git](https://belkadan.com/blog/2020/02/Flexible-Identities-in-git/)
  proposal (to avoid "deadnaming", and bury an old name, while preserving link to things done under the old name)
  by Jordan Rose on -dealloc blog (2020).


__Easy watching__

+ [Git From the Bits Up](https://www.youtube.com/watch?v=mdvlu_R8EWE)
  by Tim Berglund, DataStax.  Recorded at [Jfokus](http://www.jfokus.com) 2016.


__Git tools and sites__

+ [dyff](https://github.com/homeport/dyff) /ˈdʏf/ is a diff tool for YAML files,
  and sometimes JSON.  Can be used as Git diff driver (see documentation).
  Written in Go, uses MIT license.
+ [Git-LaTeXdiff](https://gitlab.com/git-latexdiff/git-latexdiff) is a tool
  to graphically visualize differences between different versions of a LaTeX file.
  It is a wrapper around Git and [latexdiff](https://www.ctan.org/pkg/latexdiff)
  (which is present [on CTAN](https://www.ctan.org/pkg/latexdiff), Comprehensive TeX Archive Network).
  `git-latexdiff` is written as BSD-licensed Bash script,
  while `latexdiff` is written in Perl (and is GPLv3 licensed).
  The git-latexdiff tool was mentioned in passing in 
  [Git Rev News Edition #8](https://git.github.io/rev_news/2015/10/14/edition-8/).
+ [git-oops](https://github.com/jvns/git-oops) is a **very experimental** tool
  allowing to undo a Git operation, without having to remember specific invocation.
  In the style of the undo features in [GitUp](https://gitup.co/), [jj](https://github.com/martinvonz/jj), and [git-branchless](https://github.com/arxanas/git-branchless).
  Meant to be just a prototype, to serve _as an inspiration_ for a better tool that actually works reliably.
  Written in Python, MIT license.
    + Contrast [thefuck](https://github.com/nvbn/thefuck), a command line application
      which corrects your previous console command (for example Git command)
      if you made an error and it _didn't_ do what you wanted;
      the tool was mentioned in
      [Git Rev News Edition #101](https://git.github.io/rev_news/2023/07/31/edition-101/).
    + Contrast [git-undo-el](https://github.com/jwiegley/git-undo-el),
      a command for Emacs editor to "undo" changes to selected region of a file
      through its Git history, mentioned in
      [Git Rev News Edition #34](https://git.github.io/rev_news/2017/12/20/edition-34/).
    + One of git-oops inspirations, the [undo command in git-branchless](https://github.com/arxanas/git-branchless/wiki/Command:-git-undo),
      was described in [git undo: We can do better](https://blog.waleedkhan.name/git-undo/),
      which was mentioned in [Git Rev News Edition #76](https://git.github.io/rev_news/2021/06/27/edition-76/).
    + A very basic and limited [Git Undo [alias]](https://megakemp.com/2016/08/25/git-undo/)
      was mentioned in [Git Rev News Edition #19](https://git.github.io/rev_news/2016/09/14/edition-19/)
      (resets state using reflog).
    + Many IDE and programming editors, their Git-related extensions/plugins,
      and Git GUIs have some kind of universal "git undo".  One example is
      Tower Git GUI, which undo abilities are described in
      [CMD+Z for Git is Here](https://css-tricks.com/cmdz-for-git-is-here/)
      (mentioned in [Git Rev News Edition #65](https://git.github.io/rev_news/2020/07/29/edition-65/)).
+ [git-vee](https://github.com/mjdominus/git-util/blob/master/bin/git-vee)
  is a shell script that prepares a brief summary of how your current branch
  has diverged from a corresponding remote branch.  Mentioned on 
  [git-vee](https://www.plover.com/misc/stop-merging/slide019.html) slide
  in [Cleaner `git` history](https://www.plover.com/misc/stop-merging/slide001.html)
  (also known as "Stop merging master") by Mark Jason Dominus (the author of the tool),
  from 2013.
+ [Breezy](https://www.breezy-vcs.org/) is a version control system implemented in Python
  with multi-format support and an emphasis on hackability.
  Currently, Breezy has built-in support for the Git and Bazaar file formats and network protocols.
  GPLv2 licensed.
+ [FlatGitHub](https://flatgithub.com/) or Flat View is a simple tool for exploring
  flat data files in GitHub repositories.
  Implements [Flat Data](https://githubnext.com/projects/flat-data) project (formerly GitHub OCTO),
  mentioned in [Git Rev News Edition #75](https://git.github.io/rev_news/2021/05/27/edition-75/)
  (under old URL) and [Edition #96](https://git.github.io/rev_news/2023/02/28/edition-96/),
  which in turn was based on [“git scraping” approach pioneered by Simon Willison](https://githubnext.com/projects/flat-data),
  mentioned in [Git Rev News Edition #82](https://git.github.io/rev_news/2021/12/30/edition-82/).
  See the example of [flat-demo-bitcoin-price](https://flatgithub.com/githubocto/flat-demo-bitcoin-price?filename=btc-price-postprocessed.json&sha=78b38f641f8f1ffccae733749545ea42cf5eddf9).
+ [AllSpice.io](https://allspice.io/) is a Git platform for hardware developers
  (named after SPICE ("Simulation Program with Integrated Circuit Emphasis"),
  a general-purpose, open-source analog electronic circuit simulator).
  No free tier.
+ [typos](https://github.com/crate-ci/typos) is a source code spell checker,
  which finds and corrects spelling mistakes among source code;
  intended to be fast enough to run on monorepos, and with low false positives
  so you can run on PRs.  Written in Rust.
    + Mentioned in [Perl Advent Calendar 2023 - Elves Versus Typos](https://perladvent.org/2023/2023-12-21.html).
+ [dat](https://github.com/dat-ecosystem/dat) is a tool for peer-to-peer sharing
  & live synchronization of files via command line.  Part of the [dat-ecosystem](dat-ecosystem.org).
  You can use the `dat` command line to share files with version control,
  back up data to servers, browse remote files on demand, and automate long-term data preservation.
  Written in JavaScript for running with Node.js.


## Releases

+ Gerrit Code Review [3.9.1](https://www.gerritcodereview.com/3.9.html#391)
+ GitHub Enterprise [3.11.2](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.2),
[3.11.1](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.1),
[3.10.4](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.4),
[3.9.7](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.7),
[3.8.12](https://help.github.com/enterprise-server@3.8/admin/release-notes#3.8.12),
[3.7.19](https://help.github.com/enterprise-server@3.7/admin/release-notes#3.7.19),
[3.11.0](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.0)
+ GitLab [16.7](https://about.gitlab.com/releases/2023/12/21/gitlab-16-7-released/)
[16.6.2, 16.5.4, 16.4.4](https://about.gitlab.com/releases/2023/12/13/security-release-gitlab-16-6-2-released/),
[16.6.1, 16.5.3, 16.4.3](https://about.gitlab.com/releases/2023/11/30/security-release-gitlab-16-6-1-released/)
+ GitKraken [9.11.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.3.6](https://desktop.github.com/release-notes/)
+ Sourcetree [4.2.6](https://product-downloads.atlassian.com/software/sourcetree/ReleaseNotes/Sourcetree_4.2.6.html)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from VonC.
