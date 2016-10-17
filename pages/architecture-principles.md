---
layout: page
title: DRAFT Architecture Principles
permalink: /architecture-principles/
published: true
---

## Why have Architecture Principles

They help address the following issues, which can have significant long term
benefits to an agencies IT footprint. In addition they enable collaboration between different business groups
that have similar technical needs, which can greatly improve the efficiency of the overall agency.

 * Ensure a system is secure and performant
 * Selection of a suite of technologies
   * Ensuring technologies last for the lifetime of a system
   * Minimisation of transition costs when adopting newer technologies
 * Cost of integartion with other systems
 * Availability and access to skills and capabilities
   * Minimisation of maintenance and enhancement costs
   * Reduction of change costs

The overall strategy is quite simple to address the above - ensure code and configuration developed
in house (by the agency itself) is minimal in contrast to the code and configuration the IT system
is built ontop of. This leads to the first principle:

## 1. Share, then re-use, then extend, then buy, then build.

### 1.1 Sharing (co-habitation of data and functions with an existing system)
If a system already exists, and data ownership and classification can be cleanly negotiated for 
co-habitance on the existing system, it is best to use the existing system. An example of this would
be [OpenStreetMap Nominatim](https://nominatim.openstreetmap.org/) - it is much lower cost to use the existing system to find addresses, than to build
a separate address lookup database. If data needs to be added, then adjusting licenses to be compatible
will greatly reduce the overall costs of maintaining and delivering the service, as opposed to even re-using the code to 
run a similar service on your own, as that service would require infrastructure, configuration, maintenance and securing - all of
which have costs.

### 1.2 Re-use (open source, or well supported commercial platforms)
Popular open source and commercial frameworks and toolkits have addressed several of the base issues in building an application,
such as the [OWASP](https://www.owasp.org/index.php/Main_Page) Top 10 critical web application flaws. Preferentially for support and
extensability open source platforms are preferred, but in areas where there are no good open source alternatives, then commercial
platforms may be more suitable, as long as they are using open data formats. The use of closed data formats is a very high risk to
future maintainability and transitions, as it encourages lock-in and makes it exceedingly difficult to move in the future.
[Closed proprietary formats](https://en.wikipedia.org/wiki/Proprietary_format#Closed_Proprietary_Formats) should be avoided at all costs.

### 1.3 Extend

### 1.4 Buy

### 1.5 Build