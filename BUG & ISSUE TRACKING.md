- [BUG & ISSUE TRACKING](#)
	- [THE VISION](#)
	- [SUMMARY](#)
- [RESOLVED VS. CLOSED](#)
	- [A HIGH LEVEL OVERVIEW OF QUALITY ASSURANCE](#)
		- [WHY WE CHOSE “RESOLVED” AND “CLOSED”](#)
		- [SOMETIMES THEY’RE NOT PERFECT](#)
		- [WHAT DOES “CLOSED” REALLY MEAN?](#)
		- [“OPEN” VS. “REOPENED”](#)
	- [WHO GETS TO CLOSE ISSUES?](#)
		- [QUALITY ASSURANCE TEAM](#)
		- [THE PERSON WHO OPENED THE ISSUE](#)
		- [TEAM LEADS](#)
		- [YOUR CLIENTS](#)
		- [OTHER TEAM MEMBERS](#)
		- [THE ASSIGNEE (THE ORIGINAL DEVELOPER)](#)
	- [THE QUALITY ASSURANCE PROCESS](#)
		- [FANCY A STAGING OR QA ENVIRONMENT?](#)
		- [SHOULD ISSUES BE REASSIGNED?](#)
		- [IS IT EVER OKAY TO SKIP “RESOLVED”?](#)
		- [CAN “CLOSED” MEAN SOMETHING ELSE?](#)
	- [SUMMARY](#)
	- [BUG AND ISSUE TRACKER WORKFLOW](#)
	- [VARYING DEGREES OF DONENESS](#)
	- [RESOLVED](#)
	- [CLOSED](#)
	- [NOTHING IS ABSOLUTE](#)


# BUG & ISSUE TRACKING

Having thought about this for years, I decided some time ago that if I was going to build an issue tracker that I’d have to start by creating a simple issue life-cycle and workflow. That was the heart of the problem, in my opinion. If the workflow wasn’t simple, the software wouldn’t be either. You might be familiar Conway’s Law which more or less states…

> Any piece of software reflects the organizational structure that produced it.

It doesn’t take much to see that a complex issue life-cycle would lead to complex software. For me, it was more important to define one clear and simple process instead of a flexible and customizable one. So I set out to create “the perfect process”, and this is the abbreviated version of how it came about.

## THE VISION

Before we get into the diagrams, it’s important to understand that I’ve come to hold two aspects of the process as sacred. The first is_status_&nbsp;which is the primary focus of this article. The second is_responsibility_. Anytime I run into a problem on this project, these factors play the most significant role in how I determine on a solution.

![The initial issue life-cycle.](https://sifterapp.com/blog/images/2007-08-14-bug-and-issue-tracking/1.gif)

1The initial issue life-cycle before any simplification.

I started with a reasonable, but thorough, life-cycle.&nbsp;1&nbsp;It bothered me that there were two steps to even get the issue to a point where someone was working on it.&nbsp;2A & 2B&nbsp;These steps enable large teams and open-source projects to verify that issues are legitimate before anyone begins working on them, but they’re overkill for smaller teams. They had to go.

By removing these steps, it freed me to simplify the name of the initial status to “Open”. So, instead of “accepting” or “confirming” an issue, we just assume that all issues are good, and if they’re not, we can close them with an explanation of why they’re invalid. It accomplishes the same thing, eliminates complexity, and provides a more natural path to a resolution. More importantly, it helps make status and responsibility more distinct. Instead of “accepted”, an issue is implicitly accepted when it’s assigned. At that point, it’s up to that person to do something with it.

![The issue life-cycle after the first round of simplification iteration.](https://sifterapp.com/blog/images/2007-08-14-bug-and-issue-tracking/2.gif)

2The issue life-cycle after the first round of simplification iteration.

While we’re on the subject of accountability, I decided that putting an issue “on hold” is like sweeping it under the rug.&nbsp;3D&nbsp;It’s a convenient way to avoid responsibility. The only benefit of putting an issue “on hold” is that it provides the illusion of progress. As far as I’m concerned, those are still open, and the distinction only serves to dilute accountability. If something or someone is preventing progress, the issues can and should be reassigned to someone who can do something about it.

In addition to removing the ability to put things on hold, I chose “Resolved” for the label on the next step instead of “Retest”.&nbsp;3EWhile I anticipate that it will primarily be used for tracking bugs, I see a lot of potential in using it to track generic issues as well, and “Retest” just doesn’t really apply to generic issues. It’s a little thing, but they all start to add up.

![The issue life-cycle after the second round of simplification iteration.](https://sifterapp.com/blog/images/2007-08-14-bug-and-issue-tracking/3.gif)

3The issue life-cycle after the second round of simplification iteration.

Now that we’ve cut out the excess, we’ve got a life-cycle that I’m comfortable using.&nbsp;4&nbsp;More importantly, the life-cycle is simple enough that even a non-technical client or coworker can understand how it works without being intimidated. And of course, now the language is flexible enough so the system can be use for both software defects and generic issues.

![The final issue life-cycle that I'm using.](https://sifterapp.com/blog/images/2007-08-14-bug-and-issue-tracking/4.gif)

4The final issue life-cycle that I’m using.

To some, I’m sure this will appear to be insufficient and an over-simplification, but it was a key step in enabling me to create a solution that was focused on getting work done. Now the process gets out of the way and lets people focus on progress.

## SUMMARY

I’ll be honest. Writing about vaporware is a little scary. However, I’m a big fan of sharing best practices and lessons learned, so I’ll be doing my best to get past that fear. Ideally, when it’s all said and done, we’ll have a whole series of informational articles like this one in addition to some great software.

I’ve looked at a lot of bug tracking solutions, and they’re all pretty complex. They work for some situations, but for the other situations, we need something simpler. Hopefully this can be it.

---

# RESOLVED VS. CLOSED

## A HIGH LEVEL OVERVIEW OF QUALITY ASSURANCE

Here’s the short version: “Resolved” is for when someone solves something, and “Closed” is for when someone verifies that it’s been resolved. And that applies for bugs or questions or feature ideas or tasks or anything else. But when it comes to software in particular, we’ve found that it really helps to have a second set of eyes to make sure that whatever is being solved is really solved.

[![The open > resolved > closed workflow visualized.](https://sifterapp.com/blog/images/2011-07-28-resolved-vs-closed/4.gif)](http://sifterapp.com/blog/2007/08/bug-issue-tracking/)

1The initial design of Sifter’s workflow from late 2007.

### WHY WE CHOSE “RESOLVED” AND “CLOSED”

We chose the names “Resolved” and “Closed” because they’re flexible enough that you can apply them to things like bugs, issues, questions, features, and other stuff. We wanted words that could apply to all of those—and we found that “Resolved” and “Closed” fit the best.

### SOMETIMES THEY’RE NOT PERFECT

The downside to words like “Resolved” and “Closed” is that they’re sometimes a compromise for certain types of issues or things you’d put into Sifter. For instance, a lot of people think of bugs as being “Fixed” rather than “Resolved.” But the reason we didn’t use “Fixed” is because that doesn’t work so well with things like new features. A new feature isn’t something that gets “Fixed” because that would imply that it was broken in the first place. Similarly, if you’re trying to hash out a question among your team, you may come to an answer, but a question isn’t something that gets “Fixed” either.

There isn’t a magical word that can work for every type of thing that people might stuff into Sifter, but we’ve found that “Resolved” is the best overall fit across most types of things you might want to track in Sifter.

### WHAT DOES “CLOSED” REALLY MEAN?

Most of the time, “Closed” means that a problem has been solved or fixed. But that’s not a hard and fast rule: sometimes “Closed” can mean that an issue won’t be worked on any more—that it’s reached the end of the line. Now and again, some customers mention that they’d like a way to put an issue on hold, and they ask for a specific “On Hold” status. That may sound tempting, but from what we’ve found, putting something “On Hold” is a bit like sweeping it under the rug or cramming it into your junk drawer. If something isn’t going to be worked on, you can instead close it and add a note in the comments saying that it might be worth working on in the future.

Or as another option, you could create a category for “On Hold” and put those types of items in there when you close them. We really think that an issue-tracking workflow works best when you think of issues as “something being worked on” or “something that’s not being worked on.” It’s okay to close things that aren’t “complete.” File them away, and if you want to reopen them later, they’ll be there.

### “OPEN” VS. “REOPENED”

You may notice that after an issue has been resolved or closed, it can be “Reopened.” That’s pretty much the same thing as being “Open” again, but we use slightly different visual cues for “Reopened” issues. And we added those visual differences because teams sometimes prefer to treat “Reopened” issues differently from regular “Open” issues. For instance, if an issue were to be reopened because a fix didn’t work out, the developer who attempted that fix may want to give it another try right away.

## WHO GETS TO CLOSE ISSUES?

There’re a bunch of ways to set up your team and your issue tracker. Whichever arrangement you go for, you’ll probably have several roles that interact with your issue tracker. Among them, there’s the “issue opener” or “reporter”—that’s the person who initially filed the issue. Then you have the “assignee,” which is the person who’s working on an issue. And then there’s typically a “reviewer” who double-checks things to make sure everything looks good—to see whether an issue has all its I’s dotted and T’s crossed.

Those three roles could be played by one person—or by three people. There’s no right or wrong way to do it, but we’ve found that things usually work best when the person working on an issue (the assignee) is different from the person checking that it’s done (the reviewer).

Let’s take a closer look at some of the options.

### QUALITY ASSURANCE TEAM

One common setup is to have a dedicated team of folks that do nothing but double-check issues. A great tester is an awesome thing to have, and if you can pull together a QA team—even if it’s just one or two people—I’d highly recommend it.

### THE PERSON WHO OPENED THE ISSUE

If you don’t happen to have a QA team, another great option is to have the person who originally opened the issue review the work on it. Since they’re the one that filed it, they probably have a pretty good handle on what’s involved and what would be expected of the work that’s done.

![A screenshot of the opener data for a Sifter issue.](https://sifterapp.com/blog/images/2011-07-28-resolved-vs-closed/screen_shot_20110728_at_8.42.50_am.png)

2Sifter keeps track of whoever originally opened an issue, the “opener.” Generally speaking, the opener remains the same person from the moment an issue is filed. But if someone happens to no longer be involved with a project, an administrator does also have the option to change an issue’s opener.

### TEAM LEADS

If your team is large enough, you probably have a team lead who’s really proficient in the type of work that you’re doing. And that makes them pretty well suited to reviewing issues and retesting bugs. As an added bonus, this type of arrangement also opens the door for teaching opportunities for more junior developers—when a team lead reopens an issue, that may give them a chance to chat with the developer about what went wrong in their issue and how they can improve.

### YOUR CLIENTS

If you’re a small team working in close contact with clients on simple projects, you might consider letting your clients test and review fixes. That’s not to say that your clients should be your only layer of testing, but it can be a great way to keep your clients engaged and up to date on how things are coming along. This very scenario is one of the reasons we created Sifter in the first place—we had clients that were willing to join in with the testing process, but all the issue trackers we tried were just too overwhelming. So we set out to build an issue tracker that could be approachable for non-technical and technical clients and team members alike.

### OTHER TEAM MEMBERS

If your team is a small group of close-knit developers, you could even have other team members review and retest fixes. But that’s not really an ideal arrangement because developers on a team are often too close to the code to offer an unbiased testing perspective. That’s not to say that this arrangement can’t ever work, but I wouldn’t go for this as your first choice.

### THE ASSIGNEE (THE ORIGINAL DEVELOPER)

You probably don’t want to have the person who worked on an issue be person who’s double-checking that it works. That kind of arrangement should only be used a last resort, but if you have no other option, I’d recommend at least having the developer test their work in a staging or QA environment—that way, you’ll have a chance to test against an environment that’s closer to real life rather than just a local environment on a developer’s machine.

## THE QUALITY ASSURANCE PROCESS

There’s no shortage of ways to develop software. And nor is there any shortage of options for managing bugs and tracking issues. A lot of these don’t have a right or wrong way about them, but I wanted to talk through a few of them to help you make informed choices.

### FANCY A STAGING OR QA ENVIRONMENT?

Some teams try to have their testers work off the team’s development environment. That can seem tempting—especially since your development environment is already up and running—but there can be some perils to that approach. The biggest shortcoming is that testing against a development environment can feel like the ground is shifting under your feet as new features and fixes are constantly being committed to the codebase.

But an easy way to remove that impediment is to set up a staging environment (sometimes also called a QA environment). And once that’s up and running, you can feel confident that everyone’s on the same page and that the testing process is working against a consistent set of code that isn’t changing from one minute to the next.

It’s crucial that your staging (or QA) environment have conditions and data that are as close to your production environment as you can get. That allows you to release code into that environment and comb through all the “Resolved” bugs to double-check that everything’s in good shape—while helping to bring to light any previously unknown side effects that might not have been evident on your development environment.

### SHOULD ISSUES BE REASSIGNED?

If an issue’s opener—the person who first filed an issue—is also the person doing the testing, we don’t think there’s a need to reassign issues as they’re completed. Rather, the person who’s looking for issues to test can just create a filter to see resolved issues that were opened by them. And then they can pick one and go from there.

On the other hand, if the people doing the testing aren’t always the same as those who filed the issues, you may want to consider reassigning issues when they’re resolved. For instance, if you have a dedicated QA or testing team who’s testing issues that may or may not have filed by them, you might choose to have the developers on your team reassign issues to a designated tester once they’re completed.

Or as another option, you could have the developers “unassign” the issues as they’re completed—assigning them to no one. And if you were to go that route, your testing team could then keep an eye out for unassigned issues and test those. (Sifter’s unassigned-issue notifications can come in rather handy in kind of scenario.)

![A screenshot of the unassigned issue notification settings.](https://sifterapp.com/blog/images/2011-07-28-resolved-vs-closed/screen_shot_20110728_at_8.49.31_am.png)

3Each project in Sifter has the option to notify certain team members when there’re unassigned issues. This can offer the flexibility to be able to unassign issues without having to worry about them falling through the cracks.

### IS IT EVER OKAY TO SKIP “RESOLVED”?

You might be wondering, “Well, could we just skip ‘Resolved’ and go straight to ‘Closed’?” Sure—when you’re dealing with things like questions, that can make a lot of sense. For instance, let’s say that someone files an issue to the boss to ask if it’s okay to work outside on Friday. Once they answer that question, the issue can go straight to its “Closed” state—there’s nothing for your QA team to do there.

### CAN “CLOSED” MEAN SOMETHING ELSE?

Here at Sifter, we use “Closed” to mean that “there’s no doubt in our mind that this can safely be released into production.” But maybe your team would prefer that “Closed” have a slightly different meaning—such as to say that an issue has made it through testing but it hasn’t yet been released. Or perhaps your team might prefer to reserve “Closed” for issues that have made it all the way into production. There’s no right or wrong here—it’s up to you. As long as everyone on your team is on the same page, that’s the important part.

## SUMMARY

We created Sifter as a simple tool to track issues. It’s flexible enough to handle a wide variety of development and testing arrangements, and we think that Sifter’s workflow options can be a great fit for most teams and their everyday needs.


## BUG AND ISSUE TRACKER WORKFLOW

One of the most important parts of keeping bug and issues organized is making sure that everyone is on the same page with regard to statuses and uses them correctly. The most important thing to remember is that&nbsp;issues don’t have to be resolved before they can be closed, and in our case, we frequently skip resolved and go straight to closed if the situation warrants it. There are situations, however, where stopping at resolved is key.

![](https://sifterapp.com/blog/images/2013-04-24-bug-and-issue-tracker-workflow/IssueTrackingWorkflow.png)

1Sifter uses a carefully considered set of statuses to provide a simple and flexible workflow or managing issues.

## VARYING DEGREES OF DONENESS

Before we go into how we do things, let’s talk about the benefits of having two layers of donneness in an issue tracker. With software, the cost of fixing a bug before the software ships is always less than the cost of fixing it after it has shipped. Even with today’s teams that are able to constantly ship new versions all day every day, nobody wants their customers to deal with bugs. So you want to be incredibly sure that when you fix something, you fix it correctly. Moreover, it’s simply more expensive to do something twice than it is do it once.

If you want to make sure that it gets done right the first time, you’ll invariably want a review layer within your workflow. With bugs, “Resolved” represents “Fixed” or “Ready for Review”. In general, a developer will fix a bug and mark it as resolved. Then, the original opener will be able to review the fix and make sure that the developer fixed the problem as expected. If everything looks right, the opener then closes the issue and moves on to the next one. This helps prevent simple miscommunication or other errors from turning into shipping bugs.

## RESOLVED

With our team, “Resolved” generally means that the fix has at least been committed to source control. Any potentially unusual situations with resolved issues are addressed with a detailed explanation, or resolution, in the comments. Don’t underestimate&nbsp;[the importance of writing a clear and detailed resolution](http://sifterapp.com/blog/2012/05/issues-resolution-tracking/). It’s easy to be in a hurry and want to simply close the issue, but taking a few extra seconds to type a detailed resolution can go a long ways to preventing future miscommunication.

Depending on whether it’s a one-off fix or part of a larger release, the fix may even be deployed to staging for easy testing. With small one-off fixes, it’s unlikely that we’d deploy to staging, but when we’re working with larger milestones, we’ll regularly release the most current version of the relevant branch to staging. For us, staging is a sort of shared public space for easy previewing and testing of significant releases for the entire team.

We also use staging as the final step of validating significant infrastructure changes. Our staging environment almost exactly mirrors our production environment, load balancer and all. For instance, if a bug is significant or relies on functionality that works slightly different in development than it does in production, then we never want to close it without reviewing it in staging. So if we make a change to our search indexing or cron jobs, testing in development isn’t enough. In these cases, we’ll mark the issue as resolved. Then, when we’re ready, usually when all other issues in the milestone are closed, we’ll release to staging and run through final checks on all of the resolved issues before closing them out.

There are several types of issues where it makes sense for an issue to stop at “Resolved” before it’s officially closed. This usually depends on the type of issue as well as the people involved. You can classify most of these scenarios as approval or review.

*   Approval.&nbsp;In these scenarios, a decision has been made or a feature implemented where someone needs to approve it. For instance, if a couple of us decide on a course of action that will lead to significant server modifications, we’d want to mark an issue as resolved and wait for our system adminstrator to chime in with his final approval.
*   Review.&nbsp;In these scenarios, it’s all about having a second set of eyes on things. If the issue opener and assignee are diferent, it’s easy for the developer to incorrectly believe that a bug has been fixed. By having the original opener review the fix or by retesting the issue in our staging environment, we’re able to have a higher degree of confidence that it’s truly fixed.

![](https://sifterapp.com/blog/images/2013-04-24-bug-and-issue-tracker-workflow/ResolvedWorkflow.png)

2When an issue is resolved, we automatically adjust the interface to help visualize the forward progress of closing an issue as well as the nature of taking a step back if you reopen an issue.

Just as it looks in the interface, “Resolved” is a liminal zone where the problem is solved but needs verification or approval to be 100% complete. It’s perfectly valid to reopen the issue and bring the discussion back to life. In our ideas project, we’ll often promote issues to “Resolved” and leave them there until we’re ready to proceed further. We aren’t quite ready to close the issues, but we do want to acknowledge that we’ve tentatively made a decision.

## CLOSED

Once an issue is closed, it’s ready to go. “Closed” doesn’t mean “Live.” It simply means “Closed.” That is, it’s either fixed and has been reviewed or it’s something that doesn’t currently need any further attention. You could say it’s basically like saying, “Nothing more to see here. Move along.” When all issues in a given milestone are closed, it’s a safe bet that the associated branch should be ready for release to production.

Like resolving an issue, there are two subtle variants behind the meaning of “Closed”. Either it’s complete and ready to go live, or it’s something that either isn’t going to happen or is no longer relevant. In either situation, no further attention is required at this time. “Closed” can even work as a sort of “On Hold” status if your team is comfortable using it that way. Remember,&nbsp;[it’s dangerous to explicitly have an “On Hold” status](http://sifterapp.com/blog/2011/07/why-on-hold-is-evil/), and Sifter provides several alternatives to achieve the same goal.

*   Complete.&nbsp;In these scenarios, the issue is both resolved and reviewed. It’s ready to go, and nothing more needs to be done.
*   Back burner.&nbsp;Closed doesn’t have to imply “fixed.” You can think of closing an issue as a simple way to get rid of an issue if you’re unlikely to do anything about it in the near future.

![](https://sifterapp.com/blog/images/2013-04-24-bug-and-issue-tracker-workflow/ClosedWorkflow.png)

3When an issue is closed, we automatically limit the options and help visually communicate the nature of taking a step backwards when reopening an issue.

It’s easy to forget, but along with closing issues, anyone can always reopen issues. Issues never die, they’re simply moved off of your todo list. They can always be brought back to life with a simple comment. Internally, this happens all of the time as we revisit old ideas or think of new ways of looking at ideas we previously believed weren’t right for Sifter.

## NOTHING IS ABSOLUTE

It’s critical that multiple layers of doneness are available in a bug tracker, but those extra layers are only a suggestion for when it’s relevant to the given issue. Don’t be afraid to close issues or skip the resolution step if there’s no review necessary. It’s structure, but it’s designed to be optional structure. There when you need it. Gone when you don’t.