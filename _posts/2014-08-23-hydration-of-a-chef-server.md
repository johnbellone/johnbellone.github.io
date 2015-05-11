---
layout: post
title: Hydration of a Chef Server
tags: Chef, DevOps, Bloomberg, WebOps, Chef Server
---
At [Bloomberg][11] my team is tasked with supporting infrastructure
for all of our consumer and subscription web properties. We have been
using Chef to solve some of our problems around configuration
management. Most of our recipes were built using Chef Solo and
eventually deployed on our cloud infrastructure without a Chef Server.
As we began to plan to deploy software services to the teams that we
support we quickly began to realize that it would be nearly impossible
to manage multiple node deployments without Chef Server.

Our immediate need was to provision a Chef Server for our build
infrastructure that we would be distributing to about twenty
teams. But in addition to this we have brought in [Chef][4] to train
several classes of our developers. After the classes concluded there
were many requests for individual Chef Server tenancies for testing.

Using Chef Server within our infrastructure was an afterthought
because most of our virtual machines had a very short lifespan. Since
we could have several dozen development teams wanting their own Chef
Server deployments we needed a solution to not only easily deploy a
Chef Server, but to hydrate it with the data necessary for each
OpenStack tenancy. This included both user and client authentication
information.

After a bit of back and forth I was able to isolate the requirements
for our Chef Server infrastructure:

1. It must use the [Chef Server community cookbook][2] and the
[Omnibus packages provided by Chef][5];

2. It should be quick and easy to deploy a new instance because we
may be doing so for several dozen tenancies in OpenStack;

3. All user and client keys should be generated locally and the server
should be hydrated during the initial convergence run;

I was first introduced to [Chef Metal][12] at this past year's
ChefConf where [John Keiser gave an excellent talk][13]. My team has a
lot of experience using Vagrant, but it made much more sense to me to
include a metal recipe with our Chef infrastructure cookbook. It could
serve as both a teaching aide, and would also make our internal
cookbooks much more versatile. Throughout the discovery process I
found the community [Chef Server Populator cookbook][6], ended up
completely rewriting it to use Chef resources to modify the Chef
Server, and ultimately used Chef Zero to bootstrap everything.

## Playing with Metal
Using Chef Metal I was able to easily distribute a recipe with our
Chef infrastructure cookbook that would provision a Chef Server very
easily using the _machine resource_. The recipe that I began with
looked very similar to what is below. It first laid down changes to
the base operating system using our base cookbook, and simply used the
community cookbook to install the Chef Server from the Omnibus
packages. It was very straight forward.
<script src="https://gist.github.com/johnbellone/64ffc30e5fe737472168.js?file=chef-server.rb">
</script>

Unfortunately I still needed to hydrate the local data into the newly
minted Chef Server. Luckily for me the cats over at
[Heavy Water Operations][7] have solved this problem and provided the
[Chef Server Populator cookbook][6]. There were only a few minor
modifications that I needed to make to support client validation
keys. But other than that everything seemed to be smooth sailing.

## Chef Zero
At first, with only a few minor changes, the Chef Server Populator
cookbook seemed to be the answer to my problems. I had a few cases
that were not covered, but these were all pretty simple extensions.
It was natural and made sense to convert our Chef infrastructure
cookbook into a Chef repository and use [Chef Zero][3] as an in-memory
Chef Server during the initial provisioning.

That worked out quite well at first. I was able to cobble together a
simple Rake task to generate and write out the private and public keys
to JSON data bag items. My metal recipe started to look a lot more
complex than I had initially intended, and it didn't seem as clean
as I thought it could be. As I was reading through the code for the
[Chef Metal Fog driver][8] a light bulb went off in my head: I could
use the [Cheffish gem][9] Chef resources and build the data on the
fly!

### Chef within Chef
I ended up completely rewriting the Chef Server Populator cookbook.
[My fork][1] now used the Chef resources provided by the Cheffish gem
to read from data bag items and create the user and client records
against the Chef Server node. The beauty of this approach is that I no
longer had to execute clunky knife commands since in Chef 11 erchef
exposed an API to pass both user and client public keys. The cookbook
is [now much more clean and simple to grok][1].

The code for creating the user and client keys was also able to use
the same Chef resources from Cheffish. Instead of operating against
our newly provisioned Chef Server it executed against the in-memory
server provided by Chef Zero.

Using keys which are generated inside of the metal recipe is not
idempotent. There were two ways that I went about solving this
problem. This first was merely reading in the private keys off disk
and delegating the generation to some external process. The second
would be to use the Chef resource to generate private keys and allow
it to manage if they needed to be updated or not. Ultimately it worked
out that if the keys were generated outside of the metal recipe it was
much more straightforward. Here is a full example where keys for
clients were generated outside, but user keys are generated on the
fly:
<script src="https://gist.github.com/johnbellone/5a72111898c7709dddeb.js">
</script>

## Tying the Bow
The final result was a complete [cookbook refactor][1] which uses Chef
resources to hydrate a newly provisioned Chef Server. The default recipe
uses node attributes and creates both client and user resources on the
new server. A data bag recipe uses a Chef data bag search to find items
and applies them to the node attributes prior to including the default
recipe.

Since Chef Zero provides a fully functioning in-memory Chef Server we
are able to use Chef resources to add data bag items with locally
generated public keys. When using the Chef Metal recipe this data is
now made accessible to the data bag search, and thus it gives us an
elegant way to hydrate a Chef Server. I have provided an example of
this [inside of my fork of the cookbook][10] which illustrates all of
the steps above.

As I mentioned at the top of this post I originally started work on
this solution to allow us to quickly deploy our build infrastructure
to multiple tenancies within our private cloud. In a future post I
will explain how my team was able to create an easily deployable
continuous integration framework using the [community Jenkins recipe][14].

If you are reading this post and are interested in joining our growing
group of Chef technologists at Bloomberg feel free to reach out to me.
[We are hiring][11]!

[1]: https://github.com/johnbellone/chef-server-populator
[2]: https://github.com/opscode-cookbooks/chef-server
[3]: https://github.com/opscode/chef-zero
[4]: https://getchef.com
[5]: https://github.com/opscode/omnibus-chef-server
[6]: https://github.com/hw-cookbooks/chef-server-populator
[7]: http://hw-ops.com
[8]: https://github.com/opscode/chef-metal-fog
[9]: https://github.com/opscode/cheffish
[10]: https://github.com/johnbellone/chef-server-populator/blob/master/examples/chef-server.rb
[11]: http://jobs.bloomberg.com/search/?q=chef
[12]: https://github.com/opscode/chef-metal
[13]: http://slides.com/jkeiser/chef-metal
[14]: https://github.com/opscode-cookbooks/jenkins
