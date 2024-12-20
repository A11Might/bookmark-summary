Title: Lazygit Turns 5: Musings on Git, TUIs, and Open Source

URL Source: https://jesseduffield.com/Lazygit-5-Years-On/

Markdown Content:
![Image 16](https://jesseduffield.com/images/posts/lazygit-5/basic-gif.gif)

_This post is brought to you by my sponsors. If you would like to support me, consider becoming a [sponsor](https://github.com/sponsors/jesseduffield)_

![Image 17](https://jesseduffield.com/images/posts/lazygit-5/sponsors.png)

[Lazygit](https://github.com/jesseduffield/lazygit), the world’s _coolest_ terminal UI for git, was released to the world on August 5 2018, five years ago today. I say _released_ but I really mean _discovered_, because I had taken a [few](https://www.reddit.com/r/webdev/comments/90ux3f/lazygit_a_terminal_ui_application_for_git/) [stabs](https://www.facebook.com/groups/319479604815804/?multi_permalinks=1819232401507176) at publicising it in the weeks prior which fell on deaf ears. When I eventually posted to Hacker News I was so sure nothing would come of it that I had already forgotten about it by that afternoon, so when I received an email asking what license the code fell under I was deeply confused. And then the journey began!

In this post I’m going to dive into a bunch of topics directly or tangetially related to Lazygit. In honour of the Hacker News commenters whose flamewar over git UIs vs the git CLI likely boosted the debut post to the frontpage, I’ve been sure to include plenty of juicy hot-takes on various topics I’m underqualified to comment on. It’s a pretty long post so feel free to pick and choose whatever topics interest you.

Contents:

*   [Where are we now?](https://jesseduffield.com/Lazygit-5-Years-On/#where-are-we-now)
*   [Lessons learnt](https://jesseduffield.com/Lazygit-5-Years-On/#lessons-learnt)
*   [What comes next?](https://jesseduffield.com/Lazygit-5-Years-On/#what-comes-next)
*   [Is git even that good?](https://jesseduffield.com/Lazygit-5-Years-On/#is-git-even-that-good)
*   [Weighing in on the CLI vs UI debate](https://jesseduffield.com/Lazygit-5-Years-On/#weighing-in-on-the-cli-ui-debate)
*   [Weighing in on the terminal renaissance](https://jesseduffield.com/Lazygit-5-Years-On/#weighing-in-on-the-terminal-renaissance)
*   [Credits](https://jesseduffield.com/Lazygit-5-Years-On/#credits)

Where are we now?
-----------------

### Stars

![Image 18](https://jesseduffield.com/images/posts/lazygit-5/stars.png)

Lazygit has 37 thousand stars on GitHub, placing it at rank [26](https://evanli.github.io/Github-Ranking/Top100/Go.html) in terms of Go projects and rank [263](https://gitstar-ranking.com/jesseduffield/lazygit) across all git repos globally.

What’s the secret? The number one factor (I hope) is that people actually like using Lazygit enough to star the repo. But there were two decisions I made that have nothing to do with the app itself that I think helped.

Firstly, I don’t have a standalone landing page site or docs site. I keep everything in the repo, which means you’re always one click away from starring. You can add a GitHub star button to your external site, but it doesn’t actually star the repo; it just links to the repo and it’s up to you to realise that you actually need to press the star button again. I suspect that is a big deal.

Secondly, Lazygit shows a popup when you first start it which at the very bottom suggests staring the repo:

```
Thanks for using lazygit! Seriously you rock. Three things to share with you:

 1) If you want to learn about lazygit's features, watch this vid:
    https://youtu.be/CPLdltN7wgE

 2) Be sure to read the latest release notes at:
    https://github.com/jesseduffield/lazygit/releases

 3) If you're using git, that makes you a programmer! With your help we can
    make lazygit better, so consider becoming a contributor and joining the fun at
    https://github.com/jesseduffield/lazygit
    You can also sponsor me and tell me what to work on by clicking the donate
    button at the bottom right.
    Or even just star the repo to share the love!
```

I know this all sounds machiavellian but at the end of the day, a high star count lends credibility to your project which makes users more likely to use it, and that leads to more contributors, which leads to more features, creating a virtuous cycle.

It’s important to note that GitHub stars don’t necessarily track real world popularity: [magit](https://github.com/magit/magit), the de facto standard git UI for emacs, has only 6.1k stars but has north of [3.8 million downloads](https://melpa.org/#/?q=magit&sort=downloads&asc=false) which as you’ll see below blows Lazygit out of the water.

### Downloads

Downloads are harder to measure than stars because there are so many sources from which to download Lazygit, and I don’t have any telemetry to lean on.

[GitHub](https://github.com/jesseduffield/lazygit) tells me we’ve had 359k total direct downloads.

[4.6%](https://pkgstats.archlinux.de/packages/lazygit) of Arch Linux users have installed Lazygit.

Homebrew ranks Lazygit at [294th](https://formulae.brew.sh/analytics/install-on-request/365d/) (two below emacs) with 15k installs-on-request in the last year (ignoring the tap with 5k of its own). For comparison `tig`, the incumbent standalone git TUI at the time of Lazygit’s creation, ranks at 480 with 8k installs.

I’m torn on how to interpret these results: being in the top 300 in Homebrew is pretty cool, but 15k installs feels lower than I would expect for that ranking. On the other hand, having almost 1 in 20 Arch Linux users using Lazygit seems huge.

Lessons Learnt
--------------

I’ve maintained Lazygit for 5 years now and it has been a wild ride. Here’s some things I’ve learnt.

### Ask for help

I don’t know why this didn’t occur to me sooner, but there is something unique and magical about writing open source software whose users are developers: any developer who raises an issue has the capacity to fix the issue themselves. All you need to do is ask! Simply asking ‘are you up to the challenge of fixing this yourself?’ and offering to provide pointers goes a long way.

I’ve gotten better over time at identifying easy issues and labelling them with the good-first-issue label so that others can help out, with a chance of becoming regular contributors.

### Get feedback

If your repo is popular enough, you’ll get plenty of feedback through the issues board. But issues are often of the form ‘this is a problem that needs fixing’ or ‘this is a feature that should be added’ and the demand for rigour is a source of friction. There are other ways you can reduce the friction on getting feedback. I pinned a google form to the top of the issues page to get general feedback on what people like/dislike about Lazygit.

![Image 19](https://jesseduffield.com/images/posts/lazygit-5/survey-dislike.png)

Something that the google form made clear was that people wanted to know what commands were being run under the hood, so I decided to add a command log (shown by default) that would tell you which commands were being run. This made a huge difference and it’s now one of the things people like best about Lazygit.

![Image 20](https://jesseduffield.com/images/posts/lazygit-5/survey-contribute.png)

Something that surprised me was how big of a barrier the language of the project is in deciding whether somebody contributes. And _Go_ of all languages: the one that’s intended to be dead-easy to pick up. Maybe I need to do a rewrite in javascript to attract more contributors ;)

### MVP is the MVP

This is not much a ‘lesson learnt’ as it was a ‘something I got right’. When I first began work on Lazygit I had a plan: hit MVP (Minimum Viable Product) and then release it to the world to see if the world had an appetite for it. The MVP was pretty basic: allow staging files, committing, checking out branches, and resolving merge conflicts. But it was enough to satisfy my own basic needs at the time and it was enough for many others as well. Development was accelerated post-release thanks to some early contributors who joined the team (shoutout to Mark Kopenga, Dawid Dziurla, Glenn Vriesman, Anthony Hamon, David Chen, and other OG contributors). This not only sped up development but I personally learned a tonne in the process.

### Tech debt is a perennial threat

In your day job, tech debt is to be expected: there are deadlines and customers to appease and competitors to race against. In open source, then, you would think that the lack of urgency would mean less tech debt. But I’ve found that where time is the limiting factor at my day job, motivation is the limiting factor in my spare time, and the siren song of tech debt is just as alluring. Does anybody want to spend their weekend writing a bunch of tests? Does anybody want to spend a week of annual leave on a mind-numbing refactoring? Not me, but I have done those things in order to improve the health of the codebase (and there is _still_ much to improve upon).

Thankfully, open source has natural incentives against tech debt that are absent from proprietary codebases. Firstly, if your codebase sucks, nobody will want to contribute to it. Contrast this to a company where no matter how broken and contemptible a codebase is, there is an amount you can pay a developer to endure it.

Secondly, because your code is public, anybody who considers hiring you in the future can skim through it to get a feel for whether you suck or not. You want your codebase to be a positive reflection on your own skills and values.

So, tech debt is still a problem, but for different reasons than in a proprietary codebase.

### Get your testing patterns right as soon as possible

The sooner you get a good test pattern in place with good coverage, the easier life will be.

In the beginning, I was doing manual regression tests before releasing each feature. Although I had unit tests, they didn’t inspire much confidence, and I had no end-to-end tests. Later on I introduced a framework based on recorded sessions: each test would have a bash script to prepare a repo, then you would record yourself doing something in Lazygit, and the resultant repo would be saved as a snapshot to compare against when the test was run and the recording was played back. This was great for writing tests but terrible for maintaining them. Looking at a minified JSON containing a sequence of keypresses, it was impossible to glean the intent, and the only way to make a change to the test was to re-record it.

I’ve spent a lot of time working on an end-to-end test framework where you define your tests with code, and although I still shiver thinking about the time it took to migrate from the old framework to the new one, every day I see evidence that the effort was worth it. Contributors find it easy to write the tests and I find it easy to read them which tightens the pull request feedback loop.

Here’s an example to give you an idea:

```
// We call them 'integration tests' but they're really end-to-end tests.
var RewordLastCommit = NewIntegrationTest(NewIntegrationTestArgs{
	Description:  "Rewords the last (HEAD) commit",
	SetupRepo: func(shell *Shell) {
		shell.
			CreateNCommits(2)
	},
	Run: func(t *TestDriver, keys config.KeybindingConfig) {
		t.Views().Commits().
			Focus().
			Lines(
				Contains("commit 02").IsSelected(),
				Contains("commit 01"),
			).
			Press(keys.Commits.RenameCommit).
			Tap(func() {
				t.ExpectPopup().CommitMessagePanel().
					Title(Equals("Reword commit")).
					InitialText(Equals("commit 02")).
					Clear().
					Type("renamed 02").
					Confirm()
			}).
			Lines(
				Contains("renamed 02"),
				Contains("commit 01"),
			)
	},
})
```

I wish I had come up with that framework from the get-go: it would have saved me a lot of time fixing bugs and migrating tests from the old framework.

What comes next?
----------------

If I could flick my wrist and secure funding to go fulltime on Lazygit I’d do it in a heartbeat, but given the limited time available, things move slower than I would like. Here are some things I’m excited for:

*   Bulk actions (e.g. moving multiple commits at once in a rebase)
*   Repo actions (e.g. pulling in three different repos at once)
*   Better integration with forges (github, gitlab) (e.g. view PR numbers against branches)
*   Improved diff functionality
*   More flexibility in deciding which args are used in a command
*   More performance improvements
*   A million small enhancements

I’ve just wrapped up worktree support, and my current focus is on improving documentation.

If you want to be part of what comes next, join the team! There are plenty of [issues](https://github.com/jesseduffield/lazygit/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc) to choose from and we’re always up to chat in the [discord channel](https://discord.gg/ehwFt2t4wt).

Okay, you’ve listened to me ramble about me and my project for long enough. Now onto the juicy stuff.

Is git even that good?
----------------------

I’m not old enough to compare git with its predecessors, and from what I’ve heard from those who _are_ old enough, it was a big improvement.

There are many who criticize git for being unnecessarily complex, in part due to its original purpose in serving the needs of linux development. [Fossil](https://www.fossil-scm.org/home/doc/trunk/www/fossil-v-git.wiki#history) is a ~recent~ (not-recent: released in 2006 as commenter nathell [points out](https://news.ycombinator.com/reply?id=37013854&goto=item%3Fid%3D37009879%2337013854)) git alternative that optimises for simplicity; serving the needs of small, high-trust teams. I disagree with a few of its [design choices](https://www.fossil-scm.org/home/doc/trunk/www/fossil-v-git.wiki#history), but it might be perfect for you!

My beef with git is not so much its complexity (I’m fine dealing with multiple remotes and the worktree/index distinction) but its UX, including:

*   lacking high-level commands
*   no undo feature
*   merge conflicts aren’t first-class

### Lacking high-level commands

Consider the common use case of ‘remove this file from my git status output’. Depending on the state of the file, the required command is different: for untracked files you do `rm <path>`, for tracked it’s `git checkout -- <path>`, and for staged files it’s `git reset -- <path> && git checkout -- <path>`. One of the reasons I made Lazygit was so that I could press ‘d’ on a file in a ‘changed files’ view and have it just go away.

### No undo feature

Git should have an undo feature, and it should support undoing changes to the working tree. Although Lazygit has an undo feature, it depends on the reflog, so we can’t undo anything specific to the working tree. If git treated the working tree like its own commit, we would be able to undo pretty much anything.

### Merge conflicts aren’t first class

I also dislike how merge conflicts aren’t first-class: when they show up you have to choose between resolving all of them or aborting an entire rebase (which may have involved other conflicts), and you can’t easily switch to another task mid-conflict (though worktrees make this easier).

One project that addresses these concerns is [Jujutsu](https://github.com/martinvonz/jj). I _highly_ recommend reading through its readme to realise how many problems you took for granted and how a few structural tweaks can provide a much better experience.

Unlike Fossil which trades power for simplicity, Jujutsu feels more like a reboot of git, representing what git _could_ have been from the start. It’s especially encouraging that Jujutsu can use git as a backend. I hope that regardless of Jujutsu’s success, git incorporates some of its ideas.

Weighing in on the CLI-UI debate
--------------------------------

If my debut hacker news post hadn’t sparked a flamewar on the legitimacy of git UIs, it probably would have gone unnoticed and Lazygit would have been relegated to obscurity forever. So thanks, [Moloch](https://slatestarcodex.com/2014/07/30/meditations-on-moloch/)!

I’ve had plenty of time to think about this endless war and I have a few things to say.

Here are the main arguments against using git UIs:

*   git UIs sometimes do things you didn’t expect which gets you in trouble
*   git UIs rarely give you everything you need and you will sometimes need to fall back to the command line
*   git UIs make you especially vulnerable when you do need to use the CLI
*   git UIs obscure what’s really happening
*   The CLI is faster

I’m going to address each of these points.

### Git UIs sometimes do things you didn’t expect

This is plainly true. Lazygit works around this by logging all the git commands that it runs so that you know what’s happening under the hood. Also, over time, lazygit’s ethos has changed to be less about compensating for git’s shortcomings via magic and more making it easier to do the things that you can naturally do in git, which means there are fewer surprises.

### Git UIs don’t cover the full API

This is indeed an issue. However, as a git UI matures, it expands to cover more and more of git’s API (until you end up like magit). And the fact you need to fall back to git is not really a point against the UI: when given the choice between using the CLI 100% of the time and using it 1% of the time, I pick the latter. If you forgive the shameless plug (is it really a plug given the topic of the post?) Lazygit also works around this with a pretty cool [custom commands system](https://github.com/jesseduffield/lazygit/wiki/Custom-Commands-Compendium) that lets you invoke that bespoke git command from the UI; making use of the selection state to spare you from typing everything out yourself.

### Git UIs make you vulnerable when you need to use the CLI

I’ve conceded the first two points. Now I go to war.

What people envision with a seasoned CLI user is that they come across some situation they haven’t seen before and using their strong knowledge of the git API and the git object model they craft an appropriate solution. The reality that I’ve experienced is that you instead just look for the answer on stack overflow, copy+paste, and then forget about it until next time when you google it again. With the advent of ChatGPT this will increasingly become the norm.

Whenever a new technology comes along that diminishes the need for the previous one, there are outcries that it will make everybody dumber. Socrates was famously suspicious of the impact that writing would have on society, [saying](http://www.perseus.tufts.edu/hopper/text?doc=Perseus%3Atext%3A1999.01.0174%3Atext%3DPhaedrus%3Apage%3D275):

> Their trust in writing, produced by external characters which are no part of themselves, will discourage the use of their own memory within them. You have invented an elixir not of memory, but of reminding; and you offer your pupils the appearance of wisdom, not true wisdom, for they will read many things without instruction and will therefore seem to know many things, when they are for the most part ignorant…

The argument perfectly applies to UIs, and is just as misguided. The truth is that some people have good memory and some people (i.e. me) have shockingly bad memory and it has little to do with technology (unless the technology is hard drugs in which case yes that does make a difference). I think that many debates about UX are actually debates between people with differing memory ability who therefore have different UX needs. UIs make things more discoverable so you don’t need to remember as much, and people with shocking memory who stick to the git CLI have no guarantee of actually remembering any of it. Yes, all abstractions are leaky, but that doesn’t mean that we should go without abstractions, any more than we should all revert to writing code in assembly.

What’s especially peculiar is that many complex git commands involve a visual component whether you like it or not: the git CLI by default will open up a text editor to prepare for an interactive rebase which is visual in the sense that you’re shown items whose position is meaningful and you can interact with them (e.g. shuffling commits around). The question is whether that interface is easy to use or not, and I find the default behaviour very difficult to use.

For the record, I’m good at helping colleagues fix their git issues, but if I’m in their terminal trying to update their remote URL I have no idea what the command is. Not to worry: I do know how to run `brew install lazygit`.

![Image 21: Harry potter meme](https://jesseduffield.com/images/posts/lazygit-5/allowed-a-terminal.png)

### Git UIs obscure what’s really happening

Again, strong disagree. Compared to the CLI, there’s nothing to obscure!

When I create a commit, several things happen:

*   my staged files disappear from my list of file changes
*   a new commit is appended to my git log
*   my branch ends up with a new head commit, diverging from its upstream

If you create a commit from the command line, you see none of this. You can query for any of this information after the fact, for example by running `git status`, but it only gives you one piece of information. If you’re a beginner using the git CLI, you want to be learning the relationship between the different entities, and it’s almost impossible to do that without seeing how these entities are changed as a direct result to your actions. Lazygit has helped some people [better understand git](https://www.reddit.com/r/git/comments/fr7o1p/lazygit_changed_how_i_understand_git/) by providing that visual context.

Perhaps UIs aren’t visually obscuring the _entities_, but they are obscuring the _commands_. Okay, fine, I concede that point. But my caveats in the _Git UIs sometimes do things you didn’t expect_ section above still apply.

### The CLI is faster

If you’re a CLI die-hard you probably have some aliases that speed you up, but when it gets to complex use cases like splitting an old commit in two or only applying a single file from a stash entry to the index, it helps to have a UI that lets you press a few keys to select what you want and then perform an action with it. In fact I’d love to pit a CLI veteran against a UI veteran in a contrived gauntlet of git challenges and see who reaches the finish line first. You could also determine the speed of light for each approach i.e. the minimum number of keypresses required to perform the action and then see which approach wins. Even if you had a thousand aliases, I still think a keyboard-centric UI (with good git API coverage) would win.

### Conclusion

As somebody who maintains a git UI, I’m clearly partial. But I also feel for the devs who I see stage files by typing `git status`, dragging their mouse over the file they want to add, and then typing `git add <path>`. It makes my stomach turn. There are some pros out there who are happy using the CLI for everything, but the average CLI user I see is taking painstakingly slow approaches to very simple problems.

Weighing in on the terminal renaissance
---------------------------------------

The terminal is making a comeback. Various companies have sprung up with the intention of improving the developer experience in the terminal:

*   [Warp](https://www.warp.dev/): a terminal emulator whose killer feature is allowing you to edit your command as if you were in vscode/sublime
*   [Fig](https://fig.io/): a suite of tools including autocomplete, terminal plugin manager, and some UI helpers for CLI tools
*   [Charm](https://charm.sh/): various tools and libraries for terminals including a terminal UI ecosystem

Warp and Fig both add original elements to the exterior of a terminal emulator to improve the UX, whereas charm is all about improving things on the inside. All of these projects have the same general idea: rather than replace the terminal, embrace it.

I’m interested to see where this goes.

### TUI vs CLI

I would say I’m pro-terminal, but borderline anti-CLI. When I’m interfacing with something I want to know the current state, the available actions, and once I’ve performed an action, I want to see how the state changes in response. So it’s state -\> action -\> new state. You can use a CLI to give you all that information, but commands and queries are typically separated and it’s left as an exercise for the user to piece it all together. The simplest example is that after you run `cd`, you have to run `ls` to know which files are in the directory. Compare this to [nnn](https://github.com/jarun/nnn) which mimics your OS’s file explorer. Another example is running `docker compose restart mycontainer` and then having to run a separate command to see whether or not your container died as soon as it started (compared to using [Lazydocker](https://github.com/jesseduffield/lazydocker)). Even programs like npm can benefit from some visualisation when it comes to linking packages (which is why I created [Lazynpm](https://github.com/jesseduffield/lazynpm)). CLI interfaces are great for scripts and composition but as a direct interface, the lack of feedback about state is jarring.

All this to say that when I see demos that show slick auto-complete functionality added to a CLI tool, I can see that it solves the problem of knowing what actions are available, but I’d rather solve the issue of exposing state.

I want to drive home how easy it is to improve on the design of many CLIs. It’s not hard to pick an existing CLI and think about what entities are involved and how they could be represented visually. A random example: `asdf` is an all-in-one version manager that can manage versions of multiple programs. So you have programs, the available versions of each program, the currently selected version, and you have some actions like CRUD operations and setting a given version as the default. This is perfectly suited to a UI! It just so happens that somebody has gone and made a TUI for it: [lazyasdf](https://www.mitchellhanberg.com/introducing-lazyasdf-a-tui-for-the-asdf-version-manager/) (I’m proud to have started a trend with the naming convention!).

### TUI vs Web

So, I’ve said my piece about how TUIs can improve upon CLIs, but what about this separate trend of re-imagining web/desktop applications in the terminal?

nsf, the author of the now unmaintained terminal UI framework [termbox](https://github.com/nsf/termbox), says the following at the top of the readme (emphasis mine):

> This library is no longer maintained. It’s pretty small if you have a big project that relies on it, just maintain it yourself. Or look for forks. Or look for alternatives. Or better - **avoid using terminals for UI**

When you think about it, the only thing that separates terminals and standalone applications is that terminals only render text. The need for terminals was obvious when there were literally no alternatives. Now that we have shiny standalone applications for many things that were once confined to the terminal, it’s harder to justify extending our terminals beyond CLI programs. But there are some reasons:

#### TUIs guarantee a keyboard-centric UX

There is nothing stopping a non-TUI application from having a keyboard centric UX, but few do. Likewise, TUIs _can_ be mouse-centric, but I’ve never encountered one that is.

#### TUIs have minimalistic designs

In a TUI, not only can you only render text, but you’re often space-constrained as well. This leads to compact designs with little in the way of superfluous clutter. On the other hand, it’s nice when your UI can render bespoke icons and images and render some text in a small font so that the info is there if you need it but it’s not taking up space. It is interesting that Charm’s UI library seems to go for more whitespace and padding than the typical TUI design: I suspect that trend will be shortlived and in the long run terminal apps will lean compact and utilitarian (No doubt Charm has room for both designs in its ecosystem).

#### TUIs are often faster than non-TUI counterparts

In one sense, this is a no-brainer: all you’re rendering is text, so your computer doesn’t need to work as hard to render it. But I don’t actually think that’s the main factor. Rather, terminal users _expect_ TUIs to be fast, because they value speed more than other people. So TUI devs put extra effort in towards speed in order to satisfy that desire. I’ve spent enough time on Lazygit’s performance to know that it doesn’t come for free.

### Conclusion

So, let’s see where this TUI renaissance goes. Even if the renaissance’s only long-term impact is to support more keyboard-centric UIs in web apps, it will have been worth it.

Credits
-------

Well, that wraps up this Anniversary mega-post. Now I’d like to thank some people who’ve helped Lazygit become what it is today.

First of all, a HUGE thankyou to the 206 people who have [contributed](https://github.com/jesseduffield/lazygit/graphs/contributors) to Lazygit over the years, and those who have supported me with donations.

I’d like to shoutout contributors who’ve been part of the journey at different stages: Ryoga, Mark Kopenga, Dawid Dziurla, Glenn Vriesman, Anthony Hamon, David Chen, Flavio Miamoto, and many many others. Thankyou all so much. I also want to thank loyal users who’ve given lots of useful feedback including Dean Herbert, Oliver Joseph Ash, and others.

I want to give a special shoutout to Stefan Haller and Luka Markušić who currently comprise the core team. You’ve both been invaluable for Lazygit’s development, maintenance, and direction. I also hereby publicly award Stefan the prize of ‘most arguments won against maintainer’ ;)

I also want to shoutout [Appwrite](https://appwrite.io/) who generously sponsored me for a year. It warms my heart when companies donate to open source projects.

As for you, dear reader: if you would like to support Lazygit’s development you can join the team by picking up an [issue](https://github.com/jesseduffield/lazygit/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc) or expressing your intent to help out in the [discord channel](https://discord.gg/ehwFt2t4wt)

And as always, if you want to support me, please consider [donating](https://github.com/sponsors/jesseduffield) <3

I now leave you with a gif of our new explosion animation when nuking the worktree.

![Image 22](https://jesseduffield.com/images/posts/lazygit-5/nuke-gif.gif)

Discussion links
----------------

*   [Hacker News](https://news.ycombinator.com/item?id=37009879)

Shameless plug: I recently quit my job to co-found Subble, a web app that helps you manage your company's SaaS subscriptions. Your company is almost certainly wasting time and money on shadow IT and unused licences and Subble can fix that. Check it out at [subble.com](https://www.subble.com/)
