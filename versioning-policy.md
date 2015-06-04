---
title: Versioning Policy
layout: page
resource: true
categories:
- Policy
---

MeSH is versioned on a yearly basis. NLM releases provisional MeSH data for the following year each September, and changes to MeSH are implemented in PubMed the following December. 2015 MeSH data was released in XML format in September, 2014. Most changes made in September of each year involve the addition of new Descriptors to the MeSH vocabulary. Supplementary Concept Records are added throughout the year, and those changes are reflected in daily updates to MeSH XML. Starting June 15, 2015, MeSH RDF data will update on a daily basis in sync with MeSH XML. 

MeSH RDF will use the following conventions for URIs, graphs and filenames:

### URIs

#### Data URIs

MeSH RDF will follow established versioning practices, but MeSH RDF will be expressed in versioned and non-versioned URIs. For example, the Descriptor for Ofloxacin will have the following URIs:

* http://id.nlm.nih.gov/mesh/D015242 (current)
* http://id.nlm.nih.gov/mesh/2015/D015242 (2015)

The non-versioned URI reflects the current state of MeSH at any given time. The versioned URI for the current year will mirror the non-versioned URI. When the next year's MeSH data is released in the Fall, then that year's versioned URI will begin to mirror the non-versioned URI, and the current year's URI will become static and archived. NLM will retain no more than three years of versioned URIs, and NLM will not produce versioned URIs for data prior to 2015. 

#### Vocabulary URIs

MeSH RDF vocabulary URIs will be versionless, though they will be derived from versioned schema files (see below). All predicate and class URIs will have the following prefix, regardless of MeSH year or schema version: http://id.nlm.nih.gov/mesh/vocab#. Resource names are in camel case, with class names having the first letter capitalized, and predicate names having the first letter in lowercase. For example,

* Predicate: http://id.nlm.nih.gov/mesh/vocab#pharmacologicalAction
* Class: http://id.nlm.nih.gov/mesh/vocab#TopicalDescriptor

#### Deprecated URIs

Currently, we do not have a mechanism for handling deprecated URIs. On occasion, Supplementary Concept Records may be removed from MeSH data. When that happens, that Supplementary Concept Record's triples will disappear from the graph, and the data will no longer be available for that URI. Requests for deprecated URIs will still return an HTTP 200 status code, but no data will be available. We intend to address this in a future release. Additionally, some non-existing URIs will return HTTP 200 status codes. Any URI that fits a pattern expressed in our [URL rewrite document](https://github.com/HHS/lodestar/blob/meshrdf/web-ui/src/main/webapp/WEB-INF/urlrewrite.xml) will return an HTTP 200 status code, whether it is a valid URI or not. Keep this in mind when making requests based on URI patterns. 

### Graphs

#### Data Graphs

MeSH RDF data is expressed in a current, versionless graph and a versioned graph:

* http://id.nlm.nih.gov/mesh (current)
* http://id.nlm.nih.gov/mesh/2015 (2015)

Use these graphs to run SPARQL queries on MeSH RDF data. NLM will retain no more than three years of versioned graphs, and NLM will not produced versioned graphs for data prior to 2015. 

#### Vocabulary Graph

MeSH RDF's vocabulary is expressed in a versionless graph:

* http://id.nlm.nih.gov/mesh/vocab 

This graph expresses the MeSH vocabulary schema, which includes the following information:

* Types of classes and properties (expressed by rdf:type)
* Class and property labels (rdfs:label)
* Subproperty and subclass relationships (rdfs:subClassOf)
* Disjoint relationships between classes or properties (owl:disjointWith, owl:propertyDisjointWith)
* Descriptions of classes and properties (dct:description)

#### VoID Graph

The VOID graph is versionless and contains metadata about MeSH RDF:

* http://id.nlm.nih.gov/mesh/void

### FTP Download Files

NLM makes available MeSH RDF files for download:

* ftp://ftp.nlm.nih.gov/online/mesh/

#### Data Files

Current MeSH RDF data is available for download in .nt (N-Triples format). 

* Filename: mesh.nt 
* Location: ftp://ftp.nlm.nih.gov/online/mesh/

MeSH XML is also available. 

Versioned MeSH data is available in subdirectories labeled by year. 

* Filename: mesh2015.nt 
* Location: ftp://ftp.nlm.nih.gov/online/mesh/2015/

#### Vocabulary Files

The MeSH vocabulary schema is expressed in a .ttl (TURTLE) file on the FTP site. This file has a version number that will increment upon changes to the vocabulary schema. 

* Filename: vocabulary_0.9.ttl 
* Location: ftp://ftp.nlm.nih.gov/online/mesh/
