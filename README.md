# earthworks-demo
Prototype for a data management platform for engineers

![Earthworks PM screenshot](./Screenshot_20171215_102540.png)

## Geotechnical asset management
Earthworks PM helps engineers manage geotechnical and geological data for site evaluations and earthworks construction projects.

Projects can be created and data entered on any desktop or mobile system with a modern browser. Because data is fetched and stored using an API server, future support can be added for other platforms such as a standalone mobile or desktop app.

The PostgreSQL database and API server (based on Django) is currently hosted at [https://earthworksqc.com/](https://earthworksqc.com/). However, it can be installed to a local machine in order to keep data contained within a local network. Please see [installation instructions](./installation.md).

### Technologies and frameworks:
#### Backend API
* OS: Linux (earthworksqc.com uses Ubuntu 16.04 LTS)
* Server: nginx (reverse proxy), gunicorn (wsgi app server)
* API/backend: Python 3, Django 1.11, Django REST Framework
* Database: PostgreSQL 9.5 with PostGIS extension (also works with PostgreSQL 10.1)
#### Frontend web app
* Framework: Vue.JS
* UI component library: Vuetify
* Libraries: vuex (state management), axios (http requests)
