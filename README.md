# OS-Data-Importers

## Goal

The aim of this project is to keep the data in OpenSpending as fresh as possible, by pro-actively fetching up-to-date fiscal data from various data-portals and other official sources. By linking the data in OpenSpending to the exact source, we also gain more credibility to the data stored in the platform.

## Means

We use the `datapackage-pipelines` framework to run the processing pipelines.

## Update a datapackage with a `fiscal.source-spec.yaml`

To update a datapackage on OpenSpending, either because the source-spec has changed, or because the data itself has been updated, you must make a change to the `fiscal.source-spec.yaml` file and commit it to the master branch of this repository. If only the data has changed, but not the source-spec, the easiest change to make is to increment the source-spec's `revision` property.

## Current Status

#### Mexico 2008-2016 Budget (Cuenta Pública): [Pipeline](https://openspending.org/pipelines/)

## Development notes

The env var `$OS_DPP_DISABLE_PIPELINES='True'` will prevent pipeline schedulers from being initialised. This is useful if you want to retain the pipeline server endpoint for your application, but not run the actual pipelines (e.g. for a staging server).

A `docker-compose.dev.yaml` file is provided to start up os-data-importers without running the entire OpenSpending suite. This can be useful during source-spec development to iterate on the specs. Run like this:

```sh
# Start the services os-data-importers uses first:
$ docker-compose -f docker-compose.dev.yaml up -d es redis fakes3 db
# Give it a few seconds for the services to become available, then
# Start up os-data-importers:
$ docker-compose -f docker-compose.dev.yaml up --build os-data-importers
```

You can access the pipelines dashboard at: `http://localhost:5000`.
