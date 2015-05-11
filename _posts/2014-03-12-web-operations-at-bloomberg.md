---
layout: post
title: Web Operations at Bloomberg
tags: devops, chef, operations, bloomberg
nav: Blog
---
For the past year I've been working on a grassroots effort building reusable
patterns for infrastructure at [Bloomberg Government][1]. Over the course of
a year [my team][2] was able to stabalize and automate datacenter operations.
Because of legacy infrastructure our focus was primarily on the applications
rather than the machines themselves.

Of course making application deployments deterministic and improving the
continuous delivery pipeline were likely the low hanging fruit at [BGOV][1].
But the larger issue needed to be managed at orchestration and provisioning
of new virtual machines. The more that we dug into the problem we realized
that BGOV was not the only organization at [Bloomberg][3] that was suffering
these problems.

As of two weeks ago I've been given a [tiger team of engineers][5] throughout
[research and development][4] to work with our cloud infrastructure and solve
these problems for all of our web verticals. We were given the charge to
automate the datacenter operations - including orchestration, provisioning and
continuous delivery - and integrate with the enterprise systems that we use
throughout our firm.

This goes hand-in-hand with implementing a culture of [DevOps][6] where the
firm promotes communication, collaboration and integration amongst all of the
stakeholders in a business unit. This includes the research and development
component of a product, but also the business and technology support teams.
The ultimate goal is to deliver a stable, higher quality product to our
customers faster.

[1]: https://bgov.com
[2]: http://thoughtlessbanter.com/2013/01/16/team-duct-tape/
[3]: https://bloomberg.com
[4]: http://careers-origin.bloomberg.com/careers/experienced-professionals/research-development/
[5]: http://en.wikipedia.org/wiki/Tiger_team
[6]: http://en.wikipedia.org/wiki/DevOps
