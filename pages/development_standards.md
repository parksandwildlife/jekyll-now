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

### Source Control

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

### Development Workflow

Software development projects being undertaken by teams greater than one person
are recommended to adopt a defined standard of development workflow in order to
use source control effectively across the team. The appropriate workflow is
context-sensitive to the project and the team. A number of different workflow
procedures that use Git are compared in this article: [Comparing
Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows/).

A simple multi-developer workflow might be as follows:

1. A developer (Aaron) is tasked to implement some new functionality for a
   project. He forks the repository on Github, clones it to his development
   environment and implements the new function.
2. Once Aaron is satisfied with his work (via suitable testing), he commits it,
   pushes the commit(s) to his fork, then creates a pull request for the change
   on Github.
3. Another developer (Brienna) has permission to merge change requests on the
   Github project. She reviews the changeset, confirms that there are no merge
   conflicts, and merges the change request on Github.
4. A third developer (Chaz) is working on a separate feature. Knowing about the
   merged change he commits his work as normal, fetches changes from the
   upstream (original) project, and merges the changes into his own fork of the
   project. This merged change is now part of his fork of the original project.

As mentioned, the specific workflow used for each project depends on the scale
of the project, the number of developers and the manner of development (local,
distributed, agile, waterfall, etc.) A good rule of thumb is that projects being
worked upon by greater than two developers should implement some sort of
agreed-upon development change workflow. Good communication is also essential
for any development project with more than one active participant.

### Private Repositories

In the event that the use of a public repository is not possible, the code may
be uploaded into a private repository.

These private repositories must be kept to a minimum, with the intention of
refactoring/stripping the code in the future to enable publishing of the code
via a public repository.

### Project dependencies and reproducibility

It is a good practice to always work in an isolated project environment. In the
case of Python/Django projects, this means making use of tools such as
[Virtualenv](https://virtualenv.pypa.io/en/stable/) to isolate and contain the
project environment and libraries from other projects. Always make use of a
mechanism such as a
[requirements.txt](https://pip.pypa.io/en/stable/user_guide/#requirements-files)
file to define project dependencies and library versions, in order that the
project can be easily reproduced.

### Testing and continuous integration

The usage of tests to check for correct behaviour, exceptions and regressions is
generally considered desirable. However, implementing tests requires an
investment of resources and the scale of testing depends on a project's scope.
Small proof-of-concept works and projects making heavy usage of agile
development may not benefit from extensive tests. Larger, mature projects with a
well-defined specification might be good candidates for test coverage
(especially where there is an expectation of ongoing updates of functionality).

Project developers will be best placed to make the decision about the type and
scope of tests that are implemented. The following points should be considered:

* Tests should be limited to code that is owned by the project; don't test the
behaviour of external libraries and dependecies.
* Prioritise testing of low-level business rules and custom methods ahead of
end-user GUI behaviour.
* Make use of framework testing tools where possible to minimise the effort
required to generate tests.
* Use generated test input as well as defined inputs to locate unexpected
behaviour.
* Use automated testing tools to run tests and record the results to minimise
developer effort and to catch regressions earlier.

A practical example of automated testing is the
[PRS](https://github.com/parksandwildlife/prs) corporate application. This
project uses test classes defined in the
[Django](https://docs.djangoproject.com/en/1.10/topics/testing/overview/)
framework, and a library ([mixer](https://mixer.readthedocs.io/en/latest/)) to
generate (most) test data. An external service called [Travis
CI](https://travis-ci.org/) is used to automatically run unit tests for new
commits and pull requests, and [Coveralls](https://coveralls.io/) is used to
record the level of code coverage.

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
