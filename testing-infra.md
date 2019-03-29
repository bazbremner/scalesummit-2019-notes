Testing infra in 2019: what are people doing to get feedback before
(and perhaps afterward) rolling out changes? Doesn't have to be tech,
can be process too

Previous role, OP used test-kitchen with chef. These days, just
running terraform plan isn't exactly going to give a lot of
confidence.

Other people:

- Using a docker container to lightweight VMs to run chef etc through
  to make sure different combination things run cleanly.
- GOSS also used for testing (although might be abandoned these days)
- Terratest was mentioned, but no-one has used it.

What problems are you trying to check for? What conditions are you
trying to find?

Quite a few tools seem to focus on testing the configuration of
software on machines, but that's not quite the same as testing the
system as a whole.

Another person has tests (using their own code) that checks for ports
being exposed, other ports explicitly not exposed, DNS records have
been created.

- test-infra is a Python library that can perform those sorts of
  black box testing.
  
- BATS, inspec, GOSS can do more black box testing.

Other tooling is tied to the infrastructure tooling itself
(i.e. test-kitchen, terratest etc).

What are people's ideal workflow? OP is from a dev background.

With code, your inputs are relatively small, but with infra, your
input is the whole internet, and some of those conditions (i.e. AWS
telling you there are no more VMs available) is difficult to mock.

One person describing problems with upgrading existing machines vs
provisioning new ones. Updates worked, new didn't, so introduced
spooling up a new machine as part of the CI run on each commit.
When ASGs were added and Terraform controlled that, added tests for
functionality on the box (i.e. connecting to clusters).
A lot of the infrastructure can depend on being networked, but that
might be hard to test.

Consider the bounded domains: does the box/service come up and listen
on a port, next look at the network requirements: can I connect to the
remote syslog server etc.
GOSS can do this.

So, how does this differ from your production suite? Perhaps it
doesn't, however you might need to filter alerts that you don't need
to get people out of bed for.

Not entirely the same as monitoring, but more making sure that you
don't break things _before_ you get to production. 

Other team has something that's closer to linting - basic checks for
security groups that don't open things to the world, don't use
'latest' container tags etc.

Parts of industry apparently moving to presenting an API/layer that
makes things above and below those layers are other teams concerns.
The low you go down the stack, the more it becomes obvious it's all
about the hardware and physical world.

One person entirely on AWS, uses Cloudformation linting and testing
and puppet testing to ensure the catalog compiles. Using AWS Config
and AWS Catalog to set up rules to flag things with 0.0.0.0 access and
is properly tagged for example.

There's not one thing that fits every case. One person's infra might
be going all the way down to the air con units, but in public cloud,
that's a little easier to consider.

Are you using one tool or many: almost certainly many.

One person looking at Rego (?) - a data query language, I've got data,
I want to make assertions against it. Oh God, another DSL, but it
looks interesting.

As far as testing that you're not opening everything to the internet,
it used to be hard, but it's getting easier to look at things like the
Terraform plan file (assiming you're using it) which will get easier
with 0.12.x, as there's JSON output that can be processed. Up to this
point, you're having to rely on Terraform tooling to process the
binary plan files.

Other people have used to Ruby landscape gem to process plan files
and make it easier to parse.

When deploying to environments, what are people doing to avoid things
being snowflaked, obviously you can process Terraform's output there
are other changes?

- Terradiff
- prowler can watch AWS APIs and kill things that aren't appropriately tagged
- Kubediff

Back to monitoring: one team has written a series of integration tests
to ensure that behaviour that some consumers depend on, which is
effectively a consumer driven contract against the system

There are lots of tools and options, do people have war stories about
what is worth the effort and what isn't worth the time.

A lot of tools we use are declarative. I don't want to test that when
I tell puppet it install a package that puppet does - puppet should be
well enough tested.
Instead they'd want to check that when the conditionals in their code
gets passed down to puppet.
Either way, it can sometimes feel like you're just defining the same
thing twice.

Seperate the assertion from the implementation or process: i.e in
production you expect something to be a particular way, but in test,
it happens a different way.
Example: can you assert something is being bought. You might not want
to actually buy things in prod with a fake card.

Consider how you split the modules/libraries from data that drives the
behaviour.

How to people work out a model where they use Terraform, but use
blessed modules? We want to have teams to use modules that give a
specific configuration and not potentially spin up VMs directly.
Terraform Enterprise is supposed to handle some of this.
Another person used the aforementioned Rega to check AWS primitives
weren't used.

Is anyone using another language to generate their config? Some people
have used Ruby to generate config. DAR was mentioned as another
configuration language.
Pulloomi you can write Typescript and take descriptions of interacting
with AWS or Kubernetes. It's not an abstraction, it's a different
syntax, mainly for people that like types in their code.

One observation from the room: lots of talk of tools to protect us,
but there are social approaches of explaining why some approaches are
bad (or making it safe to make bad changes).

Is this the thing we're trying to address? Answer from several:
breaking prod is bad, but we're trying to make sure we all avoid
impacting other teams.

Some teams have tried automating impact assessments, scoring based on
components being affected etc.

Isolating systems and reducing how many things are affected can help.

Talk about pushing changes to each teams, you're not responsible for
changing everything, each team. Apparently Google are all the way to
making that live with the person making the change - if you want to
change TLS versions, you have to change _everything_.

Is anyone testing config? Linting certainly popular, but most people
will test behaviour, not the config.

One team have 2 other environments ahead of prod that are pushed to as
part of CI (a popular arrangement, but interestingly not something our
key note speaker was not keen on).

Further questions: is one environment a dev thing, or infra? Does it
matter, how do we use the existing tooling.

One example was upgrading from k8s 1.11 to 1.14, at one point you get
two environments (or do you? maybe it's just semantics).

You can't mock AWS on your laptop. A few teams are carefully managing
traffic to deploy into production and use canary deploys to test code.

One thing with this is what is "the production version" - everything
is in flux. Done properly, this shouldn't matter.
