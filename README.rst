================
Rotor Persistent
================

:Status: Proof of Concept

The library that simplifies writing client protocols with persistent
connections, auto-reconnecting, DNS resolving and refreshing of DNS records,
and pluggable name services in future.


Motivation
==========

There are two models of working with client connections:

1. *On-demand* connections: when you need to request some resource, you
   establish a client connection, do request, then probably close it, or
   reuse for subsequent requests
2. *Persistent* connections: connection is established at application startup
   and kept alive indefinitely

While there are clear use-cases for both of them, there is a clear prevalence
of on-demand connections in cases where it's not the best solution:

* Database connections
* Memory cache connections
* Connections between micro-services
* Connections to monitoring systems

The good example of the on-demand connection is perhaps the `github webhooks`_:
there are lots of target hosts and each of them is mostly inactive (and even
github could use persistent connections for super-popular services like
Travis CI).

We believe that ubiquity of the on-demand connections is not because that
model is great but for two reasons:

* it's *easier* to create a protocol for on-demand connection
* the inherent problems of that model are deferred to the production system
  and usually to some catastrophic conditions

Another *miserable* thing about using inherently on-demand protocol
implementation is that if you use a single connection for long time duration
you can't change the target server where connection is established. Name
resolving is usually done at connection time.

So we opted-in to seamless integration with service discovery
including refreshing already established connections. Note, you don't need
to setup a fully featured name discovery cluster to use the library, working
DNS with nicely tuned TTL (time to live, i.e. cache expiration time) is enough
for the start.

So this library aims to bring **implementation simplicity** to the persistent connection world.

.. _github webhooks: https://developer.github.com/webhooks/


License
=======

Licensed under either of

* Apache License, Version 2.0,
  (./LICENSE-APACHE or http://www.apache.org/licenses/LICENSE-2.0)
* MIT license (./LICENSE-MIT or http://opensource.org/licenses/MIT)
  at your option.

Contribution
------------

Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion in the work by you, as defined in the Apache-2.0
license, shall be dual licensed as above, without any additional terms or
conditions.

