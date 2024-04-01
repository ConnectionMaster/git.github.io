---
title: Git Rev News Edition 109 (March 31st, 2024)
layout: default
date: 2024-03-31 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 109 (March 31st, 2024)

Welcome to the 109th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of February and March 2024.

## Discussions

<!---
### General
-->

### Reviews

* [[PATCH] rebase: make warning less passive aggressive](https://lore.kernel.org/git/pull.1669.git.1708442603395.gitgitgadget@gmail.com/)

  Harmen Stoppels sent a patch to the mailing list that changed an
  error message from "No rebase in progress?" to "No rebase in
  progress". The rationale is that this error appears when one runs
  `git rebase --continue` while there is no rebase going on, so there
  is no reason for the question mark.

  Junio Hamano, the Git maintainer, replied to Harmen suggesting using
  the imperative mood in the commit message, and saying that the
  change in itself is good but that the patch shouldn't have touched
  the `po/*.po` files in the project that are used for localization.
  Junio also said that we could later add tests for this as it
  appeared there was none.

  Michal Suchánek replied to Junio saying that it might have been OK
  to touch the `po/*.po` files if the patch had updated the
  translations in those files but it hadn't.

  Junio replied to Michal saying that knowing the target language was
  needed before removing question marks in those files as it might not
  be enough to change a question into a statement. Even if the
  author of the patch knew enough, reviewers of the patch might
  not, but the biggest problem was bypassing the languages teams.

  Michal replied to Junio asking what was the problem "with not
  involving several language teams to remove a question mark".

  Jean-Noël Avila, who is a translator, replied that it didn't bother
  him much to edit a sentence to remove a question mark and possibly
  adjust it, compared to "translating again and again similar
  sentences".

  This led to some confusion as Junio thought that Jean-Noël said that
  the "everything in one patch" approach would help translators by not
  having them translate "again and again". But Jean-Noël clarified
  that he didn't consider changing a question to an assertion is
  translating "again and again". He agreed that it was perfectly fine
  for translators to have to do those kinds of changes. With "again
  and again" he was referring to strings like "could not stat '%s'"
  and then "could not stat file '%s'".

  In the meantime Patrick Steinhardt replied to Harmen's initial
  message. He suggested converting the error message to start with a
  lowercase letter as our guidelines for error messages recommend.

  Harmen, then sent
  [a version 2 of his patch](https://lore.kernel.org/git/pull.1669.v2.git.1708537097448.gitgitgadget@gmail.com/)
  which didn't change any `po/*.po` file and had the error message
  start with a lowercase letter. Patrick reviewed that patch and found
  it good.

  Kristoffer Haugsbakk chimed into the discussion saying he had
  interpreted the original error message as saying "I’m not quite sure
  but it looks like you are not in the middle of a rebase?"

  Junio replied to Kristoffer saying that there are indeed examples of
  "less assertive" messages in the same rebase command, like "It looks
  like 'git am' is in progress. Cannot rebase." But we should be more
  assertive as it could help us get valuable bug reports saying for
  example "The command said I was not rebasing, but I was! Here is
  what I did..." Such bug reports could help us improve how we
  determine the state we are in.

  The version 2 of Harmen's patch was later merged to the 'master'
  branch.

<!---
### Support
-->

## Developer Spotlight: Linus Arver

* Who are you and what do you do?

  I'm one of those so-called "self-taught" developers. My educational
  background is in English and tax law (I know, boring right?). Over a
  decade ago I thought I would be a corporate attorney, but in law
  school I discovered programming and fell completely in love with the
  craft, and never looked back! In hindsight it was the second-best
  decision I've made in life (the first being getting married to my
  lovely wife four years ago).

  I said that I fell into programming during law school. But actually my
  original journey started in 7th grade when I tried to pick up C++. I
  remember learning control flow, structs and pointers in the first few
  chapters of the book I was using, but when it came to the chapter on
  OOP and classes, I could not understand why OOP was necessary.
  The book I was using just explained why OOP was great, and not
  why it would ever be bad.

  Of course, years later I realized that OOP is one of several
  paradigms, so perhaps my instinct to question OOP as a panacea was
  onto something.  In high school and university I remember tinkering
  with HTML and websites before smartphones became popular. What a
  simpler time it was, back then!

  Fast forward to law school, where I had the idea of writing class
  notes using plaintext. Soon after I had the idea of converting these
  plaintext notes to prettified outlines, so I needed a way to convert
  them to HTML. For better or worse, all this happened before I
  discovered Emacs and Orgmode (or even Markdown).

  Anyway, I first wrote a plaintext-to-HTML converter in Ruby. Then I
  rewrote it in C just for fun. Then again in Haskell (using a minimal
  subset of Orgmode syntax). As you can see, I sort of got carried away,
  haha.

  I would go on to write dozens of pet projects (rudimentary chess
  engine, game modding tools, etc) where I got to write tons of code.
  I've had the "ugh, did I really write this?" moment too many times to
  count. I like to believe that I did the tech industry a favor by not
  entering it until I was well versed in fundamental programming and
  architectural concepts. 😉

  Since those law school days I've taken an interest in learning more
  languages/ecosystems (e.g., Elixir and Rust). Recently, I've taken a
  renewed interest in Literate Programming. I'm toying with the idea of
  using it in a somewhat large scale in a future project. It takes a ton
  of work to do LP right, but in many ways it's the best possible way to
  document code (case in point, the absolutely stellar documentation
  standards of the TeX community, such as the glorious TikZ user
  manual).

  And I believe that readability is the most important attribute when it
  comes to code --- even before correctness! Because at least if the
  intent of the author is clear, we can have a (fairly) easy way to fix
  things to make it correct. The other way around (correct, but
  unreadable code) suffers from stagnation because people become afraid
  of touching it, because it's hard to understand. It becomes harder to
  extend and grow, which is required of any software worth maintaining
  (we call it <em>soft</em>ware for a reason).

  Going back to the question (sorry for rambling a bit there), in my
  $DAYJOB I work on microservices, APIs, and backend systems.
  Professionally I've always been a backend/infra engineer. In my spare
  time I contribute to this wonderful community!

* What would you name your most important contribution to Git?

  I would say my contributions to the documentation come out on top.
  At the end of the day, Git is meant for human consumption.
  So getting a bit more polish here and there for user-facing docs is
  well worth the trouble, and I am most proud of my work in this area so
  far.

  If I had more time, I would overhaul the documentation to make things
  easier to understand. Truly, Git has a very simple conceptual model
  (thanks to the brilliance of its original author). You just have to
  understand that commits come from one or more other commits (sort of
  like family trees). That's it! But sadly we have a reputation of
  having absolutely terrible user-facing docs, so much so that it pushed
  people away to Mercurial and other more friendly VCSs. We need to fix
  that.

* What are you doing on the Git project these days, and why?

  Last year I started trying to add unit tests to the (perhaps obscure)
  `git interpret-trailers` command, but this effort has morphed into
  "let's also overhaul the entire subsystem around how trailers are
  handled, with the aim of creating a reusable C library around it"
  [ [ref 1](https://lore.kernel.org/git/pull.1563.git.1691211879.gitgitgadget@gmail.com/) ]
  [ [ref 2](https://lore.kernel.org/git/pull.1632.git.1704869487.gitgitgadget@gmail.com/) ].

  I'm afraid I've bitten off more than I can chew, but I do have a
  backlog of about 60 patches that I need to get sent up for review. Not
  all at once, of course haha. Hopefully I can get these sent up and
  merged over the coming months. The review process can be lengthy you
  see, but for good reason --- we take time to try to make sure things
  are right the first time.

* If you could get a team of expert developers to work full time on
  something in Git for a full year, what would it be?

  At the risk of being unoriginal, it would be libification (see
  [Calvin Wan's interview](https://git.github.io/rev_news/2023/08/31/edition-102/#developer-spotlight-calvin-wan)
  from edition 102). But to be more precise, it would be the complete
  banning of "shelling out" which we do in many places (where Git
  spawns another Git process to do something). Instead we could
  (and should) be using libraries internally inside Git's own codebase.
  I believe that once we can get Git to start treating itself
  as a library, that external library consumption will soon follow.

  There are many others interested in this area as Git has a massive
  footprint in our industry. I hope that the many large companies that
  benefit from Git can grow their roster of Git contributors.

* If you could remove something from Git without worrying about
  backwards compatibility, what would it be?

  `git checkout`. I believe `git switch` and `git restore` replaced the
  need to have `git checkout`. I believe in the "there should be only
  one way to do the right thing" camp when it comes to the CLI, so I don't
  like how we have multiple commands with a lot of overlap.

  I say this even though personally I've been using Git for over 15
  years and have always used `git checkout` (even after the introduction
  of `git {switch,restore}`). Simplicity matters!

* What is your favorite Git-related tool/library, outside of
  Git itself?

  [Tig](https://jonas.github.io/tig/). I use it all the time, every
  day. It's so good that I basically never use `git log`, unless I'm
  searching through it interactively with the pager.

  Every time I see someone proudly showing off their latest "git-log"
  incantation (with all its bells and whistles), I think to myself "I
  guess they've never heard of `tig`".

  Being an Emacs user, I tried to get into [Magit](https://magit.vc/)
  but could not get used to the keybindings that conflicted with my
  Vim-styled bindings. (Yes, I use [Evil](https://github.com/emacs-evil/evil)
  mode via [Doom](https://github.com/doomemacs/doomemacs) Emacs if you're
  into that sort of thing.) OTOH I get so much done with the basic
  `git-*` commands and `tig` that I'm rather happy with my workflow.

* Do you happen to have any memorable experience w.r.t. contributing to
  the Git project? If yes, could you share it with us?

  Nine years ago, I contributed my first patch series. I was so proud of
  this work that I wrote [a blog post](https://funloop.org/post/2014-09-09-my-first-contribution-to-git.html)
  about it.

  The TL;DR of that post is that anyone can contribute to Git, and
  really we are a welcoming community. Junio goes out of his way to
  accommodate new contributors (I admire his patience), so please, feel
  free to join us!

* What is your toolbox for interacting with the mailing list and for
  development of Git?

  So my first contribution 9 years ago was via (the traditional)
  `git send-email` command. These days there is this very neat service
  called [GitGitGadget](https://gitgitgadget.github.io/) that allows
  you to create pull requests on GitHub and does all the housekeeping
  work of keeping mailing list discussions in sync (you'll get comments
  on your PR which come from mailing list responses). Plus you can get
  previews of your patch series (exactly how they'll look like on the
  list) before you submit it, which is always nice.

  For local Git development, honestly I don't do anything special or
  unusual. One window for Emacs, one window for (re)compiling Git and
  running tests, and maybe one more for Tig. From Emacs I use [notmuch](https://wiki.archlinux.org/title/Notmuch)
  to browse the mailing list emails (which I sync to Gmail with
  [lieer](https://github.com/gauteh/lieer)).

  I use Orgmode in Emacs heavily for organizing code snippets and ideas.

  Last but not least, I use [tmux](https://github.com/tmux/tmux/wiki) to organize terminal windows and
  navigate quickly across them, even if I'm not using SSH.

* What is your advice for people who want to start Git development?
  Where and how should they start?

  The hard part is figuring out which area you want to work on. Git has
  a large codebase, so I recommend starting out with documentation
  changes to familiarize yourself with the current state of things.
  There's always a typo or grammofix hiding in there!

  Many of our manpages read like dictionaries, when they should read
  more like user guides. Some manpages have helpful "EXAMPLES" sections
  to show you how to actually use various options and commands, so if
  you can think of additional examples, that would be most welcome.
  Getting familiar with how things work with user-facing docs should
  help you understand the intent behind the large C codebase we have.

  Try to make your contributions as small as possible, but make an
  effort to write good commit messages. Copy the style of veterans like
  Junio, Peff (Jeff King), Christian Couder, and others I am forgetting
  (sorry!) who've been doing this for a long time.

  Once your change is submitted, nag people weekly to get things moving
  (yes, we need prodding occasionally). But also don't get offended if
  there are a lot of review comments for seemingly small things ---
  we're just trying to maintain a certain level of quality. Git is used
  by almost everyone in the software industry, so it's important for us
  to keep a high bar for quality, that's all.

* If there's one tip you would like to share with other Git
  developers, what would it be?

  Junio has been our maintainer for nearly two decades. It's a tough job and
  somehow he's kept going at it all this time. Still, let's do our best
  to help make his job easier, because honestly we are truly lucky to
  have someone of his caliber lead our project.

  More concretely, this means helping out with code reviews. If you're
  not sure which ones to review, see the "What's Cooking" emails that
  Junio sends out regularly to look for patches that need help from
  reviewers. They are commented as "Needs review" or "Comments?", so
  they're easy enough to spot.

  Cheers!


## Other News

__Various__


__Light reading__

* Julia Evans continues her series of blog posts about Git with
  [How HEAD works in git](https://jvns.ca/blog/2024/03/08/how-head-works-in-git/) and
  [The "current branch" in git](https://jvns.ca/blog/2024/03/22/the-current-branch-in-git/).
  The first entry in this series of blog posts can be found 
  in [Git Rev News Edition #103](https://git.github.io/rev_news/2023/09/30/edition-103/).
* [Keeping repository maintainer information accurate](https://github.blog/2024-03-04-keeping-repository-maintainer-information-accurate/):
  ensuring that [CODEOWNERS file](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
  is up to date with the help of tools like the [cleanowners](https://github.com/github/cleanowners) tool.
  By Zack Koppert on GitHub Blog.
* [De Programmatica Ipsum, Issue #66: Version Control - Twenty Years Is Nothing](https://deprogrammaticaipsum.com/twenty-years-is-nothing/)
  by Adrian Kosmaczewski.
* [Git Worktrees and GitButler](https://blog.gitbutler.com/git-worktrees/):
  How do Git worktrees help you work on more than one branch at the same time,
  and how does that differ from virtual branches in GitButler?
  Written by Scott Chacon on GitButler Blog.
* [Fixing up [a series of] Git [commits] with Autosquash](https://blog.gitbutler.com/git-autosquash/)
  by Scott Chacon on GitButler Blog.
* [Advanced git commands every senior software developer needs to know](https://optimizedbyotto.com/post/advanced-git-commands/)
  by Otto Kekäläinen on Optimized by Otto blog.
* [Five Ways to Be More Productive with Git](https://laravel-news.com/five-ways-to-be-more-productive-with-git)
  by Paul Redmond on Laravel News blog.  The blog post lists
  a few useful Git aliases, setting up a commit template, using password manager for SSH keys
  (that can be used for signing commits), making use of GitHub CLI tool (`gh`), 
  and configuring `mergetool` and `difftool`.
* [Git: programmatic staging](https://choly.ca/post/git-programmatic-staging/)
  (with the help of the [`expect`](https://linux.die.net/man/1/expect) tool,
  or with [`grepdiff`](https://linux.die.net/man/1/grepdiff))
  by Ilia Choly on Choly's Blog.  The author uses described technique
  as a cleanup step after rewriting/refactoring code using automatic tools,
  such as [Semgrep](https://semgrep.dev/), [ast-grep](https://ast-grep.github.io/),
  LLMs (Large Language Models) such as ChatGPT, and one-off scripts.
    * [Semgrep](https://semgrep.dev/) was mentioned in [Git Rev News Edition #75](https://git.github.io/rev_news/2021/05/27/edition-75/);
      you can test it with [Semgrep Playground](https://semgrep.dev/playground/new).
    * [Another article](https://choly.ca/post/semgrep-autofix-llm/)
      by the same author mentions other similar tools, namely
      [CodeQL](https://codeql.github.com/) (mentioned in passing
      in [Git Rev News Edition #79](https://git.github.io/rev_news/2021/09/30/edition-79/)),
      and [Comby](https://comby.dev/).  It also talks about newly created
      [`semgrepx`](https://github.com/icholy/semgrepx) tool for rewriting `semgrep` matches
      using externals tools (such as Datasette's [`llm`](https://llm.datasette.io/) CLI tool
      and Python library).
* [Unleashing the Power of Git Bisect](https://dzone.com/articles/unleashing-the-power-of-git-bisect)
  by Shai Almog on DZone (DevOps Zone).
* [Moving Code from One Repository to Another Using Git Patch](https://joelcolaco.hashnode.dev/moving-code-from-one-repository-to-another-using-git-patch)
  by Joel Colaco on his blog - though a better solution would be to use
  `git format-patch` and `git am` (or alternates and `git cherry-pick`).
* [Extremely Linear Git History](https://westling.dev/b/extremely-linear-git),
  with first commit in a repo having a hash that starts with `0000000`,
  the second commit is `0000001`, and so on; written by Gustav Westling
  on his blog (2022).
* [Witty.rb - A very simple Ruby Script demonstrating how to parse a Git index file (`.git/index`)](https://gist.github.com/Chubek/1fa1c037d280dfc7952676cb4ee89e11).
  Published as Gist by Chubak Bidpaa.
* [Dr. Git-Love or: How I Learned to Stop Worrying and Love the Rebase](https://escodebar.github.io/trainings/git/meetup/#/)
  are HTML slides for Git training course by Pablo Vergés (escodebar).

- [Toy/demo: using ChatGPT to summarize lengthy LKML threads (b4 integration)](https://lore.kernel.org/all/20240227-flawless-capybara-of-drama-e09653@lemur/t/#u)
  thread on Linux kernel mailing list, started by Konstantin Ryabitsev.


__Easy watching__

* [So You Think You Know Git Part 2 - DevWorld 2024](https://www.youtube.com/watch?v=Md44rcw13k4)
  by Scott Chacon on GitButler YouTube channel, continues the
  [FOSDEM version](https://www.youtube.com/watch?v=aolI_Rz0ZqY) of the talk,
  which was mentioned in the [previous Git Rev News](https://git.github.io/rev_news/2024/02/29/edition-108/).
  [DevWorld Git Slides](https://blog.gitbutler.com/devworld-git-slides/)
  are available on GitButler Blog.


__Git tools and sites__

* [extremely-linear](https://github.com/zegl/extremely-linear), also known as `git-linearize`,
  is a tool to create commits with SHA-1 identifier beginning with `0000000` for the first commit,
  `0000001` for the second, `0000002` for the third, and so on.  This tool uses 
  [lucky_commit](https://github.com/not-an-aardvark/lucky-commit),
  which inserts invisible whitespace characters at the end of the commit message
  until it gets a SHA-1 (or SHA-256) hash with the desired prefix.
    * Compare and contrast with [git-vain](https://git.anna.lgbt/anna/git-vain)
      (mentioned in [Git Rev News Edition #103](https://git.github.io/rev_news/2023/09/30/edition-103/))
      and [git-vanity-sha](https://github.com/mattbaker/git-vanity-sha)
      (mentioned in [Git Rev News Edition #39](https://git.github.io/rev_news/2018/05/16/edition-39/))
      tools to generate vanity hashes, for example to make SHA-1 hash of the HEAD begin with `c0ffee`.
* [Nosey Parker](https://github.com/praetorian-inc/noseyparker/) is a command-line program
  that finds secrets and sensitive information in textual data and Git history.
  Written in Rust, under Apache 2.0 license.
* [gitu](https://github.com/altsem/gitu) - a TUI Git client inspired by Magit.
  Written in Rust, under MIT license.
* [Vim-Flog](https://github.com/rbong/vim-flog) is a powerful git branch viewer for Vim.
  In Vim 8/9, it requires LuaJIT (preferred) or Lua installed.
* [gcd](https://github.com/davvid/gcd) - Git worktree navigator,
  lets you quickly navigate to Git worktrees on your filesystem,
  and quickly navigate to directories within your current worktree.
  Written as a set of shell functions, to be sourced into `~/.zshrc` or `~/.bashrc`.
* [grepdiff](https://pkg.go.dev/rsc.io/grepdiff) is a command line tool that reads unified diffs
  from the files passed as arguments (or standard input), and prints a reduced diff
  containing only the hunks matching the regular expression.  Written in Go.
* [Gitstr](https://github.com/fiatjaf/gitstr) is a tool to send and receive Git patches
  over [Nostr][], using [NIP-34](https://github.com/nostr-protocol/nips/pull/997).
    * Compare and contrast with [git-ssb](https://scuttlebot.io/apis/community/git-ssb.html)
      (see [git-ssb-intro](https://github.com/hackergrrl/git-ssb-intro) guide):
      decentralized Git repo hosting and issue tracking on Secure-ScuttleButt (SSB),
      mentioned in [Git Rev News Edition #26](https://git.github.io/rev_news/2017/04/19/edition-26/)
      and [#40](https://git.github.io/rev_news/2018/06/20/edition-40/).

[Nostr]: https://nostr.com/ "A decentralized social network with a chance of working"


## Releases

+ libgit2 [1.8.0](https://github.com/libgit2/libgit2/releases/tag/v1.8.0)
+ Gerrit Code Review [3.7.8](https://www.gerritcodereview.com/3.7.html#378),
[3.9.2](https://www.gerritcodereview.com/3.9.html#392)
+ GitHub Enterprise [3.12.1](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.1),
[3.11.7](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.7),
[3.10.9](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.9),
[3.9.12](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.12),
[3.8.17](https://help.github.com/enterprise-server@3.8/admin/release-notes#3.8.17),
[3.12.0](https://help.github.com/enterprise-server@3.12/admin/release-notes#3.12.0),
[3.11.6](https://help.github.com/enterprise-server@3.11/admin/release-notes#3.11.6),
[3.10.8](https://help.github.com/enterprise-server@3.10/admin/release-notes#3.10.8),
[3.9.11](https://help.github.com/enterprise-server@3.9/admin/release-notes#3.9.11),
[3.8.16](https://help.github.com/enterprise-server@3.8/admin/release-notes#3.8.16)
+ GitLab [16.10.1, 16.9.3, 16.8.5](https://about.gitlab.com/releases/2024/03/27/security-release-gitlab-16-10-1-released/),
[16.10](https://about.gitlab.com/releases/2024/03/21/gitlab-16-10-released/),
[16.9.2](https://about.gitlab.com/releases/2024/03/06/security-release-gitlab-16-9-2-released/)
+ GitKraken [9.13.0](https://help.gitkraken.com/gitkraken-client/current/)
+ GitHub Desktop [3.3.12](https://desktop.github.com/release-notes/),
[3.3.11](https://desktop.github.com/release-notes/),
[3.3.10](https://desktop.github.com/release-notes/)
+ Tower for Windows [6.0](https://www.git-tower.com/release-notes/windows?show_tab=release-notes) ([Release blog post](https://www.git-tower.com/blog/tower-windows-6/))
+ Tower for Mac [10.5](https://www.git-tower.com/release-notes/mac?show_tab=release-notes)
+ git-credential-azure [0.3.0](https://github.com/hickford/git-credential-azure/releases/tag/v0.3.0)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from Linus Arver, Eric Sunshine,
Ghanshyam Thakkar, Kristoffer Haugsbakk and Bruno Brito.
