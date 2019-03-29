The attitude of 'we're just going to run it' doesn't work well,
especially when handed off to another team.

You need to build incentives so people understand what's at stake, or
can understand that previous shortcuts affect the system now.

When you're in the thick of it, it always feels like you've got legacy
and problems, and sometimes you need to look at the context.

Other sources of issues is with teams taking on software built by
third parties, possibly with not enough information.

Budgets don't always work: there's a percentage that'll go to running
a service yourself, but if it's outsourced, that might come from
another budget and yet that's acceptable.

One org had microsites built for specific products being released, but
it wasn't being maintained, webservers couldn't be updated etc.
The change they made was to follow the money: the site had to be run
in an AWS account, when the money stopped coming, the site was
decommissioned. 

Someone attended a talk about "Software cell death", it seemed that
always more and more was being written. 60 apps running, everyone
working on the tip of the iceberg of code, then had to down tools to
fix all those apps.
Do they need to try harder to shut off old apps, or expose the
ecomonics better?

Another person worked in an org where there was a quarterly reviewing
apps that were in place and reap unnecessary ones.

Q: has anyone worked in a place where the apps are abandoned.
One org has ~50 apps that didn't have clear ownership after several
years, and now have created a platform health team to own ~40 of these
apps that are still required.

Another org has a group that owns the unowned apps, but every
application group has to pay into funding the unowned app, if the
teams want more money, one solution is for them to take one or more of
the unowned apps from the central team and give them a new home (and
get the budget associated with running that app).

Making the maintenance of these apps open and visible can go a ways to
help solving the problem. Too many ops/SRE teams running things in the
shadows.

One company talking around the Google SRE model, with a central team
owning all the unowned apps. They turned that around and pointed out
there are standards to having apps accepted and that if there is no
budget, docs, source code and it spurred people to accept and fund
apps.

When you think about maintainability, has anyone worked on those
teams? How do you make it humane?
One person worked in such a team, but they got a mix of keeping the
old stuff up and running, but were granted time to also learn newer
skills.
Another team improved apps to the point where they were acceptable and
were owned again, helped team's profile.
Another took a product developed by a third party and expected to keep
it running, however keeping it running required more understanding and
improvements, so it morphed into some active development as well,

One org had two teams developing in sprints and a third group that was
formed for the sprint to act as an internal consultancy to help other
team improve software.

Consultancy feels like a better solution to the 'bribery model' of
shovelling shit.

There's a tension between the org that just want things done and done
now, and ensuring that maintenance and initial engineering quality is
carried out.

One person was at a startup that delivered in small pieces, but not
much attention to the bigger picture. Pitched _appropriate_ levels of
quality for robustness, testing, and other metrics. Also trying to
show things as a service, rather than as a product. Services being an
ongoing cost in public infrastructure, rather than something that was
built and shipped once.

Retorical question: are the 3 users a month we get really worth the
1k/mo in expendature?

People don't have much love for legacy systems, because it's harder to
understand the number of customers those systems support, or how much
they cost.
Sometimes those legacy systems are provide huge amounts of value.

If I have an existing brown field site that no one owns, how do I take
the first steps to start getting that owned and improved and improve
the culture?

One person was brought in to improve things tried:

- getting everyone involved in having an understanding
- consider code as a liability
- represent customers/reliability as another other feature
- improving culture around owning systems

Another approach was to amorise a replacement fee for a service as
part of the running cost of a new service. Build up a slush fund ahead
of a service needing replacing in N years.

Another org has created a 'tiger team' that takes code from the dev
teams. People from dev teams rotate onto the tiger team, so there's
still a feedback cycle; you might not fix your broken code, but you'll
probably encounter others.
However, there's no long term ownership of code; the dev teams don't
see the same code in the longer run.

One experience: taking code that's been built and improving it over
time. If people can see the benefit of engineering well it does help.
Lots of people are terrible at pricing things. A lot of the work is
explaining the costs of demanding immediate delivery, and they might
not consider the ongoing costs or hidden costs of keeping systems
updated.

Another org is considering "tech debt" (perhaps not the definition of
'a short term compromise to fix later') and are now considering that
there's some 'gardening' to improve the whole estate and it's now
being factored in.

Lots of talk of budgets. People on the other side of the table are
balancing that against business they might win vs spending money.

Person is a big fan of Don Reinertsen's 'cost of delay'. Getting tht
cost of delay figure can be very hard. You should try to engage with
accounting/finance people.  Another +1 for that.

Also look at Steve Freeman's talk on A Bluffer's Guide to Techical
Debt.

Phoenix project also mentioned.

There are cultural problems in some orgs - they don't necessarily want
to know how the sausage is made. Just give a date.
If you're in an org that you can discuss tech debt, you're well ahead
of the game.

Tech debt is like paying the mortgage. You can miss one or two
payments, but eventually they'll come and take the house.

It's all about incentives.
