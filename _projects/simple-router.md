---
layout: page
title: Simple Router
description: Mininet simple router
permalink: /projects/router/
redirect_from:
    - /projects/simple-router/
---

As part of my course work for [CSC458 - Computer Networks](https://fas.calendar.utoronto.ca/course/csc458h1)
at the University of Toronto, I implemented a simple router in C using the Mininet system.
The assignment description can be found [here](https://github.com/mininet/mininet/wiki/Simple-Router).

In brief, the router needed to correctly direct packets through the network.
We implemented functionality to correctly route IP packets, and process ARP
packets. We construct ARP replies for received ARP requests. For ARP replies,
we cache the information to be used in future routing decisions.

IP packet handling involved verifying the checksum of IP packets, and forwarding
those packets to the next hop identified by querying a static routing table
using [Longest Prefix Match](https://en.wikipedia.org/wiki/Longest_prefix_match)
searching. Ethernet packets to that next hop were constructed using cached
information from our ARP cache. If we had no cached information regarding
the destination of a packet, an ARP request would be sent by our router.

The router I implemented also received ICMP and TCP / UDP packets
for the purposes of ping and traceroute. We respond to ICMP echo replies
to ICMP echo requests, and ICMP errors for TCP and UDP packets (as this
is required functionality for traceroute). ICMP errors were also
sent for any errors encountered in other functional areas.

As this assignment continues to be used for future offerings
of CSC458, my implementation is not publicly available.
