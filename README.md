# OntoUML/UFO Catalog

<p align="center"><img src="https://user-images.githubusercontent.com/8641647/223740939-1abcd2af-e954-4d19-b087-56f1be4417c3.png" width="500">

The FAIR Model Catalog for Ontology-Driven Conceptual Modeling Research, commonly referred to as **OntoUML/UFO Catalog**, is a structured and open-source catalog that contains OntoUML and UFO ontology models. It was conceived to allow collaborative work and to be easily accessible to all its users.

The goal of the OntoUML/UFO Catalog is to support empirical research in OntoUML and UFO, as well as for the general conceptual modeling area, by providing high-quality curated, structured, and machine-processable data on *why*, *where*, and *how* different modeling approaches are used.

The catalog offers a diverse collection of models, created by modelers with varying modeling skills, for a range of domains and different purposes. The models are available in machine-readable formats (JSON and Turtle) and are accessible via permanent identifiers.

The catalog has two data services through which we store and publish its content: this Git online repository for data storage, and a FAIR Data Point (FDP) for data discovery. While we outline the FDP in this document, the focus of this documentation is on the catalog’s repository. 

## Table of Contents

- [OntoUML/UFO Catalog](#ontoumlufo-catalog)
  - [Table of Contents](#table-of-contents)
  - [Catalog’s Content](#catalogs-content)
    - [Data Organization](#data-organization)
    - [Catalog Releases](#catalog-releases)
    - [Data Schemas](#data-schemas)
      - [OntoUML Metamodel](#ontouml-metamodel)
      - [OntoUML Schema](#ontouml-schema)
      - [Models in Linked Data](#models-in-linked-data)
    - [Metadata](#metadata)
      - [Resource](#resource)
      - [Dataset](#dataset)
      - [Catalog](#catalog)
      - [Semantic Artifact](#semantic-artifact)
      - [Distribution](#distribution)
    - [FAIR Data Point: The Data Discovery Service](#fair-data-point-the-data-discovery-service)
  - [Catalog's Persistent URLs](#catalogs-persistent-urls)
  - [How to Contribute](#how-to-contribute)
    - [Contribute by Submitting an Ontology](#contribute-by-submitting-an-ontology)
    - [Other Ways to Contribute](#other-ways-to-contribute)
  - [Relevant Associated Works](#relevant-associated-works)
  - [Catalog administration](#catalog-administration)
  - [How to Cite this Catalog](#how-to-cite-this-catalog)
  - [Acknowledgements](#acknowledgements)
  - [License disclaimer](#license-disclaimer)

## Catalog’s Content

### Data Organization

This repository contains OntoUML and UFO models and all their distributions, serving as our *de facto* data storage service. We describe below the catalog's repository structure and the files it contains:

```txt
/ontouml-models
|--- catalog.ttl
+--- /models
|     +--- /"model-directory-1"
|          |--- ontology.vpp
|          |--- ontology.json
|          |--- ontology.ttl
|          +--- /original-diagrams
|          |    |--- "diagram-1".png
|          +--- /new diagrams
|          |    |--- "diagram-1".png
|          |--- metadata.ttl
|          |--- metadata-vpp.ttl
|          |--- metadata-json.ttl
|          |--- metadata-turtle.ttl
|          |--- metadata-png-o-"diagram-1".ttl
|          |--- metadata-png-n-"diagram-1".ttl
+--- /shapes
     |--- Resource-shape.ttl
     |--- Dataset-shape.ttl
     |--- Catalog-shape.ttl
     |--- SemanticArtefact-shape.ttl
     |--- Distribution-shape.ttl
```

- `catalog.ttl`: the Turtle file that contains all metadata about the catalog in linked data format.

- `/models`: the directory containing all cataloged models.

- `/"model-directory-1"`: a directory containing a single model and distributions that materialize it. Most model directories' names are composed of information about the model itself, such as the name of the first author, the year of publication, or the name of the model.

- `ontology.*`: the file generated by the modeling tool used to create or reproduce the model. The modeling tool in question must be able to serialize the model in JSON format in conformance with the [Ontouml Schema](https://w3id.org/ontouml/schema) (e.g., the [Visual Paradigm UML CASE](https://www.visual-paradigm.com/download/community.jsp), `.vpp` extension, with the [OntoUML Plugin for Visual Paradigm](https://purl.org/ontouml-vp)).

- `ontology.json`: the JSON serialization of the model in conformance with the [Ontouml Schema](https://w3id.org/ontouml/schema).

- `ontology.ttl`: the Turtle serialization of the model in linked data format described with the [OntoUML Vocabulary](https://w3id.org/ontouml/vocabulary). This file is automatically generated after the JSON serialization.

- `/original-diagrams`: the directory containing all diagrams of the model in PNG format. These diagrams are either (i) created from the original file generated by the modeling used, or (ii) extracted from the source where the model was published (e.g., screenshots from the original publication).

- `/new-diagrams`: the directory containing all diagrams of the model in PNG format.

- `metadata.ttl`: the Turtle file that contains all metadata about the model in linked data format.

- `metadata-vpp.ttl`: the Turtle file that contains all metadata about the model file, the `ontology.vpp` distribution, in linked data format. This file is automatically generated.

- `metadata-json.ttl`: the Turtle file that contains all metadata about the model's JSON serialization file, the `ontology.json` distribution, in linked data format. This file is automatically generated.

- `metadata-turtle.ttl`: the Turtle file that contains all metadata about the model's Turtle serialization file, the `ontology.ttl` distribution, in linked data format. This file is automatically generated.

- `metadata-png-o-"diagram-1".ttl`: a Turtle file that contains all metadata about one of the model's original diagrams, a `/original-diagrams/"diagram-1".png` distribution, in linked data format. A file is automatically generated for each original diagram.

- `metadata-png-n-"diagram-1".ttl`: a Turtle file that contains all metadata about one of the model's new diagrams, a `/new-diagrams/"diagram-1".png` distribution, in linked data format. A file is automatically generated for each new diagram.

- `/shapes`: the directory containing the SHACL shapes used in the validation of metadata schemas.

- `Resource-shape.ttl`: the Turtle file that contains the SHACL shape used to validate metadata about resources of type `dcat:Resource`.

- `Dataset-shape.ttl`: the Turtle file that contains the SHACL shape used to validate metadata about resources of type `dcat:Dataset`.

- `Catalog-shape.ttl`: the Turtle file that contains the SHACL shape used to validate metadata about resources of type `dcat:Catalog`.

- `SemanticArtefact-shape.ttl`: the Turtle file that contains the SHACL shape used to validate metadata about resources of type `mod:SemanticArtefact`.

- `Distribution-shape.ttl`: the Turtle file that contains the SHACL shape used to validate metadata about resources of type `dcat:Distribution`.

### Catalog Releases

The catalog also offers releases comprising all its data and metadata compiled into a single Turtle file. Releases are tagged after the following nomenclature `<YYYY><MM><DD>` and can be accessed via the permanent identifier https://w3id.org/ontouml-models/release/_<release_tag>_.

### Data Schemas

The cataloged OntoUML and UFO models are documented in two different formats, referred to as data schemas: the [OntoUML Schema](https://w3id.org/ontouml/schema) and the [OntoUML Vocabulary](https://w3id.org/ontouml/vocabulary). Both formats are build upon an implementation-independent metamodel, the [OntoUML Metamodel](https://w3id.org/ontouml/metamodel), and are equivalent in terms of the content being represented and are automatically generated by software, but tailored for their individual use cases.

#### OntoUML Metamodel

The [OntoUML Metamodel](https://w3id.org/ontouml/metamodel) allows its specialization on implementation-specific metamodels to be used as manipulation and exchange of OntoUML models by software agents focused on the UML features relevant to OntoUML. It covers several features of the UML metamodel related to its class diagram language, however, simplified to meet the needs of OntoUML.

#### OntoUML Schema

Designed to support the development of model intelligence services in OntoUML, the [Ontouml Schema](https://w3id.org/ontouml/schema) specializes the [OntoUML Metamodel](https://w3id.org/ontouml/metamodel) to specify how to serialize OntoUML models in JSON. In this format, OntoUML can be easily exchanged between clients and servers communicating over HTTP, with extensive support from all major tech stacks, including easy processing within browser applications.

The JSON is a format better suited for manipulation within software code than linked data formats. It supports the exchange of models between modeling tools and the OntoUML server, providing model intelligent services (e.g., model verification and transformation).

#### Models in Linked Data

While JSON offers a suitable solution for exchanging and manipulating models with software, the ability to query models is extremely useful for analyzing them. This is even more pronounced in the context of a catalog of models, where the significant size of the catalog enables, for example, the generation of statistical reports and the detection of recurrent patterns. The serialization of OntoUML models in a linked data format allows us to feed them to a knowledge graph and perform complex analysis using the SPARQL querying language, all with no need for additional software.

### Metadata

![metadata-schema](documentation/metadata-schema.png)

The catalog’s schema, depicted in the image above, reuses classes and properties from the following RDF/OWL vocabularies:

- [Data Catalog Vocabulary (DCAT)](http://www.w3.org/ns/dcat): The central vocabulary in our metadata schema, DCAT was “*designed to facilitate interoperability between data catalogs published on the Web*”.

- [Dublin Core Terms (DCT)](http://purl.org/dc/terms/): A vocabulary that defines properties to describe basic metadata of resources on the web.

- [Friend of a Friend (FOAF)](http://xmlns.com/foaf/0.1): A vocabulary that offers terms to describe people, groups, companies, and other types of agents.

- [Metadata for Ontology Description and Publication (MOD)](https://w3id.org/mod/2.0): A vocabulary that defines properties to describe the metadata of ontologies and other semantic artefacts.

- [Simple Knowledge Organization System (SKOS)](http://www.w3.org/2004/02/skos/core): A vocabulary for representing and linking knowledge organization systems.

- [vCard](http://www.w3.org/2006/vcard/ns): A vocabulary to describe contact information (e.g., email, phone number).

As we could not satisfy the metadata needs of our stakeholders using the existing vocabularies alone, we complemented them with one of our own—the [OntoUML/UFO Catalog Metadata Vocabulary](https://w3id.org/ontouml-models/vocabulary), associated to the following URLs:
- Turtle file: https://w3id.org/ontouml-models/vocabulary
- Specification: https://w3id.org/ontouml-models/vocabulary/docs
- Git repository: https://w3id.org/ontouml-models/vocabulary/git
- Releases:
  - Latest release: https://w3id.org/ontouml-models/vocabulary/latest
  - Specific release: https://w3id.org/ontouml-models/vocabulary/release/_<version_number>_
    - _<version_number>_ must be substituted by a release version number starting with the letter 'v' (e.g., 'v1.0.0')

The elements defined there are identified below by the prefix **ocmv**.

#### Resource

A `dcat:Resource`' is an object that we keep track in the catalog (including the catalog itself). A resource can be described by the following properties:

- `dct:title`: Determines a title for the resource. Accepts `xsd:string` and `rdf:langString` literals. E.g., "Common Ontology of Value and Risk"@en, "FAIR Model Catalog for Ontology-Driven Conceptual Modeling Research"@en. There must be at most one title per language.
  
- `dct:alternative`: Determines an alternative title for the resource. Accepts `xsd:string` and `rdf:langString` literals. E.g., "OntoUML/UFO Catalog"@en.

- `dct:description`: Determines a free-text account of the resource. Accepts `xsd:string` and `rdf:langString` literals.

- `dct:issued`: Determines when the resource was created. Accepts literals of the types `xsd:dateTime`, `xsd:date`, `xsd:gYearMonth`, and `xsd:gYear`.  e.g., "2018"^^xsd:gYear, "2018-01-15"^^xsd:date. When cataloging a model from documents, we recommend using the publication date from the first one.

- `dct:modified`: Determines when the resource was last modified. Accepts literals of the types `xsd:dateTime`, `xsd:date`, `xsd:gYearMonth`, and `xsd:gYear`. When cataloging a model based on documents, we recommend using the publication date from the latest one.

- `dct:license`: Identifies a legal document under which the resource is made available. E.g., https://creativecommons.org/licenses/by/4.0/.

- `dct:accessRights`: Identifies a `dct:RightsStatement` or a text concerning who and how the resource can be accessed. E.g., the statement http://publications.europa.eu/resource/authority/access-right/PUBLIC informs that something is "publicly accessible by everyone".

- `skos:editorialNote`: Determines a general note relative to the resource documentation process. Accepts `xsd:string` and `rdf:langString` literals. E.g., "The model was originally designed in Portuguese and translated by the publisher."@en.

- `dct:contributor`: Identifies a `foaf:Agent` who contributed to the development of the resource. 

- `dct:creator`: Identifies a `foaf:Agent` who contributed to the creation of the resource.

- `dct:publisher`: Identifies the `foaf:Agent` who added the resource to the catalog. The publisher does not need to have created or contributed to the resource.

Whenever referring to a `foaf:Agent`, we recommend the usage of a persistent and resolvable identifier, such as those provided by DBLP (e.g., https://dblp.org/pid/96/8280) or ORCID. If such an identifier is absent, we suggest the use of a URL that references the agent’s profile in a digital platform (e.g., https://github.com/tgoprince) or a webpage about the agent (e.g., http://www.mattspace.net/).

#### Dataset

A `dcat:Dataset` is a `dct:Resource` that comprises a collection of data items and is available for access or download in one or more distributions. Here, we describe datasets with the following properties:


- `dcat:landingPage`: Identifies a web page where one can access the dataset, its metadata, its distributions, and additional information about it. E.g., https://www.model-a-platform.com is the landing page of the Digital Platform Ontology.

- `dct:bibliographicCitation`: Determines a bibliographic reference for the dataset in textual format. Accepts `xsd:string` and `rdf:langString` literals. E.g., "Weigand, H., Johannesson, P., & Andersson, B. (2021). An artifact ontology for design science research. Data & Knowledge Engineering, 133."@en

- `ocmv:storageUrl`: Determines a URL of a service in which the data and metadata of the dataset are stored. Accepts values in `xsd:anyURI`.

- `dcat:distribution`: Identifies an available `dcat:Distribution` of the dataset. 

- `dcat:contactPoint`: Identifies a `vcard:vCard` that contains information on how to contact an agent responsible for the dataset. We required that at least an email is provided.

#### Catalog

A `dcat:Catalog` is a curated `dcat:Dataset` consisting of metadata about resources. Here, we naturally focus on single catalog instance, the OntoUML/UFO Catalog, which contains metadata about conceptual models and their distributions. A fragment of its metadata record is shown in this section's initial image. The additional properties we used are discussed below.


- `dcat:themeTaxonomy`: Identifies a knowledge organization system used to classify the semantic artifacts in the catalog. In our catalog, we use the [Library of Congress Classification (LCC)](https://www.loc.gov/catdir/cpso/lcco/) system, which exists as a `skos:ConceptScheme`.

- `dcat:dataset`: Identifies a `mod:SemanticArtefact` listed in the catalog.

#### Semantic Artifact

The conceptual models in our catalog are categorized as instances of `mod:SemanticArtefact`, a type of `dcat:Dataset` whose data items are the formalization of concepts, properties, relations, and constraints about a domain of interest. The metadata record of a semantic artefact, exemplified in this section's image, extends that of a `dcat:Dataset` with the following properties:

- `dcat:keyword`: Determines a domain (partially) described by the semantic artefact. Accepts `xsd:string` and `rdf:langString` literals. E.g., the User Feedback Ontology is described with the keywords "online user feedback", "software engineering", "requirements engineering".

- `mod:acronym`: Determines an acronym one can use to refer to the semantic artefact. Accepts only `xsd:string` literals. E.g., "RDBS-O", "COVER", "ROT".

- `dct:source`: Identifies resources that contain, present, or significantly influenced the development of the semantic artifact. We recommend the use of persistent and resolvable identifiers to refer to these resources, such as the Digital Object Identifier (DOI) or DBLP's URI. E.g., https://doi.org/10.3233/AO-150150, https://dblp.org/rec/journals/ao/Morales-Ramirez15.

- `dct:language`: Determines a language in which the lexical labels of the semantic artefact are written. We require the use of values listed in the [IANA Language Sub Tag Registry](https://www.iana.org/assignments/language-subtag-registry). E.g., "en", "pt".

- `dcat:theme`: Identifies the central theme of the semantic artifact according to a theme taxonomy. In our catalog, the theme of an artifact must be a `skos:Concept` from the LCC. E.g., "Class S - Agriculture", "Class T - Technology".

- `mod:designedForTask`: Identifies a goal that motivated the development of the semantic artefact. To standardize the use of this property, we documented some recurrent modeling goals:

  - `ocmv:ConceptualClarification`: The artifact was created as the result of an ontological analysis of a concept, language, or domain of interest that sought to conceptually clarify and untangle complex notions and relations.

  - `ocmv:DataPublication`: The artifact was created to support the publication of some datasets. For instance, a conceptual model used to generate an OWL vocabulary to publish tabular data as linked open data on the web.

  - `ocmv:DecisionSupportSystem`: The artifact was created during the development of a decision support system.

  - `ocmv:Example`: The artifact was created to demonstrate how OntoUML can be used to solve a certain modeling challenge, to support an experiment involving OntoUML, or to exemplify how a generic model can be reused in more concrete scenarios.

  - `ocmv:InformationRetrieval`: The artifact was created to support the design of a information retrieval system.

  - `ocmv:Interoperability`: The artifact was created to support data integration, vocabulary alignment, or the interoperability of software systems.

  - `ocmv:LanguageEngineering`: The artifact was created for the design of a domain-specific modeling language.

  - `ocmv:Learning`: The artifact was created so that its authors could learn UFO and OntoUML. This usually applies to models developed by students as part of their course assignments. 

  - `ocmv:SoftwareEngineering`: The artifact was created during the development of an information system. For instance, a conceptual model used to generate a relational database.

- `ocmv:context`: Identifies an `ocmv:Context` in which the artifact was developed, namely:

  - `ocmv:Research`: The artifact was developed as part of a research project. This usually implies that the artifact was featured in a scientific publication.

  - `ocmv:Industry`: The artifact was developed for a public or private organization. 

  - `ocmv:Classroom`: The artifact was developed within the context of a course on conceptual modeling, most likely as a course assignment.

- `ocmv:representationStyle`:  Identifies an `ocmv:OntologyRepresentationStyle` representation styles adopted in the artefact. We account for the existence of two values: 

  - `ocmv:OntoumlStyle`: Characterizes a model that contains at least one class, relation, or property using a valid OntoUML stereotype.

  - `ocmv:UfoStyle`: Characterizes a model that contains at least one class or relation from UFO without an OntoUML stereotype.

- `ocmv:ontologyType`: Identifies the categorization of the ontology according to its scope. For this catalog, we adopt the following three categories proposed by [Roussey et al.](https://doi.org/10.1007/978-0-85729-724-2_2):

  - `ocmv:Core`: An ontology that grasps the central concepts and relations of a given domain, possibly integrating several domain ontologies and being applicable in multiple scenarios. e.g., UFO-S, a commitment-based ontology of services, can be considered a core ontology because it applies to services in multiple domains, such as medical, financial, and legal services.

  - `ocmv:Domain`: An ontology that describes how a community conceptualizes a phenomenon of interest. In general, a domain ontology formally characterizes a much narrower domain than a core ontology does. e.g., OntoBio is a domain ontology of biodiversity.

  - `ocmv:Application`: An ontology that specializes a domain ontologies where there could be no consensus or knowledge sharing. It represents the particular model of a domain according to a single viewpoint of a user or a developer.

#### Distribution

A `dcat:Distribution` is a `dcat:Resource` that materializes a `dcat:Dataset`. The characterization of a distribution, -metadata, accounts the following additional properties:

- `dcat:downloadURL`: Identifies a URL that can be used to download the distribution. 
        
- `dcat:mediaType`: Identifies the media type of the distribution. Valid media types are only those defined by IANA, such as https://www.iana.org/assignments/media-types/application/json. If there is no media type for the format of the distribution, the type application/octet-stream must be used for binary files and the type text/plain must be used for text files. 
    
- `dct:format`: Identifies the format of the distribution. This property should be used to complement `dcat:mediaType` when the distribution format is not listed by IANA. We limit the use of this property with URIs so that more context about how to manipulate a distribution can be provided. e.g., https://www.file-extension.info/format/vpp.
    
- `ocmv:isComplete`: Determines if a distribution contains all the data from the `dcat:Dataset` it materializes. In the catalog, the distributions of models in VPP, JSON, and Turtle are complete, while those in image format are not.
    
- `ocmv:conformsToSchema`: Identifies a schema upon which the distribution can be validated against. e.g., a JSON Schema document, a SHACL shape, and an XML Schema document. The identified schema should be compatible with the media type of the distribution. That is, if a distribution is in JSON, the schema cannot be an XML Schema.

### FAIR Data Point: The Data Discovery Service

The [OntoUML FAIR Data Point](https://w3id.org/ontouml-models) is a deployment of [the FAIR Data Point (FDP) reference implementation](https://doi.org/10.1162/dint_a_00160), which is a FAIR-compliant platform designed to expose semantically rich metadata of FAIR digital objects. Deployed as a web server, the FDP provides important features to the catalog, including the generation of global unique IDs, the generation of webpages for each resource in the catalog based on their semantic annotations, and the search of resources based on textual information or user-defined SPARQL queries. The FDP is automatically synchronized with the data storage, service serving as the *data discovery service* for the catalog.

## Catalog's Persistent URLs

We created persistent URLs for the following resources:

- FDP Catalog page: https://w3id.org/ontouml-models
- GitHub repository: https://w3id.org/ontouml-models/git
- OntoUML vocabulary: https://w3id.org/ontouml
- Catalog's releases:
  - Latest release: https://w3id.org/ontouml-models/release
  - Specific release: https://w3id.org/ontouml-models/release/_<release_tag>_
    - *\<release_tag\>* must be substituted by a release tag string (e.g., '20230602')
- Catalog Vocabulary TTL file: https://w3id.org/ontouml-models/vocabulary
- Shape TTL files:
  - https://w3id.org/ontouml-models/shape/Catalog
  - https://w3id.org/ontouml-models/shape/Dataset
  - https://w3id.org/ontouml-models/shape/Distribution
  - https://w3id.org/ontouml-models/shape/Resource
  - https://w3id.org/ontouml-models/shape/SemanticArtefact

## How to Contribute

Your contribution is fundamental to the catalog's success. We highly encourage authors to submit their models and tools to this catalog. With that, you will be supporting research in (ontology-driven) conceptual modeling, ontology engineering, software design, and several others.

***We greatly appreciate your contribution to this project!***

### Contribute by Submitting an Ontology

The easiest way to contribute to this catalog is to simply send us the following:

1.  your ontology model project;
2.  the model's metadata information; and
3.  the model's associated bibliography (when available).

If you wish to contribute to this initiative by submitting your ontology, use the [catalog's contribution form](https://forms.gle/wNSMfaJfkS3hi69o7).

Note that **anonymous ontologies are allowed in the catalog**. So, if you do not want your name to be displayed in your ontology’s metadata, you just have to inform us and we will keep the model’s authorship anonymous. It is important that, in such case, you must be the owner of the ontology’s legal rights.

If you wish to contribute by submitting someone else's ontology, please chose one entry from the "*Not Started*" or "*Started*" sheets from the [List of UFO and OntoUML Ontology Models](https://docs.google.com/spreadsheets/d/1JXEA3k58yAkV_jbmEc7HP9QK7RgZC5Jk1y8MR7ylFyQ/edit?usp=sharinghttps://docs.google.com/spreadsheets/d/1JXEA3k58yAkV_jbmEc7HP9QK7RgZC5Jk1y8MR7ylFyQ/edit?usp=sharing). Ontologies in the *Started* sheet already have files available in a branch (informed in the spreadsheet), simplifying the collaboration process.

For providing high-quality data, submissions are required to comply with the defined rules to be accepted as part of the catalog. If you have any questions about submitting new models or reusing those available in this catalog, please [create an issue](https://github.com/OntoUML/ontouml-models/issues).

### Other Ways to Contribute

If you wish to contribute to this initiative by **creating and reporting an application** for the catalog, please inform us through the [catalog's contribution form](https://forms.gle/wNSMfaJfkS3hi69o7) or [create an issue](https://github.com/OntoUML/ontouml-models/issues).

If you find any problems in the repository or have ideas for its improvement, please let us know through the [catalog's contribution form](https://forms.gle/wNSMfaJfkS3hi69o7) or by [creating an issue](https://github.com/OntoUML/ontouml-models/issues).

## Relevant Associated Works

The list of works that use the data provided by the OntoUML/UFO Catalog to test algorithms and perform other tasks grows over time. Instead of keeping a manual list in this document, we recommend you access its [Google Scholar](https://scholar.google.com/scholar?cites=3857815022699931555&as_sdt=2005&sciodt=0,5&hl=en) and [ResearchGate](https://www.researchgate.net/publication/364289037_A_FAIR_Model_Catalog_for_Ontology-Driven_Conceptual_Modeling_Research/citations) citation lists to access an updated information.

## Catalog administration

The OntoUML/UFO Catalog is maintained by the [Semantics, Cybersecurity & Services (SCS) Group](https://www.utwente.nl/en/eemcs/scs/) of the [University of Twente](https://www.utwente.nl/), in The Netherlands. Its principal administrators are:

- [Pedro Paulo F. Barcelos](https://orcid.org/0000-0003-2736-7817) [\[GitHub\]](https://github.com/pedropaulofb) [\[LinkedIn\]](https://www.linkedin.com/in/pedro-paulo-favato-barcelos/)
- [Tiago Prince Sales](https://orcid.org/0000-0002-5385-5761) [\[GitHub\]](https://github.com/tgoprince) [\[LinkedIn\]](https://www.linkedin.com/in/tiago-sales/)
- [Mattia Fummagali](https://orcid.org/0000-0003-3385-4769) [\[GitHub\]](https://github.com/Matt-81) [\[LinkedIn\]](https://www.linkedin.com/in/mattiafumagalli/)
- [Claudenir M. Fonseca](https://orcid.org/0000-0003-2528-3118) [\[GitHub\]](https://github.com/claudenirmf) [\[LinkedIn\]](https://www.linkedin.com/in/claudenir-fonseca-52b251216/)

Feel free to get in contact with the administrators using the links provided. For questions, contributions, or to report any problem, you can [open an issue](https://github.com/OntoUML/ontouml-models/issues) at this repository.

## How to Cite this Catalog

Please cite the OntoUML/UFO Catalog as:

*Barcelos, P. P. F., Sales, T. P., Fumagalli, M., Fonseca, C. M., Sousa, I. V., Romanenko, E., Kritz, J., & Guizzardi, G.* (2022). A FAIR Model Catalog for Ontology-Driven Conceptual Modeling Research. In: Ralyté, J., Chakravarthy, S., Mohania, M., Jeusfeld, M.A., Karlapalem, K. (eds) Conceptual Modeling. ER 2022. Lecture Notes in Computer Science, vol 13607. Springer, Cham. <https://doi.org/10.1007/978-3-031-17995-2_1>. Permanent URL: <https://w3id.org/ontouml-models/>.

For creating citations using different formats, refer to the [webpage of the paper's publisher](https://link.springer.com/chapter/10.1007/978-3-031-17995-2_1#citeas) for getting the paper's complete information.

For obtaining the paper's complete BibTeX record, we recommend downloading this information on [the same webpage](https://citation-needed.springer.com/v2/references/10.1007/978-3-031-17995-2_1?format=bibtex&flavour=citation) or accessing it on the [DBLP BibTeX record](https://dblp.org/rec/conf/er/BarcelosSFFSRKG22.html?view=bibtex).

This paper reflects the state of the catalog as of June 2022.

## Acknowledgements

We would like to thank all the [contributors](https://github.com/OntoUML/ontouml-models/graphs/contributors) to the OntoUML/UFO Catalog, as well as all the modelers who shared their work and allowed us to include it here.

## License disclaimer

The OntoUML/UFO Catalog is licensed under the [Creative Commons Attribution-ShareAlike 4.0 International Public License.](https://creativecommons.org/licenses/by-sa/4.0/)

Although the OntoUML/UFO Catalog is an open project with a permissive license, special attention must be given to the following licensing clauses:

- The OntoUML/UFO Catalog is a noncommercial work created strictly for academic research purposes.
- This license only applies to the catalog structure itself, not to the models included in the repository.
- Information about licensing of individual ontologies included in the catalog can be found on their related metadata.yaml file.
- The models included in the repository were obtained directly from the authors or academic sources using open or valid licensed access.
- This license by no means overwrites the license of the models included in the repository, which maintain their original license.
- All catalog ontologies that are without explicit licensing information on their associated metadata.yaml file must be interpreted as being private and having a restrictive license.
- License holders sending their models to the OntoUML/UFO Catalog expressly agree that the sent content is going to be hosted and made available for other users in the terms of this license.
- Whoever uses the OntoUML/UFO Catalog expressly understands and agrees with its licensing information.

Ontologies are going to be immediately removed from the catalog in case of a request by the original license holders. For content removal, please [create an issue](https://github.com/OntoUML/ontouml-models/issues) or report it through the [catalog's contribution form](https://forms.gle/wNSMfaJfkS3hi69o7).
