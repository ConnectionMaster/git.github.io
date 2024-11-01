---
title: Git Rev News Edition 116 (October 31st, 2024)
layout: default
date: 2024-10-31 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 116 (October 31st, 2024)

Welcome to the 116th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of September and October 2024.

## Discussions

<!---
### General
-->

<!---
### Reviews
-->

### Support

* [fatal from `submodule status --recursive` when used with `grep -q`](https://lore.kernel.org/git/CAKDm0rNaHbzoiPg=DeuCoxzooNAsxw2BJfc0wg7fC_-=o9uJ7w@mail.gmail.com/)

  Matt Liberty reported that when he tried using
  `git submodule status --recursive | grep -q "^+"` on a repo with
  a submodule, he got an error message like "fatal: failed to recurse
  into submodule XXX", where XXX is the name of the submodule.

  He expected no error message, no output and a 0 exit code from the
  whole command line as it should have succeeded. He guessed that Git
  didn't like that `grep` when used with `-q` exits immediately
  (without printing anything) when there is a match.

  Phillip Wood replied to Matt saying he assumed that `grep`'s exit
  broke the pipe between `git` and `grep`, so `git` received a
  `SIGPIPE` signal which killed it. Phillip suggested consuming the
  whole output from Git if the exit code from it was wanted.

  Matt replied to Phillip that he was interested in the exit code from
  `grep`, not from `git`, and that Git shouldn't output any error when
  its output is connected to a pipe that gets broken, in the same way
  as the `yes` command, for example, doesn't output any error when
  piped to `grep -q y`.

  Junio Hamano, the Git maintainer, also replied to Phillip's first
  message that the error Git emitted in such a case wasn't useful to
  the user.

  Matt replied to Junio that he thought no error at all should be
  emitted as most Unix tools don't output any error.

  Then Phillip replied to Matt's first reply to him. He asked if all
  Matt wanted was that `git submodule status` did not print any error
  message when it receives a `SIGPIPE` signal. Matt replied that he
  wanted both no error message and a 0 exit code from it.

  Junio replied to Matt that it was reasonable to ask for no error
  message, but it should be OK if the exit code was related to the
  `SIGPIPE` message that the Git command received and that killed
  it. Junio used the example that even `yes` exited with code 130 when
  killed using the Control-C keys on a terminal.

  The exit code associated with a signal is '128 + the signal number',
  for example as the Control-C keys send a `SIGINT` signal, whose signal
  number is 2, processes killed this way should exit with code '128 + 2',
  so 130.

  Eric Sunshine replied to Junio that it wasn't clear how the exit
  code from Git was important in the discussion as in the original
  command line, Git appears before the pipe, so its exit code might be
  lost.

  Matt replied to Eric that the exit code mattered if the `pipefail`
  shell option was used.

  Phillip replied to Matt suggesting he remap the exit code
  associated with `SIGPIPE`, which is 141 (128 + 13), to 0, if he was
  using `pipefail` but still wanted a 0 exit code. Phillip also gave
  an example shell function to help with that remapping, and sent
  [a first version of a patch](https://lore.kernel.org/git/pull.1799.git.1726837642511.gitgitgadget@gmail.com/)
  to fix the error message.

  Junio reviewed that patch and found that it was unnecessarily
  including the "signal.h" system header.

  Phillip fixed that issue in
  [version 2 of the patch](https://lore.kernel.org/git/pull.1799.v2.git.1726925150113.gitgitgadget@gmail.com/)
  which was merged and part of Git v2.47.0.


## Developer Spotlight: Chandra Pratap

_Editor's note: Just like in our previous edition, we return with another
 GSoC retrospective interview in this issue. We hope the reflections shared
 by GSoC students will provide an insightful perspective that benefits
 the community. As always, we welcome your thoughts and feedback!_

* Who are you and what do you do?

  Hey! I am Chandra Pratap (prefer going by Chand) and I am an
  undergraduate student of Mathematics at SVNIT, Surat, India. I have
  a passion for everything computing and like to solve leetcode-styled
  problems in my free time or contribute to open-source software.

* How did you initially become interested in contributing to Git, and
  what motivated you to choose it as your GSoC project?

  C was the first programming language that I learnt, and I wanted to
  try working on a non-trivial software project. I watched a YouTube
  video on open source and that’s where I got the idea of looking for
  open-source projects to contribute to. Git and VLC were the only
  open-source C-written software that I was familiar with and used in
  day-to-day life, so I decided to start contributing to Git out of the two.
  By the time GSoC came around, Git was the only open-source
  community that I was familiar with, so I decided to choose it as my
  GSoC organization.

* How do you feel your contribution has impacted the Git community
  or the broader open-source ecosystem?

  [My project](https://summerofcode.withgoogle.com/programs/2024/projects/tlh611d7)
  was about moving and improving reftable tests, so I think
  my contributions made life somewhat easier for other Git hackers,
  especially those who frequent the reftable sub-project. My project
  didn’t really affect any user-facing aspect of Git, so I don’t think it had
  a huge impact on the broader open-source ecosystem, besides the
  fact that it gained another lifelong contributor.

* Is there any aspect of Git that you now see differently after having
  contributed to it?

  Everything, to be honest. Working on and with Git for the duration of
  my project completely changed my mental model for the tool. Before
  GSoC, Git was a clunky tool reserved for software development work
  but post-Git, I know the most frequent commands like the back of my
  hand, and I’ve already used Git to version control many of my non-software
  files. I feel like I’ve learnt enough Git to last my entire career.

* How do you balance your contributions with other responsibilities like
  work or school?

  I had summer vacation for the entire duration of GSoC and no other work
  commitments, so I had no problems finding time for my GSoC project.

* Can you share how GSoC helped enhance your technical and non-technical
  skills (like communication, project management, etc.)?

  In terms of technical skills, I think my C and Git skills saw the biggest jump.
  I am a lot more comfortable working with those two tools than when I
  was pre-GSoC. Besides that, I’m a lot less scared of the command line
  now. In terms of non-technical skills, I believe I’ve gotten a lot better at
  composing mails and communicating with other professionals. I’ve learnt
  to write with the right amount of professionalism, so I don’t appear too
  uptight or too lax, the right way to respond to constructive feedback, how
  to time my schedule to fit with others’, especially those living in other
  parts of the globe, and how to ask good questions.

* What was your biggest takeaway or learning from GSoC that you now
  apply regularly in your work?

  I’d say the biggest takeaway from GSoC for me was that it is normal for
  everyone to face difficulties when trying to learn a new codebase, tool, etc,
  or even a different part of the same codebase. It is important to persevere
  and not be afraid of asking questions to achieve the desired results. Other
  than that, I’ve learnt a lot about good practices in software development,
  like appropriately splitting commits and writing good commit messages,
  that I subconsciously incorporate in my work now.

* What was the biggest challenge you faced during your contributions
  to Git, and how did you overcome it?

  The biggest challenge in contributing to Git was the initial phase of
  getting involved. I remember starting out working on a small patch for
  about 2 months with a lot of help from other contributors before it got
  accepted into Git’s upstream. After a few initial contributions, I grew more
  confident and could steadily find things to work on and produce
  acceptable results. The key to overcoming this challenge was to be
  persistent and patient, and not being afraid of asking silly questions.

* Have you thought about mentoring new GSoC students?

  I’m not sure about being a full-on mentor, but I’d love to co-mentor
  any future GSoC student(s) interested in working on the reftable
  project.

* If you could get a team of expert developers to work full time on
  something in Git for a full year, what would it be?

  The [Git GUI](https://git-scm.com/docs/git-gui) tool. I believe that
  would make Git far more accessible than it currently is and get it
  incorporated in a lot more people’s day-to-day works.

* If you could remove something from Git without worrying about
  backwards compatibility, what would it be?

  The packed-refs format for refs seems redundant to me now that
  reftable is a core part of Git.

* What is your favourite Git-related tool/library, outside of Git itself?

  [GitGitGadget](https://gitgitgadget.github.io/) was a lifesaver when
  I had just started contributing to Git, so that is probably my favourite
  Git related tool.

* What is your toolbox for interacting with the mailing list and for
  development of Git?

  I used Git’s `send-email` to send patches to the mailing list (especially
  the `--compose` and `--annotate` flags) and Gmail’s online client to
  convey non-patch mails. For developing Git, I used Vim as the editor
  on an Ubuntu machine and Git as the version control software (duh).

* How do you envision your own involvement with Git or other
  open-source projects in the future?

  I plan on making small contributions to Git from time to time, since I
  cannot find enough time for larger patches. Other than that, I’ll try to
  volunteer as a Git mentor for future GSoC or Outreachy cohorts.
  Regarding other open-source projects, I’ll try contributing to them when
  I learn a new technology and want a real-world experience.

* What is your advice for people who want to start Git development?
  Where and how should they start?

  Go through Git’s [‘My First Contribution tutorial’](https://git-scm.com/docs/MyFirstContribution)
  for the initial setup and to get an idea of what’s it like
  to work on Git. Then work on a few ‘microprojects’ ([more information on
  the Git Developer's website](https://git.github.io/General-Microproject-Information/))
  to dip your toes in the Git Development community. From there, you
  can figure out interesting stuff to work on by yourself.

* Would you recommend other students or contributors to participate in
  the GSoC, or other mentoring programs, working on Git? Why? Do you
  have advice for them?

  Yes. I believe that Git is a tool that every working professional can find
  useful regardless of whether they work in the software industry or not,
  and working on Git through an open-source program is an excellent way
  to get good at it in a short period of time. There’s also the added benefit
  of joining a large and active community of amazingly experienced
  developers who can teach you a lot about writing software, and the
  software development workflow in general.

  I think the key to getting selected as a participant in GSoC or other
  mentoring programs is getting involved as early as possible. The more
  time you allow yourself to get familiar with Git’s codebase and
  development workflow, the easier it becomes to find an apt project and
  write a reasonable proposal for it. Also, the initial phase of contributions is
  the most difficult part of getting involved with an open-source project, so it
  is better to allow yourself ample time to tackle that initial hurdle.


## Other News

__Various__
+ [Highlights from Git 2.47](https://github.blog/open-source/git/highlights-from-git-2-47/)
  by Taylor Blau on GitHub Blog.  Includes features like incremental multi-pack indexes,
  `%(is-base:)` atom for `git for-each-ref`, the new
  “[Platform Support Policy](https://github.com/git/git/blob/v2.47.0/Documentation/technical/platform-support.txt)” document,
  `git mergetool` directly supporting Visual Studio Code merge tool, and others.
+ [What's new in Git 2.47.0?](https://about.gitlab.com/blog/2024/10/07/whats-new-in-git-2-47-0/)
  by Justin Tobler on GitLab Blog.  Highlights include
  `init.defaultRefFormat` configuration option that can be set to use `reftable` backend
  (see [Beginner's guide to the Git reftable format](https://about.gitlab.com/blog/2024/05/30/a-beginners-guide-to-the-git-reftable-format/)),
  `init.defaultObjectFormat` configuration option that can be set to `sha256`,
  `git refs verify`, and others.
+ Tower is running a [Git GUIs User's Survey](https://gittower.typeform.com/git-survey)
  for people who do not 100% of the time use Git in the terminal.


__Light reading__
+ [How Typefully Uses Tower [Git GUI Client] to Conquer Social Media Publishing](https://www.git-tower.com/blog/how-typefully-uses-tower)
  by Bruno Brito on Tower Blog.
+ [Moving all our Python code to a monorepo: pytendi](https://attendi.nl/moving-all-our-python-code-to-a-monorepo-pytendi/).
+ [Bruno — An API Client Using Git to Fight for Developer Experience](https://www.git-tower.com/blog/bruno-api-client-using-git/)
  by Ryan Reynolds on Tower Blog.
+ [Using Git as Your Personal To-Do List](https://dev.to/munemprionto/using-git-as-your-personal-to-do-list-3kkd)
  by Munem Prionto on DEV\.to - more as a way of learning Git by the way of managing
  a TODO list, rather than for practical reasons.
    + Contrast with [Using Git to Manage Todos](https://jezenthomas.com/2015/10/using-git-to-manage-todos/
      by Jezen Thomas (2015), mentioned in [Git Rev News Edition #9](https://git.github.io/rev_news/2015/11/11/edition-9/),
      which is about using Git to help manage TODO or FIXME comments in the codebase
      (assuming that for example your IDE does not have a plugin for managing TODOs).
    + One can also consider using a CLI tool that stores data in plain text files
      for managing TODOs, like [Taskwarrior](https://taskwarrior.org/).  Plain text
      files work well with Git.

+ [Python PGP proposal poses packaging puzzles](https://lwn.net/Articles/993787/)
  by Joe Brockmeier on LWN\.net - [Sigstore](https://docs.sigstore.dev/) vs [OpenPGP](https://www.openpgp.org/).
  Sigstore was mentioned in [Git Rev News Edition #91](https://git.github.io/rev_news/2022/09/30/edition-91/)
  and [#111](https://git.github.io/rev_news/2024/05/31/edition-111/).
+ [A look at the aerc mail client](https://lwn.net/Articles/993498/)
  by Joe Brockmeier on LWN\.net.

+ [Git For Each Ref](https://alchemists.io/articles/git_for_each_ref) by Brooke Kuhlmann. Learn how
  to use this command to make use of references for information dumping, statistcs, and much more. Included in this article is use of the new `is-base` field name recently added in link:https://raw.githubusercontent.com/git/git/master/Documentation/RelNotes/2.47.0.txt[Git 2.47.0].

+ [Searching for and navigating Git commits](https://alexharri.com/blog/searching-and-navigating-git-commits)
  by Alex Harri.
+ [Why some of us like "interdiff" code review](https://gist.github.com/thoughtpolice/9c45287550a56b2047c6311fbadebed2)
  by Austin Seipp.
+ [How I Review GitHub PRs](https://www.bitquabit.com/post/how-i-do-github-prs/)
  by Benjamin Pollack.

<!---
__Easy watching__
-->

__Scientific papers__
+ Tsukasa Yagi, Shinpei Hayashi: _"Toward Interactive Optimization of Source Code Differences:
  An Empirical Study of Its Performance"_,
  [arXiv:2409.13590]((https://arxiv.org/abs/2409.13590)),
  with dataset at <https://doi.org/10.5281/zenodo.13618978> (but no source code).
    + based on a prior study:
      Nugroho, et al.: _"How different are different diff algorithms in Git?:
      Use --histogram for code changes"_ (2019),
      <https://doi.org/10.1007/s10664-019-09772-z>

__Git tools and sites__
+ [Reviewing git contributions via email](https://git-am.io/) (<https://git-am.io/>)
  is a companion piece to [interactive guide on sending patches with git send-email](https://git-send-email.io/)
  (<https://git-send-email.io/>); the latter was mentioned in
  [Git Rev News Edition #50](https://git.github.io/rev_news/2019/04/26/edition-50/)
  [#68](https://git.github.io/rev_news/2020/10/30/edition-68/), and
  [#92](https://git.github.io/rev_news/2022/10/26/edition-92/).
+ ["Data Management" section of Awesome MLOps](https://github.com/kelvins/awesome-mlops#data-management)
  also includes tools related to versioning data like
    + [Dolt](https://github.com/dolthub/dolt) ([Git Rev News #62](https://git.github.io/rev_news/2020/04/23/edition-62/)),
    + [DVC](https://dvc.org/) (first mentioned in [Git Rev News #42](https://git.github.io/rev_news/2018/08/22/edition-42/),
      then in [#63](https://git.github.io/rev_news/2020/05/28/edition-63/),
      [#64](https://git.github.io/rev_news/2020/06/25/edition-64/),
      [#100](https://git.github.io/rev_news/2023/06/30/edition-100/),
      [#107](https://git.github.io/rev_news/2024/01/31/edition-107/), and
      [#113](https://git.github.io/rev_news/2024/07/31/edition-113/),
      among others),
    + [Dud](https://kevin-hanselman.github.io/dud/), improving on DVC, but with narrowed scope,
    + [Intake](https://intake.readthedocs.io/) ([Git Rev News #96](https://git.github.io/rev_news/2023/02/28/edition-96/)),
        + See also the discussion in issue #337 in the Intake repository:
          [Data versioning/validation: Comparing Intake with DVC, Quilt and Great Expectations](https://github.com/intake/intake/issues/337)
    + [lakeFS](https://lakefs.io/) ([Git Rev News #78](https://git.github.io/rev_news/2021/08/31/edition-78/)),
    + [Quilt](https://www.quiltdata.com/) / [Quilt Data](https://www.quiltdata.com/)
      ([Git Rev News #99](https://git.github.io/rev_news/2023/05/31/edition-99/)).
+ [git-task](https://github.com/jhspetersson/git-task) is
  a local-first task manager/bug tracker that stores everything within your git repository,
  and which can sync issues to/from GitHub or GitLab.
  Written in Rust, under MIT license.
+ [Bruno](https://www.usebruno.com/) is a fast and Git-friendly open-source API client,
  similar to Postman, Insomnia and similar tools.  It stores collections directly
  in a folder on your filesystem in a plain text markup language, Bru.
    + Compare with [Simple Web Application Test (SWAT)](https://github.com/melezhik/swat),
      web application oriented testing framework, with test plan stored as plain text files
      in specially named directories.

## Releases

+ Git [2.47.0](https://public-inbox.org/git/xmqqa5fg9bsz.fsf@gitster.g/),
[2.47.0-rc1](https://public-inbox.org/git/xmqqploiphj3.fsf@gitster.g/)
+ Git for Windows [2.47.0(2)](https://github.com/git-for-windows/git/releases/tag/v2.47.0.windows.2),
[2.47.0(1)](https://github.com/git-for-windows/git/releases/tag/v2.47.0.windows.1),
[2.47.0-rc1(1)](https://github.com/git-for-windows/git/releases/tag/v2.47.0-rc1.windows.1)
+ libgit2 [1.8.3](https://github.com/libgit2/libgit2/releases/tag/v1.8.3)
+ GitLab [17.5.1, 17.4.3, 17.3.6](https://about.gitlab.com/releases/2024/10/23/patch-release-gitlab-17-5-1-released/),
[17.5](https://about.gitlab.com/releases/2024/10/17/gitlab-17-5-released/),
[17.4.2, 17.3.5, 17.2.9](https://about.gitlab.com/releases/2024/10/09/patch-release-gitlab-17-4-2-released/)
+ Gerrit Code Review [3.10.2](https://www.gerritcodereview.com/3.10.html#3102),
[3.8.9](https://www.gerritcodereview.com/3.8.html#389),
[3.9.7](https://www.gerritcodereview.com/3.9.html#397)
+ GitHub Enterprise [3.14.2](https://help.github.com/enterprise-server@3.14/admin/release-notes#3.14.2),
[3.13.5](https://help.github.com/enterprise-server@3.13/admin/release-notes#3.13.5),
[3.12.10](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.10),
[3.11.16](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.16)
+ GitKraken [10.4.1](https://help.gitkraken.com/gitkraken-client/current/),
[10.4.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.4.8](https://desktop.github.com/release-notes/),
[3.4.7](https://desktop.github.com/release-notes/),
[3.4.6](https://desktop.github.com/release-notes/)
+ Garden [1.9.0](https://github.com/garden-rs/garden/releases/tag/v1.9.0),
[1.8.0](https://github.com/garden-rs/garden/releases/tag/v1.8.0)
+ GitButler [0.13.7](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.13.7),
[0.13.6](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.13.6)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Brandon Pugh.
