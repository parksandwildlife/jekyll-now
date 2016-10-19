---
layout: page
title: DRAFT Architecture Principles
permalink: /architecture-principles/
published: true
---

## Introduction

An agency develops and procures a multitude of IT systems over time. If not appropriately architected these systems can result in growing costs and risks, as
system acquisition typically focuses on business needs, tending to neglect long term and non-functional requirements. On the other hand, resorting to enforcing
a strict set of rules for an agencies IT environment, can result in stagnation and the inability to capitalise on opportunities when they arise. The principles below
have been written in an educational style, with several examples to demonstrate what real world implementations of them would look like.

## Scope

This document is targeted at any role involved in the design, build or acquisition of IT systems for Parks and Wildlife. It aims to provide a clear understanding and approach
to selecting technologies and vendors to expand the agencies IT capabilities to meet business needs. Note that the first 3 principles apply to all IT systems, while the remainder
are more focused on managing the development and deployment processes themselves - and as such may not be relevant to "As A Service" type IT systems.

## Why have IT Architecture Principles

They help address the following issues, which can have significant long term
benefits to an agencies IT footprint. In addition they enable collaboration between different business groups
that have similar technical needs, which can greatly improve the efficiency of the overall agency.

 * Ensure a system is secure and performant
 * Selection of a suite of technologies
   * Ensuring technologies last for the lifetime of a system
   * Minimisation of transition costs when adopting newer technologies
 * Cost of integration with other systems
 * Availability and access to skills and capabilities
   * Minimisation of maintenance and enhancement costs
   * Reduction of change costs

The overall strategy is quite simple to address the above - ensure code and configuration developed
in house (by the agency itself) is minimal in contrast to the code and configuration that is re-used.
This leads to the first principle:

## 1. Share > re-use > extend > rent or build.

### 1.1 Sharing (co-habitation of data and functions with an existing system)
If a system already exists, and data ownership and classification can be cleanly negotiated for 
co-habitance on the existing system, it is best to use the existing system. An example of this would
be [OpenStreetMap Nominatim](https://nominatim.openstreetmap.org/) - it is much lower cost to use the existing system to find addresses, than to build
a separate address lookup database. If data needs to be added, then adjusting licenses to be compatible (see the [Open Database License](http://opendatacommons.org/licenses/odbl/summary/))
will greatly reduce the overall costs of maintaining and delivering the service, as opposed to even re-using the code to 
run a similar service on your own, as that service would require infrastructure, configuration, maintenance and securing - all of
which have costs.

### 1.2 Re-use (open source, or well supported commercial platforms)
In some cases data may not be appropriate to reside in the same system instance (e.g. due to security/legislative constraints). In this scenario
if the system meets the requirements of the business, re-using it's code and configuration in a new instance is preferrable, though consideration
is required to ensure the support of the code and config for the new system is appropriately shared between the two or more distinct parts of an 
agency that may use it. Preference is given to [open-source](https://opensource.org/) platforms due to the ability to modify and provide back to the upstream authors any
changes that may be required, which is typically lower cost and less restricted than proposing agency specific changes to a commercial product.
The [Linux Foundation's](https://www.linuxfoundation.org/about) [Long Term Support Iniative](https://ltsi.linuxfoundation.org/what-is-ltsi) 
has a good breakdwon on the [advantages of upstream alignment](https://ltsi.linuxfoundation.org/what-is-ltsi/advantages-upstream-alignment).

### 1.3 Extend (build on top of an existing system / framework / toolkit)
Popular open source and commercial frameworks and toolkits have addressed several of the base issues in building an application,
such as the [OWASP](https://www.owasp.org/index.php/Main_Page) Top 10 critical web application flaws. Preferentially for support and
extensability open source platforms are preferred, but in areas where there are no good open source alternatives, then commercial
platforms may be more suitable, as long as they are using open data formats. The use of closed data formats is a very high risk to
future maintainability and transitions, as it encourages lock-in and makes it exceedingly difficult to move in the future.
[Closed proprietary formats](https://en.wikipedia.org/wiki/Proprietary_format#Closed_Proprietary_Formats) should be avoided at all costs.

### 1.4 Rent or Build (purchase as a service, or build from scratch)
In some situations (these should be quite rare), existing systems and available commercial products an agency has access to may not address a unique
problem that the business faces. In these scenarios, renting a commercial product to be used in isolation is preferred, until such a time that it can be integrated
more cohesively with other agency systems or decommissioned (i.e. single use for a short term project).

## 2. Confidentiality, Integrity and Availability
Proxy config, authentication, access control, logging, monitoring should all be separated from the core system (to maximise reuse of these components across an agencies systems).
An example architecture is below:

![Separation of Concerns](/images/separation-of-concerns.png "Separation of Concerns")

In the above diagram, most components that can be utilised across several systems have been split into a shared baseline, that newly introduced systems can adopt. The 
re-usable components should minimise repetition in line with the [DRY principle of software development](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

## 3. Separation of concerns

The design of IT systems and schemas, should attempt to be 'normalised' into standalone components, each which address a reusable function. A great example of this is email - 
messaging between systems and end users is handled quite well via email for most message volumes, so implementing yet another way to notify a user (other than email) is typically
avoided. (TODO: complete)

## 4. Revision Control (bespoke systems)

![Codebase](/images/codebase.png "Codebase")

Code and configuration should always be tracked in a version control system (TODO: complete)

## 5. Disposability

Deployments should be scripted, so that servers are disposable (TODO: complete)