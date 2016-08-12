---
layout: page
title: IT System Development Standards
permalink: /development-standards/
---

## Code Repositories

### Storage and Upload Management

Where possible, all relevant code for systems should be stored in public
repositories on GitHub.

In order to enable this, there are a number of items that need to be considered
before making the code repository available. These include, but are not limited
to:

- Separation of department-specific configuration (e.g. references to URLs, file
and folder paths, etc.) into files and must not uploaded to the repository
- Separation of all security credentials (e.g. usernames, passwords, etc.) into
a file and must not uploaded to the repository
- Department-specific media and static content (e.g. uploaded files, customised
styles, etc.) must not be uploaded to the repository
- Extraneous files generated during development (e.g. database dumps, fixture
data) must not be uploaded into the repository

Essentially, the code repository should only contain the bare minimum code
required for anyone (i.e. public users) to download and build the system for own
use, and therefore must not contain any department-specific details or
information that may compromise our internal systems.

### Source Control and Development Workflow

All code repositories should make use of source control software to record
changes to that repository over time (this is also called version control).
[Git](https://git-scm.com/) and [Mercurial](https://www.mercurial-scm.org/)
are both recommended for this purpose.

All repositories should include a exclusion blacklist suitable for the source
control software being used (e.g. ``.gitignore`` or ``.hgignore``). This should
be defined at the beginning of a respository's life and maintained throughout.
The blacklist can help prevent extraneous or sensitive information being
committed into the repository unintentionally.

A useful library of ``.gitignore`` templates is maintained in this repository:
[github/gitignore](https://github.com/github/gitignore). Standard templates for
source control exclusion are also recorded here: [Source Control ignore
templates](/source-control-ignore/).

Software development projects being undertaken by teams greater than one person
are recommended to adopt a defined standard of development workflow in order to
use source control effectively across the team. The appropriate workflow is
context-sensitive to the project and the team. A number of different workflow
procedure that use Git are compared in this article: [Comparing
Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/).

### Private Repositories

In the event that the use of a public repository is not possible, the code may
be uploaded into a private repository.

These private repositories must be kept to a minimum, with the intention of
refactoring/stripping the code in the future to enable publishing of the code
via a public repository.

## Environment Controls

### Development and Test

Development and test environments are maintained by OIM, and are made available
to development teams throughout the department. If requested, full access to the
relevant files, folders and user accounts (e.g. database account) may be granted
to enable the team(s) to carry out the required work.

### UAT and Production

UAT and production environments are maintained by OIM, but are not made directly
available to other development teams. With this restriction in place, all
deployments to UAT and production environments must be carried out via requests
to OIM.

This ensures that there is quality control of the future deployment to systems
in the production environment by first carrying out and analysing the deployment
in the UAT environment.

All changes to production must be approved by OIM through the Change Management
process (i.e. submission of a Request for Change, approved by the Change
Advisory Board) before deployment can commence.

### Exceptions

Exceptions to the rules above regarding controlled environments may be granted
upon agreement with OIM.

A typical case for an exception would be if the target system environment is
isolated from system environments owned by other business units within the
department, and therefore any changes to the target system will not impact other
business units.

In all cases, production changes must still be approved through the Change
Management process before they can be carried out.

## External Contract Developer Engagement

### Code Access and System Deployment

External contractors only have access to code repositories, carrying out any
development work on local environments. No direct access to code deployed to
internal systems is to be granted to external contractors.

Deployment of these systems to departmental environments are controlled
internally, and are to be carried out once a request for deployment has been
issued by the external contractor with any relevant details.
