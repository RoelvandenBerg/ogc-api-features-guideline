## Examples of implementations

From earlier tests Geonovum concluded that tools were not compliant with the requirements for OAS, OGC, INSPIRE and Dutch ADR. 
For that reason Geonovum set up an open tender at the beginning of the year 2023, with the goal of improving the compliance of OGC API tooling.
This resulted in demo services that each show how you can be compliant with the requirements.
These demo services used the same selection of the Dutch INSPIRE Addresses in a simplified GML file, constructed by Wetransform as input.
Next to these demoservices, an other service that is in production is reviewed in regards to the standards.

|   tool    | main contributions   | landing page|
|-----------|----------------------|-------------|
| Pygeoapi  |Justobjects and Geocat|https://apitestbed.geonovum.nl/adr_pygeoapi/v1 |
| Geoserver |Geosolutions          |https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1 |
| Deegree   |Wetransform           |https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1 |
| Gokoala   |PDOK                  |https://api.pdok.nl/brt/top10nl/ogc/v1 |

Per tool, findings are elaborated in the next chapters when relevant. They are held to the requirements in the standards as stated in chapter 3.
Not all standards are regarded, since they were not yet astablished at the time the services were set online. This counts for the common and filtering standard.

### Pygeoapi versus requirements

The following findings show how Pygeoapi complies to the requirements with an OAPIF service for INSPIRE harmonized Dutch Addresses.

#### OAS

The OAS document is available: https://apitestbed.geonovum.nl/adr_pygeoapi/v1/openapi

#### OGC 

The OGC CITE validator gave no error at the [landing page](https://apitestbed.geonovum.nl/adr_pygeoapi/v1).

***Filtering***  

For the use of filters, the bbox and items options were already available. In addition, one can filter on the attributes which can be retrieved from
https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL/queryables.
https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL/items?filter=locator_designator_postalDeliveryIdentifier=%279901AA%27 does unfortunately not work.

The OGC API specification for filtering [[PUB-6]] did not not yet have the status "approved" at the time of this service publication and has therefor not been considered further.

***CRS***

The crs identifier list and storage-crs can be found at the end of:
https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL?f=json 

With the following command line request, one can see the Content-CRS value in the header:

`curl -i https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL/items/1?f=json`

An adjustment has been made to the bbox filter. It now also supports the bbox-crs parameter.
Only 2 addresses are available in the below defined bbox.
https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL/items?f=json&bbox-crs=http://www.opengis.net/def/crs/EPSG/0/28992&bbox=252200,593000,252710,594000


#### Dutch API design rules  

It complies with all the rules, except for rule https://gitdocumentatie.logius.nl/publicatie/api/adr/#/core/no-trailing-slash.
This rule in the Dutch ADR prescribes that none of the API endpoints should have a trailing slash. However, the OGC specification states that the landing page (i.e. "Home") should have a trailing slash. So the rules contradict.
It is expected that in future, this ADR-rule will make an exception for the landing page.

#### INSPIRE

***CRS ETRS89 and WGS84***

The required CRS's are available:
- RD: https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL/items/1?f=json&crs=http://www.opengis.net/def/crs/EPSG/0/28992
- WGS84: https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL/items/1?f=json&crs=http://www.opengis.net/def/crs/OGC/1.3/CRS84
- ETRS89:  https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL/items/1?f=json&crs=http://www.opengis.net/def/crs/EPSG/0/4258

***Predefined download***  

Link to metadata of dataset: passed at `/collections/AddressesNL` and at `/collections` level:  
`{"href": "https://www.nationaalgeoregister.nl/geonetwork/srv/dut/catalog.search#/metadata/a5f961e9-ebdd-41e2-b8e8-ab33ed340a83",
  "hreflang": "nl",
  "type": "text/html",
  "rel": "describedby",
  "title": "Metadata as HTML"}`

`{"href": "https://www.nationaalgeoregister.nl/geonetwork/srv/api/records/a5f961e9-ebdd-41e2-b8e8-ab33ed340a83/formatters/xml",
  "hreflang": "nl",
  "type": "application/xml",
  "rel": "describedby",
  "title": "Metadata as ISO 19139 XML"}`
        
Link to INSPIRE feature concept dictionary: passed at /collections/AddressesNL and at /collections level:  
`{"href": "https://inspire.ec.europa.eu/featureconcept/Address",
  "hreflang": "en",
  "type": "text/html",
  "rel": "tag",
  "title": "INSPIRE feature concept dictionary for addresses"}`
        
Link to the license: passed at /collections/AddressesNL and at /collections level:  
`{"href": "https://creativecommons.org/publicdomain/zero/1.0/deed.en",
  "hreflang": "en",
  "type": "text/html",
  "rel": "license",
  "title": "CC0 1.0 Public Domain license"}`

See also https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections?f=json and 
https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL?f=json

***bulk download***

Link to bulk download of dataset: passed at /collections/AddressesNL and at /collections level.

See also https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections?f=json and   
https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL?f=json
`{"href": "https://service.pdok.nl/kadaster/ad/atom/downloads/addresses.gml.gz",
  "hreflang": "nl",
  "length": 685450191,
  "type": "application/x-gmz",
  "rel": "enclosure",
  "title": "Download complete dataset as GML"}`

***GeoJSON***

Items can be retrieved in GeoJSON by requesting:  

`https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL/items?f=json`

***GML*** 

As input, a simple features GML file was used as produced by Wetransform from the complex feature GML with the transformation software Hale.  

As output, there is a link to the original complex feature GML-file:
https://service.pdok.nl/kadaster/ad/atom/downloads/addresses.gml.gz 

Pygeoapi does not support GML-output at item-level, but this is not a requirement.

***Describing encoding***  

There is a link to https://github.com/INSPIRE-MIF/2017.2/tree/master/GeoJSON/ads at [collections/AddressesNL level](https://apitestbed.geonovum.nl/adr_pygeoapi/v1/collections/AddressesNL?f=json ):  

`{"href": "https://github.com/INSPIRE-MIF/2017.2/tree/master/GeoJSON/ads",
  "hreflang": "en",
  "type": "text/html",
  "rel": "about",
  "title": "Description of the encoding"}`  
          
#### Other findings on Pygeoapi

More information about the Pygeoapi adjustments to the standards can be found at https://pygeoapi.io/presentations/geonovum-tender-2023/

### Geoserver versus requirements

The following findings show how Geoserver complies to the requirements with an OAPIF service for INSPIRE harmonized Dutch Addresses.

#### OAS

The OAS document is available: https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/openapi

#### OGC  

The OGC CITE validator gave no error at the landing page https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1.

***Filtering***  

For the use of filters, the bbox and items options were already available. In addition, one can filter on the attributes which can be retrieved from:
https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress?queryables.
https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress/items?filter=locator_designator_postalDeliveryIdentifier=%279901AA%27 only gives the addresses with postal code '9901AA'. 

The OGC API specification for filtering [[PUB-6]] did not not yet have the status "approved" at the time of this service publication and has therefor not been considered further.

***CRS***

The crs identifier list and the storage-crs can be found at:
https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress?f=json

With the following command line request, one can see the Content-CRS value in the header :

`curl -i https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress/items/1?f=json`

An adjustment has been made to the bbox filter. It now also supports the bbox-crs parameter.
Only 2 addresses are available in the below defined bbox.  

https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress/items?f=json&bbox-crs=http://www.opengis.net/def/crs/EPSG/0/28992&bbox=252200,593000,252710,594000


#### Dutch API design rules  

It complies with all the rules, except for rule https://gitdocumentatie.logius.nl/publicatie/api/adr/#/core/no-trailing-slash.
This rule in the Dutch ADR prescribes that none of the API endpoints should have a trailing slash. However, the OGC specification states that the landing page (i.e. "Home") should have a trailing slash. So the rules contradict.
It is expected that in future, this ADR-rule will make an exception for the landing page.

At first the collection was named "AddressesNL". At a later stage, it has been changed to "SimpleAddress". This is not according to the [rule for naming collections](https://gitdocumentatie.logius.nl/publicatie/api/adr/#/core/naming-collections) because it is not a plural.  

#### INSPIRE

***CRS ETRS89 and WGS84***

The required CRS's are available:
- RD: https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress/items/1?f=json&crs=http://www.opengis.net/def/crs/EPSG/0/28992
- WGS84: https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress/items/1?f=json&crs=http://www.opengis.net/def/crs/OGC/1.3/CRS84
- ETRS89:  https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress/items/1?f=json&crs=http://www.opengis.net/def/crs/EPSG/0/4258

***Predefined download***  

Link to metadata of dataset: passed at [/collections/collection level](https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress?f=json) and at [/collections level](https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections?f=json). 
`{"href":"https://www.nationaalgeoregister.nl/geonetwork/srv/api/records/a5f961e9-ebdd-41e2-b8e8-ab33ed340a83/formatters/xml?approved=true","rel":"describedBy","type":"application/xml","title":"ISO metadata for this dataset"}`
  
Link to INSPIRE feature concept dictionary: passed at [/collections/collection level](https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress?f=json). 
`{"href":"https://inspire.ec.europa.eu/featureconcept/Address","rel":"tag","type":"text/html","title":"INSPIRE Address feature concept."}`

Link to the license: passed at [/collections level](https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections?f=json). 
`{"href":"http://creativecommons.org/publicdomain/zero/1.0/deed.nl","rel":"license","type":"text/html","title":"Dataset license."}`

***bulk download***

Link to bulk download of dataset: passed at [/collections/collection level](https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress?f=json).  
`{"href":"https://geonovum.geosolutionsgroup.com/geoserver/www/ADNL.gpkg","rel":"enclosure","type":"application/geopackage+sqlite3","title":"Addresses raw data."}`

***GeoJSON***

Items can be retrieved in GeoJSON by requesting:

`https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress/items/1?f=application%2Fgeo%2Bjson`

***GML*** 

As input, a simple features GML file was used as produced by Wetransform from the complex feature GML with the transformation software Hale.  

As output, the following link can be found at [/collections/collection level](https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress?f=json). It can be used to download the first 50 records. 

`{"href":"https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress/items?f=application%2Fgml%2Bxml%3Bversion%3D3.2","rel":"items","type":"application/gml+xml;version=3.2","title":"Addresses items as application/gml+xml;version=3.2"}` 

***Describing encoding***  

There is a link to https://github.com/INSPIRE-MIF/2017.2/blob/master/GeoJSON/ads/simple-addresses.md at [/collections/collection level](https://geonovum.geosolutionsgroup.com/geoserver/inspire/ogc/features/v1/collections/SimpleAddress?f=json). 

`{"href":"https://github.com/INSPIRE-MIF/2017.2/blob/master/GeoJSON/ads/simple-addresses.md","rel":"describedBy","type":"text/html","title":"GeoJSON Encoding Rule for INSPIRE Addresses"}`

#### Other findings on Geoserver

More information about the Geoserver adjustments to the standards can be found at https://www.geonovum.nl/uploads/documents/Geosolutions.pdf
 
### Deegree versus requirements

The following findings show how Geoserver complies to the requirements with an OAPIF service for INSPIRE harmonized Dutch Addresses.

#### OAS 

The OAS document is available: https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/openapi

#### OGC

The OGC CITE validator gave no error at the landing page: https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1.

***Filtering***  

For the use of filters, the bbox and items options were already available.

The OGC API specification for filtering [[PUB-6]] did not not yet have the status "approved" at the time of this service publication and has therefor not been considered.

***CRS***

The crs identifier list and storage-crs can be found at:
https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress?f=json

With the following command line request, one can see the Content-CRS value in the header :

`curl -i https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress/items?limit=1`

An adjustment has been made tot the bbox filter. It now also supports the bbox-crs parameter.
Only 2 addresses are available in the below defined bbox.
https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress/items?f=json&bbox-crs=http://www.opengis.net/def/crs/EPSG/0/28992&bbox=252200,593000,252710,594000


#### Dutch API design rules  

It complies with all the rules, except for 2.
It does not comply with the rule https://gitdocumentatie.logius.nl/publicatie/api/adr/#/core/no-trailing-slash.
This rule in the Dutch ADR prescribes that none of the API endpoints should have a trailing slash. However, the OGC specification states that the landing page (i.e. "Home") should have a trailing slash. So the rules contradict.
It is expected that in future, this ADR-rule will make an exception for the landing page.

Secondly, the collection is named "SimpleAddress". This is not according to the [rule for naming collections](https://gitdocumentatie.logius.nl/publicatie/api/adr/#/core/naming-collections) because it is not a plural.  

#### INSPIRE

***CRS ETRS89 and WGS84***

The required CRS's are available:
- RD: https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress/items/nl-imbag-ad-address-0003200000133985?f=json&crs=http://www.opengis.net/def/crs/EPSG/0/28992
- WGS84: https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress/items/nl-imbag-ad-address-0003200000133985?f=json&crs=http://www.opengis.net/def/crs/OGC/1.3/CRS84
- ETRS89: https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress/items/nl-imbag-ad-address-0003200000133985?f=json&crs=http://www.opengis.net/def/crs/EPSG/0/4258

***Predefined download***  

Link to metadata of dataset: passed at [/collections level](https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections?f=json):  

`{"href":"https://www.nationaalgeoregister.nl/geonetwork/srv/dut/catalog.search#/metadata/a5f961e9-ebdd-41e2-b8e8-ab33ed340a83","rel":"describedby","type":"text/html","title":"Metadata"}`

Link to INSPIRE feature concept dictionary: passed at [/collections/collection level](https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress?f=json) and at [/collections level](https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections?f=json):  

`{"href":"https://inspire.ec.europa.eu/featureconcept/Address","rel":"tag","type":"text/html","title":"Feature concept Address"}`

Link to the license: passed at [/collections level](https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections?f=json):  

`{"href":"http://creativecommons.org/publicdomain/zero/1.0/deed.nl","rel":"license","type":"text/html","title":"License"}`

***bulk download***

Link to bulk download of dataset: passed at [/collections/collection level](https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress?f=json) and at [/collections level](https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections?f=json). 

`{"href":"http://test.haleconnect.de/ogcapi/datasets/simplified-addresses/collections/SimpleAddress/items?bulk=true","rel":"enclosure","type":"application/xml","title":"Download all features as GML"}` 
`{"href":"http://test.haleconnect.de/ogcapi/datasets/simplified-addresses/collections/SimpleAddress/items?bulk=true","rel":"enclosure","type":"application/json","title":"Download all features as GeoJSON"}` 

***GeoJSON***

Items can be retrieved in GeoJSON by requesting:  

`https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/collections/SimpleAddress/items?f=json&limit=1`

 or

`https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/collections/SimpleAddress/items/nl-imbag-ad-address-0003200000133985?f=json`

***GML*** 

As input, a simple features GML file was used as produced by Wetransform from the complex feature GML with the transformation software Hale.
As output, the following links can be found at [/collections/collection level](https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections/SimpleAddress?f=json). They can be used to download specific records.

`{"href":"http://test.haleconnect.de/ogcapi/datasets/simplified-addresses/collections/SimpleAddress/items?bulk=true","rel":"enclosure","type":"application/xml","title":"Download all features as GML"}` 

or 

`{"href":"http://test.haleconnect.de/ogcapi/datasets/simplified-addresses/collections/SimpleAddress/items","rel":"items","type":"application/gml+xml;version=3.2","title":"Features as GML"}`

[use parameter `f=xml`](http://test.haleconnect.de/ogcapi/datasets/simplified-addresses/collections/SimpleAddress/items?f=xml)

***Describing encoding***  

There is a link to https://github.com/INSPIRE-MIF/2017.2/blob/master/GeoJSON/ads at [/collections/collection level](https://test.haleconnect.de/ogcapi/datasets/simplified-addresses/v1/collections?f=json). 

`{"href":"https://github.com/INSPIRE-MIF/2017.2/tree/master/GeoJSON/ads","rel":"describedby","type":"text/html","title":"Encoding description"}`

#### Other findings on Deegree

More information about the Deegree adjustments to the standards can be found at https://www.geonovum.nl/uploads/documents/deegree%20OGC%20API%20Features.pdf

### Gokoala BRT versus requirements

The following findings show how Gokoala with the OAF service for the BRT dataset complies to the requirements.

#### OAS 

The OAS document is available at: https://api.pdok.nl/brt/top10nl/ogc/v1/api

#### OGC

The OGC CITE validator gave no error at the landing page: https://api.pdok.nl/brt/top10nl/ogc/v1.

***Filtering***  

For the use of filters, the bbox and items options were available.
https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/queryables is not supported.

The OGC API specification for filtering [[PUB-6]] did not not yet have the status "approved" at the time of this service publication and has therefor not been considered further.

***CRS***

The crs identifier list and storage-crs can be found at:
https://api.pdok.nl/brt/top10nl/ogc/v1/collections?f=json where it is repeated for each collection.
and at each collection level, for instance: https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt?f=json

With the following command line request, one can see the Content-CRS value in the header :

`curl -i https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/items?limit=1`

It supports the bbox filter and the bbox-crs parameter.
Only 5 points are available in the below defined bbox:
https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/items?bbox-crs=http://www.opengis.net/def/crs/EPSG/0/28992&bbox=252000,593000,253000,594000


#### Dutch API design rules  

It complies with all the rules, except for rule https://gitdocumentatie.logius.nl/publicatie/api/adr/#/core/no-trailing-slash.  
The rule "no-trailing-slash" in the Dutch ADR prescribes that none of the API endpoints should have a trailing slash. However, the OGC specification states that the landing page (i.e. "Home") should have a trailing slash. So the rules contradict.
It is expected that in future, this ADR-rule will make an exception for the landing page.  

#### INSPIRE

The dataset BRT is an INSPIRE dataset AsIs and not an INSPIRE harmonized dataset, so not all the INSPIRE requirements are applicable.
Because the INSPIRE requirements can still be relevant they have been viewed, despite the fact that they are not all applicable. 

***CRS ETRS89 and WGS84***

The required CRS's are available:
- RD: https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/items?limit=1&f=json&crs=http://www.opengis.net/def/crs/EPSG/0/28992
- WGS84: https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/items?limit=1&f=json&crs=http://www.opengis.net/def/crs/OGC/1.3/CRS84
- ETRS89: https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/items?limit=1&f=json&crs=http://www.opengis.net/def/crs/EPSG/0/4258

***Predefined download***  

Link to metadata of dataset: passed at [Landingpage level](https://api.pdok.nl/brt/top10nl/ogc/v1?f=json):  

`{"href":"https://www.nationaalgeoregister.nl/geonetwork/srv/dut/catalog.search#/metadata/29d5310f-dd0d-45ba-abad-b4ffc6b8785f","rel":"http://www.opengis.net/def/rel/ogc/1.0/data-meta","title":"Metadata for dataset at Nationaal Georegister"}`

No Link to INSPIRE feature concept dictionary, because it is not an INSPIRE harmonized dataset.

Link to the license: passed at [/collections level](https://api.pdok.nl/brt/top10nl/ogc/v1/collections?f=json) and [Landingpage level](https://api.pdok.nl/brt/top10nl/ogc/v1?f=json):  

`{"href":"https://creativecommons.org/licenses/by/4.0/deed.nl","rel":"license","type":"text/html","title":"CC BY 4.0"}`

***bulk download***

No Link to bulk download of dataset is provided, although it does exist: https://service.pdok.nl/brt/topnl/atom/top10nl.xml.

***GeoJSON***

The first items can be retrieved in GeoJSON or JsonFG by requesting:  

`https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/items?limit=1&f=json` or `https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/items?limit=1&f=jsonfg`

 or items can be retrieved by ID:

`https://api.pdok.nl/brt/top10nl/ogc/v1/collections/gebouw_punt/items/a7b7566b-9be9-57fb-bd05-33dd417505f3?f=json`

***GML*** 

The input encoding options of Gokoala have not been investigated and are unknown for this dataset. The output of GML is not supported.

***Describing encoding***  

The describing of the encoding is not relevant, since it is no INSPIRE harmonized dataset.

#### Other findings on Gokoala BRT OAPIF.

More information about the Gokoala can be found at https://github.com/PDOK/gokoala and https://api.pdok.nl/

### General findings

1. There has been discussion whether the predefined download links should be at collections or collections/collection level. See also: https://github.com/INSPIRE-MIF/gp-ogc-api-features/issues/91.  
During the project of adjusting the tools we had the opinion that both should be possible.  
Afterwards, we found out that it should be at collections level since it is one of the [main principles](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#main-principles) in [PUB-2] to use one data set in one API.
Again, later we realized other kinds of OGC-API services like Tiles, can exist together on the same landing page. In that case, these links could also be provided on the landing page, also because not all OGC-API types have collections. 
This was discussed at https://github.com/INSPIRE-MIF/gp-ogc-api-features/issues/93.
2. The protocol element in the metadata is based on a codelist. The protocol element is used to state the type of service.
A new protocol "OGC API-Features" was added to the list of [protocol values](https://inspire.ec.europa.eu/metadata-codelist/ProtocolValue:1). 
But the given [link](http://www.opengis.net/def/docs/17-069r3) behind the label does not resolve.
The Dutch [ISO19115 metadata standard](https://docs.geostandaarden.nl/md/mdprofiel-iso19115/#protocol) also provides a codelist for the protocol element to state the type of service. 
It has the value: "OGC:API features" in https://docs.geostandaarden.nl/md/mdprofiel-iso19115/#codelist-protocol.
The [uri](http://www.opengis.net/def/interface/ogcapi-features) provided there, does also not resolve.
3. Another blocking issue before implementation of the OAPIF for INSPIRE is that descriptions of encodings other than GML are not yet available for most INSPIRE themes.
4. Complex GML as input and output are difficult as long as tooling (server and client) expects simple encodings.
5. One could discuss if it is useful to publish complex GML as output, because it is not in line with the aim of OGI API Features: easy to use for developers.
6. Complex GML as input needs a flattening of the data. This is needed for the software that publishes the features. It can only work with simple features, with one value per attribute and without relations to other objects.
This is often not the case with the more complex INSPIRE models.

### Documentation

Presentations of tool adjustments can be found here: https://www.geonovum.nl/over-geonovum/actueel/presentatie-resultaten-aanbesteding-ogc-api-features-toolaanpassing

Gecertificeerde software door OGC: https://portal.ogc.org/public_ogc/compliance/compliant.php?display_opt=1&specid=1022 
Overige software: https://github.com/opengeospatial/ogcapi-features/tree/master/implementations 
Deze lijsten zijn groeiende en incompleet

