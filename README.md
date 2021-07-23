# pygeoapi-odc-provider

Provider plugin for pygeoapi to include Open Data Cube as a data resource.

Install: `python setup.py install` or `python -m pip install .`

## API Coverages

A new collection can be added to the pygeoapi config.yaml with the following provider section after this library was installed:

```yaml
providers:
  - type: coverage
    name: odcprovider.OpenDataCubeCoveragesProvider
    data: <product_name>
    format:
        name: NetCDF
        mimetype: application/netcdf
```

## API Processes

Add new process can be configured by adding the following to the `config.yaml`:

```yaml
[...]
  resources:
      hello-world:
      type: process
      processor:
        name: odcprovider.HelloWorldProcessor
```

Use the following curl call for testing the process:

```sh
curl -i -s -H "Content-Type: application/json" -X POST -d @request.json 'https://17.testbed.dev.52north.org/geodatacube/processes/hello-world/execution'
```

with `request.json`:

```json
{
   "inputs": {
      "name": "Mr Test McTestface",
      "message": "Your are so testy today!"
   }
}
```


## API Records

To use the OpenDataCubeRecordsProvider, add the following collection resource. The name **catalog** is not required but
useful. Adjust the bbox to your data.

```yaml
resources:
    catalog:
      type: collection
      title: Catalog
      description: Catalog collection providing metadata using OGC API records
      keywords:
        - records
        - metadata
        - search
      links:
        - type: text/html
          rel: canonical
          title: OGC API records DRAFT OGC#20-004
          href: https://docs.ogc.org/DRAFTS/20-004.html#record-schema-overview
          hreflang: en-US
      extents:
        spatial:
          bbox: [-142.2750,41.6276,-58.2405,83.5941]
          # EPSG#4617
          crs: http://www.opengis.net/def/crs/OGC/1.3/CRS84
      providers:
        - type: record
          name: odcprovider.OpenDataCubeRecordsProvider
          data: not-used-atm
```

## Changelog

* **0.3.0**: WIP records provider
* **0.2.0**: add first processors
* **0.0.1**: WIP coverages provider

## ToDos

* [ ] Clarify License: MIT vs GPLv2 vs Apache 2.0 for service libs @52N
