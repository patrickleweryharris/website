---
layout: page
title: Hoard Implementation
description: Hoard memory allocator implementation
permalink: /projects/hoard/
redirect_from:
    - /projects/hoard-impl/
---

By Hsuan-Hao Chen & Patrick Harris.

As part of our course work for [CSC469], we
implemented a parallel memory allocator, based on the Hoard allocator.[^1]
We sought to understand the various strategies that can be used to improve
memory performance on a modern multi-processor system. The design of our parallel
memory allocator mainly follows the design laid out in the Hoard paper.
In keeping with the Hoard design, we trade
"increased (but bounded) memory consumption for reduced synchronization
costs."[^1] Hoard also seeks to avoid false sharing,[^1] through seperating
the memory blocks which different threads access.

The Hoard design avoids costly synchronization of the whole heap. Rather,
synchronization is on a per processor heap level. So, a different thread could
satisfy it's allocations while other operations are going on. Since a different
portion of the heap is accessed, there are no false sharing issues.

[CSC469]: https://fas.calendar.utoronto.ca/course/csc469h1
[^1]: Emery D. Berger, Kathryn S. McKinley, Robert D. Blumofe, and Paul R. Wilson. Hoard: A scalable memory allocator for multithreaded applications. SIGOPS Oper. Syst. Rev., 34(5):117–128, November 2000
