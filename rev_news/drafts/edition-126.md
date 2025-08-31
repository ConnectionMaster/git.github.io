---
title: Git Rev News Edition 126 (August 31st, 2025)
layout: default
date: 2025-08-31 12:06:51 +0100
author: chriscool
categories: [news]
navbar: false
---

## Git Rev News: Edition 126 (August 31st, 2025)

Welcome to the 126th edition of [Git Rev News](https://git.github.io/rev_news/rev_news/),
a digest of all things Git. For our goals, the archives, the way we work, and how to contribute or to
subscribe, see [the Git Rev News page](https://git.github.io/rev_news/rev_news/) on [git.github.io](http://git.github.io).

This edition covers what happened during the months of July 2025 and August 2025.

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

## Developer Spotlight: Seyi Kuforiji

_Editor’s note: This edition features a retrospective interview with a
contributor who contributed to Git through a mentoring program. We hope
the reflections shared by the Outreachy contributor will provide an
insightful perspective that benefits the community. As always, we
welcome your thoughts and feedback!_

* **Who are you and what do you do?**

  My name is Seyi Kuforiji, and I’m an Outreachy alum who worked on
  [modernizing Git’s unit testing platform](https://seyi-kuforiji-902b48.gitlab.io/posts/week-1-Introduce-yourself)
  by converting its homegrown unit test framework to use [Clar](https://github.com/clar-test/clar).
  I studied geography at the University of Lagos, but my curiosity
  and passion for computers and software drove me to start learning
  Python and Git immediately after graduating.

  Since then, I’ve enjoyed exploring different areas of IT, from
  software engineering to data science and DevOps, because I genuinely
  love learning and experimenting with new tools. I also earned a
  certification in Health Data Science and Precision Medicine from
  Stanford University, which reflects my commitment to leveraging
  technology to improve lives. Participating in Outreachy through Git
  demonstrated to me the impact of open-source collaboration, and it has
  strengthened my passion for developing solutions that give back to the
  community.

  Outside of work, I’m usually diving into something new. Right now, the
  [Linux graphics stack](https://lwn.net/Articles/955376/) has caught my
  attention, but when I decide to give my brain a break from tech, I play
  chess or watch sports.

* **How did you initially become interested in contributing to Git,
  and what motivated you to choose it as your Outreachy project?**

  Git was one of the first tools I ever learned years ago. At first, I
  didn’t really understand it; I only knew a few commands like
  `git clone`, `git add .`, and `git commit -m "<message>"`, and I was
  living life with just those. I remember during my 12-month software
  engineering bootcamp, I helped some of my colleagues with Git because
  I had this so-called “prior knowledge” and for a while, I was treated
  like a genius, at least until they caught up!

  So when I saw Git on the list of Outreachy projects, I knew right away
  that this was where I needed to be: to deepen my understanding of the
  tool and maybe level up from “genius” to something closer to expert
  wizardry. These days, some say I’m a wizard, others say I’m a maestro,
  but I’m just a humble guy who enjoys learning and sharing knowledge.

* How do you feel your contribution has impacted the Git community
  or the broader open source ecosystem?

  My contribution to Git, which was modernizing its homegrown unit
  testing framework to use Clar, has helped improve Git’s testing
  capabilities by making the tests more maintainable, easier to
  understand, and easier to extend to cover more edge cases in the
  future. Clar brings additional benefits such as clearer test
  reporting, a more structured way to organize tests, and improved
  readability, which makes the testing process more approachable for new
  contributors. While this was primarily an internal-facing improvement,
  I believe it plays an important role in maintaining the reliability of
  Git’s functions and operations. A stronger testing framework makes it
  easier for both new and experienced contributors to work with the
  codebase confidently, which in turn strengthens Git for the millions
  of people who rely on it every day.

* **Is there any aspect of Git that you now see differently after
  having contributed to it?**

  Like I said earlier, I started out only knowing a handful of Git
  commands to do basic operations. My biggest takeaway since
  contributing to Git has been discovering the full power of its
  interactive rebase. I always saw rebase on cheat sheets but never
  really experienced its capabilities until I worked more deeply with
  Git. The best way I can describe it is that it feels like a time
  machine: I make changes and commits, Git captures those states in
  time, and with interactive rebase, I can go back, rewrite history, and
  improve it as if it were the first time.

  I still find it so cool that in my text editor, I can see files I had
  already deleted in later commits come back to life during a rebase. It
  completely changed how I view Git, not just as a version control
  system, but as a powerful storytelling tool for code.

* **How do you balance your contributions with other responsibilities
  like work or school?**

  I usually create a schedule with a clear timeframe dedicated to
  working on the Git project. For example, during Outreachy, I set aside
  specific blocks of time each day, treating it almost like a regular
  job. This helped me stay consistent, avoid distractions, and make
  steady progress.

  I’ve learned that balancing open-source contributions with other
  responsibilities is all about structure and prioritization. By
  planning my week ahead, I can make sure that my work, personal life,
  and contributions don’t clash. Of course, I also try to stay flexible;
  some weeks are more demanding than others, but having a framework
  keeps me grounded and ensures I can keep giving my best to Git.

* **Can you share how GSoC helped enhance your technical and
  non-technical skills (like communication, project management, etc.)?**

  My C and low-level engineering skills have improved immensely through
  this experience. I now feel much more confident working in a large and
  complex codebase, and I’ve built the mindset to take on hard problems
  without shying away. This confidence is what’s encouraging me to dive
  deeper into the Linux kernel, where I’ve been learning and
  experimenting with the graphics stack and GPU drivers. My knowledge of
  Git itself has also grown significantly, particularly with the
  interactive rebase functionality, which has completely changed how I
  think about version control and history management.

  On the non-technical side, I grew a lot in communication and project
  management. I learned how to break down tasks into smaller, achievable
  goals, track progress against deadlines, and ask for help effectively
  when I was stuck. Collaborating with mentors and the wider Git
  community also taught me the importance of giving clear updates in
  blog posts and writing thoughtful commit messages.

  Overall, the experience didn’t just make me a better programmer; it
  made me more disciplined, collaborative, and confident in working on
  real-world projects.

* **What was your biggest takeaway or learning from Outreachy that
  you now apply regularly in your work?**

  My biggest takeaway from Outreachy is the balance between
  understanding deeply and taking action. My mentor encouraged me to not
  just know how things work but also to dig into why they work. At the
  same time, I learned that it’s easy to get stuck in the learning
  phase, waiting until you feel "ready." During my first few weeks, I
  hesitated too much. What really helped me was realizing that you don’t
  need to know everything before you start; you just need enough to
  begin, and the rest comes as you build and iterate. That shift has
  stayed with me and is something I now apply regularly in my life.

* **What was the biggest challenge you faced during your contributions
  to Git, and how did you overcome it?**

  One of the biggest challenges I faced was understanding the Git
  codebase. Git is a very large and complex project with many
  interconnected parts, and even though my task was limited to the unit
  testing section, I also needed to understand the underlying
  functionality being tested. At first, it felt daunting, but I overcame
  this by burning the midnight candle, digging deeper, and committing
  myself to continuous learning. Bit by bit, things started to make
  sense. What really helped was breaking down the complexity into
  smaller pieces and focusing on one area at a time, while also asking
  lots of questions and referring back to documentation.

* **Have you thought about mentoring new GSoC / Outreachy students?**

Yes, I hope to mentor future Outreachy interns if the opportunity arise.

* **If you could get a team of expert developers to work full time on
  something in Git for a full year, what would it be?**

  A first-class graphical interface officially maintained by the Git
  project, for those who prefer using an app instead of the command
  line.

* **What upcoming features or changes in Git are you particularly
  excited about?**

  I’ve been reading recent discussions on the Git mailing list about how
  Git might evolve in the age of AI, particularly around enabling
  integrations with AI agents. The idea of extending Git’s capabilities
  so that AI tools can better understand, interact with, and even
  automate certain workflows is quite exciting. For example, AI-assisted
  code reviews, intelligent merge conflict resolution, or automated
  repository maintenance could become more seamless if Git had
  standardized ways for agents to plug into its internals.

* **What is your favorite Git-related tool/library, outside of Git
  itself?**

  GitHub and GitLab

* **What is your toolbox for interacting with the mailing list and for
  development of Git?**

  I mostly work from the command line. For sending contributions, I use
  `git format-patch` and `git send-email`, since I’m more comfortable with
  CLI tools.

* **How do you envision your own involvement with Git or other open
  source projects in the future?**

  I intend to remain active in the Git community for many years by
  making steady contributions. At the moment, I’m still learning and
  exploring the project to identify areas where I can improve and add
  value. Over time, I hope to grow into a consistent contributor and
  take on more responsibility within the project.

* What is your advice for people who want to start Git development?
  Where and how should they start?

  For anyone starting Git development, I’d recommend a few key
  resources. The "[Hacking Git](https://git.github.io/Hacking-Git/)”
  guide is definitely a go-to resource for understanding how the
  project is structured and how to navigate the codebase.
  The [MyFirstContribution](https://git-scm.com/docs/MyFirstContribution)
  page is also very helpful for learning how to get started with making
  changes. Beyond that, the general Git documentation is valuable for
  building a solid foundation. Starting small, asking questions, and
  getting familiar with these resources can make the process much
  smoother.

* **Would you recommend other students or contributors to participate in
  the GSoC, Outreachy or other mentoring programs, working on Git?
  Why? Do you have advice for them?**

  100% yes. Programs like GSoC and Outreachy give you the unique
  opportunity to learn directly from some of the smartest and most
  experienced contributors in the Git community. Having a mentor to
  guide you through real contributions accelerates your learning, helps
  you build confidence and good practices early on. I’d absolutely
  recommend it. My advice would be: come with curiosity, patience, and
  the willingness to learn. Don’t worry if you don’t understand
  everything at first. Ask questions, read the documentation, and engage
  with the community. The mentorship and the experience you gain are
  invaluable.


## Other News

__Various__


__Light reading__

<!---
__Easy watching__
-->

__Git tools and sites__


## Releases

+ Git [2.51.0](https://lore.kernel.org/git/xmqqikikk1hr.fsf@gitster.g/),
[2.51.0-rc2](https://lore.kernel.org/git/xmqqh5ybcfwt.fsf@gitster.g/),
[2.51.0-rc1](https://lore.kernel.org/git/xmqqikizoybn.fsf@gitster.g/),
[2.51.0-rc0](https://lore.kernel.org/git/xmqqms8f5889.fsf@gitster.g/)
+ Git for Windows [v2.51.0(1)](https://github.com/git-for-windows/git/releases/tag/v2.51.0.windows.1),
[v2.51.0-rc2(1)](https://github.com/git-for-windows/git/releases/tag/v2.51.0-rc2.windows.1),
[v2.51.0-rc1(1)](https://github.com/git-for-windows/git/releases/tag/v2.51.0-rc1.windows.1),
[v2.51.0-rc0(1)](https://github.com/git-for-windows/git/releases/tag/v2.51.0-rc0.windows.1)
+ GitLab [18.3.1, 18.2.5, 18.1.5](https://about.gitlab.com/releases/2025/08/27/patch-release-gitlab-18-3-1-released/),
[18.3](https://about.gitlab.com/releases/2025/08/21/gitlab-18-3-released/),
[18.2.4](https://about.gitlab.com/releases/2025/08/18/gitlab-18-2-4-released/),
[17.11.7](https://about.gitlab.com/releases/2025/08/15/gitlab-17-11-7-released/),
[18.2.2, 18.1.4, 18.0.6](https://about.gitlab.com/releases/2025/08/13/patch-release-gitlab-18-2-2-released/)
+ Gerrit Code Review [3.10.8](https://www.gerritcodereview.com/3.10.html#3108),
[3.11.5](https://www.gerritcodereview.com/3.11.html#3115),
[3.12.2](https://www.gerritcodereview.com/3.12.html#3122)
+ GitHub Enterprise [3.17.5](https://docs.github.com/enterprise-server@3.17/admin/release-notes#3.17.5),
[3.16.8](https://docs.github.com/enterprise-server@3.16/admin/release-notes#3.16.8),
[3.15.12](https://docs.github.com/enterprise-server@3.15/admin/release-notes#3.15.12),
[3.14.17](https://docs.github.com/enterprise-server@3.14/admin/release-notes#3.14.17)
+ GitKraken [11.3.0](https://help.gitkraken.com/gitkraken-client/current/)
+ Git Cola [4.14.0](https://github.com/git-cola/git-cola/releases/tag/v4.14.0)
+ GitButler [0.15.16](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.15.16),
[0.15.15](https://github.com/gitbutlerapp/gitbutler/releases/tag/release/0.15.15)
+ Sublime Merge [Build 2112](https://www.sublimemerge.com/download)

## Credits

This edition of Git Rev News was curated by
Christian Couder &lt;<christian.couder@gmail.com>&gt;,
Jakub Narębski &lt;<jnareb@gmail.com>&gt;,
Markus Jansen &lt;<mja@jansen-preisler.de>&gt; and
Kaartic Sivaraam &lt;<kaartic.sivaraam@gmail.com>&gt;
with help from XXX.
