It takes time and money, but one team has found it relatively
easy. 5-600 containers, 50 tenants.
Upgrades is the hardest part. Using kops, using in-place updates.

Are people running one cluster, or several?

Q: what does kops give you? Creates AWS resources, creates masters and
nodes, can do updates.

Maintainence windows for components (i.e. docker vs kubernetes) don't
necessarily line up. Not really an issue, given kops, aks-engine etc
ship combinations of components and you could chose to install your
own versions if you really have to.

What about backups, etcd. One team is running kubenetes on bare metal,
spinning up new clusters isn't really an option.

Hands up for who is running kubernetes? 4/20 people. The rest are here
for the horror stories.

Someone not running interested to know if they should run it, pay
someone else, is something like kops worth having.
One person: kops pretty good, things have happened, haven't had major
issues.
Sometimes see network blips, blow that node away, try and treat as
much as possible as cattle.
Try to keep state off the cluster.

Some people running Elasticsearch as stateful sets. 100s GiB of
data. Other was in the single digit TiB range of data.

For people running it, how big are the teams. All teams were 3-4
people, ranging from part to full time on the cluster.

What tasks? Rolling updates, patches, helm updates.

Fear one person has is standing up the cluster is easy. There's a lot
of stuff happending under the hood, then what happens 3 months down
the road and something breaks. Do things self-heal?

Are there references you go to? No further info.

Reply: yes, it is easy, getting easier. Some of the magic around
iptables for routing is harder. It's moved IPVS and it's easier to see
what's going on.
ipvs adm easier than iptables.

Metrics out of the box is a shit show. Gone from heapster to metrics
serve, things like HPAs using different metrics from dashboards varied
across migration period.

Is there still a choice about network stack. One team using network
router, hasn't used others.
IPVS rolled out, this team enabled as a beta.

How opinionated is it? Mostly pretty sensible out of the box, but
everyone seems to get a little confused around which networking
tooling to use and why.

Choosing the networking is probably more important if you're running
on your own tin.

With managed k8s, the feature set varies across providers.

Ingress controller healtchecks on GCP was confusing for one person and
there's an open bug.

For people running their own, why not run a public offering.
- One team: use large amounts of bandwidth, and could get that much
  cheaper than being in public cloud and k8s was an aside.

The managed implementations seem different in their own way, has
anyone compared/got prefences?
- EKS manages the masters, but you still need to do a lot of
  management of the agent nodes.
- GKE probably easiest to get going with

Do all the cloud providers give integration with things like IAM?
For being on AWS:
- kube2iam for pods, although that's being replaced by something else
  (sorry, can't remember name)
- heptio/aws-authenticator for kubectl auth
