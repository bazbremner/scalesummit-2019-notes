What hell am I running in production, how do I update it, how do you
deal with the images updating? Do you just update the world?

There's different things: are there things with known CVEs? Is the
thing I'm deploying what I think I'm deploying?

Q: mutability of tags, or signing?
(Folk in the room concerned about both)

Mutability of tags is a feature of the _registry_ - it should be
possible to set that as an option (but docker hub and others allows
for mutability)

One person building based off of digests, not of tags, but that's been
awkward, as updates are generally useful.

Having sufficient testing gives confidence that functionality isn't
regressed, in more mature orgs that should also include
security/correctness bests.

Do people test the images that come from the library
i.e. _java. generally people do trust them and trust open source, but
there are people will attempt to inject malicious content.

The official images go through a whole bunch of checks. Random builds
don't see much, but the official builds go through alot.

A lot of teams seem to trust that all security updates are being
supplied by library/base images in a timely fashion.

Do consider that certain classes of attacks could be mitigated when
the breakout is only into the container.

The alternative to trusting the community images are building it
yourself. You need to spend time making sure it's done reguarly and
kept up to date

Where do build their images? Several people building in CI.

Ask for a show of hands for internal base images. Probably 25-30% of
room raises hands. Some this seems to be in the hands of one person
and needs more automation.

Any 3rd party services to build containers and keep them to date?
Docker Hub builder was one option.
Requester was focusing on can you pay to ensure security updates are
applied in a timely fashion. "Do you want to start a business?
[ie. no, not that anyone knows of]

How do you really know that the new images are trustworthy? Perhaps
that one person _is_ the check? Quay does layer scanning.

Which tools are people using to scan containers?

- Anchore
- Quay (which uses Clair)

Most use public package vulnerability information and misses a few
things, then you look at paying more money 

Other options:

- Aqua
- Synk
- Blackduck
- Twistlock

Does anyone pentest against individual containers? Zero hands -
everyone that is testing uses pentests against the whole system

Consider balancing your risks and potential outcomes.

Most mass attempts to compromise images is bitcoin mining. You're
probably not that important, but if you're likely to be directly
targetted, you've got other problems and workarounds to put in place.

Are most compromises botnets or bitcoin mining? Bitcoin mining is the
right profile as containers are probably running in the datacentre
with good power/CPU. Botnets are better scattered all over the place.

For a lot of criminal groups, the soft, cheap targets are the best:
Wordpress, Drupal etc. 

What are people doing for fan-out and making sure they pick up the new
images? If you trust the public python image and it gets updated, how
do you force that out, other than rebuild every 2 weeks regardless?

Does dependbot do this now? No, due to mutate tags?

This might well relate to a later session today about building
sustainability: build to change/update everything all of the
time/regularly: consider not re-deploying/updating a service in a
while an incident.

Doing it regularly does give you confidence if something big does
happen, then you're in a better position to push out more changes.

This does depend on what else in the org has to change/permit rapid
updates. If there are many changes that depend on each other, just
re-rolling and re-deploying every 2 weeks it can still take a very
long time from base image being updates, dev teams updating, etc etc.

If you are in a change controlled environment, of course, try to get
to the point where such updates are considered BAU.

Teams that build their own images, what sort of testing do you do? One
team was building a platform-team owned hello world app that did basic
API/web plus database connectivity and deployed into the platform to
perform basic smoke testing, each team still needs to do its own
diligence.

Openshift Image stream and tekton can do fanout of dependancies
between images.
