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

## 1. Avoid lock-in

Being locked in to a specific service, product or technology  can lead to rising support and maintenance costs, slow and expensive change processes, 
and the prospect of prohibitive costs to develop and migrate to an equivalent solution from scratch. Along with the below points on ownership the risks of lock-in
can be reduced by:

  * Confirming appropriate mindshare before adopting a technology
  * Preferencing extensibility over features
    * Choose the ability to extend a product/service/technology compared to a large list of features that may not be used.

### 1.1 Retain ownership of your data

If data is held inside a black box – that is a system has stored it in its own way, it can be a major task to get access. Ensuring there is a method to export the data 
to an open standard format (i.e. spreadsheets, database exports, OGC formats, JSON/XML) can make future migration significantly easier and cheaper. It is important to establish 
procedures for extracting the data, ensuring the exports still work, and checking that the format is well documented, as the critical moment when the data is needed is the worst time 
to discover that the export functionality hasn’t worked since the last update, or the perfectly exported data is encoded in an unknown format.

### 1.2 Retain ownership of your intellectual property

Intellectual property typically refers to source code or design work. There is a danger with bespoke development of moving away from a supplier only to discover 
that they own critical parts of a system, forcing a system owner to negotiate continuing use of those subsystems. This can be avoided by a contractual agreement 
that the client owns all custom work, or alternatively all custom work is released under a license that allows free reuse and extension.

To insure against a breakdown in the relationship between site owner and vendor does occur, or the case of a vendor ceasing trading, it’s reassuring to have guaranteed access 
to any intellectual property. Running a source control system and wiki and obligating development partners to store project related information and code in them is the best way 
to ensure that the work generated for a project stays under the control of the business.

![Codebase](/images/codebase.png "Codebase")

Code and configuration should always be tracked in a version control system - this enables developers to co-operate efficiently. Most developers will be using one of these systems (e.g Git) already, 
and should be happy to work with one supplied by their client, as long as it is well managed, maintained and backed up. A dedicated provider or a regular hosting supplier could host the system,
but partner development agencies should not be hampered by the source control so it’s worth discussing the choice of system and access controls with them.

A wiki like MediaWiki or Confluence should be hosted similarly, and provide a central point to store documentation, related information, and any other assets. These ensure that the information 
is available whenever needed, and provide a useful starting point for future partners and suppliers. However, a sprawling, unmaintained wiki is often less of a help and more of a hindrance, 
so users from both parties should be encouraged to keep information up to date, and sensibly structured. 

## 2. Share > re-use > extend > rent or build

### 2.1 Sharing (co-habitation of data and functions with an existing system)
If a system already exists, and data ownership and classification can be cleanly negotiated for 
co-habitance on the existing system, it is best to use the existing system. An example of this would
be [OpenStreetMap Nominatim](https://nominatim.openstreetmap.org/) - it is much lower cost to use the existing system to find addresses, than to build
a separate address lookup database. If data needs to be added, then adjusting licenses to be compatible (see the [Open Database License](http://opendatacommons.org/licenses/odbl/summary/))
will greatly reduce the overall costs of maintaining and delivering the service, as opposed to even re-using the code to 
run a similar service on your own, as that service would require infrastructure, configuration, maintenance and securing - all of which have costs.

### 2.2 Re-use (open source, or well supported commercial platforms)
In some cases data may not be appropriate to reside in the same system instance (e.g. due to security/legislative constraints). In this scenario
if the system meets the requirements of the business, re-using it's code and configuration in a new instance is preferrable, though consideration
is required to ensure the support of the code and config for the new system is appropriately shared between the two or more distinct parts of an 
agency that may use it. Preference is given to [open-source](https://opensource.org/) platforms due to the ability to modify and provide back to the upstream authors any
changes that may be required, which is typically lower cost and less restricted than proposing agency specific changes to a commercial product.
The [Linux Foundation's](https://www.linuxfoundation.org/about) [Long Term Support Iniative](https://ltsi.linuxfoundation.org/what-is-ltsi) 
has a good breakdwon on the [advantages of upstream alignment](https://ltsi.linuxfoundation.org/what-is-ltsi/advantages-upstream-alignment).

### 2.3 Extend (build on top of an existing system / framework / toolkit)
Popular open source and commercial frameworks and toolkits have addressed several of the base issues in building an application,
such as the [OWASP](https://www.owasp.org/index.php/Main_Page) Top 10 critical web application flaws. Preferentially for support and
extensability open source platforms are preferred, but in areas where there are no good open source alternatives, then commercial
platforms may be more suitable, as long as they are using open data formats. The use of closed data formats is a very high risk to
future maintainability and transitions, as it encourages lock-in and makes it exceedingly difficult to move in the future.
[Closed proprietary formats](https://en.wikipedia.org/wiki/Proprietary_format#Closed_Proprietary_Formats) should be avoided at all costs.

### 2.4 Rent or Build (purchase as a service, or build from scratch)
In some situations (these should be quite rare), existing systems and available commercial products an agency has access to may not address a unique
problem that the business faces. In these scenarios, renting a commercial product to be used in isolation is preferred, until such a time that it can be integrated
more cohesively with other agency systems or decommissioned (i.e. single use for a short term project).

## 3. Confidentiality, Integrity and Availability
Proxy config, authentication, access control, logging, monitoring should all be separated from the core system (to maximise reuse of these components across an agencies systems).
An example architecture is below:

![Separation of Concerns](/images/separation-of-concerns.png "Separation of Concerns")

In the above diagram, most components that can be utilised across several systems have been split into a shared baseline, that newly introduced systems can adopt. The 
re-usable components should minimise repetition in line with the [DRY principle of software development](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

## 4. Shared component architecture

![Shared Component Architecture](/images/Shared Component Architecture.png "Shared Component Architecture")

The design of IT systems and schemas, should attempt to be 'normalised' into standalone components, each which address a reusable function. A great example of this is email - 
messaging between systems and end users is handled quite well via email for most message volumes, so implementing yet another way to notify a user (other than email) is typically
avoided. (TODO: complete)

## 5. Disposability

Deployments should be scripted, so that servers are disposable (TODO: complete)