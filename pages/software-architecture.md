---
layout: page
title: Software Architecture and Design Patterns
permalink: /software-architecture/
published: true
---

Some tips on software development

## Relational Data

[PostgreSQL](http://www.postgresql.org/) is the preferred database for storing
all types of relational data. When architecting tables, try to design them
using [Django models](https://docs.djangoproject.com/en/1.10/topics/db/models/),
and generally take following approach:

* Structured data for querying should be in standard normalised relational tables
* Use Django
[ForeignKey](https://docs.djangoproject.com/en/1.10/ref/models/fields/#django.db.models.ForeignKey)
fields to define relationships, in order to make use of the object-relational
mapper (ORM) that is part of Django.
* For unstructured, sparse or highly variable data, make use of
[JSONFields](https://docs.djangoproject.com/en/1.10/ref/contrib/postgres/fields/#jsonfield).
* Extremely large tables (>10 million records) should make use of [table
partitioning](https://www.postgresql.org/docs/current/static/ddl-partitioning.html),
to optimise queries and updates. Table partitioning allows data to be divided
into "active" and "seldom-used" records, and is typically based on age of data.

## Application Logic

[Django](https://www.djangoproject.com/) is the preferred application framework
for implementing logic. For performance, run under
[uwsgi](https://docs.djangoproject.com/en/1.9/howto/deployment/wsgi/uwsgi/) with
the [Gevent](http://uwsgi-docs.readthedocs.io/en/latest/Gevent.html) loop
engine. Try to serve static files directly from
[uwsgi](http://uwsgi-docs.readthedocs.io/en/latest/StaticFiles.html) and/or
[nginx](https://www.nginx.com/resources/admin-guide/serving-static-content/).

Data served to clients should be in JSON format or via standard spatial services
from [GeoServer](http://geoserver.org/).

Realtime client publishing should use [Django
Channels](https://channels.readthedocs.io/en/latest/inshort.html)

## HTML User Interface

Client interfaces should be built in modern responsive html. The recommended CSS
framework is [Foundation 6](http://foundation.zurb.com/sites/docs/) using the
[Flex
Grid](http://foundation.zurb.com/sites/docs/flex-grid.html#vertical-alignment)
(to support vertical alignment). Javascript libraries are always changing,
though we have had good results from the following:

 * [JQuery](https://jquery.com/) for general purpose convenience and ajax
 requests
 * [localForage](https://github.com/mozilla/localForage) for working with
 offline storage
 * [Vue.js](https://vuejs.org/) for client side template rendering and data
 binding
 * [OpenLayers 3](http://openlayers.org/) for web mapping and spatial work

## Custom mobile forms

Build them with [CyberTracker](http://www.cybertracker.org/) pointing to a
PostgreSQL database.
