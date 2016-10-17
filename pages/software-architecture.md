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

These are quite difficult due to the locked down nature of mobile development. 
HTML/JS/CSS is still an ideal delivery platform for mobile applications, but it does reduce discoverability. It may be worth 
packaging mobile applications that are shortcuts to a URL in a good mobile browser just for discovery in mobile app stores.

 * **Lowest effort:** Make a web application with [Vue.js](https://vuejs.org/) that stores content in local storage 
 and can use the HTML5 file api to export data as a CSV, that can be emailed or saved on the device.
 * **Opensource option:** Build a mobile formset with a tool like [CyberTracker](http://www.cybertracker.org/) pointing to a PostgreSQL database.
 * **Commercial option:** [ArcGIS online](https://www.arcgis.com/home/index.html) integrates with [Esri Collector](http://doc.arcgis.com/en/collector/) and provides similar functionality for simple datasets.
