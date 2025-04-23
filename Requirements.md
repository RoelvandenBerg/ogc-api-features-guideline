## Requirements

Below the most relevant requirements (or requirement classes) for setting up an OAPIF are listed:

| Source   | requirements | reference | 
|----------|--------------|-----------| 
| OAS      | Open API Specification| https://www.openapis.org/ |
| OGC      | [OGC API Features-Part1: Core](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0) | [[PUB-1]] |
| OGC      | [OGC API Features-Part2: CRS](https://www.opengis.net/doc/IS/ogcapi-features-2/1.0) | [[PUB-5]] |
| OGC      | [OGC API Features-Part3: filtering](https://www.opengis.net/doc/IS/ogcapi-features-3/1.0) | [[PUB-6]] |
| OGC      | [OGC API common](https://www.ogc.org/publications/standard/ogcapi-common/) | [[PUB-7]]
| Dutch ADR| [Dutch API design rules](https://www.geonovum.nl/over-geonovum/actueel/rest-api-design-rules-op-pas-toe-leg-uit-lijst) | [[PUB-3]] |
| INSPIRE  | [INPSIRE-MIF document: Setting up an INSPIRE Download service based on the OGC API-Features standard](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md) | [[PUB-2]] |
| INSPIRE  | [CRS requirements](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#req-crs) | [[PUB-2]] #req-crs |
| INSPIRE  | [multilinguality](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#82-requirements-class-inspire-multilinguality-) |  [[PUB-2]] #82-requirements-class-inspire-multilinguality- |
| INSPIRE  | [predefined download](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#req-pre-defined | [[PUB-2]] #req-pre-defined |
| INSPIRE  | [bulk download](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#req-bulk-download) | [[PUB-2]] #req-bulk-download  |
| INSPIRE  | [GeoJSON](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#req-oapif-json) | [[PUB-2]] #req-oapif-json |
| INSPIRE  | INSPIRE validated GML as [input](https://inspire.ec.europa.eu/validator/about/) and [output](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#_requirements_class_geography_markup_language_gml_simple_features_profile_level_2) | https://inspire.ec.europa.eu/validator/about/ and [[PUB-1]] #_requirements_classes_for_encodings |
| INSPIRE  | [describing encoding](https://github.com/INSPIRE-MIF/2017.2/blob/master/GeoJSON/geojson-encoding-rule.md#inspire-requirements-for-encoding-rules) | [[PUB-4]] |

### OAS

The Open API Specification as set up by the [OpenAPI Initiative](https://openapis.org/) requires a document that describes an API or elements of an API. 
It can mostly be obtained by typing "openapi" behind the URL of the landing page of the service.
An OpenAPI document uses and conforms to the [OpenAPI Specification](https://spec.openapis.org/oas/v3.1.0).
It describes all the possible fields that can or should be used in the OpenAPI document.
The fields "openapi", "info" are required.
If the servers field is not provided, or contains an empty array, the default value would be a Server Object with a url value of /.
The OpenAPI document MUST contain at least one paths field, a components field or a webhooks field.

### OGC

#### OGC common

[The OGC-common standard](https://www.opengis.net/doc/is/ogcapi-common-1/1.0) has been established after the establishment of other OGC-standards like the OGC API Features Core standard.
In the course of developing these Standards, some practices proved to be common across multiple OGC Web API Standards.
The purpose of the OGC API — Common — Part 1: Core Standard (API-Core) is to define those fundamental building blocks and requirements which are applicable to all OGC Web API Standards.
It contains 4 requirement classes:
1. Core Requirements Class. It is about: HTTP protocol, parameters, Support for Cross-Origin Requests, resourceencoddings
2. Landing Page Requirements Class. It is about: conformances and API-definitions
3. Encoding Requirements Classes: Json and HTML
4. OpenAPI 3.0 Requirements Class: [OpenAPI Specification 3.0](https://spec.openapis.org/oas/v3.0) is required in json and html which is not in accordance with the OGC API Features Core standard.

#### OGC API Features Core

[OGC API Features Core](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0), [[PUB-1]] describes the basic requirements (51) and recommendations (22) according to OGC that one needs to follow, independent of INSPIRE. 
It describes which paths can be used and what responses one should receive. 
It does not make the use of the [OpenAPI Specification 3.0](https://spec.openapis.org/oas/v3.0) mandatory, but if it is used, it gives an extra [requirement class](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#rc_oas30).
Presumably, this also counts for higher versions of the OpenAPI Specification.

The [GeoJSON requirement class](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#_requirements_class_geojson) in [[PUB-1]] recommends to support GeoJSON for features with geometry, but as stated in https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#_encodings, no encoding is mandatory. 

[Metadata links](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#rec_core_fc-md-descriptions) are recommended in [[PUB-1]] #rec_core_fc-md-descriptions.

There is an [INSPIRE validation](https://inspire.ec.europa.eu/validator/home/index.html) on the OGC standards for OAPIF available. It tests on OGC requirements, but it does not test the requirements as stated in [[PUB-2]].
&nbsp;&nbsp;![INSPIRE Validator](media/INSPIRE_validator_OAPIF.png "Validation on the OGC standards for OAPIF")

#### OGC CRS requirements

Both OGC and INSPIRE have requirements related to the CRS's used in addition to the basic requirement from the OGC API Features Core standard.
The [CRS requirement](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#_coordinate_reference_systems) in the OGC API Features Core standard [[PUB-1]], requires [WGS84](http://www.opengis.net/def/crs/OGC/1.3/CRS84) for 2D-data and [WGS84h](http://www.opengis.net/def/crs/OGC/0/CRS84h) for 3D-data as default.
The [OGC API - Features - Part 2 standard](https://www.opengis.net/doc/IS/ogcapi-features-2/1.0), [[PUB-5]] prescribes how to support different coordinate systems with OAPIF.
Among other requirements, the requirements concern a CRS identifier list, Storage-CRS, a bbox-crs parameter and a content-CRS in the header of the body of the response.

#### OGC Filtering

The specification for [filtering](https://www.opengis.net/doc/IS/ogcapi-features-3/1.0), [[PUB-6]] has become an established standard after the publication of the examples. 
This standard has therefore not yet been taken into account in chapter 4.
Some basic filtering requirements are described in [OGC API - Features - Part 1: Core](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#_items_) [[PUB-1]].
This only concerns filtering with a bounding box and on properties.
The specification for [filtering](https://www.opengis.net/doc/IS/ogcapi-features-3/1.0) gives a full overview of extra requirement regarding filtering.
Some of them are listed below:
- Queryables: This requirements class defines the Queryables resource for discovering a list of resource properties with their types and constraints that may be used to construct filter expressions on a collection of resources, for example, a set of features.
- For every feature collection, the server SHALL support the Queryables resource at the path /collections/{collectionId}/queryables.
- There is a parameter [filter](https://www.opengis.net/doc/IS/ogcapi-features-3/1.0#filter-param) to define the filter as a string like _filter='property=value'_
- There is a parameter [filter-lang](https://www.opengis.net/doc/IS/ogcapi-features-3/1.0#filter-lang-param)  to define the filter language (CQL2-json or CQL2-text)
- There is a parameter [filter-crs](https://www.opengis.net/doc/IS/ogcapi-features-3/1.0#filter-crs-param) to define the crs for posted geomtries for filtering
- If the server supports CQL2 and the requirements class "Functions", then a resource '/functions' is published that allows clients to discover the list of functions that a server offers. 


### Dutch API design rules

Dutch data providers are recommended to follow the [Dutch API design rules](https://www.geonovum.nl/over-geonovum/actueel/rest-api-design-rules-op-pas-toe-leg-uit-lijst), [[PUB-3]] and the [Geomodule](https://docs.geostandaarden.nl/api/API-Strategie-mod-geo/). 

For the Dutch data providers, it is recommended to also support [RD-coordinatesystem](https://www.opengis.net/def/crs/EPSG/0/28992) for 2D data or [RD +NAP](https://www.opengis.net/def/crs/EPSG/0/7415) for 3D data. See also: https://docs.geostandaarden.nl/crs/crs. 

### INSPIRE

In the context of INSPIRE, the European member states are creating a digital network for exchanging information about the environment. [INSPIRE-MIF document: Setting up an INSPIRE Download service based on the OGC API-Features standard](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md), [[PUB-2]] describes the specific INSPIRE requirements.
Most of them are explained in the next chapters.
This document does propose in [Note 2](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#81-requirements-class-inspire-pre-defined-data-set-download-oapif--) to make it a mandatory requirement for INSPIRE to comply with [OAPIF requirements class OpenAPI 3.0.](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#rc_oas30)

#### INSPIRE CRS

The [INSPIRE-CRS requirement class](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#req-crs) in [[PUB-2]] requires also one of the INSPIRE CRS's based on ETRS89 to be supported.

#### INSPIRE Multilinguality

The [multilinguality requirement class](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#82-requirements-class-inspire-multilinguality-), [[PUB-2]] is mandatory for all data sets that contain information in more than one natural language.
This is mostly not the case in the Netherlands, so it is of less importance.

#### INSPIRE Predefined download

The [predefined download requirement class](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#req-pre-defined),[[PUB-2]] consists of 3 requirements for each collection to include links to:
1. the [metadata of the corresponding dataset](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#metadata-elements-of-the-data-set) in [[PUB-2]]
2. the corresponding entry in the [INSPIRE feature concept dictionary](https://inspire.ec.europa.eu/featureconcept)
3. the [license](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#terms-of-use)

#### INSPIRE Bulk download

The [bulk download requirement class](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#req-bulk-download), [[PUB-2]] requires links for enclosure of the total data set and/or of each separate collection.

#### INSPIRE and GeoJSON

The [GeoJSON requirement class](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md#req-oapif-json) in [[PUB-2]] recommends to document how the GeoJSON encoding is retrieved from the INSPIRE data models.

#### INSPIRE and GML
The use of GML as encoding for INSPIRE data can be considered in two ways: as input and as output.

When we consider the input, one would like to be able to use a source dataset of harmonized data. In most cases, this will be a GML encoded dataset. 
The GML encoding is at least needed to validate the data set with the [EU INSPIRE  validator](https://inspire.ec.europa.eu/validator/about/).  
Unfortunately, not many tooling for creating an OAPIF service is able to use GML as input. Especially when it concerns a complex GML dataset. So, a transformation to another encoding like GeoJSON is needed.

Output of GML from the OAPIF service can only be in simple features [level 0](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#_requirements_class_geography_markup_language_gml_simple_features_profile_level_0) and [level 2](https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#_requirements_class_geography_markup_language_gml_simple_features_profile_level_2).
So no complex features will be supported.

#### INSPIRE Describing encoding

The standards considered in this guideline do not set a specific encoding as mandatory (see https://www.opengis.net/doc/IS/ogcapi-features-1/1.0#_encodings) [[PUB-1]].
If another encoding than GML is used for publishing an INSPIRE dataset, data providers need to document how the encoding relates to the concerned INSPIRE data model.
The good practice on [GeoPackages encoding of INSPIRE datasets](https://github.com/INSPIRE-MIF/gp-geopackage-encodings/blob/main/spec/GeoPackage_Good_Practice_initiation_fiche.md) describes how this can be done.

###	Relevant documentation 

Relevant documentation is shown in [appendix A. References](#references).
