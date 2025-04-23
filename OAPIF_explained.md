## OGC API Features explained

OGC API Features (OAPIF) is a multi-part standard for services that offer the capability to create, modify, and query spatial data on the Web. 
It specifies requirements and recommendations for APIs that want to follow a standard way of sharing feature data. 
The specification is a multi-part document. [[PUB-1]], [[PUB-5]], [[PUB-6]].
OAPIF is also the term used for a feature download service by means of an API (Application Program Interface) based on OGC standards. 

OAPIF is one of the service types in a larger family of [OGC APIs](https://www.ogc.org/publications/). 
Other types are OGC-API Tiles(https://www.ogc.org/publications/standard/ogcapi-tiles/) or OGC-API Maps(https://www.ogc.org/publications/standard/ogcapi-maps/). 
The OGC-APIs are a new generation of API's based on a REST protocol, where the older generation (WFS en WMS) are based on SOAP.  

&nbsp;![OGC-APIs](media/OGC-APIs.jpg "A new generation of geoservices: OGC-APIs").

Since October 2024, a change has been made to the Geostandards on the [Dutch "Apply or Explain" list](https://www.geonovum.nl/over-geonovum/actueel/rest-api-design-rules-op-pas-toe-leg-uit-lijst) (Pas Toe of Leg Uit (PTLU) lijst in Dutch) of the Dutch Standardization Forum. 
This list now includes the new generation of standards: OGC API Features and OGC API Tiles. The WMS and WFS profiles have been moved to the list of recommended standards.

OAPIF has been considered as the successor of the OGC WFS standard, but that does not mean it will replace it in the near future, although eventually it might.
At this moment, they are complementary to each other. Where WFS is mainly known and used in the GIS community, the OAPIF is aiming broader at both the GIS- and non GIS-community, like web developers. 
OAPIF is easier to use and needs less knowledge in the spatial domain.
Note as well that WFS adopts the Geography Markup Language (GML) as a default data format. In contrast, OAPIF includes recommendations to support HTML and GeoJSON as encodings.
Implementations of OAPIF may also optionally support GML.

The basis of an OAPIF is the landing page. Examples are shown in [chapter 4](https://geonovum.github.io/ogc-api-features-guideline/#H04).
An OAPIF consists of resources that can be retrieved by typing the corresponding path after the landing page of the OAPIF in a web browser or web application.

|Resource               |Path                                         |Purpose                                                                                      |
|-----------------------|---------------------------------------------|---------------------------------------------------------------------------------------------|
|Landing page           |/                                            |This is the top-level resource, which serves as an entry point.                              |
|Conformance declaration|/conformance                                 |This resource presents information about the functionality that is implemented by the server.|
|API definition         |/openapi or /api                             |This resource provides metadata about the API itself. Note that the use of /api on the server is optional and the API definition may be hosted on a completely separate server.|
|Feature collections    |/collections                                 |This resource lists the feature collections that are offered through the API.                |
|Feature collection     |/collections/{collectionId}                  |This resource describes the feature collection identified in the path.                       |
|Features               |/collections/{collectionId}/items            |This resource presents the features that are contained in the collection.                    |
|Feature                |/collections/{collectionId}/items/{featureId}|This resource presents the feature that is identified in the path.                           |

In the API definition, one can find all the supported encodings (HTML, JSON) and parameters that can be given along with the URL, such as a bounding box or a limit of the amount of features.
By default, an OAPIF service will provide access to a single dataset.
Rather than sharing the data as a complete dataset, the OGC API Features standards offer direct, fine-grained access to the data at the feature (object) level.

The best way of understanding the concept is looking at the examples that are discussed in the chapter of [examples](#H04).

Since providing a download service is an [[ INSPIRE ]] requirement when responsible for an INSPIRE dataset, the use of OAPIF can be considered for this purpose.
It is even seen as an endorsed <a href="https://inspire.ec.europa.eu/portfolio/good-practice-library/" target="_blank">Good Practice</a> within the INSPIRE community.
In the European Open Data Directive (EU) 2019/1024, the European Commission designates a list of thematic categories of high-value datasets (the ‘High Value Datasets’ (HVD)). This directive also endorses the use of OGC-APIs.
For the Dutch data providers there is a special [HVD guideline](https://docs.geostandaarden.nl/eu/handreiking-hvd/#289E9E05) and an [INSPIRE guideline](https://docs.geostandaarden.nl/eu/INSPIRE-handreiking/).

While the OAPIF is also aiming at the non GIS-community, it is also easy to use for GIS-specialists within a GIS-client as is shown in the image below.
It works the same as loading a WFS. Only a service name and landing page is required. 
&nbsp;![GIS-example](media/GIS-example.png "Example of using OAPIF in QGIS")
