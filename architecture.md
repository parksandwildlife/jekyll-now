---
---
# Software Architecture

Current software architecture model

## Relational Data

[PostgreSQL](http://www.postgresql.org/) is the preferred database for storing all types of relational records. When architecting tables, try to design them using [django models](https://docs.djangoproject.com/en/1.9/topics/db/models/), and generally take following approach:

 * Structured data for querying should be in standard normalised relational tables
  * Typically use [ForeignKey](https://docs.djangoproject.com/en/1.9/topics/db/examples/many_to_one/) fields for this
 * Unstructured data should use [JSONFields](https://docs.djangoproject.com/en/1.9/ref/contrib/postgres/fields/#jsonfield)
 * Extremely large tables (>10million records) should be split into an active/historical table, with all joins occuring on the active records, and partitioning typically done based on time.

## Application Logic

[Django](https://www.djangoproject.com/) is the preferred application framework for implementing logic. For performance, run under [uwsgi](https://docs.djangoproject.com/en/1.9/howto/deployment/wsgi/uwsgi/) with the [Gevent](http://uwsgi-docs.readthedocs.io/en/latest/Gevent.html) loop engine. Try to serve static files directly from [uwsgi](http://uwsgi-docs.readthedocs.io/en/latest/StaticFiles.html) and/or [nginx](https://www.nginx.com/resources/admin-guide/serving-static-content/).

Data served to clients should be in JSON format or via standard spatial services from [GeoServer](http://geoserver.org/).

Realtime client publishing should use [Django Channels](https://channels.readthedocs.io/en/latest/inshort.html)

## HTML User Interface

Client interfaces should be built in modern responsive html. The recommended CSS framework is [Foundation 6](http://foundation.zurb.com/sites/docs/) using the [Flex Grid](http://foundation.zurb.com/sites/docs/flex-grid.html#vertical-alignment) (to support vertical alignment). Javascript libraries are always changing, though we have had good results from the following:

 * [JQuery](https://jquery.com/) for general purpose convenience and ajax requests
 * [localForage](https://github.com/mozilla/localForage) for working with offline storage
 * [Handlebars.js](http://handlebarsjs.com/) for client side template rendering
 * [OpenLayers 3](http://openlayers.org/) for web mapping and spatial work
 * [Turf.js](http://turfjs.org/) for client side topological and spatial calculations
 * [DataTables](https://datatables.net/) for grids and table sorting/filtering/editing/pagination
 
Note when using something like DataTables make sure to render content with Handlebars.js first hidden, then upgrade to a datatable, then reveal the table. This reduces DOM repaint events significantly for large tables.

For dynamic content, Foundation provides several tools for revealing/hiding divs with CSS only, recommendation to hide a div, update it's content using jquery/handlebars, then reveal it with foundation CSS. This is mainly for UI performance optimisation, and significantly improves mobile and low powered device usability.
 
## Custom mobile forms

Build them with [CyberTracker](http://www.cybertracker.org/) pointing to a PostgreSQL database.
