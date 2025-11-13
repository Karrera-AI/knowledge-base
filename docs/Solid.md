# Solid

All user's information will be stored in a Solid POD. This structure will guarantee that the users's personal data are not stored in our servers and therefore prevent these information from being used without user's approval.

This data repository stores various aspects of an individual's professional and personal profile, career capital, and interactions, organized using a structured schema. The files are primarily .ttl (Turtle) files, which are a syntax for RDF (Resource Description Framework), indicating a graph-like data structure where relationships between entities are explicit.

## FOLDER STRUCTURE

The application data are stored using a folder struture as follows:

![image info](./assets/FolderStructure.jpg)

![image info](./assets/PodFolder.png)

## List of Files

These files are used to store specific information from each user and will be described further in this document:

* YYYY-MM-DDThhmmssZ.kar
* .version.ttl
* .artifacts-index.ttl
* .narrative-index.ttl
* .item-index.ttl
* .memory-working-index.ttl
* .memory-discarded-index.ttl
* .memory-longterm-index.ttl
* .persona-index.ttl
* .organization-index.ttl
* .person-index.ttl
* .project-index.ttl
* .CCIH-Definitions.ttl
* CCIH-history.ttl
* CCIH.ttl
* .WorkDNA-Definitions.ttl
* WorkDNA-history.ttl
* WorkDNA.ttl
* PAI.ttl
* MSG.ttl
* PI-history.ttl
* PI.ttl
* item.ttl
* organization.ttl
* person.ttl
* project.ttl

## Files Descriptions

### YYYY-MM-DDThhmmssZ.kar

**Description**

This is an encripted tar file that contains the whole **KarreraAi** folder content. It will be used as a source to restore user's data in case of file corruption and/or deletion.

**Workflow Diagram**

![image info](./assets/BackupFlow.jpg)

### .version.ttl

**File Location**

<User's POD>/KarreraAI/.system/

**Description**

This file is used to define the **KarreraAi Data Structure** version. It will be used to check version and decide whether to update the structure or reject the user login depending on the situation.

**File Structure**

```ttl title=".version.ttl" linenums="1"
@prefix : <#>.
@prefix dct: 	<http://purl.org/dc/terms/>.
@prefix xsd: 	<http://www.w3.org/2001/XMLSchema#>.
@prefix schem:	<https://schema.org/>.

:POD
    a schem:Dataset;
    dct:date "2025-04-24"^^xsd:date;
    dct:hasVersion "1.0";
    schem:description "Versão do POD do usuário".

:ONTOLOGY
    a schem:Dataset;
    dct:date "2025-04-24"^^xsd:date;
    dct:hasVersion "KOIN-v1.0";
    schem:description "Versão da Ontologia".
```

**Fields Description**

* **dcterms:date** - Last modified date (Format: YYYY-MM-DD)

* **dcterms:hasVersion** - Data structure version

* **schema:description** - File description

### .artifacts-index.ttl

**File Location**

<User's POD>/KarreraAI/artifacts/

**Description**

This file is used to store the list of artifacts uploaded to users's pod. This artifacts can be uploaded by the user itself or by the application backoffice agents. It includes some informations from each artifact that will be described later in this documet.

**File Structure**

```ttl title=".artifacts-index.ttl" linenums="1"
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX esco:    <http://data.europa.eu/esco/model#>
PREFIX schema:  <https://schema.org/>
PREFIX skos:    <http://www.w3.org/2004/02/skos/core#>
PREFIX xsd:     <http://www.w3.org/2001/XMLSchema#>

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/artifacts/.artifacts-index.ttl>
    a schema:ItemList;
    schema:itemListElement  [
                            a schema:DigitalDocument;
                            schema:encodingFormat     "application/pdf";
                            schema:datePublished      "YYYY-MM-YYThhmmssZ"^^xsd:dateTime;
                            schema:description        "File Description";
                            schema:genre              "Tipo do arquivo";
                            schema:name               "File Name";
                            schema:archivedAt         </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/artifacts/CV.pdf>;
                            schema:url                <File URL>;
                            schema:creativeWorkStatus "Processed";
                            schema:subjectOf    [
                                                a schema:Event;
                                                schema:name "Upload event"
                                                ]
                            ] .
```

**Fields Description**

* **schema:encodingFormat** - File encoding format
* **schema:datePublished** - Date and Time when the file was uploaded (Format: YYYY-MM-DDThhmmssZ) 
* **schema:description** - File description
* **schema:genre** - The genre of the file. It is used to define the category of the file. It can be one of the following options:
    * CV
    * Scrape
    * Personal Document
    * Project Document
* **schema:name** - Artifact name
* **schema:archivedAt** - Folder where the file is stored at users's POD
* **schema:url** - URL from where the file was downloaded
* **schema:creativeWorkStatus** - File processment status. It can be one of the following options:
    * Processed
    * Pending
* **schema:subjectOf**
    * **schema:name** - Name of the process that generated that file. It can be one of the following options:
        * Uploaded by user
        * Scrape from WEB
        * Upload during first login

### .narrative-index.ttl

**File Location**

<User's POD>/KarreraAI/narrative/

**Description**

This file stores a list o narratives for the user. Each narrative is a collection of memories. Each entry describes the nature of the narratives, its purpose, and the memory targets it contains.

**File Structure**

```ttl title=".narrative-index.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <https://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/.narrative-index.ttl>
        a schema:ItemList;
        schema:itemListElement  <#f8feeb3c-0a1f-4222-873e-e216a5978eb3> .    
        
<#f8feeb3c-0a1f-4222-873e-e216a5978eb3> 
    a schema:action ;
    schema:name         "Narrative name" ;
    schema:description  "Narrative description" ;
    schema:target       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/2025/04/.memory-working-index.ttl#4c5cc5d2-63fe-4554-a17f-b68403573f43> ,
                        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/2025/04/.memory-longterm-index.ttl#79a65b9a-7bd2-4605-ac8e-6a89d8ff720a> ,
                        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/2025/04/.memory-discarded-index.ttl#daaefefd-442c-44fb-a616-5a8a82ca505c> ;
    schema:endTime      "YYYY-MM-DDThhmmssZ"^^xsd:dateTime .
```

**Fields Description**

* **schema:name** - Narrative name
* **schema:description** - Description of the narrative and its purpose
* **schema:target** - References to memories included in this narrative
* **schema:endTime** - Timestamp indicating when the action was completed (Format: YYYY-MM-DDThhmmssZ)

### .item-index.ttl

**File Location**

<User's POD>/KarreraAI/narrative/item/

**Description**

This file stores a list o items of memories generated for the user. Each entry represents the results of a specific memory process extraction including its status, result location, and completion timestamp. These items are part of a memory that will be described in another topic.

**File Structure**

```ttl title=".item-index.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <https://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/.item-index.ttl>
    a schema:ItemList;
    schema:itemListElement  [ 
                            a schema:action ;
                            schema:endTime  "YYYY-MM-DDThhmmssZ"^^xsd:dateTime ;
                            schema:result   </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/11c741e6-3f7c-4919-9334-8d3118ae6bec.ttl> ;
                            schema:object   "The process that generate this item" ;
                            schema:status   "Item status"                                 
                            ] .
```

**Fields Description**

* **schema:endTime** - Timestamp indicating when the process was completed (Format: YYYY-MM-DDThhmmssZ)
* **schema:result** - Link to the resulting item generated by the process
* **schema:object** - Name of the process that generated this item. It can be one of the following:
    * CV Extraction
    * Scrape WEB
* **schema:status** - Item processment status. It can be one of the following options:
    * Working
    * Long-Term
    * Discarded

### .memory-working-index.ttl

**File Location**

<User's POD>/KarreraAI/narrative/memory/

**Description**

This file stores a list of working memories generated for the user. Each entry represents a specific working memory and its items. These memories will be waiting for users revision in order to be used or not. They are generated by AI extraction and scrapping agents.

**File Structure**

```ttl title=".memory-working-index.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <https://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/.memory-working-index.ttl>
    a schema:ItemList;
    schema:itemListElement  <#4c5cc5d2-63fe-4554-a17f-b68403573f43> .

<#4c5cc5d2-63fe-4554-a17f-b68403573f43>
    a schema:action ;
    schema:instrument   "CV Scrapping Agent" ;
    schema:target       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/artifacts/FileName> ,
                        "Text extracted from source data that was used to generate this memory" ;
    schema:endTime      "YYYY-MM-DDThhmmssZ"^^xsd:dateTime ;
    schema:result       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/11c741e6-3f7c-4919-9334-8d3118ae6bec.ttl> ,
                        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/591799bc-58b8-4e86-9291-316a181d813d.ttl> ;
    schema:object       "Object name" ;
    schema:status       "Memory Status" .
```

**Fields Description**

* **schema:instrument** - It is the agent that is generating the memory
* **schema:target** - This is a list of 2 information. The first information is the URL of the file used during the process. The second information source text, extracted from the document, that is used on the process
* **schema:endTime** - Timestamp indicating when the process was completed (Format: YYYY-MM-DDThhmmssZ)
* **schema:result** - List of items that were generated on this process
* **schema:status** - Status of this memory. It must be Working

### .memory-discarded-index.ttl

**File Location**

<User's POD>/KarreraAI/narrative/memory/YYYY/MM

**Description**

This file stores a list of discarded memories indicated by the user. Each entry represents a specific discarded memory and its items. These memories will be stored by month so each file contains the memories that were discarded in the month MM of year YYYY.

**File Structure**

```ttl title=".memory-discarded-index.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <https://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/YYYY/MM/.memory-discarded-index.ttl>
    a schema:ItemList;
    schema:itemListElement  <#4c5cc5d2-63fe-4554-a17f-b68403573f43> .

<#4c5cc5d2-63fe-4554-a17f-b68403573f43>
    a schema:action ;
    schema:instrument   "CV Scrapping Agent" ;
    schema:target       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/artifacts/FileName> ,
                        "Text extracted from source data that was used to generate this memory" ;
    schema:endTime      "YYYY-MM-DDThhmmssZ"^^xsd:dateTime ;
    schema:result       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/11c741e6-3f7c-4919-9334-8d3118ae6bec.ttl> ,
                        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/591799bc-58b8-4e86-9291-316a181d813d.ttl> ;
    schema:object       "Object name" ;
    schema:status       "Memory Status" .
```

**Fields Description**

* **schema:instrument** - It is the agent that is generating the memory
* **schema:target** - This is a list of 2 information. The first information is the URL of the file used during the process. The second information source text, extracted from the document, that is used on the process
* **schema:endTime** - Timestamp indicating when the process was completed (Format: YYYY-MM-DDThhmmssZ)
* **schema:result** - List of items that were generated on this process
* **schema:status** - Status of this memory. It must be Discarded

### .memory-longterm-index.ttl

**File Location**

<User's POD>/KarreraAI/narrative/memory/YYYY/MM

**Description**

This file stores a list of long-term memories accepted by the user. Each entry represents a specific accepted memory and its items. These memories will be stored by month so each file contains the memories that were accepted in the month MM of year YYYY.

**File Structure**

```ttl title=".memory-longterm-index.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <https://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/YYYY/MM/.memory-longterm-index.ttl>
    a schema:ItemList;
    schema:itemListElement  <#4c5cc5d2-63fe-4554-a17f-b68403573f43> .

<#4c5cc5d2-63fe-4554-a17f-b68403573f43>
    a schema:action ;
    schema:instrument   "CV Scrapping Agent" ;
    schema:target       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/artifacts/FileName> ,
                        "Text extracted from source data that was used to generate this memory" ;
    schema:endTime      "YYYY-MM-DDThhmmssZ"^^xsd:dateTime ;
    schema:result       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/11c741e6-3f7c-4919-9334-8d3118ae6bec.ttl> ,
                        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/591799bc-58b8-4e86-9291-316a181d813d.ttl> ;
    schema:object       "Object name" ;
    schema:status       "Memory Status" .
```

**Fields Description**

* **schema:instrument** - It is the agent that is generating the memory
* **schema:target** - This is a list of 2 information. The first information is the URL of the file used during the process. The second information source text, extracted from the document, that is used on the process
* **schema:endTime** - Timestamp indicating when the process was completed (Format: YYYY-MM-DDThhmmssZ)
* **schema:result** - List of items that were generated on this process
* **schema:status** - Status of this memory. It must be Long-term

### .persona-index.ttl

**File Location**

<User's POD>/KarreraAI/personas

**Description**

This file stores a list of personas created by the user. Each entry represents a specific persona and its description fields. 

**File Structure**

```ttl title=".persona-index.ttl" linenums="1"
PREFIX :       <https://storage.inrupt.com/a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/.persona-index.ttl#>
PREFIX schema: <https://schema.org/>
PREFIX xsd:    <http://www.w3.org/2001/XMLSchema#>

<https://storage.inrupt.com/a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/.persona-index.ttl>
    a schema:ItemList;
    schema:itemListElement  [ a schema:Person;
                                schema:dateCreated   "YYYY-MM-DD"^^xsd:date;
                                schema:dateModified  "YYYY-MM-DD"^^xsd:date;
                                schema:description   "User Description";
                                schema:folder        "POD/KarreraAI/personas/main/";
                                schema:image         <POD/KarreraAI/personas/main/avatar.jpg>;
                                schema:name          "User Name";
                                schema:position      "0";
                                schema:status        "active";
                                schema:title         "User Title";
                                schema:url           <https://id.inrupt.com/karrera51>
                            ] .
```

**Fields Description**

* **schema:dateCreated** - Timestamp indicating when the persona was created (Format: YYYY-MM-DD)
* **schema:dateModified** - Timestamp indicating when the persona was last modified (Format: YYYY-MM-DD)
* **schema:description** - Description defined by the user. This information can be modified editing the specific profile inside the application 
* **schema:folder** - Folder where the personas files are stored. The default persona, created by the application, should be stored in a folder named main. The remaining personas will be stored in folders with their specific names.
* **schema:image** - URL of the avatar uploaded by the user for that persona.
* **schema:name** - Name of the persona
* **schema:position** - The position number of the persona
* **schema:title** - Title of the persona defined by the user
* **schema:url** - User webid

### .organization-index.ttl

**File Location**

<User's POD>/KarreraAI/personas/main/

**Description**

This file stores a list of organizations where the user had some relationships. Each entry represents a url linking to a specific organization file. 

**File Structure**

```ttl title=".organization-index.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <https://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/.project-index.ttl> 
    a schema:ItemList;

    schema:itemListElement  </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/project/c160b433-0709-4bfa-92c6-30a3e9cc224e.ttl> ,
                            </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/Project/af443277-c582-4e41-98c5-9cbf5e570447.ttl> .
```

**Fields Description**

* **schema:itemListElement** - List of URLs of each organization

### .person-index.ttl

**File Location**

<User's POD>/KarreraAI/personas/main/

**Description**

This file stores a list of persons the user had some relationships. Each entry represents a url linking to a specific person file or webID. 

**File Structure**

```ttl title=".person-index.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <https://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/.person-index.ttl> 
    a schema:ItemList;

    schema:itemListElement  </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/project/c160b433-0709-4bfa-92c6-30a3e9cc224e.ttl> ,
                            </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/Project/af443277-c582-4e41-98c5-9cbf5e570447.ttl> .
```

**Fields Description**

* **schema:itemListElement** - List of URLs of each person. It can be a WebID in case the user is already registered.

### .project-index.ttl

**File Location**

<User's POD>/KarreraAI/personas/main/

**Description**

This file stores a list of project where the user had some participation. Each entry represents a url linking to a specific project file. 

**File Structure**

```ttl title=".project-index.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <http://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/.project-index.ttl> 
    a schema:ItemList;

    schema:itemListElement  </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/project/c160b433-0709-4bfa-92c6-30a3e9cc224e.ttl> ,
                            </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/Project/af443277-c582-4e41-98c5-9cbf5e570447.ttl> .
```

**Fields Description**

* **schema:itemListElement** - List of URLs of each project

### .CCIH-Definitions.ttl

**File Location**

<User's POD>/KarreraAI/.system

**Description**

This file stores the definitions of each (Career Capital & Impact Horizon) CCIH indicator. CCIH is a multi-dimensional, dynamic, and contextual framework for measuring **Professional Lifetime Value (PLV)**.

**File Structure**

```ttl title=".CCIH-Definitions.ttl" linenums="1"
@prefix dcterms: 	<http://purl.org/dc/terms/> .
@prefix esco:    	<http://data.europa.eu/esco/model#> .
@prefix schema:  	<http://schema.org/> .
@prefix skos:    	<http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/.system/.CCIH-Definitions.ttl>
    a schema:DefinedTermSet ;
	
	# CCIH - Career Capital & Impact Horizon
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:termCode "CCIH" ;
        schema:name "Career Capital & Impact Horizon (CCIH)" ;
        schema:bestRating "100" ;
		schema:description "A multi-dimensional, dynamic, and contextual framework for measuring Professional Lifetime Value (PLV)." ;

        # HCA - Human Capital Assets
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "HCA" ;
            schema:name "Human Capital Assets (HCA)" ;
            schema:description "The foundation of an individual's professional value, including skills and adaptability." ;
			schema:bestRating "100" ;
			schema:hasDefinedTerm <#AQ>, <#SMI>
			] ;
			
		# SRC - Social & Relational Capital
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "SRC" ;
            schema:name "Social & Relational Capital (SRC)" ;
            schema:description "Quantifies the value derived from an individual's professional network and collaborations." ;
			schema:bestRating "100" ;
			schema:hasDefinedTerm <#NDS>, <#IRI>
			] ;
			
		# IOV - Impact & Output Value
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "IOV" ;
            schema:name "Impact & Output Value (IOV)" ;
            schema:description "It measures the direct and demonstrable contributions an individual makes in their professional role." ;
			schema:bestRating "100" ;
			schema:hasDefinedTerm <#IAC>, <#SAR>
			] ;
			
		# GTMA - Growth Trajectory & Market Alignment
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "GTMA" ;
            schema:name "Growth Trajectory & Market Alignment (GTMA)" ;
            schema:description "It tracks trajectories rather than just snapshots, emphasizing future potential and benchmarking against peers while also tracking personal growth." ;
			schema:bestRating "100" ;
			schema:hasDefinedTerm <#BETA>, <#ORL>
			] ;
			
		# WS - Well-being & Sustainability
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "WS" ;
            schema:name "Well-being & Sustainability (WS)" ;
            schema:description "It acknowledges non-linear careers and ethical contributions as core principles of the CCIH Framework." ;
			schema:bestRating "100" ;
			schema:hasDefinedTerm <#SJFA>, <#GSI>
			] ;		
		
	] .
	# End of CCIH - Career Capital & Impact Horizon (CCIH)
	
<#AQ> # Adaptability Quotient
a schema:DefinedTerm ;
schema:termCode "AQ" ;
schema:name "Adaptability Quotient (AQ)" ;
schema:description "It serves as a measure of an individual's capacity for successful transitions across different professional domains" ;
schema:bestRating "100" .

<#SMI> # Skill Maturity Index
a schema:DefinedTerm ;
schema:termCode "SMI" ;
schema:name "Skill Maturity Index (SMI)" ;
schema:description "It is a metric designed to track the depth and breadth of an individual's skills against the WorkDNA taxonomy's" ;
schema:bestRating "100" .

<#NDS> # Network Diversity Score
a schema:DefinedTerm ;
schema:termCode "NDS" ;
schema:name "Network Diversity Score (NDS)" ;
schema:description "It is a metric designed to quantify the breadth of high-value connections an individual possesses." ;
schema:bestRating "100" .

<#IRI> # Influence Reach Index
a schema:DefinedTerm ;
schema:termCode "IRI" ;
schema:name "Influence Reach Index (IRI)" ;
schema:description "It is a metric that measures an individual's impact beyond their immediate projects." ;
schema:bestRating "100" .

<#IAC> #  Impact-Adjusted Contribution
a schema:DefinedTerm ;
schema:termCode "IAC" ;
schema:name " Impact-Adjusted Contribution (IAC)" ;
schema:description "is a metric to quantifying the tangible results an individual produces." ;
schema:bestRating "100" .

<#SAR> # Strategic Alignment Ratio
a schema:DefinedTerm ;
schema:termCode "SAR" ;
schema:name "Strategic Alignment Ratio (SAR)" ;
schema:description "It tracks an individual's work toward high-value goals." ;
schema:bestRating "100" .

<#BETA> # Career Beta (β) Tracker
a schema:DefinedTerm ;
schema:termCode "BETA" ;
schema:name "Career Beta (β) Tracker" ;
schema:description "It measures an individual's alignment with high-growth skills and industries." ;
schema:bestRating "100" .

<#ORL> # Opportunity Readiness Level
a schema:DefinedTerm ;
schema:termCode "ORL" ;
schema:name "Opportunity Readiness Level (ORL)" ;
schema:description "It is designed to predict an individual's success in aspirational roles." ;
schema:bestRating "100" .

<#SJFA> # Skill-Job Fit Alignment
a schema:DefinedTerm ;
schema:termCode "SJFA" ;
schema:name "Skill-Job Fit Alignment (SJFA)" ;
schema:description "It measures engagement through competency utilization." ;
schema:bestRating "100" .

<#GSI> # Growth Sustainability Index
a schema:DefinedTerm ;
schema:termCode "GSI" ;
schema:name "Growth Sustainability Index (GSI)" ;
schema:description "It is designed to balance an individual's pace of development with their well-being." ;
schema:bestRating "100" .
```

**Fields Description**

Each indicator is represented using the same data structure described below:

* **schema:termCode** - Acronym
* **schema:name** - Name
* **schema:description** - Description
* **schema:bestRating** - Highest value

### CCIH.ttl

**File Location**

<User's POD>/KarreraAI/personas/main

**Description**

This file stores the (Career Capital & Impact Horizon) CCIH 10 indicators for the main persona.

**File Structure**

```ttl title="CCIH.ttl" linenums="1"
@prefix dcterms:    <http://purl.org/dc/terms/> .
@prefix esco:       <http://data.europa.eu/esco/model#> .
@prefix schema:     <http://schema.org/> .
@prefix skos:       <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix ccih:       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/.system/CCIH-Definitions.ttl>

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/persona1/CCIH.ttl>
    a schema:DefinedTermSet ;

    # Adaptability Quotient (AQ)
    schema:hasDefinedTerm [
        a schema:DefinedTermSet ;
        schema:inDefinedTermSet <ccih:#AQ> ;
        schema:termCode "AQ" ;
        schema:ratingValue "10%" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;

    # Skill Maturity Index (SMI)
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <ccih:#SMI> ;
        schema:termCode "SMI" ;
        schema:ratingValue "0" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;
	
	# Network Diversity Score (NDS)
    schema:hasDefinedTerm [
        a schema:DefinedTermSet ;
        schema:inDefinedTermSet <ccih:#NDS> ;
        schema:termCode "NDS" ;
        schema:ratingValue "5%" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;

    # Influence Reach Index (IRI)
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <ccih:#IRI> ;
        schema:termCode "IRI" ;
        schema:ratingValue "0" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;
	
	# Impact-Adjusted Contribution (IAC)
    schema:hasDefinedTerm [
        a schema:DefinedTermSet ;
        schema:inDefinedTermSet <ccih:#IAC> ;
        schema:termCode "IAC" ;
        schema:ratingValue "0" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;

    # Strategic Alignment Ratio (SAR)
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <ccih:#SAR> ;
        schema:termCode "SAR" ;
        schema:ratingValue "0" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;
	
	# Career Beta (β) Tracker (BETA)
    schema:hasDefinedTerm [
        a schema:DefinedTermSet ;
        schema:inDefinedTermSet <ccih:#BETA> ;
        schema:termCode "BETA" ;
        schema:ratingValue "0" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;

    # Opportunity Readiness Level (ORL)
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <ccih:#ORL> ;
        schema:termCode "ORL" ;
        schema:ratingValue "0" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;
	
	# Skill-Job Fit Alignment (SJFA)
    schema:hasDefinedTerm [
        a schema:DefinedTermSet ;
        schema:inDefinedTermSet <ccih:#SJFA> ;
        schema:termCode "SJFA" ;
        schema:ratingValue "0" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] ;

    # Growth Sustainability Index (GSI)
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <ccih:#GSI> ;
        schema:termCode "GSI" ;
        schema:ratingValue "0" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime
    ] .
```

**Fields Description**

Each indicator is represented using the same data structure described below:

* **schema:inDefinedTermSet** - Link to the indicator definition in .CCIH-Definitions.ttl file
* **schema:termCode** - Acronym
* **schema:ratingValue** - indicator values
* **schema:subjectOf** - Link to the memory file that last changed the indicator
* **schema:validFrom** - Timestamp of the last change (Format: YYYY-MM-YYThhmmssZ)

### .WorkDNA-Definitions.ttl

**File Location**

<User's POD>/KarreraAI/.system

**Description**

This file stores the definitions and hierarchy structure of each **WorkDNA** attribute.

**File Structure**

```ttl title=".WorkDNA-Definitions.ttl" linenums="1"
@prefix dcterms: 	<http://purl.org/dc/terms/> .
@prefix esco:    	<http://data.europa.eu/esco/model#> .
@prefix schema:  	<http://schema.org/> .
@prefix skos:    	<http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/.system/.WorkDNA-Definitions.ttl>
    a schema:DefinedTermSet ;
	
	# K1 - Abilities (56)
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:termCode "K1" ;
        schema:name "Abilities" ;
        schema:description "Innate and developed aptitudes that facilitate the acquisition of knowledge and skills to carry out expected work." ;

        # K101 - Cognitive Abilities (21)
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "K101" ;
            schema:name "Cognitive Abilities" ;
            schema:description "Abilities that influence the acquisition and application of knowledge in performing various mental processes at work." ;

			# K101a - Idea Generation and Reasoning Abilities (06)
            schema:hasDefinedTerm [
                a schema:DefinedTerm ;
                schema:termCode "K101a" ;
                schema:name "Idea Generation and Reasoning Abilities" ;
                schema:description "" ;
				schema:hasDefinedTerm <#K101a01>, <#K101a02>, <#K101a03>, <#K101a04>, <#K101a05>, <#K101a06>
			] ;
			
			# K101b - Quantitative Abilities (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K101b" ;
				schema:name "Quantitative Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K101b01>, <#K101b02>		
			] ;
			
			# K101c - Memory Abilities (05)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K101c" ;
				schema:name "Memory Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K101c01>, <#K101c02>, <#K101c03>, <#K101c04>, <#K101c05>		
			] ;
			
			# K101d - Spacial Abilities (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K101d" ;
				schema:name "Spacial Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K101d01>, <#K101d02>, <#K101d03>, <#K101d04>, <#K101d05>			
			] ;
		
		    # K101e - Communication Abilities (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K101e" ;
				schema:name "Communication Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K101e01>, <#K101e02>, <#K101e03>			
			] ;

			# K101f - Other Cognitive Abilities (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K101f" ;
				schema:name "Other Cognitive Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K101f01>, <#K101f02>, <#K101f03>
			]

		] ;
		# End of K101 - Cognitive Abilities

		# K102 - Physical Abilities (10)
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "K102" ;
            schema:name "Physical Abilities" ;
            schema:description "Abilities to perform physical activities that require strength, endurance, flexibility, balance or coordination." ;
			
		    # K102a - Physical Strength Abilities (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K102a" ;
				schema:name "Physical Strength Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K102a01>, <#K102a02>, <#K102a03>, <#K102a04>			
			] ;

			# K102b - Flexibility, Balance, and Coordination (05)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K102b" ;
				schema:name "Flexibility, Balance, and Coordination" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K102b01>, <#K102b02>, <#K102b03>, <#K102b04>, <#K102b05>
			] ;

			# K102c - Endurance (01)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K102c" ;
				schema:name "Endurance" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K102c01>
			]
			
		] ;
		# End of K102 - Physical Abilities
		
		# K103 - Psychomotor Abilities (10)
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "K103" ;
            schema:name "Psychomotor Abilities" ;
            schema:description "Abilities needed to manipulate and control objects." ;

            # K103a - Fine Manipulative Abilities (03)
			schema:hasDefinedTerm [
                a schema:DefinedTerm ;
                schema:termCode "K103a" ;
                schema:name "Fine Manipulative Abilities" ;
                schema:description "" ;
				schema:hasDefinedTerm <#K103a01>, <#K103a02>, <#K103a03>
            ] ;

            # K103b - Control Movement Abilities (04)
			schema:hasDefinedTerm [
                a schema:DefinedTerm ;
                schema:termCode "K103b" ;
                schema:name "Control Movement Abilities" ;
                schema:description "" ;
				schema:hasDefinedTerm <#K103b01>, <#K103b02>, <#K103b03>, <#K103b04>
            ] ;

            # K103c - Reaction Time and Speed Abilities (03)
			schema:hasDefinedTerm [
                a schema:DefinedTerm ;
                schema:termCode "K103c" ;
                schema:name "Reaction Time and Speed Abilities" ;
                schema:description "" ;
				schema:hasDefinedTerm <#K103c01>, <#K103c02>, <#K103c03>
            ]
			
        ] ;
		# End of K103 - Psychomotor Abilities
		
		# K104 - Sensory Abilities (15)
		schema:hasDefinedTerm [
            a schema:DefinedTerm ;
            schema:termCode "K104" ;
            schema:name "Sensory Abilities" ;
            schema:description "Abilities needed to perform activities that require visual, auditory, tactile, olfactory or speech perception." ;
			
			# K104a - Auditory and Speech Abilities (05)
		    schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K104a" ;
				schema:name "Auditory and Speech Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K104a01>, <#K104a02>, <#K104a03>, <#K104a04>, <#K104a05>
			] ;

			# K104b - Visual Abilities (06)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K104b" ;
				schema:name "Visual Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K104b01>, <#K104b02>, <#K104b03>, <#K104b04>, <#K104b05>, <#K104b06>
			] ;

			# K104c - Other Sensory Abilities (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K104c" ;
				schema:name "Other Sensory Abilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K104c01>, <#K104c02>, <#K104c03>
			]
		
		]
		# End of K104 - Sensory Abilities
		
	] ;
	# End of K1 - Abilities
	
	# K2 - Personal Attributes (32)
	schema:hasDefinedTerm [
		a schema:DefinedTerm ;
		schema:termCode "K2" ;
		schema:name "Personal Attributes" ;
		schema:description "Personal characteristics that are innate and developed through the social context and personal experiences to which the individual is exposed. These qualities influence the way one is and does things and are considered valuable assets for work performance." ;

		# K201 - Social Traits (07)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K201" ;
			schema:name "Social Traits" ;
			schema:description "The personal characteristics related to the positive attitudes one has toward other people that most often lead to positive relationships." ;

			# K201a - Social Influence (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K201a" ;
				schema:name "Social Influence" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K201a01>, <#K201a02>
			] ;

			# K201b - Interpersonal Orientation (05)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K201b" ;
				schema:name "Interpersonal Orientation" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K201b01>, <#K201b02>, <#K201b03>, <#K201b04>, <#K201b05>
			]
			
		] ;
		# End of K201 - Social Traits

		# K202 - Self-Improvement (09)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K202" ;
			schema:name "Self-Improvement" ;
			schema:description "The personal characteristics related to the improvement of one's knowledge, status, or character by one's own efforts." ;
			
			# K202a - Adjustment (05)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K202a" ;
				schema:name "Adjustment" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K202a01>, <#K202a02>, <#K202a03>, <#K202a04>, <#K202a05>
			] ;

			# K202b - Self-Reflective Orientation (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K202b" ;
				schema:name "Self-Reflective Orientation" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K202b01>, <#K202b02>
			] ;

			# K202c - Learning Orientation (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K202c" ;
				schema:name "Learning Orientation" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K202c01>, <#K202c02>
			]
		
		] ;
		# End of K202 - Self-Improvement
		
		# K203 - Results-Based Attributes (07)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K203" ;
			schema:name "Results-Based Attributes" ;
			schema:description "The personal characteristics related to the drivers around bringing things to completion." ;

			# K203a - Action-Oriented (07)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K203a" ;
				schema:name "Action-Oriented" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K203a01>
			]
			
		] ;
		# End of K203 - Results-Based Attributes
		
		# K204 - Professional Conscientiousness (03)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K204" ;
			schema:name "Professional Conscientiousness" ;
			schema:description "The personal characteristics related to the drivers around fulfilling commitments." ;

			# K204a - Sense of Responsibility (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K204a" ;
				schema:name "Sense of Responsibility" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K204a01>, <#K204a02>, <#K204a03>
			]
			
		] ;
		# End of K204 - Professional Conscientiousness

		# K205 - Dynamic Thinking (06)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K205" ;
			schema:name "Dynamic Thinking" ;
			schema:description "The personal characteristics related to bubbling ideas and critical thinking." ;

			# K205a - Practical Thinking (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K205a" ;
				schema:name "Practical Thinking" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K205a01>, <#K205a02>, <#K205a03>
			] ;

			# K205b - Unconventional Thinking (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K205b" ;
				schema:name "Unconventional Thinking" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K205b01>, <#K205b02>, <#K205b03>
			]
			
		]
		# End of K205 - Dynamic Thinking
		
	] ;
	# End of K2 - Personal Attributes
		
	# K3 - Interests (06)
	schema:hasDefinedTerm [
		a schema:DefinedTerm ;
		schema:termCode "K3" ;
		schema:name "Interests" ;
		schema:description "Preferences for work environments and outcomes." ;

		# K301 - Holland Codes (06)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K301" ;
			schema:name "Holland Codes" ;
			schema:description "Holland codes, also referred to as RIASEC codes, refer to John L. Holland's six interest personality types. Each of them are characterized by the dominant activities, preferences and interests most often expected." ;

			# K301a - Interests - Holland Codes (06)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K301a" ;
				schema:name "Interests - Holland Codes" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K301a01>, <#K301a02>, <#K301a03>, <#K301a04>, <#K301a05>, <#K301a06>
			]
			
		]
		# End of K301 - Holland Codes
		
	] ;
	# End of K3 - Interests
		
	# K4 - Skills (43)
	schema:hasDefinedTerm [
		a schema:DefinedTerm ;
		schema:termCode "K4" ;
		schema:name "Skills" ;
		schema:description "Developed capabilities that an individual must have to be effective in a job, role, function, task or duty." ;

		# K401 - Foundational Skills (07)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K401" ;
			schema:name "Foundational Skills" ;
			schema:description "Developed capabilities that facilitate the more rapid acquisition of other skills and knowledge." ;

			# K401a - Verbal Skills (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K401a" ;
				schema:name "Verbal Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K401a01>, <#K401a02>, <#K401a03>
			] ;

			# K401b - Reading and Writing Skills (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K401b" ;
				schema:name "Reading and Writing Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K401b01>, <#K401b02>
			] ;

			# K401c - Mathematical Skills (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K401c" ;
				schema:name "Mathematical Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K401c01>, <#K401c02>
			]
			
		] ;
		# End of K401 - Foundational Skills	
			
		# K402 - Process Analysis Skills (08)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K402" ;
			schema:name "Analytical Skills" ;
			schema:description "Developed capability that people need to process information and data logically to produce useable results." ;

			# K402a - Process Analysis Skills (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K402a" ;
				schema:name "Process Analysis Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K402a01>, <#K402a02>, <#K402a03>
			] ;

			# K402b - Operations and Systems Analysis Skills (05)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K402b" ;
				schema:name "Operations and Systems Analysis Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K402b01>, <#K402b02>, <#K402b03>, <#K402b04>, <#K402b05>
			]
			
		] ;
		# End of K402 - Process Analysis Skills

		# K403 - Technical Skills (10)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K403" ;
			schema:name "Technical Skills" ;
			schema:description "Developed capabilities that relate to the practical or mechanical side of an activity, the application of a set of technical processes and required know-how." ;

			# K403a - Technical Skills (10)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K403a" ;
				schema:name "Technical Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K403a01>, <#K403a02>, <#K403a03>, <#K403a04>, <#K403a05>, <#K403a06>, <#K403a07>, <#K403a08>, <#K403a09>, <#K403a10>
			]
			
		] ;
		# End of K403 - Technical Skills

		# K404 - Resource Management Skills (11)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K404" ;
			schema:name "Resource Management Skills" ;
			schema:description "Developed capabilities to plan, organize, monitor or control the resources to achieve goals." ;

			# K404a - Resource Management Skills (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K404a" ;
				schema:name "Resource Management Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K404a01>, <#K404a02>, <#K404a03>
			] ;
			
			# K404b - Planning Skills (05)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K404b" ;
				schema:name "Planning Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K404b01>, <#K404b02>, <#K404b03>, <#K404b04>, <#K404b05>
			] ;

			# K404c - Monitoring (01)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K404c" ;
				schema:name "Monitoring" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K404c01>
			] ;
		
			# K404d - Change Management and Crisis Management Skills (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K404d" ;
				schema:name "Change Management and Crisis Management Skills" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K404d01>, <#K404d02>, <#K404d03>, <#K404d04>
			]

		] ;
		# End of K404 - Resource Management Skills
		
		# K405 - Interpersonal Skills (07)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K405" ;
			schema:name "Interpersonal Skills" ;
			schema:description "Developed capabilities used to work with people to achieve goals." ;
			
			# K405a - Interpersonal Skills (07)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K405a" ;
				schema:name "Interpersonal Skills" ;
				schema:description "Developed capabilities used to work with people to achieve goals." ;
				schema:hasDefinedTerm <#K405a01>, <#K405a02>, <#K405a03>, <#K405a04>, <#K405a05>, <#K405a06>, <#K405a07>
			]
		
		]
		# End of K405 - Interpersonal Skills
		
	] ;
	# End of K4 - Skills
		
	# K5 - Knowledge (46)
	schema:hasDefinedTerm [
		a schema:DefinedTerm ;
		schema:termCode "K5" ;
		schema:name "Knowledge" ;
		schema:description "Organized sets of principles and practices used for the execution of tasks and activities within a particular domain." ;

		# K501 - Administration and Management (07)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K501" ;
			schema:name "Administration and Management" ;
			schema:description "Organized set of principles and practices relating to administration and management domains." ;

			# K501a - Administration and Management (07)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K501a" ;
				schema:name "Administration and Management" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K501a01>, <#K501a02>, <#K501a03>, <#K501a04>, <#K501a05>, <#K501a06>, <#K501a07>
			]
			
		] ;
		# End of K501 - Administration and Management

		# K502 - Communication (01)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K502" ;
			schema:name "Communication" ;
			schema:description "Organized set of principles and practices relating to communication domains." ;

			# K502a - Communication (01)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K502a" ;
				schema:name "Communication" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K502a01>
			]
			
		] ;
		# End of K502 - Communication
		
		# K503 - Education (02)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K503" ;
			schema:name "Education" ;
			schema:description "Organized set of principles and practices relating to education domains." ;

			# K503a - Education (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K503a" ;
				schema:name "Education" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K503a01>, <#K503a02>
			]
		
		] ;
		# End of K503 - Education

		# K504 - Health and Wellbeing (06)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K504" ;
			schema:name "Health and Wellbeing" ;
			schema:description "Organized set of principles and practices relating to health and wellbeing domains." ;

			# K504a - Health and Wellbeing (06)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K504a" ;
				schema:name "Health and Wellbeing" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K504a01>, <#K504a02>, <#K504a03>, <#K504a04>, <#K504a05>, <#K504a06>
			]
			
		] ;
		# End of K504 - Health and Wellbeing

		# K505 - Law, Government and Safety (04)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K505" ;
			schema:name "Law, Government and Safety" ;
			schema:description "Organized set of principles and practices relating to law, government and safety." ;

			# K505a - Law, Government and Safety (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K505a" ;
				schema:name "Law, Government and Safety" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K505a01>, <#K505a02>, <#K505a03>, <#K505a04>
			]
			
		] ;
		# End of K505 - Law, Government and Safety
		
		# K506 - Logistics, Design and Evaluation (04)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K506" ;
			schema:name "Logistics, Design and Evaluation" ;
			schema:description "Organized set of principles and practices relating to logistics, design and evaluation domains." ;

			# K506a - Logistics, Design and Evaluation (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K506a" ;
				schema:name "Logistics, Design and Evaluation" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K506a01>, <#K506a02>, <#K506a03>, <#K506a04>
			]
			
		] ;
		# End of K506 - Logistics, Design and Evaluation

		# K507 - Natural Resources (05)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K507" ;
			schema:name "Natural Resources" ;
			schema:description "Organized set of principles and practices relating to natural resources domains." ;

			# K507a - Natural Resources (05)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K507a" ;
				schema:name "Natural Resources" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K507a01>, <#K507a02>, <#K507a03>, <#K507a04>, <#K507a05>
			]
			
		] ;
		# End of K507 - Natural Resources
		
		# K508 - Physical Sciences (04)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K508" ;
			schema:name "Physical Sciences" ;
			schema:description "Organized set of principles and practices relating to physical sciences domains." ;

			# K508a - Physical Sciences (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K508a" ;
				schema:name "Physical Sciences" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K508a01>, <#K508a02>, <#K508a03>, <#K508a05>
			]
			
		] ;
		# End of K508 - Physical Sciences

		# K509 - Socioeconomic Systems (05)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K509" ;
			schema:name "Socioeconomic Systems" ;
			schema:description "Organized set of principles and practices relating to socioeconomics domains." ;

			# K509a - Socioeconomic Systems (05)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K509a" ;
				schema:name "Socioeconomic Systems" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K509a01>, <#K509a02>, <#K509a03>, <#K509a04>, <#K509a05>
			]
			
		] ;

		# K510 - Technology, Electrical, Material and Mechanical (06)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K510" ;
			schema:name "Technology, Electrical, Material and Mechanical" ;
			schema:description "Organized set of principles and practices relating to technology, electrical, material and mechanical." ;

			# K510a - The Technology, Electrical, Material and Mechanical (06)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K510a" ;
				schema:name "The Technology, Electrical, Material and Mechanical" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K510a01>, <#K510a02>, <#K510a03>, <#K510a04>, <#K510a05>, <#K510a06>
			]
			
		] ;
		# End of K510 - Technology, Electrical, Material and Mechanical

		# K511 - Foundational Knowledge (02)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K511" ;
			schema:name "Foundational Knowledge" ;
			schema:description "Organized set of principles and practices that are fundamental to the acquisition of new knowledge." ;

			# K511a - Foundational Knowledge (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K511a" ;
				schema:name "Foundational Knowledge" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K511a01>, <#K511a02>
			]
			
		]
		# End of K511 - Foundational Knowledge
		
	] ;
	# End of K5 - Knowledge
	
	# K6 - Work Context (73)
	schema:hasDefinedTerm [
		a schema:DefinedTerm ;
		schema:termCode "K6" ;
		schema:name "Work Context" ;
		schema:description "Physical, environmental, and social factors that influence the nature of work." ;

		# K601 - Structural Job Characteristics (13)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K601" ;
			schema:name "Structural Job Characteristics" ;
			schema:description "The components that define the structural aspect of the job." ;

			# K601a - Criticality of Position (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K601a" ;
				schema:name "Criticality of Position" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K601a01>, <#K601a02>, <#K601a03>, <#K601a04>
			] ;
			
			# K601b - Various Challenge Types (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K601b" ;
				schema:name "Various Challenge Types" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K601b01>, <#K601b02>, <#K601b03>, <#K601b04>
			] ;

			# K601c - Pace and Scheduling (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K601c" ;
				schema:name "Pace and Scheduling" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K601c01>, <#K601c02>, <#K601c03>, <#K601c04>
			] ;
			
			# K601d - Level of Competition (01)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K601d" ;
				schema:name "Level of Competition" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K601d01>
			]

		] ;
		# End of K601 - Structural Job Characteristics

		# K602 - Physical Work Environment (25)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K602" ;
			schema:name "Physical Work Environment" ;
			schema:description "The physical surroundings in which the worker performs their job." ;

			# K602a - Exposure to Job Hazards (09)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K602a" ;
				schema:name "Exposure to Job Hazards" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K602a01>, <#K602a02>, <#K602a03>, <#K602a04>, <#K602a05>, <#K602a06>, <#K602a07>, <#K602a08>, <#K602a09>
			] ;

			# K602b - Work Setting (07)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K602b" ;
				schema:name "Work Setting" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K602b01>, <#K602b02>, <#K602b03>, <#K602b04>, <#K602b05>, <#K602b06>, <#K602b07>
			] ;

			# K602c - Environmental Conditions (07)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K602c" ;
				schema:name "Environmental Conditions" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K602c01>, <#K602c02>, <#K602c03>, <#K602c04>, <#K602c05>, <#K602c06>, <#K602c07>
			] ;

			# K602d - Safety Equipment Required (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K602d" ;
				schema:name "Safety Equipment Required" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K602d01>, <#K602d02>
			]
		
		] ;
		# End of K602 - Physical Work Environment
		
		# K603 - Physical Demands (20)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K603" ;
			schema:name "Physical Demands" ;
			schema:description "The physical activities the job requires the worker to do." ;

			# K603a - Body Positioning (14)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K603a" ;
				schema:name "Body Positioning" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K603a01>, <#K603a02>, <#K603a03>, <#K603a04>, <#K603a05>, <#K603a06>, <#K603a07>, <#K603a08>, <#K603a09>, <#K603a10>, <#K603a11>, <#K603a12>, <#K603a13>, <#K603a14>
			] ;
			
			# K603b - Body Exertion (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K603b" ;
				schema:name "Body Exertion" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K603b01>, <#K603b02>, <#K603b03>, <#K603b04>
			] ;

			# K603c - Speaking and Seeing (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K603c" ;
				schema:name "Speaking and Seeing" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K603c01>, <#K603c02>
			]
			
		] ;
		# End of K603 - Physical Demands
			
		# K604 - Interpersonal Relations (15)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K604" ;
			schema:name "Interpersonal Relations" ;
			schema:description "The human interactions required to perform the job." ;

			# K604a - Job interactions (07)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K604a" ;
				schema:name "Job interactions" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K604a01>, <#K604a02>, <#K604a03>, <#K604a04>, <#K604a05>, <#K604a06>, <#K604a07>
			] ;

			# K604b - Communication Methods (06)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K604b" ;
				schema:name "Communication Methods" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K604b01>, <#K604b02>, <#K604b03>, <#K604b04>, <#K604b05>, <#K604b06>
			] ;

			# K604c - Interpersonal Responsibilities (02)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K604c" ;
				schema:name "Interpersonal Responsibilities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K604c01>, <#K604c02>
			]
			
		]
		# End of K604 - Interpersonal Relations
		
	] ;
	# End of K6 - Work Context
		
	# K7 - General types of work-related activities. (56)
	schema:hasDefinedTerm [
		a schema:DefinedTerm ;
		schema:termCode "K7" ;
		schema:name "Work Activities" ;
		schema:description "General types of work-related activities." ;

		# K701 - Information-Oriented Activities (12)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K701" ;
			schema:name "Information-Oriented Activities" ;
			schema:description "Information and data management and processing activities that are necessary to meet the requirements of the job." ;

			# K701a - Looking for and Receiving Job-Related Information (08)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K701a" ;
				schema:name "Looking for and Receiving Job-Related Information" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K701a01>, <#K701a02>, <#K701a03>, <#K701a04>, <#K701a05>, <#K701a06>, <#K701a07>, <#K701a08>
			] ;

			# K701b - Identify and Evaluating Job-Relevant Information (04)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K701b" ;
				schema:name "Identify and Evaluating Job-Relevant Information" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K701b01>, <#K701b02>, <#K701b03>, <#K701b04>
			]

		] ;
		# End of K701 - Information-Oriented Activities

		# K702 - Physically-Oriented Activities (15)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K702" ;
			schema:name "Physically-Oriented Activities" ;
			schema:description "The physical activities that are performed, equipment and vehicles that are operated, or any other technical activities accomplished to meet the requirements of the job." ;

			# K702a - Performing Physical and Manual Work Activities (09)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K702a" ;
				schema:name "Performing Physical and Manual Work Activities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K702a01>, <#K702a02>, <#K702a03>, <#K702a04>, <#K702a05>, <#K702a06>, <#K702a07>, <#K702a08>, <#K702a09>
			] ;
			
			# K702b - Performing Complex and Technical Activities (06)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K702b" ;
				schema:name "Performing Complex and Technical Activities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K702b01>, <#K702b02>, <#K702b03>, <#K702b04>, <#K702b05>, <#K702b06>
			]
			
		] ;
		# End of K702 - Physically-Oriented Activities
			
		# K703 - Mental Process-Oriented Activities (11)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K703" ;
			schema:name "Mental Process-Oriented Activities" ;
			schema:description "The processing, planning, problem solving, and decision-making activities that are necessary for the overall completion of a job." ;

			# K703a - Information and Data Processing (03)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K703a" ;
				schema:name "Information and Data Processing" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K703a01>, <#K703a02>, <#K703a03>
			] ;
			
			# K703b - Reasoning and Decision Making (08)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K703b" ;
				schema:name "Reasoning and Decision Making" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K703b01>, <#K703b02>, <#K703b03>, <#K703b04>, <#K703b05>, <#K703b06>, <#K703b07>, <#K703b08>
			]
			
		] ;
		# End of K703 - Mental Process-Oriented Activities
		
		# K704 - People-Oriented Activities (18)
		schema:hasDefinedTerm [
			a schema:DefinedTerm ;
			schema:termCode "K704" ;
			schema:name "People-Oriented Activities" ;
			schema:description "The activities where social interaction with others is necessary to meet the requirements of the job." ;

			# K704a - Communicating and Interacting (11)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K704a" ;
				schema:name "Communicating and Interacting" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K704a01>, <#K704a02>, <#K704a03>, <#K704a04>, <#K704a05>, <#K704a06>, <#K704a07>, <#K704a08>, <#K704a09>, <#K704a11>, <#K704a12>
			] ;

			# K704b - Coordinating, Developing, Managing, and Advising (06)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K704b" ;
				schema:name "Coordinating, Developing, Managing, and Advising" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K704b01>, <#K704b02>, <#K704b03>, <#K704b04>, <#K704b05>, <#K704b06>
			] ;

			# K704c - Performing Administrative Activities (01)
			schema:hasDefinedTerm [
				a schema:DefinedTerm ;
				schema:termCode "K704c" ;
				schema:name "Performing Administrative Activities" ;
				schema:description "" ;
				schema:hasDefinedTerm <#K704c01>
			]
		
		]
		#End of K704 - People-Oriented Activities
		
	] .
	# End of K7 - General types of work-related activities.

<#K101a01> # Information Ordering
    a schema:DefinedTerm ;
    schema:termCode "K101a01" ;
    schema:name "Information Ordering" ;
    schema:description "The ability to arrange things or actions in a certain order or pattern according to a specific rule or set of rules (e.g., patterns of numbers, letters, words, pictures, mathematical operations)." ;
    schema:bestRating "5" .

<#K101a02> # Categorization Flexibility
    a schema:DefinedTerm ;
	schema:termCode "K101a02" ;
	schema:name "Categorization Flexibility" ;
	schema:description "The ability to generate or use different sets of rules for combining or grouping things in different ways." ;
	schema:bestRating "5" .

<#K101a03> # Deductive Reasoning
    a schema:DefinedTerm ;
	schema:termCode "K101a03" ;
	schema:name "Deductive Reasoning" ;
	schema:description "The ability to apply general rules to produce logical answers for specific problems." ;
	schema:bestRating "5" .

<#K101a04> # Inductive Reasoning
    a schema:DefinedTerm ;
	schema:termCode "K101a04" ;
	schema:name "Inductive Reasoning" ;
	schema:description "The ability to combine pieces of information to form general rules or conclusions, which includes finding a relationship among seemingly unrelated events." ;
	schema:bestRating "5" .

<#K101a05> # Fluency of Ideas
    a schema:DefinedTerm ;
	schema:termCode "K101a05" ;
	schema:name "Fluency of Ideas" ;
	schema:description "The ability to come up with multiple ideas about a topic." ;
	schema:bestRating "5" .

<#K101a06> # Problem Identification
    a schema:DefinedTerm ;
	schema:termCode "K101a06" ;
	schema:name "Problem Identification" ;
	schema:description "The ability to identify an existing or potential problem. It is not about solving the problem, but only about recognizing its presence." ;
	schema:bestRating "5" .

<#K101b01> # Numerical Ability
    a schema:DefinedTerm ;
	schema:termCode "K101b01" ;
	schema:name "Numerical Ability" ;
	schema:description "The ability to carry out arithmetical processes accurately such as addition, subtraction, multiplication or division." ;
	schema:bestRating "5" .

<#K101b02> # Mathematical Reasoning
    a schema:DefinedTerm ;
	schema:termCode "K101b02" ;
	schema:name "Mathematical Reasoning" ;
	schema:description "The ability to choose the right mathematical methods or formulas to solve a problem." ;
	schema:bestRating "5" .

<#K101c01> # Memorizing
    a schema:DefinedTerm ;
	schema:termCode "K101c01" ;
	schema:name "Memorizing" ;
	schema:description "The ability to remember information such as words, numbers, pictures, or procedures." ;
	schema:bestRating "5" .

<#K101c02> # Multitasking
    a schema:DefinedTerm ;
	schema:termCode "K101c02" ;
	schema:name "Multitasking" ;
	schema:description "The ability to shift back and forth between two or more activities or sources of information during the same time period (such as speech, sounds, touch, or other sources)." ;
	schema:bestRating "5" .

<#K101c03> # Pattern Identification
    a schema:DefinedTerm ;
	schema:termCode "K101c03" ;
	schema:name "Pattern Identification" ;
	schema:description "The ability to identify or detect a known pattern such as a figure, object, word, or sound that is hidden in other information or material." ;
	schema:bestRating "5" .

<#K101c04> # Pattern Organization Speed
    a schema:DefinedTerm ;
	schema:termCode "K101c04" ;
	schema:name "Pattern Organization Speed" ;
	schema:description "The ability to quickly combine and organize information into meaningful patterns." ;
	schema:bestRating "5" .

<#K101c05> # Perceptual Speed
    a schema:DefinedTerm ;
	schema:termCode "K101c05" ;
	schema:name "Perceptual Speed" ;
	schema:description "The ability to compare, quickly and accurately, similarities and differences among sets of letters, numbers, objects, pictures, or patterns. The things to be compared may be presented at the same time, one after the other, or with a remembered object." ;
	schema:bestRating "5" .

<#K101d01> # Spatial Orientation
    a schema:DefinedTerm ;
	schema:termCode "K101d01" ;
	schema:name "Spatial Orientation" ;
	schema:description "The ability to know your location in relation to the environment or know where objects are in relation to you." ;
	schema:bestRating "5" .

<#K101d02> # Spatial Visualization
    a schema:DefinedTerm ;
	schema:termCode "K101d02" ;
	schema:name "Spatial Visualization" ;
	schema:description "The ability to think visually about geometric forms, comprehend the two-dimensional representation of three-dimensional objects and recognize the relationships resulting from the movement of objects in space." ;
	schema:bestRating "5" .

<#K101e01> # Verbal Ability
    a schema:DefinedTerm ;
	schema:termCode "K101e01" ;
	schema:name "Verbal Ability" ;
	schema:description "The ability to understand the meaning, precise use, associated ideas, and relationships of spoken words; and to use them in the proper context when presenting information or ideas." ;
	schema:bestRating "5" .

<#K101e02> # Written Comprehension
    a schema:DefinedTerm ;
	schema:termCode "K101e02" ;
	schema:name "Written Comprehension" ;
	schema:description "The ability to read and understand information and ideas presented in written form." ;
	schema:bestRating "5" .

<#K101e03> # Written Expression
    a schema:DefinedTerm ;
	schema:termCode "K101e03" ;
	schema:name "Written Expression" ;
	schema:description "The ability to communicate information and ideas in writing and adapting the writing style to the audience so that they can understand." ;
	schema:bestRating "5" .

<#K101f01> # Selective Attention
    a schema:DefinedTerm ;
	schema:termCode "K101f01" ;
	schema:name "Selective Attention" ;
	schema:description "The ability to concentrate on a task over a period of time without being distracted." ;
	schema:bestRating "5" .

<#K101f02> # Form Perception
    a schema:DefinedTerm ;
	schema:termCode "K101f02" ;
	schema:name "Form Perception" ;
	schema:description "The ability to perceive pertinent detail in objects and graphic material; to make visual comparisons and discriminations and to see slight differences in shapes and shadings of figures and widths and lengths of lines." ;
	schema:bestRating "5" .

<#K101f03> # General Learning Ability
    a schema:DefinedTerm ;
	schema:termCode "K101f03" ;
	schema:name "General Learning Ability" ;
	schema:description "The ability to catch on or understand instructions and underlies principles to reason and make judgments." ;
	schema:bestRating "5" .

<#K102a01> # Trunk Strength
    a schema:DefinedTerm ;
	schema:termCode "K102a01" ;
	schema:name "Trunk Strength" ;
	schema:description "The ability to exert your abdominal and lower back muscles to support part of the body repeatedly or continuously over time without giving out or fatiguing." ;
	schema:bestRating "5" .

<#K102a02> # Static Strength
    a schema:DefinedTerm ;
	schema:termCode "K102a02" ;
	schema:name "Static Strength" ;
	schema:description "The ability to exert muscle force to lift, push, pull, carry, or transfer objects." ;
	schema:bestRating "5" .

<#K102a03> # Dynamic Strength
    a schema:DefinedTerm ;
	schema:termCode "K102a03" ;
	schema:name "Dynamic Strength" ;
	schema:description "The ability to exert muscle force repeatedly or continuously over time. This involves muscular endurance and resistance to muscle fatigue." ;
	schema:bestRating "5" .

<#K102a04> # Explosive Strength
    a schema:DefinedTerm ;
	schema:termCode "K102a04" ;
	schema:name "Explosive Strength" ;
	schema:description "The ability to exert short bursts of muscle force to propel oneself (as in jumping or sprinting), to throw an object, or to apply force with a tool." ;
	schema:bestRating "5" .

<#K102b01> # Multi-Limb Coordination
    a schema:DefinedTerm ;
	schema:termCode "K102b01" ;
	schema:name "Multi-Limb Coordination" ;
	schema:description "The ability to coordinate two or more limbs, such as two arms, two legs, or one leg and one arm, while sitting, standing, or lying down. It does not involve performing the activities while the whole body is in motion." ;
	schema:bestRating "5" .

<#K102b02> # Gross Body Coordination
    a schema:DefinedTerm ;
	schema:termCode "K102b02" ;
	schema:name "Gross Body Coordination" ;
	schema:description "The ability to coordinate the movement of your arms, legs, and torso together when the whole body is in motion." ;
	schema:bestRating "5" .

<#K102b03> # Gross Body Equilibrium
    a schema:DefinedTerm ;
	schema:termCode "K102b03" ;
	schema:name "Gross Body Equilibrium" ;
	schema:description "The ability to keep or regain your body balance or stay upright when in an unstable position." ;
	schema:bestRating "5" .

<#K102b04> # Body Flexibility
    a schema:DefinedTerm ;
	schema:termCode "K102b04" ;
	schema:name "Body Flexibility" ;
	schema:description "The ability to bend, stretch, twist, or reach with your body, arms, and/or legs." ;
	schema:bestRating "5" .

<#K102b05> # Dynamic Flexibility
    a schema:DefinedTerm ;
	schema:termCode "K102b05" ;
	schema:name "Dynamic Flexibility" ;
	schema:description "The ability to quickly and repeatedly bend, stretch, twist, or reach out with your body, arms, and/or legs." ;
	schema:bestRating "5" .

<#K102c01> # Stamina
    a schema:DefinedTerm ;
	schema:termCode "K102c01" ;
	schema:name "Stamina" ;
	schema:description "The ability to perform intense physical activities over long periods without becoming winded or out of breath." ;
	schema:bestRating "5" .

<#K103a01> # Arm-Hand Steadiness
    a schema:DefinedTerm ;
	schema:termCode "K103a01" ;
	schema:name "Arm-Hand Steadiness" ;
	schema:description "The ability to keep your hand and arm steady while moving or holding them in one position." ;
	schema:bestRating "5" .

<#K103a02> # Finger Dexterity
    a schema:DefinedTerm ;
	schema:termCode "K103a02" ;
	schema:name "Finger Dexterity" ;
	schema:description "The ability to make precisely coordinated movements of the fingers of one or both hands to grasp, manipulate, or assemble small objects." ;
	schema:bestRating "5" .

<#K103a03> # Manual Dexterity
    a schema:DefinedTerm ;
	schema:termCode "K103a03" ;
	schema:name "Manual Dexterity" ;
	schema:description "The ability to move your hand, your hand together with your arm, or your two hands to grasp, manipulate, or assemble objects or tools." ;
	schema:bestRating "5" .

<#K103b01> # Motor Coordination
    a schema:DefinedTerm ;
	schema:termCode "K103b01" ;
	schema:name "Motor Coordination" ;
	schema:description "The ability to coordinate eyes, hands and fingers accurately to respond with precise movements." ;
	schema:bestRating "5" .

<#K103b02> # Rate Control
    a schema:DefinedTerm ;
	schema:termCode "K103b02" ;
	schema:name "Rate Control" ;
	schema:description "The ability to time your movements or the movement of a piece of equipment in anticipation of changes in the speed and/or direction of a moving object." ;
	schema:bestRating "5" .

<#K103b03> # Control of Settings
    a schema:DefinedTerm ;
	schema:termCode "K103b03" ;
	schema:name "Control of Settings" ;
	schema:description "The ability to adjust the controls of a machine or a vehicle to exact positions." ;
	schema:bestRating "5" .

<#K103b04> # Multi-Signal Response
    a schema:DefinedTerm ;
	schema:termCode "K103b04" ;
	schema:name "Multi-Signal Response" ;
	schema:description "The ability to choose quickly between one or more movements with the hand, finger, or foot in response to the appearance of two or more different signals such as lights, sounds, or images." ;
	schema:bestRating "5" .

<#K103c01> # Reaction Time
    a schema:DefinedTerm ;
	schema:termCode "K103c01" ;
	schema:name "Reaction Time" ;
	schema:description "The ability to respond quickly with one or more limbs to a stimulus such as noise, light or image." ;
	schema:bestRating "5" .

<#K103c02> # Speed of Limb Movement
    a schema:DefinedTerm ;
	schema:termCode "K103c02" ;
	schema:name "Speed of Limb Movement" ;
	schema:description "The ability to quickly move the arms and legs." ;
	schema:bestRating "5" .

<#K103c03> # Finger-Hand-Wrist Motion
    a schema:DefinedTerm ;
	schema:termCode "K103c03" ;
	schema:name "Finger-Hand-Wrist Motion" ;
	schema:description "The ability to make fast, simple, and repeated movements of the fingers, hands, and wrists." ;
	schema:bestRating "5" .

<#K104a01> # Auditory Attention
    a schema:DefinedTerm ;
	schema:termCode "K104a01" ;
	schema:name "Auditory Attention" ;
	schema:description "The ability to give full attention on a single source of sound in the presence of other distracting sounds." ;
	schema:bestRating "5" .

<#K104a02> # Hearing Sensitivity
    a schema:DefinedTerm ;
	schema:termCode "K104a02" ;
	schema:name "Hearing Sensitivity" ;
	schema:description "The ability to detect or distinguish the differences between sounds in terms of pitch and volume." ;
	schema:bestRating "5" .

<#K104a03> # Speech Clarity
    a schema:DefinedTerm ;
	schema:termCode "K104a03" ;
	schema:name "Speech Clarity" ;
	schema:description "The ability to articulate and pronounce words clearly, so others can understand you when you speak." ;
	schema:bestRating "5" .

<#K104a04> # Speech Recognition
    a schema:DefinedTerm ;
	schema:termCode "K104a04" ;
	schema:name "Speech Recognition" ;
	schema:description "The ability to identify and understand the speech of another person." ;
	schema:bestRating "5" .

<#K104a05> # Sound Localization
    a schema:DefinedTerm ;
	schema:termCode "K104a05" ;
	schema:name "Sound Localization" ;
	schema:description "The ability to identify the direction, origin and distance from which a sound comes." ;
	schema:bestRating "5" .

<#K104b01> # Far Vision
    a schema:DefinedTerm ;
	schema:termCode "K104b01" ;
	schema:name "Far Vision" ;
	schema:description "The ability to see details of objects and people at a distance." ;
	schema:bestRating "5" .

<#K104b02> # Near Vision
    a schema:DefinedTerm ;
	schema:termCode "K104b02" ;
	schema:name "Near Vision" ;
	schema:description "The ability to see details at close range." ;
	schema:bestRating "5" .

<#K104b03> # Peripheral Vision
    a schema:DefinedTerm ;
	schema:termCode "K104b03" ;
	schema:name "Peripheral Vision" ;
	schema:description "The ability to see objects, people, or their movement in the peripheral field of vision when looking ahead." ;
	schema:bestRating "5" .

<#K104b04> # Depth Perception
    a schema:DefinedTerm ;
	schema:termCode "K104b04" ;
	schema:name "Depth Perception" ;
	schema:description "The ability to discern which of several objects is closer or farther away from you, or to estimate the distance between you and an object." ;
	schema:bestRating "5" .

<#K104b05> # Glare Tolerance
    a schema:DefinedTerm ;
	schema:termCode "K104b05" ;
	schema:name "Glare Tolerance" ;
	schema:description "The ability to see objects or people, in the presence of glare or bright lighting." ;
	schema:bestRating "5" .

<#K104b06> # Night Vision
    a schema:DefinedTerm ;
	schema:termCode "K104b06" ;
	schema:name "Night Vision" ;
	schema:description "The ability to see under low light conditions." ;
	schema:bestRating "5" .

<#K104c01> # Colour Perception
    a schema:DefinedTerm ;
	schema:termCode "K104c01" ;
	schema:name "Colour Perception" ;
	schema:description "The ability to match or detect differences or similarities between colours, including shades of colour and brightness." ;
	schema:bestRating "5" .

<#K104c02> # Smell
    a schema:DefinedTerm ;
	schema:termCode "K104c02" ;
	schema:name "Smell" ;
	schema:description "The ability to perceive odours through the nose." ;
	schema:bestRating "5" .

<#K104c03> # Taste
    a schema:DefinedTerm ;
	schema:termCode "K104c03" ;
	schema:name "Taste" ;
	schema:description "The ability to recognize or verify a particular flavor of a substance by tasting it." ;
	schema:bestRating "5" .

<#K104c04> # Touch 
    a schema:DefinedTerm ;
	schema:termCode "K104c04" ;
	schema:name "Touch" ;
	schema:description "The ability to acquire information about the environment through skin contact." ;
	schema:ratingValue "0" ;
	schema:bestRating "5" .

<#K201a01> # Leadership
    a schema:DefinedTerm ;
	schema:termCode "K201a01" ;
	schema:name "Leadership" ;
	schema:description "The quality of leading others towards a common goal by guiding, influencing, and inspiring them." ;
	schema:bestRating "5" .

<#K201a02> # Charisma
    a schema:DefinedTerm ;
	schema:termCode "K201a02" ;
	schema:name "Charisma" ;
	schema:description "The quality of possessing charm, attracting and arousing the interest, attention, or admiration of others through speeches, attitudes, temperament, or actions." ;
	schema:bestRating "5" .

<#K201b01> # Concern for Others
    a schema:DefinedTerm ;
	schema:termCode "K201b01" ;
	schema:name "Concern for Others" ;
	schema:description "The quality of having empathy towards others' feelings and needs and being understanding and helpful." ;
	schema:bestRating "5" .

<#K201b02> # Collaboration
    a schema:DefinedTerm ;
	schema:termCode "K201b02" ;
	schema:name "Collaboration" ;
	schema:description "The quality of contributing and working cooperatively while being supportive and inclusive of others to achieve a common goal." ;
	schema:bestRating "5" .

<#K201b03> # Service Orientation
    a schema:DefinedTerm ;
	schema:termCode "K201b03" ;
	schema:name "Service Orientation" ;
	schema:description "The quality of actively looking for ways to help, serve, or assist others." ;
	schema:bestRating "5" .

<#K201b04> # Trust in Others
    a schema:DefinedTerm ;
	schema:termCode "K201b04" ;
	schema:name "Trust in Others" ;
	schema:description "The quality of establishing and maintaining a relationship of trust with the people around you." ;
	schema:bestRating "5" .

<#K201b05> # Social Orientation
    a schema:DefinedTerm ;
	schema:termCode "K201b05" ;
	schema:name "Social Orientation" ;
	schema:description "The quality of seeking to work with others and relating to them on the job." ;
	schema:bestRating "5" .

<#K202a01> # Adaptability
    a schema:DefinedTerm ;
	schema:termCode "K202a01" ;
	schema:name "Adaptability" ;
	schema:description "The quality of adapting oneself to expected or unexpected changes and different situations while continuing to achieve past or renewed goals." ;
	schema:bestRating "5" .

<#K202a02> # Self-Control
    a schema:DefinedTerm ;
	schema:termCode "K202a02" ;
	schema:name "Self-Control" ;
	schema:description "The quality of maintaining composure, keeping emotions in check, controlling anger, and avoiding aggressive behaviour, even in very difficult situations." ;
	schema:bestRating "5" .

<#K202a03> # Stress Tolerance
    a schema:DefinedTerm ;
	schema:termCode "K202a03" ;
	schema:name "Stress Tolerance" ;
	schema:description "The quality of being able to remain calm, without being carried away by stress situations and to deal effectively with such situations." ;
	schema:bestRating "5" .

<#K202a04> # Tolerance of Ambiguity
    a schema:DefinedTerm ;
	schema:termCode "K202a04" ;
	schema:name "Tolerance of Ambiguity" ;
	schema:description "The quality of being able to function in an environment where there is uncertainty, unpredictability, conflicting directions or multiple demands and to approach these situations as challenges to improve." ;
	schema:bestRating "5" .

<#K202a05> # Resilience
    a schema:DefinedTerm ;
	schema:termCode "K202a05" ;
	schema:name "Resilience" ;
	schema:description "The quality of recovering from difficulties or changes, one has had to face, to bounce back and then move forward." ;
	schema:bestRating "5" .

<#K202b01> # Self-Awareness
    a schema:DefinedTerm ;
	schema:termCode "K202b01" ;
	schema:name "Self-Awareness" ;
	schema:description "The quality of being aware of own personality, character, and feelings including strengths, weaknesses, thoughts, behaviors, beliefs, motivation, and emotions." ;
	schema:bestRating "5" .

<#K202b02> # Self-Confidence
    a schema:DefinedTerm ;
	schema:termCode "K202b02" ;
	schema:name "Self-Confidence" ;
	schema:description "The quality of trust in ones ability to achieve goals, believing in ones potential and abilities, and knowing that one is capable of achieving goals when facing challenges." ;
	schema:bestRating "5" .

<#K202c01> # Active Learning
    a schema:DefinedTerm ;
	schema:termCode "K202c01" ;
	schema:name "Active Learning" ;
	schema:description "Pro-actively looking to understand the implications of new information in the current and changing workplace." ;
	schema:bestRating "5" .

<#K202c02> # Continuous Learning
    a schema:DefinedTerm ;
	schema:termCode "K202c02" ;
	schema:name "Continuous Learning" ;
	schema:description "Wanting to continuously develop and improve one's skills, abilities and knowledge in order to adapt to changes and work effectively." ;
	schema:bestRating "5" .

<#K203a01> # Achievement
    a schema:DefinedTerm ;
	schema:termCode "K203a01" ;
	schema:name "Achievement" ;
	schema:description "The quality of establishing and maintaining goals and exerting all effort to accomplish them successfully." ;
	schema:bestRating "5" .

<#K203a02> # Initiative
    a schema:DefinedTerm ;
	schema:termCode "K203a02" ;
	schema:name "Initiative" ;
	schema:description "The quality of taking on responsibilities and challenges, proposing, doing or organizing something by oneself without being prompted by others." ;
	schema:bestRating "5" .

<#K203a03> # Motivation
    a schema:DefinedTerm ;
	schema:termCode "K203a03" ;
	schema:name "Motivation" ;
	schema:description "The quality of being driven by interest, need, reason or reward to achieve something or to reach a set outcome." ;
	schema:bestRating "5" .

<#K203a04> # Perseverance
    a schema:DefinedTerm ;
	schema:termCode "K203a04" ;
	schema:name "Perseverance" ;
	schema:description "The quality of voluntarily and deliberately putting forth the effort required by a task or activity despite difficulties, failure or obstacles." ;
	schema:bestRating "5" .

<#K203a05> # Risk-Taking
    a schema:DefinedTerm ;
	schema:termCode "K203a05" ;
	schema:name "Risk-Taking" ;
	schema:description "The quality of being willing to make a risky choice, with regard for the consequences, in the hope of achieving a desired result or benefit in return." ;
	schema:bestRating "5" .

<#K203a06> # Competitiveness
    a schema:DefinedTerm ;
	schema:termCode "K203a06" ;
	schema:name "Competitiveness" ;
	schema:description "The quality of being driven by a deep desire to be as good as or better than others to perform well in a comparable context." ;
	schema:bestRating "5" .

<#K203a07> # Independence
    a schema:DefinedTerm ;
	schema:termCode "K203a07" ;
	schema:name "Independence" ;
	schema:description "The quality of developing one's own way of doing things, guiding oneself with little or no supervision, and depending on oneself to get things done." ;
	schema:bestRating "5" .

<#K204a01> # Reliable
    a schema:DefinedTerm ;
	schema:termCode "K204a01" ;
	schema:name "Reliable" ;
	schema:description "The quality of being dependable and respectful of commitments." ;
	schema:bestRating "5" .

<#K204a02> # Integrity
    a schema:DefinedTerm ;
	schema:termCode "K204a02" ;
	schema:name "Integrity" ;
	schema:description "The quality of being honest, ethical, and authentic." ;
	schema:bestRating "5" .

<#K204a03> # Being Responsible
    a schema:DefinedTerm ;
	schema:termCode "K204a03" ;
	schema:name "Being Responsible" ;
	schema:description "The quality of taking responsibility for ones own actions and the actions of a group." ;
	schema:bestRating "5" .

<#K205a01> # Having Judgement
    a schema:DefinedTerm ;
	schema:termCode "K205a01" ;
	schema:name "Having Judgement" ;
	schema:description "The quality of forming an opinion consistent with common sense based on an assessment of an event or fact." ;
	schema:bestRating "5" .

<#K205a02> # Analytical Thinking
    a schema:DefinedTerm ;
	schema:termCode "K205a02" ;
	schema:name "Analytical Thinking" ;
	schema:description "The quality of analyzing information and using logic to address issues and problems." ;
	schema:bestRating "5" .

<#K205a03> # Attention to Detail
    a schema:DefinedTerm ;
	schema:termCode "K205a03" ;
	schema:name "Attention to Detail" ;
	schema:description "The quality of being meticulous in the execution of tasks." ;
	schema:bestRating "5" .

<#K205b01> # Creativity
    a schema:DefinedTerm ;
	schema:termCode "K205b01" ;
	schema:name "Creativity" ;
	schema:description "The quality of coming up with unusual or clever ideas about a given topic or situation, or to develop original ways to solve a problem." ;
	schema:bestRating "5" .

<#K205b02> # Innovativeness
    a schema:DefinedTerm ;
	schema:termCode "K205b02" ;
	schema:name "Innovativeness" ;
	schema:description "The quality of alternative thinking to develop new products or services to make improvement or to develop a new approach." ;
	schema:bestRating "5" .

<#K205b03> # Entrepreneurial Spirit
    a schema:DefinedTerm ;
	schema:termCode "K205b03" ;
	schema:name "Entrepreneurial Spirit" ;
	schema:description "The quality of identifying and seizing opportunities and moving from idea to achievement." ;
	schema:bestRating "5" .

<#K301a01> # Realistic
    a schema:DefinedTerm ;
	schema:termCode "K301a01" ;
	schema:name "Realistic" ;
	schema:description "Realistic occupations are characterized by the dominance of activities that entail the explicit, ordered or systematic manipulation of objects, tools, machines and animals. Many of these occupations do not involve a lot of paperwork or working closely with others." ;
	schema:bestRating "5" .

<#K301a02> # Investigative
    a schema:DefinedTerm ;
	schema:termCode "K301a02" ;
	schema:name "Investigative" ;
	schema:description "Investigative occupations are characterized by the dominance of activities that entail the observation and systematic or creative investigation of physical, biological, or cultural phenomena. These occupations require an extensive amount of thinking and frequently involve working with ideas, searching for facts and figuring out problems mentally." ;
	schema:bestRating "5" .

<#K301a03> # Artistic
    a schema:DefinedTerm ;
	schema:termCode "K301a03" ;
	schema:name "Artistic" ;
	schema:description "Artistic occupations are characterized by the dominance of activities that entail artistic expression to create, compose or produce visual, performing, literary or applied art. These occupations frequently involve working with forms, designs and patterns and often require self-expression and the accomplishment of work without following a clear set of rules." ;
	schema:bestRating "5" .

<#K301a04> # Social
    a schema:DefinedTerm ;
	schema:termCode "K301a04" ;
	schema:name "Social" ;
	schema:description "Social occupations are characterized by the dominance of activities that entail the interaction with others to inform, train, aid, develop, cure, or enlighten. These occupations often involve helping or providing service to others, teaching, working or communicating with people." ;
	schema:bestRating "5" .

<#K301a05> # Enterprising
    a schema:DefinedTerm ;
	schema:termCode "K301a05" ;
	schema:name "Enterprising" ;
	schema:description "Enterprising occupations are characterized by the dominance of action-oriented activities to attain organizational or self-interest goals. They frequently involve starting up and carrying out projects, influencing, leading or mobilizing people, making decisions, and sometimes require risk taking and dealing with business." ;
	schema:bestRating "5" .

<#K301a06> # Conventional
    a schema:DefinedTerm ;
	schema:termCode "K301a06" ;
	schema:name "Conventional" ;
	schema:description "Conventional occupations are characterized by the dominance of activities that entail following sets of procedures and routines. These activities may include systematic manipulation of data, such as keeping records, filing materials, reproducing materials, organizing written and numerical data according to a prescribed plan, and operating business and data processing. They often require following a clear line of authority and usually involve working with data and details more than with ideas." ;
	schema:bestRating "5" .

<#K401a01> # Oral Communication: Active Listening
    a schema:DefinedTerm ;
	schema:termCode "K401a01" ;
	schema:name "Oral Communication: Active Listening" ;
	schema:description "The capability to give full attention to what other people are saying, take time to understand the points being made, ask questions as appropriate, and not interrupt at inappropriate times." ;
	schema:bestRating "5" .

<#K401a02> # Oral Communication: Oral Comprehension
    a schema:DefinedTerm ;
	schema:termCode "K401a02" ;
	schema:name "Oral Communication: Oral Comprehension" ;
	schema:description "The capability to listen to and understand information and ideas presented through spoken words and sentences." ;
	schema:bestRating "5" .

<#K401a03> # Oral Communication: Oral Expression
    a schema:DefinedTerm ;
	schema:termCode "K401a03" ;
	schema:name "Oral Communication: Oral Expression" ;
	schema:description "The capability to talk to others to convey information effectively." ;
	schema:bestRating "5" .

<#K401b01> # Reading Comprehension
    a schema:DefinedTerm ;
	schema:termCode "K401b01" ;
	schema:name "Reading Comprehension" ;
	schema:description "The capability to understand written information presented through words, sentences, paragraphs, symbols, and images in work-related documents." ;
	schema:bestRating "5" .

<#K401b02> # Writing
    a schema:DefinedTerm ;
	schema:termCode "K401b02" ;
	schema:name "Writing" ;
	schema:description "The capability to communicate in writing by using written words, sentences, paragraphs, symbols, and images and adapted for the needs of the audience." ;
	schema:bestRating "5" .

<#K401c01> # Numeracy
    a schema:DefinedTerm ;
	schema:termCode "K401c01" ;
	schema:name "Numeracy" ;
	schema:description "The capability to understand, use and report numbers and other mathematical information presented through words, numbers, symbols, and graphics." ;
	schema:bestRating "5" .

<#K401c02> # Digital Literacy
    a schema:DefinedTerm ;
	schema:termCode "K401c02" ;
	schema:name "Digital Literacy" ;
	schema:description "The capability to understand and use digital devices and tools to obtain, exchange, create or process digital information in a secure manner." ;
	schema:bestRating "5" .

<#K402a01> # Critical Thinking
    a schema:DefinedTerm ;
	schema:termCode "K402a01" ;
	schema:name "Critical Thinking" ;
	schema:description "The capability to use logic and reasoning to question, discern, interpret and analyze various types of information to form an evidence-based conclusion or judgment." ;
	schema:bestRating "5" .

<#K402a02> # Learning and Teaching Strategies
    a schema:DefinedTerm ;
	schema:termCode "K402a02" ;
	schema:name "Learning and Teaching Strategies" ;
	schema:description "The capability to select and use training/instructional methods and procedures appropriate for the situation when learning or teaching new things." ;
	schema:bestRating "5" .

<#K402a03> # Decision Making
    a schema:DefinedTerm ;
	schema:termCode "K402a03" ;
	schema:name "Decision Making" ;
	schema:description "The capability to analyze information among a set of alternatives, to evaluate potential outcomes and choose the most appropriate solution to achieve a predetermined objective." ;
	schema:bestRating "5" .

<#K402b01> # Evaluation
    a schema:DefinedTerm ;
	schema:termCode "K402b01" ;
	schema:name "Evaluation" ;
	schema:description "The capability to systematically assess products, services or processes using measurable indicators with the goal of ensuring or improving performance." ;
	schema:bestRating "5" .

<#K402b02> # Requirements Analysis
    a schema:DefinedTerm ;
	schema:termCode "K402b02" ;
	schema:name "Requirements Analysis" ;
	schema:description "The capability to analyze needs and product requirements to create a design." ;
	schema:bestRating "5" .

<#K402b03> # Systems Analysis
    a schema:DefinedTerm ;
	schema:termCode "K402b03" ;
	schema:name "Systems Analysis" ;
	schema:description "The capability to determine how a system should work and how changes in conditions, operations, and the environment will affect outcomes." ;
	schema:bestRating "5" .

<#K402b04> # Researching and Investigating
    a schema:DefinedTerm ;
	schema:termCode "K402b04" ;
	schema:name "Researching and Investigating" ;
	schema:description "The capability to conduct studies and to examine information and data to increase knowledge, understand facts, find causes, test hypotheses and draw conclusions or make recommendations." ;
	schema:bestRating "5" .

<#K402b05> # Problem Solving
    a schema:DefinedTerm ;
	schema:termCode "K402b05" ;
	schema:name "Problem Solving" ;
	schema:description "The capability to identify problems and review related information to develop solutions or feasible options to achieve the desired end state." ;
	schema:bestRating "5" .

<#K403a01> # Equipment and Tool Selection
    a schema:DefinedTerm ;
	schema:termCode "K403a01" ;
	schema:name "Equipment and Tool Selection" ;
	schema:description "The capability to choose between two or more types of tools, equipment or machinery to perform a job." ;
	schema:bestRating "5" .

<#K403a02> # Preventative Maintenance
    a schema:DefinedTerm ;
	schema:termCode "K403a02" ;
	schema:name "Preventative Maintenance" ;
	schema:description "The capability to perform maintenance on equipment, devices, buildings or machinery to keep them functional and to prevent damage or failures." ;
	schema:bestRating "5" .

<#K403a03> # Setting Up
    a schema:DefinedTerm ;
	schema:termCode "K403a03" ;
	schema:name "Setting Up" ;
	schema:description "The capability to set up, adjust, install and assemble equipment, machines, parts or to prepare them for their functioning and use." ;
	schema:bestRating "5" .

<#K403a04> # Operation and Control
    a schema:DefinedTerm ;
	schema:termCode "K403a04" ;
	schema:name "Operation and Control" ;
	schema:description "The capability to maneuver and control operations of equipment, machines, vehicles or systems." ;
	schema:bestRating "5" .

<#K403a05> # Operation Monitoring of Machinery and Equipment
    a schema:DefinedTerm ;
	schema:termCode "K403a05" ;
	schema:name "Operation Monitoring of Machinery and Equipment" ;
	schema:description "The capability to watch gauges, dials, digital displays or other indicators to ensure a machine or piece of equipment is working according to specifications." ;
	schema:bestRating "5" .

<#K403a06> # Troubleshooting
    a schema:DefinedTerm ;
	schema:termCode "K403a06" ;
	schema:name "Troubleshooting" ;
	schema:description "The capability to determine causes of operating errors in equipment, machinery, or technological systems and decide how to resolve the issues." ;
	schema:bestRating "5" .

<#K403a07> # Repairing
    a schema:DefinedTerm ;
	schema:termCode "K403a07" ;
	schema:name "Repairing" ;
	schema:description "The capability to replace, restore or adjust defective or deficient components in equipment, machines, and technical systems and test for function, appearance, operation and safety." ;
	schema:bestRating "5" .

<#K403a08> # Quality Control Testing
    a schema:DefinedTerm ;
	schema:termCode "K403a08" ;
	schema:name "Quality Control Testing" ;
	schema:description "The capability to conduct tests or inspections of prototypes, products, services, or processes to ensure their quality." ;
	schema:bestRating "5" .

<#K403a09> # Product Design
    a schema:DefinedTerm ;
	schema:termCode "K403a09" ;
	schema:name "Product Design" ;
	schema:description "The capacity to design and develop layouts for the construction of objects, equipment, machinery, structures, or engineering systems (excluding software and hardware)." ;
	schema:bestRating "5" .

<#K403a10> # Digital Production
    a schema:DefinedTerm ;
	schema:termCode "K403a10" ;
	schema:name "Digital Production" ;
	schema:description "The capacity to design, develop, adapt, or integrate hardware, software applications, electronic devices or digital technologies while adhering to cybersecurity standards." ;
	schema:bestRating "5" .

<#K404a01> # Management of Financial Resources
    a schema:DefinedTerm ;
	schema:termCode "K404a01" ;
	schema:name "Management of Financial Resources" ;
	schema:description "The capability to plan, organize, direct, control or monitor financial resources and activities and account for the use of these resources to ensure their utilization is conform to the objectives and purposes." ;
	schema:bestRating "5" .

<#K404a02> # Management of Material Resources
    a schema:DefinedTerm ;
	schema:termCode "K404a02" ;
	schema:name "Management of Material Resources" ;
	schema:description "The capability to plan and manage the purchase, inventory, warehousing, transportation, or distribution of products or materials and their use." ;
	schema:bestRating "5" .

<#K404a03> # Management of Personnel Resources
    a schema:DefinedTerm ;
	schema:termCode "K404a03" ;
	schema:name "Management of Personnel Resources" ;
	schema:description "The capability to recruit, train, motivate, develop and direct employees, identify the best person for the tasks to be performed and establish their work objectives in relation to the objectives of the organization." ;
	schema:bestRating "5" .

<#K404b01> # Operational Planning
    a schema:DefinedTerm ;
	schema:termCode "K404b01" ;
	schema:name "Operational Planning" ;
	schema:description "The capability to determine phases and steps, define activities and tasks, and establish schedules to complete objectives on time and within budget." ;
	schema:bestRating "5" .

<#K404b02> # Projecting Outcomes
    a schema:DefinedTerm ;
	schema:termCode "K404b02" ;
	schema:name "Projecting Outcomes" ;
	schema:description "The capability to estimate, predict and forecast results and outcomes of an action or a series of actions based on data and indicators." ;
	schema:bestRating "5" .

<#K404b03> # Risk Management
    a schema:DefinedTerm ;
	schema:termCode "K404b03" ;
	schema:name "Risk Management" ;
	schema:description "The capability to identify and assess risks and determine procedures to be followed to reduce or avoid their impact." ;
	schema:bestRating "5" .

<#K404b04> # Strategic Planning
    a schema:DefinedTerm ;
	schema:termCode "K404b04" ;
	schema:name "Strategic Planning" ;
	schema:description "The capability to set goals according to organizations needs, to develop strategies, and action plans to achieve." ;
	schema:bestRating "5" .

<#K404b05> # Time Management
    a schema:DefinedTerm ;
	schema:termCode "K404b05" ;
	schema:name "Time Management" ;
	schema:description "The capability to manage one's own time and the time of others." ;
	schema:bestRating "5" .

<#K404c01> # Monitoring
    a schema:DefinedTerm ;
	schema:termCode "K404c01" ;
	schema:name "Monitoring" ;
	schema:description "The capability to monitor and assess the performance of yourself, other individuals or the organization to make improvements or take corrective action." ;
	schema:bestRating "5" .

<#K404d01> # Change Management
    a schema:DefinedTerm ;
	schema:termCode "K404d01" ;
	schema:name "Change Management" ;
	schema:description "The capability to plan and implement strategies for effecting change, communicate the effects of change, and provide guidance and support to those affected by change." ;
	schema:bestRating "5" .

<#K404d02> # Crisis Management
    a schema:DefinedTerm ;
	schema:termCode "K404d02" ;
	schema:name "Crisis Management" ;
	schema:description "The capability to establish a response plan for emergencies, to apply it and adapt it to situations while limiting the impact on people, customers, employees and the organisation." ;
	schema:bestRating "5" .

<#K405a01> # Coordinating
    a schema:DefinedTerm ;
	schema:termCode "K405a01" ;
	schema:name "Coordinating" ;
	schema:description "The capability to organize people or groups by adjusting activities in relation to others' activities so that they work effectively as a whole." ;
	schema:bestRating "5" .

<#K405a02> # Instructing
    a schema:DefinedTerm ;
	schema:termCode "K405a02" ;
	schema:name "Instructing" ;
	schema:description "The capability to teach others knowledge, or how to do something." ;
	schema:bestRating "5" .

<#K405a03> # Negotiating
    a schema:DefinedTerm ;
	schema:termCode "K405a03" ;
	schema:name "Negotiating" ;
	schema:description "The capability to participate in, or facilitate communication between parties, in order to resolve differences, and reach a mutually acceptable or viable agreement." ;
	schema:bestRating "5" .

<#K405a04> # Persuading
    a schema:DefinedTerm ;
	schema:termCode "K405a04" ;
	schema:name "Persuading" ;
	schema:description "The capability to convince others to change their minds, beliefs, intentions or behaviours." ;
	schema:bestRating "5" .

<#K405a05> # Social Perceptiveness
    a schema:DefinedTerm ;
	schema:termCode "K405a05" ;
	schema:name "Social Perceptiveness" ;
	schema:description "The capability to be aware of others' reactions, unspoken communication, body language cues and feelings and discern the reasons behind their behaviours." ;
	schema:bestRating "5" .

<#K405a06> # Cross-Cultural Sensitivity
    a schema:DefinedTerm ;
	schema:termCode "K405a06" ;
	schema:name "Cross-Cultural Sensitivity" ;
	schema:description "The capability to communicate, interact and work appropriately with people from different cultural backgrounds, in recognition that diversity is being both between and within cultural groups and can be expressed in customs, values, and ways of thinking and acting." ;
	schema:bestRating "5" .

<#K405a07> # Managing Conversation
    a schema:DefinedTerm ;
	schema:termCode "K405a07" ;
	schema:name "Managing Conversation" ;
	schema:description "The capability to lead and facilitate dialogue between two or more people." ;
	schema:bestRating "5" .

<#K501a01> # Accounting
    a schema:DefinedTerm ;
	schema:termCode "K501a01" ;
	schema:name "Accounting" ;
	schema:description "Knowledge of concepts, principles, methods and practices for budgeting, storing, tracking, controlling, analyzing, and reporting on financial transactions." ;
	schema:bestRating "5" .

<#K501a02> # Business Management
    a schema:DefinedTerm ;
	schema:termCode "K501a02" ;
	schema:name "Business Management" ;
	schema:description "Knowledge of concepts, principles and practices of managing business operations such as strategic planning, resource allocation, production management, and coordination of people and activities." ;
	schema:bestRating "5" .

<#K501a03> # Clerical
    a schema:DefinedTerm ;
	schema:termCode "K501a03" ;
	schema:name "Clerical" ;
	schema:description "Knowledge of administrative concepts, principles, methods, procedures and practices for the functioning of the daily office operations." ;
	schema:bestRating "5" .

<#K501a04> # Finance
    a schema:DefinedTerm ;
	schema:termCode "K501a04" ;
	schema:name "Finance" ;
	schema:description "Knowledge of concepts, principles, methods and practices related to financial operations, systems and institutions." ;
	schema:bestRating "5" .

<#K501a05> # Human Resources and Labour relations
    a schema:DefinedTerm ;
	schema:termCode "K501a05" ;
	schema:name "Human Resources and Labour relations" ;
	schema:description "Knowledge of concepts, principles, procedures and practices for personnel recruitment, selection, hiring, training, deploying, compensation and benefits, labour relations and negotiation, and personnel information systems." ;
	schema:bestRating "5" .

<#K501a06> # Sale and Marketing
    a schema:DefinedTerm ;
	schema:termCode "K501a06" ;
	schema:name "Sale and Marketing" ;
	schema:description "Knowledge of concepts, principles, techniques, practices and tools for determining consumer behaviour and needs, developing business opportunities and promoting and selling products and services." ;
	schema:bestRating "5" .

<#K501a07> # Client Service
    a schema:DefinedTerm ;
	schema:termCode "K501a07" ;
	schema:name "Client Service" ;
	schema:description "Knowledge of concepts, principles, and practices of providing services and support to satisfy clients' requirements and needs." ;
	schema:bestRating "5" .

<#K502a01> # Communications and Media
    a schema:DefinedTerm ;
	schema:termCode "K502a01" ;
	schema:name "Communications and Media" ;
	schema:description "Knowledge of concepts, principles, methods and techniques of creation, production, distribution or dissemination of written, oral, audiovisual or visual communications." ;
	schema:bestRating "5" .

<#K503a01> # Teaching
    a schema:DefinedTerm ;
	schema:termCode "K503a01" ;
	schema:name "Teaching" ;
	schema:description "Knowledge of the concepts, principles, methods and practices of instructing individuals and groups, designing educational curriculum and measuring learning outcome." ;
	schema:bestRating "5" .

<#K503a02> # Training, Mentoring and Coaching
    a schema:DefinedTerm ;
	schema:termCode "K503a02" ;
	schema:name "Training, Mentoring and Coaching" ;
	schema:description "Knowledge of concepts and principles of learning and readiness to learn, and of methods for guiding, advising, directing and supporting career or personal goals for the individuals or groups to gain experience and improve competencies." ;
	schema:bestRating "5" .

<#K504a01> # Hospitality
    a schema:DefinedTerm ;
	schema:termCode "K504a01" ;
	schema:name "Hospitality" ;
	schema:description "Knowledge of concepts, principles, techniques and tools or equipment for managing facilities and providing food, accommodation or tourism services with the focus on client experience." ;
	schema:bestRating "5" .

<#K504a02> # Mental Health
    a schema:DefinedTerm ;
	schema:termCode "K504a02" ;
	schema:name "Mental Health" ;
	schema:description "Knowledge of concepts, principles, methods, and procedures for assessment, diagnosis, treatment, rehabilitation, counseling or guidance to address neurological and cognitive processes, behaviours, and disorders or to maintain balanced mental health and well-being." ;
	schema:bestRating "5" .

<#K504a03> # Personal Services
    a schema:DefinedTerm ;
	schema:termCode "K504a03" ;
	schema:name "Personal Services" ;
	schema:description "Knowledge of concepts, principles, techniques and tools for providing services of personal nature related to body care, childcare and other in-home services." ;
	schema:bestRating "5" .

<#K504a04> # Physical Health
    a schema:DefinedTerm ;
	schema:termCode "K504a04" ;
	schema:name "Physical Health" ;
	schema:description "Knowledge of concepts and principles of the human anatomy, organic systems, biomedical sciences, genetics, and of procedures, techniques and tools needed to diagnose and treat injuries and diseases, to restore and maintain physical health by the prevention and treatment." ;
	schema:bestRating "5" .

<#K504a05> # Recreation, Leisure and Fitness
    a schema:DefinedTerm ;
	schema:termCode "K504a05" ;
	schema:name "Recreation, Leisure and Fitness" ;
	schema:description "Knowledge of concepts, principles, practices, and equipment for physical fitness and for managing and providing recreational, leisure and fitness programs or services." ;
	schema:bestRating "5" .

<#K504a06> # Veterinarian and Animal Care
    a schema:DefinedTerm ;
	schema:termCode "K504a06" ;
	schema:name "Veterinarian and Animal Care" ;
	schema:description "Knowledge of concepts, principles, practices, techniques and tools for the prevention, care, diagnostics, and treatment of diseases, disorders and injuries, and the maintenance of wellbeing of animals." ;
	schema:bestRating "5" .

<#K505a01> # Military
    a schema:DefinedTerm ;
	schema:termCode "K505a01" ;
	schema:name "Military" ;
	schema:description "Knowledge of organisations, structures, practices and strategies related to defence, security, intelligence and peacekeeping missions." ;
	schema:bestRating "5" .

<#K505a02> # Law
    a schema:DefinedTerm ;
	schema:termCode "K505a02" ;
	schema:name "Law" ;
	schema:description "Knowledge of concepts, principles, functioning and processes of the provincial-territorial, federal or international legal systems for the establishment, implementation and application of laws, legal codes and documents, and court procedures." ;
	schema:bestRating "5" .

<#K505a03> # Public Affairs and Government Relations
    a schema:DefinedTerm ;
	schema:termCode "K505a03" ;
	schema:name "Public Affairs and Government Relations" ;
	schema:description "Knowledge of concepts, principles, processes, and functioning of governments and political systems for the establishment and implementation of policies, rules, regulations, and executive orders." ;
	schema:bestRating "5" .

<#K505a04> # Public Safety and Security
    a schema:DefinedTerm ;
	schema:termCode "K505a04" ;
	schema:name "Public Safety and Security" ;
	schema:description "Knowledge of concepts, principles, regulations, procedures and practices of public safety and security operations and systems for the protection of people, data and properties." ;
	schema:bestRating "5" .

<#K506a01> # Manufacturing, Processing and Production
    a schema:DefinedTerm ;
	schema:termCode "K506a01" ;
	schema:name "Manufacturing, Processing and Production" ;
	schema:description "Knowledge of concepts, principles, methods and techniques of production and transformation, including manual and mechanical processes." ;
	schema:bestRating "5" .

<#K506a02> # Logistics
    a schema:DefinedTerm ;
	schema:termCode "K506a02" ;
	schema:name "Logistics" ;
	schema:description "Knowledge of concepts, principles, infrastructures and processes for planning, organizing and coordinating the transportation of people and animals or for the acquisition, transportation, and storage of goods and resources." ;
	schema:bestRating "5" .

<#K506a03> # Performance Measurement
    a schema:DefinedTerm ;
	schema:termCode "K506a03" ;
	schema:name "Performance Measurement" ;
	schema:description "Knowledge of concepts, principles, methods, practices and strategies of monitoring the development, delivery and quality of products, programs or services." ;
	schema:bestRating "5" .

<#K506a04> # Technical Design
    a schema:DefinedTerm ;
	schema:termCode "K506a04" ;
	schema:name "Technical Design" ;
	schema:description "Knowledge of technical design concepts, principles, methods, techniques, and tools involved in the creation and production of technical plans, blueprints, drawings or models." ;
	schema:bestRating "5" .

<#K507a01> # Agriculture and Horticulture
    a schema:DefinedTerm ;
	schema:termCode "K507a01" ;
	schema:name "Agriculture and Horticulture" ;
	schema:description "Knowledge of concepts, principles, techniques, materials, and equipment for planting, growing, harvesting, storing or preserving plants and plant-sourced food products." ;
	schema:bestRating "5" .

<#K507a02> # Forestry
    a schema:DefinedTerm ;
	schema:termCode "K507a02" ;
	schema:name "Forestry" ;
	schema:description "Knowledge of concepts, principles, techniques, materials, and equipment for sourcing, processing, and managing harvested forestry resources, and monitoring and preserving sustainable forestry resources." ;
	schema:bestRating "5" .

<#K507a03> # Geological Resources
    a schema:DefinedTerm ;
	schema:termCode "K507a03" ;
	schema:name "Geological Resources" ;
	schema:description "Knowledge of concepts, principles, techniques, materials, and equipment for sourcing, processing, managing, monitoring or preserving mineral and metals resources." ;
	schema:bestRating "5" .

<#K507a04> # Livestock, Farm Animals & Wildlife
    a schema:DefinedTerm ;
	schema:termCode "K507a04" ;
	schema:name "Livestock, Farm Animals & Wildlife" ;
	schema:description "Knowledge of concepts, principles, techniques, materials, and equipment for sourcing, raising, fishing, hunting, managing, monitoring, or preserving stored sustainable animal resources and wildlife conservation." ;
	schema:bestRating "5" .

<#K507a05> # Water Resources
    a schema:DefinedTerm ;
	schema:termCode "K507a05" ;
	schema:name "Water Resources" ;
	schema:description "Knowledge of concepts, principles, techniques, materials, and equipment for sourcing, processing, managing, monitoring or preserving water resources such as rivers, lakes, oceans, and underground aquifers." ;
	schema:bestRating "5" .

<#K508a01> # Biology
    a schema:DefinedTerm ;
	schema:termCode "K508a01" ;
	schema:name "Biology" ;
	schema:description "Knowledge of concepts and principles of living organisms including their structure, function, growth, origin, evolution, distribution and classification and their interdependencies and interactions with each other and the environment, as well as safe and ethical handling methods and techniques." ;
	schema:bestRating "5" .

<#K508a02> # Chemistry
    a schema:DefinedTerm ;
	schema:termCode "K508a02" ;
	schema:name "Chemistry" ;
	schema:description "Knowledge of the composition, structure, and properties of chemical substances including their interactions, transformations and use, as well as the production techniques, risk factors, and disposal methods." ;
	schema:bestRating "5" .

<#K508a03> # Geoscience
    a schema:DefinedTerm ;
	schema:termCode "K508a03" ;
	schema:name "Geoscience" ;
	schema:description "Knowledge of concepts, principles, methods, and techniques for understanding material quality, physical characteristics, composition, structure, and natural systems, and the evolution of earth, ocean, and atmosphere phenomena." ;
	schema:bestRating "5" .

<#K508a05> # Physics
    a schema:DefinedTerm ;
	schema:termCode "K508a05" ;
	schema:name "Physics" ;
	schema:description "Knowledge of concepts, principles, fundamental properties, and laws that govern space, time, energy and matter and of equipment and methods required to study and apply the interactions of objects including atoms, particles and celestial bodies." ;
	schema:bestRating "5" .

<#K509a01> # Arts
    a schema:DefinedTerm ;
	schema:termCode "K509a01" ;
	schema:name "Arts" ;
	schema:description "Knowledge of concepts, principles and techniques of artistic expression required to create, compose or produce visual, applied, performing or literary art." ;
	schema:bestRating "5" .

<#K509a02> # Economics
    a schema:DefinedTerm ;
	schema:termCode "K509a02" ;
	schema:name "Economics" ;
	schema:description "Knowledge of concepts and principles of the production, distribution, and consumption of goods and services and the methods of analysis including simulation and forecasting techniques." ;
	schema:bestRating "5" .

<#K509a03> # Humanities
    a schema:DefinedTerm ;
	schema:termCode "K509a03" ;
	schema:name "Humanities" ;
	schema:description "Knowledge of concepts, principles, methods for understanding human social interaction and structures, and events throughout time and their effects on civilizations, cultures and environment." ;
	schema:bestRating "5" .

<#K509a04> # Library, Conservation, and Heritage
    a schema:DefinedTerm ;
	schema:termCode "K509a04" ;
	schema:name "Library, Conservation, and Heritage" ;
	schema:description "Knowledge of concepts, principles, techniques, and tools in the classification, storage, retrieval, display and management of documentation and records in various media, museum artifacts or works of fine art." ;
	schema:bestRating "5" .

<#K509a05> # Theology and Philosophy
    a schema:DefinedTerm ;
	schema:termCode "K509a05" ;
	schema:name "Theology and Philosophy" ;
	schema:description "Knowledge of concepts and principles of religious and philosophical systems, and of fundamental questioning of existence, reason, values, ethics, ways of thinking, customs, practices and their impact on individuals, human culture and society." ;
	schema:bestRating "5" .

<#K510a01> # Building and Construction
    a schema:DefinedTerm ;
	schema:termCode "K510a01" ;
	schema:name "Building and Construction" ;
	schema:description "Knowledge of concepts, principles, methods, materials and tools involved in the construction, maintenance and repair of houses, buildings, or infrastructures such as highways and roads." ;
	schema:bestRating "5" .

<#K510a02> # Computer, Technology and Information Systems
    a schema:DefinedTerm ;
	schema:termCode "K510a02" ;
	schema:name "Computer, Technology and Information Systems" ;
	schema:description "Knowledge of concepts, principles, processes, techniques, and tools for technological and digital systems, devices and products, such as hardware or software development, assembling, programming, use, troubleshooting or maintenance." ;
	schema:bestRating "5" .

<#K510a03> # Electrical and Electronics
    a schema:DefinedTerm ;
	schema:termCode "K510a03" ;
	schema:name "Electrical and Electronics" ;
	schema:description "Knowledge of concepts, principles, techniques, and tools applied for the development, use, repair and maintenance of electronic and electrical products and devices." ;
	schema:bestRating "5" .

<#K510a04> # Mechanics and Machinery
    a schema:DefinedTerm ;
	schema:termCode "K510a04" ;
	schema:name "Mechanics and Machinery" ;
	schema:description "Knowledge of parts, standards, and functioning of machines, vehicles, equipment or tools, and techniques used for their repair or maintenance." ;
	schema:bestRating "5" .

<#K510a05> # Telecommunications
    a schema:DefinedTerm ;
	schema:termCode "K510a05" ;
	schema:name "Telecommunications" ;
	schema:description "Knowledge of concepts, principles, processes, techniques and tools of the transmission of information via wire, radio, optical fiber or other electromagnetic system for the use, repair, maintenance, control, or operation of telecommunications systems." ;
	schema:bestRating "5" .

<#K510a06> # Vehicle, Machinery and Equipment Operations
    a schema:DefinedTerm ;
	schema:termCode "K510a06" ;
	schema:name "Vehicle, Machinery and Equipment Operations" ;
	schema:description "Knowledge of the parts and functioning of vehicles, machinery or equipment, and of techniques and practices for their safe and efficient use." ;
	schema:bestRating "5" .

<#K511a01> # Languages
    a schema:DefinedTerm ;
	schema:termCode "K511a01" ;
	schema:name "Languages" ;
	schema:description "Knowledge of vocabulary, grammar structure and rules, spelling, and pronunciation of words in one or both official languages, Indigenous languages, and non-official languages." ;
	schema:bestRating "5" .

<#K511a02> # Mathematics
    a schema:DefinedTerm ;
	schema:termCode "K511a02" ;
	schema:name "Mathematics" ;
	schema:description "Knowledge of concepts, principles, methods, and applications of arithmetic, algebra, geometry, trigonometry, differential and integral calculus, probability, and statistics." ;
	schema:bestRating "5" .

<#K601a01> # Consequence of Error
    a schema:DefinedTerm ;
	schema:termCode "K601a01" ;
	schema:name "Consequence of Error" ;
	schema:description "The impact on outcomes of a mistake, which was not readily correctable, made by the worker." ;
	schema:bestRating "5" .

<#K601a02> # Freedom to Make Decisions
    a schema:DefinedTerm ;
	schema:termCode "K601a02" ;
	schema:name "Freedom to Make Decisions" ;
	schema:description "The job allows the worker to make decisions without supervision." ;
	schema:bestRating "5" .

<#K601a03> # Frequency of Decision Making
    a schema:DefinedTerm ;
	schema:termCode "K601a03" ;
	schema:name "Frequency of Decision Making" ;
	schema:description "The job requires the worker to make decisions that affect other people, the financial resources, and/or the image and reputation of the organization." ;
	schema:bestRating "5" .

<#K601a04> # Impact of Decisions
    a schema:DefinedTerm ;
	schema:termCode "K601a04" ;
	schema:name "Impact of Decisions" ;
	schema:description "The impact on the organization or colleagues of the decisions made by the worker (a decision should be understood as a conclusion or resolution reached after consideration)." ;
	schema:bestRating "5" .

<#K601b01> # Automation
    a schema:DefinedTerm ;
	schema:termCode "K601b01" ;
	schema:name "Automation" ;
	schema:description "The job requires operation, manipulation or handling of automated systems, processes or machines." ;
	schema:bestRating "5" .

<#K601b02> # Precision
    a schema:DefinedTerm ;
	schema:termCode "K601b02" ;
	schema:name "Precision" ;
	schema:description "The job requires the worker to be exact or accurate." ;
	schema:bestRating "5" .

<#K601b03> # Structured versus Unstructured Work
    a schema:DefinedTerm ;
	schema:termCode "K601b03" ;
	schema:name "Structured versus Unstructured Work" ;
	schema:description "The extent to which the job is structured for the worker, rather than allowing the worker to determine tasks, priorities, and goals." ;
	schema:bestRating "5" .

<#K601b04> # Tasks Repetition
    a schema:DefinedTerm ;
	schema:termCode "K601b04" ;
	schema:name "Tasks Repetition" ;
	schema:description "The job requires repetitive tasks in the performance of work." ;
	schema:bestRating "5" .

<#K601c01> # Pace Determined by Speed of Equipment
    a schema:DefinedTerm ;
	schema:termCode "K601c01" ;
	schema:name "Pace Determined by Speed of Equipment" ;
	schema:description "The job requires maintaining pace with the speed of the equipment, machines, or computers. This does not refer to always being occupied while in the position." ;
	schema:bestRating "5" .

<#K601c02> # Time Pressure
    a schema:DefinedTerm ;
	schema:termCode "K601c02" ;
	schema:name "Time Pressure" ;
	schema:description "The job requires working under pressure, meeting strict deadlines or dealing with competing priorities." ;
	schema:bestRating "5" .

<#K601c03> # Type of Work Schedules
    a schema:DefinedTerm ;
	schema:termCode "K601c03" ;
	schema:name "Type of Work Schedules" ;
	schema:description "The type of schedule usually required for the job." ;
	schema:bestRating "5" .

<#K601c04> # Work Week Duration
    a schema:DefinedTerm ;
	schema:termCode "K601c04" ;
	schema:name "Work Week Duration" ;
	schema:description "Number of hours typically worked over a period of 7 days." ;
	schema:bestRating "5" .

<#K601d01> # Competition
    a schema:DefinedTerm ;
	schema:termCode "K601d01" ;
	schema:name "Competition" ;
	schema:description "The job requires to compete against co-workers or to be aware of competitive pressure between them or between businesses within the same industry." ;
	schema:bestRating "5" .

<#K602a01> # Dangerous Locations
    a schema:DefinedTerm ;
	schema:termCode "K602a01" ;
	schema:name "Dangerous Locations" ;
	schema:description "The job requires working in locations that are inherently treacherous and are potential sources of injury. Such work locations include among others, construction sites, underground sites, erected support structures, and marine environments." ;
	schema:bestRating "5" .

<#K602a02> # Fire, Steam, Hot Surfaces
    a schema:DefinedTerm ;
	schema:termCode "K602a02" ;
	schema:name "Fire, Steam, Hot Surfaces" ;
	schema:description "The job requires being exposed to fire (rather than being exposed to flammable substances that may ignite), to emissions of steam or to intensely hot surfaces that are potential sources of injury." ;
	schema:bestRating "5" .

<#K602a03> # Flying Particles, Falling Objects
    a schema:DefinedTerm ;
	schema:termCode "K602a03" ;
	schema:name "Flying Particles, Falling Objects" ;
	schema:description "The job requires being exposed to flying particles and falling objects or materials in the work environment that pose the risk of bodily injury. Flying particles refer to particles such as wood chips, metal particles, and rock chips generated by the handling, crushing, grinding, rapid impact, or explosion of materials." ;
	schema:bestRating "5" .

<#K602a04> # Hazardous Conditions
    a schema:DefinedTerm ;
	schema:termCode "K602a04" ;
	schema:name "Hazardous Conditions" ;
	schema:description "The job requires being exposed to conditions that involves risks of accidents such as high voltage electricity, flammable material, or explosives." ;
	schema:bestRating "5" .

<#K602a05> # Hazardous Equipment, Machinery, Tools
    a schema:DefinedTerm ;
	schema:termCode "K602a05" ;
	schema:name "Hazardous Equipment, Machinery, Tools" ;
	schema:description "The job requires working near or with equipment, instruments, machinery, or power/hand tools that may be a potential source of accident or injury." ;
	schema:bestRating "5" .

<#K602a06> # High Places
    a schema:DefinedTerm ;
	schema:termCode "K602a06" ;
	schema:name "High Places" ;
	schema:description "The job requires being exposed to elevated places such as poles, scaffolding, catwalks, or ladders longer than two meters in length." ;
	schema:bestRating "5" .

<#K602a07> # Radiation
    a schema:DefinedTerm ;
	schema:termCode "K602a07" ;
	schema:name "Radiation" ;
	schema:description "The job requires being exposed to ionizing radiation such as X-rays and radioactive substances or non-ionizing radiation such as radio frequencies and infrared, ultraviolet or visible light that may affect health adversely." ;
	schema:bestRating "5" .

<#K602a08> # Cramped Work Space, Awkward Positions
    a schema:DefinedTerm ;
	schema:termCode "K602a08" ;
	schema:name "Cramped Work Space, Awkward Positions" ;
	schema:description "The job requires working in confined space that requires getting into uncomfortable positions." ;
	schema:bestRating "5" .

<#K602a09> # Skin Injury
    a schema:DefinedTerm ;
	schema:termCode "K602a09" ;
	schema:name "Skin Injury" ;
	schema:description "The job requires being exposed to the risks of minor burns, cuts, bites, or stings." ;
	schema:bestRating "5" .

<#K602b01> # In an Enclosed Vehicle or Equipment
    a schema:DefinedTerm ;
	schema:termCode "K602b01" ;
	schema:name "In an Enclosed Vehicle or Equipment" ;
	schema:description "The job requires working in a closed vehicle or equipment (e.g., car, truck or heavy equipment)." ;
	schema:bestRating "5" .

<#K602b02> # In an Open Vehicle or Equipment
    a schema:DefinedTerm ;
	schema:termCode "K602b02" ;
	schema:name "In an Open Vehicle or Equipment" ;
	schema:description "The job requires working in an open vehicle or equipment (e.g., tractor)." ;
	schema:bestRating "5" .

<#K602b03> # Indoors, Environmentally Controlled
    a schema:DefinedTerm ;
	schema:termCode "K602b03" ;
	schema:name "Indoors, Environmentally Controlled" ;
	schema:description "The job requires working inside a building with controlled temperature and humidity conditions." ;
	schema:bestRating "5" .

<#K602b04> # Indoors, Not Environmentally Controlled
    a schema:DefinedTerm ;
	schema:termCode "K602b04" ;
	schema:name "Indoors, Not Environmentally Controlled" ;
	schema:description "The job requires working inside a building where the temperature and humidity are not controlled (e.g., warehouse without heat)." ;
	schema:bestRating "5" .

<#K602b05> # Outside, Exposed to Weather
    a schema:DefinedTerm ;
	schema:termCode "K602b05" ;
	schema:name "Outside, Exposed to Weather" ;
	schema:description "The job requires working outdoors and being subject to variations in weather conditions and seasonal weather patterns." ;
	schema:bestRating "5" .

<#K602b06> # K602b06
    a schema:DefinedTerm ;
	schema:termCode "K602b06" ;
	schema:name "K602b06" ;
	schema:description "The job requires working outdoors, protected from variations in weather conditions and seasonal weather patterns by a covered space (e.g., structure with roof but no walls)." ;
	schema:bestRating "5" .

<#K602b07> # Physical Proximity
    a schema:DefinedTerm ;
	schema:termCode "K602b07" ;
	schema:name "Physical Proximity" ;
	schema:description "The job requires performing tasks while being physically close to other people." ;
	schema:bestRating "5" .

<#K602c01> # Biological Agents
    a schema:DefinedTerm ;
	schema:termCode "K602c01" ;
	schema:name "Biological Agents" ;
	schema:description "The job requires being exposed to bacteria, viruses and fungi that may cause illness due to direct or indirect contact." ;
	schema:bestRating "5" .

<#K602c02> # Dangerous Chemical Substances
    a schema:DefinedTerm ;
	schema:termCode "K602c02" ;
	schema:name "Dangerous Chemical Substances" ;
	schema:description "The job requires being exposed to contaminants, such as pollutants, gases or dust, through inhalation, ingestion, or contact with skin." ;
	schema:bestRating "5" .

<#K602c03> # Vibration
    a schema:DefinedTerm ;
	schema:termCode "K602c03" ;
	schema:name "Vibration" ;
	schema:description "The job requires being exposed to oscillating or quivering motion of the body while performing tasks." ;
	schema:bestRating "5" .

<#K602c04> # Sound and Noise
    a schema:DefinedTerm ;
	schema:termCode "K602c04" ;
	schema:name "Sound and Noise" ;
	schema:description "The job requires being exposed to sound and noise levels that are distracting or uncomfortable, regardless of the equipment used by the workers." ;
	schema:bestRating "5" .

<#K602c05> # Extremely Bright or Inadequate Lighting
    a schema:DefinedTerm ;
	schema:termCode "K602c05" ;
	schema:name "Extremely Bright or Inadequate Lighting" ;
	schema:description "The job requires working in extremely bright or inadequate lighting conditions." ;
	schema:bestRating "5" .

<#K602c06> # Extreme Temperatures
    a schema:DefinedTerm ;
	schema:termCode "K602c06" ;
	schema:name "Extreme Temperatures" ;
	schema:description "The job requires being exposed to very hot (above 32.2 °C) or very cold (below 0 °C) temperatures." ;
	schema:bestRating "5" .

<#K602c07> # Odours
    a schema:DefinedTerm ;
	schema:termCode "K602c07" ;
	schema:name "Odours" ;
	schema:description "The job requires being exposed to noxious, intense or prolonged odours." ;
	schema:bestRating "5" .

<#K602d01> # Specialized Safety Equipment
    a schema:DefinedTerm ;
	schema:termCode "K602d01" ;
	schema:name "Specialized Safety Equipment" ;
	schema:description "The job requires wearing specialized protective or safety equipment such as breathing apparatus, safety harness, full protection suits, or radiation protection." ;
	schema:bestRating "5" .

<#K602d02> # Standard Safety Equipment
    a schema:DefinedTerm ;
	schema:termCode "K602d02" ;
	schema:name "Standard Safety Equipment" ;
	schema:description "The job requires wearing common protective or safety equipment such as safety shoes, glasses, gloves, hard hats, or life jackets." ;
	schema:bestRating "5" .

<#K603a01> # Bending or Twisting the Body
    a schema:DefinedTerm ;
	schema:termCode "K603a01" ;
	schema:name "Bending or Twisting the Body" ;
	schema:description "The job requires leaning forwards or backwards or moving the body torsionally." ;
	schema:bestRating "5" .

<#K603a02> # Climbing
    a schema:DefinedTerm ;
	schema:termCode "K603a02" ;
	schema:name "Climbing" ;
	schema:description "The job requires going up and down ladders, scaffolds, or poles." ;
	schema:bestRating "5" .

<#K603a03> # Crawling
    a schema:DefinedTerm ;
	schema:termCode "K603a03" ;
	schema:name "Crawling" ;
	schema:description "The job requires moving in a prone position, with the body resting on or close to the ground, on the hands and knees." ;
	schema:bestRating "5" .

<#K603a04> # Crouching
    a schema:DefinedTerm ;
	schema:termCode "K603a04" ;
	schema:name "Crouching" ;
	schema:description "The job requires powering the body stance by bending the legs." ;
	schema:bestRating "5" .

<#K603a05> # Handling Material Manually
    a schema:DefinedTerm ;
	schema:termCode "K603a05" ;
	schema:name "Handling Material Manually" ;
	schema:description "The job requires using your hands to handle, control, or feel objects, tools, or controls (excluding mouse and keyboard)." ;
	schema:bestRating "5" .

<#K603a06> # Keeping or Regaining Balance
    a schema:DefinedTerm ;
	schema:termCode "K603a06" ;
	schema:name "Keeping or Regaining Balance" ;
	schema:description "The job requires maintaining your body in a steady position or recovering balance." ;
	schema:bestRating "5" .

<#K603a07> # Kneeling
    a schema:DefinedTerm ;
	schema:termCode "K603a07" ;
	schema:name "Kneeling" ;
	schema:description "The job requires positioning the body so that one or both knees rest on the floor." ;
	schema:bestRating "5" .

<#K603a08> # Making Repetitive Motions
    a schema:DefinedTerm ;
	schema:termCode "K603a08" ;
	schema:name "Making Repetitive Motions" ;
	schema:description "The job requires repeating the same movement." ;
	schema:bestRating "5" .

<#K603a09> # Sitting
    a schema:DefinedTerm ;
	schema:termCode "K603a09" ;
	schema:name "Sitting" ;
	schema:description "The job requires being in a position where the body weight is supported by the buttocks." ;
	schema:bestRating "5" .

<#K603a10> # Standing
    a schema:DefinedTerm ;
	schema:termCode "K603a10" ;
	schema:name "Standing" ;
	schema:description "The job requires maintaining an upright position supported by ones feet." ;
	schema:bestRating "5" .

<#K603a11> # Walking and Running
    a schema:DefinedTerm ;
	schema:termCode "K603a11" ;
	schema:name "Walking and Running" ;
	schema:description "The job requires lifting and setting down each foot in turn in order to move forward at a certain pace." ;
	schema:bestRating "5" .

<#K603a12> # Reaching
    a schema:DefinedTerm ;
	schema:termCode "K603a12" ;
	schema:name "Reaching" ;
	schema:description "The job requires extending one or both arms to grasp or touch a person or an object." ;
	schema:bestRating "5" .

<#K603a13> # Stooping
    a schema:DefinedTerm ;
	schema:termCode "K603a13" ;
	schema:name "Stooping" ;
	schema:description "The job requires standing or walking with an inclination of the head, body, or shoulders." ;
	schema:bestRating "5" .

<#K603a14> # Keyboarding
    a schema:DefinedTerm ;
	schema:termCode "K603a14" ;
	schema:name "Keyboarding" ;
	schema:description "The job requires using a panel of keys for typing on an electronic device or computer." ;
	schema:bestRating "5" .

<#K603b01> # Carrying
    a schema:DefinedTerm ;
	schema:termCode "K603b01" ;
	schema:name "Carrying" ;
	schema:description "The job requires holding things while moving." ;
	schema:bestRating "5" .

<#K603b02> # Lifting
    a schema:DefinedTerm ;
	schema:termCode "K603b02" ;
	schema:name "Lifting" ;
	schema:description "The job requires raising an object using the hands and arms." ;
	schema:bestRating "5" .

<#K603b03> # Pulling
    a schema:DefinedTerm ;
	schema:termCode "K603b03" ;
	schema:name "Pulling" ;
	schema:description "The job requires taking hold of an object to move it toward oneself." ;
	schema:bestRating "5" .

<#K603b04> # Pushing
    a schema:DefinedTerm ;
	schema:termCode "K603b04" ;
	schema:name "Pushing" ;
	schema:description "The job requires exerting force in order to move an object forward." ;
	schema:bestRating "5" .

<#K603c01> # Speaking
    a schema:DefinedTerm ;
	schema:termCode "K603c01" ;
	schema:name "Speaking" ;
	schema:description "The job requires conveying information in spoken language." ;
	schema:bestRating "5" .

<#K603c02> # Visual Acuity
    a schema:DefinedTerm ;
	schema:termCode "K603c02" ;
	schema:name "Visual Acuity" ;
	schema:description "The job requires distinguishing fine details in things or in the environment." ;
	schema:bestRating "5" .

<#K604a01> # Conflict Situations
    a schema:DefinedTerm ;
	schema:termCode "K604a01" ;
	schema:name "Conflict Situations" ;
	schema:description "The job requires being confronted with disputes or disagreements with or between customers, employees, or other parties." ;
	schema:bestRating "5" .

<#K604a02> # Contact with Others
    a schema:DefinedTerm ;
	schema:termCode "K604a02" ;
	schema:name "Contact with Others" ;
	schema:description "The job requires being in contact with others (face-to-face, by telephone, or otherwise) to perform tasks." ;
	schema:bestRating "5" .

<#K604a03> # Coordinating or Leading Others
    a schema:DefinedTerm ;
	schema:termCode "K604a03" ;
	schema:name "Coordinating or Leading Others" ;
	schema:description "The job requires providing guidance or direction to co-workers or subordinates in accomplishing work activities." ;
	schema:bestRating "5" .

<#K604a04> # Deal With External Customers
    a schema:DefinedTerm ;
	schema:termCode "K604a04" ;
	schema:name "Deal With External Customers" ;
	schema:description "The job requires working with members outside of the organization, including clients and the public." ;
	schema:bestRating "5" .

<#K604a05> # Work with Work Group or Team
    a schema:DefinedTerm ;
	schema:termCode "K604a05" ;
	schema:name "Work with Work Group or Team" ;
	schema:description "The job requires working with others in a group or team." ;
	schema:bestRating "5" .

<#K604a06> # Deal with Physically Aggressive People
    a schema:DefinedTerm ;
	schema:termCode "K604a06" ;
	schema:name "Deal with Physically Aggressive People" ;
	schema:description "The job requires dealing with individuals that have violent behaviour." ;
	schema:bestRating "5" .

<#K604a07> # Dealing With Unpleasant or Angry People
    a schema:DefinedTerm ;
	schema:termCode "K604a07" ;
	schema:name "Dealing With Unpleasant or Angry People" ;
	schema:description "The job requires dealing with disagreeable, furious, or discourteous individuals." ;
	schema:bestRating "5" .

<#K604b01> # Electronic Mail
    a schema:DefinedTerm ;
	schema:termCode "K604b01" ;
	schema:name "Electronic Mail" ;
	schema:description "The job requires the use of an electronic communication device to send and receive messages." ;
	schema:bestRating "5" .

<#K604b02> # Face-to-Face Discussions
    a schema:DefinedTerm ;
	schema:termCode "K604b02" ;
	schema:name "Face-to-Face Discussions" ;
	schema:description "The job requires having in-person discussions with individuals or teams." ;
	schema:bestRating "5" .

<#K604b03> # Written Communications
    a schema:DefinedTerm ;
	schema:termCode "K604b03" ;
	schema:name "Written Communications" ;
	schema:description "The job requires producing administrative or creative written communications." ;
	schema:bestRating "5" .

<#K604b04> # Public Speaking
    a schema:DefinedTerm ;
	schema:termCode "K604b04" ;
	schema:name "Public Speaking" ;
	schema:description "The job requires delivering speeches to an audience (a minimum of five persons)." ;
	schema:bestRating "5" .

<#K604b05> # Telephone
    a schema:DefinedTerm ;
	schema:termCode "K604b05" ;
	schema:name "Telephone" ;
	schema:description "The job requires communicating with others by using a telephone or hand-held radios." ;
	schema:bestRating "5" .

<#K604b06> # Videoconference
    a schema:DefinedTerm ;
	schema:termCode "K604b06" ;
	schema:name "Videoconference" ;
	schema:description "The job requires using videoconference software to participate in meetings and conversations." ;
	schema:bestRating "5" .

<#K604c01> # Responsibility for Outcomes and Results of Other Workers
    a schema:DefinedTerm ;
	schema:termCode "K604c01" ;
	schema:name "Responsibility for Outcomes and Results of Other Workers" ;
	schema:description "The job requires assuming the responsibility for the end product and effects of other workers work." ;
	schema:bestRating "5" .

<#K604c02> # Responsible for Others' Health and Safety
    a schema:DefinedTerm ;
	schema:termCode "K604c02" ;
	schema:name "Responsible for Others' Health and Safety" ;
	schema:description "The job requires ensuring the health, safety and security of others." ;
	schema:bestRating "5" .

<#K701a01> # Getting Information
    a schema:DefinedTerm ;
	schema:termCode "K701a01" ;
	schema:name "Getting Information" ;
	schema:description "Observing, receiving, or obtaining information from all relevant sources." ;
	schema:bestRating "5" .

<#K701a02> # Monitoring Processes, Materials, or Surroundings
    a schema:DefinedTerm ;
	schema:termCode "K701a02" ;
	schema:name "Monitoring Processes, Materials, or Surroundings" ;
	schema:description "Tracking and reviewing information from materials, events, or the environment to detect or assess problems and progress." ;
	schema:bestRating "5" .

<#K701a03> # Document Use
    a schema:DefinedTerm ;
	schema:termCode "K701a03" ;
	schema:name "Document Use" ;
	schema:description "Reading, understanding, retaining, and using relevant information from texts, numbers, symbols, graphics, and images in electronic or paper format." ;
	schema:bestRating "5" .

<#K701a04> # Information Synthesis
    a schema:DefinedTerm ;
	schema:termCode "K701a04" ;
	schema:name "Information Synthesis" ;
	schema:description "Gather information from multiple sources into a coherent whole and summarize it." ;
	schema:bestRating "5" .

<#K701a05> # Comparing
    a schema:DefinedTerm ;
	schema:termCode "K701a05" ;
	schema:name "Comparing" ;
	schema:description "Determining the functional or structural characteristics of data, people, or things by finding similarities and differences from a model or established standards." ;
	schema:bestRating "5" .

<#K701a06> # Analyzing Data or Information
    a schema:DefinedTerm ;
	schema:termCode "K701a06" ;
	schema:name "Analyzing Data or Information" ;
	schema:description "Identifying the underlying principles, reasons, or facts of information by breaking down information or data into separate parts." ;
	schema:bestRating "5" .

<#K701a07> # Developing Technical Instructions
    a schema:DefinedTerm ;
	schema:termCode "K701a07" ;
	schema:name "Developing Technical Instructions" ;
	schema:description "Providing documentation, detailed instructions, drawings, or specifications to tell others about how devices, parts, equipment, or structures are to be fabricated, constructed, assembled, modified, maintained, or used." ;
	schema:bestRating "5" .

<#K701a08> # Clerical Activities
    a schema:DefinedTerm ;
	schema:termCode "K701a08" ;
	schema:name "Clerical Activities" ;
	schema:description "Entering, transcribing, recording, storing, or maintaining all types of information in written or electronic form." ;
	schema:bestRating "5" .

<#K701b01> # Identifying Objects, Actions, and Events
    a schema:DefinedTerm ;
	schema:termCode "K701b01" ;
	schema:name "Identifying Objects, Actions, and Events" ;
	schema:description "Identifying information by categorizing, recognizing differences or similarities, measuring, investigating, and detecting changes in circumstances or events." ;
	schema:bestRating "5" .

<#K701b02> # Estimating the Quantifiable Characteristics
    a schema:DefinedTerm ;
	schema:termCode "K701b02" ;
	schema:name "Estimating the Quantifiable Characteristics" ;
	schema:description "Estimating cost, resources or materials needed to perform a work activity." ;
	schema:bestRating "5" .


<#K701b03> # Inspecting Equipment, Structures, or Material
    a schema:DefinedTerm ;
	schema:termCode "K701b03" ;
	schema:name "Inspecting Equipment, Structures, or Material" ;
	schema:description "Inspecting equipment, structures, or material to identify the cause of errors, problems or defects." ;
	schema:bestRating "5" .

<#K701b04> # Processing Information				
    a schema:DefinedTerm ;
	schema:termCode "K701b04" ;
	schema:name "Processing Information" ;
	schema:description "Compiling, categorizing, tabulating, auditing, or verifying information or data." ;
	schema:bestRating "5" .

<#K702a01> # Handling and Moving Objects
    a schema:DefinedTerm ;
	schema:termCode "K702a01" ;
	schema:name "Handling and Moving Objects" ;
	schema:description "Using hands and arms to install, fabricate and, repair objects; or to move or manipulate objects and materials (excluding construction occupations)." ;
	schema:bestRating "5" .

<#K702a02> # Operating Vehicles, Mechanized Devices, or Equipment
    a schema:DefinedTerm ;
	schema:termCode "K702a02" ;
	schema:name "Operating Vehicles, Mechanized Devices, or Equipment" ;
	schema:description "Manoeuvring, navigating, or driving vehicles or mechanized equipment, such as forklifts, passenger vehicles, aircraft, or watercraft." ;
	schema:bestRating "5" .

<#K702a03> # Constructing
    a schema:DefinedTerm ;
	schema:termCode "K702a03" ;
	schema:name "Constructing" ;
	schema:description "Joining building materials into a structure, applying interior or exterior finishes or installing building systems according to specifications and plans." ;
	schema:bestRating "5" .

<#K702a04> # Controlling Machines and Processes
    a schema:DefinedTerm ;
	schema:termCode "K702a04" ;
	schema:name "Controlling Machines and Processes" ;
	schema:description "Using mechanisms or physical activity to control the operation of machines or processes (excluding computers or vehicles)." ;
	schema:bestRating "5" .

<#K702a05> # Manipulating> # Operating
    a schema:DefinedTerm ;
	schema:termCode "K702a05" ;
	schema:name "Manipulating> # Operating" ;
	schema:description "Using hand-held and power tools or special devices to move, remove, guide, install and place objects or materials." ;
	schema:bestRating "5" .

<#K702a06> # Sorting
    a schema:DefinedTerm ;
	schema:termCode "K702a06" ;
	schema:name "Sorting" ;
	schema:description "Handling, retrieving, sorting, separating, or arranging materials or information, according to established patterns or procedures." ;
	schema:bestRating "5" .

<#K702a07> # Catering
    a schema:DefinedTerm ;
	schema:termCode "K702a07" ;
	schema:name "Catering" ;
	schema:description "Preparing or cooking food and beverage by combining ingredients." ;
	schema:bestRating "5" .

<#K702a08> # Performing Janitorial Services
    a schema:DefinedTerm ;
	schema:termCode "K702a08" ;
	schema:name "Performing Janitorial Services" ;
	schema:description "Cleaning and maintaining commercial, public, or private places." ;
	schema:bestRating "5" .

<#K702a09> # Performing General Physical Activities
    a schema:DefinedTerm ;
	schema:termCode "K702a09" ;
	schema:name "Performing General Physical Activities" ;
	schema:description "Performing physical activities that require use of your arms and legs and moving your whole body, such as climbing, lifting, balancing, walking, stooping, and handling materials." ;
	schema:bestRating "5" .

<#K702b01> # Debugging and Reprogramming
    a schema:DefinedTerm ;
	schema:termCode "K702b01" ;
	schema:name "Debugging and Reprogramming" ;
	schema:description "Modifying systems through upgrading, amending procedures, or correcting faults." ;
	schema:bestRating "5" .

<#K702b02> # Artistic Designing
    a schema:DefinedTerm ;
	schema:termCode "K702b02" ;
	schema:name "Artistic Designing" ;
	schema:description "Creating and designing artistic drawing and visual representation, and arranging displays, exhibits or decorations." ;
	schema:bestRating "5" .

<#K702b03> # Electronic Maintenance
    a schema:DefinedTerm ;
	schema:termCode "K702b03" ;
	schema:name "Electronic Maintenance" ;
	schema:description "Servicing, repairing, calibrating, regulating, fine-tuning, or testing machines, devices, and equipment that operate on electrical or electronic principles." ;
	schema:bestRating "5" .

<#K702b04> # Interacting with Computers
    a schema:DefinedTerm ;
	schema:termCode "K702b04" ;
	schema:name "Interacting with Computers" ;
	schema:description "Using computers and computer systems (including hardware and software), and equipment with digital interface to program, write software, set up functions, enter data, process information, or control machines." ;
	schema:bestRating "5" .

<#K702b05> # Mechanical Maintenance
    a schema:DefinedTerm ;
	schema:termCode "K702b05" ;
	schema:name "Mechanical Maintenance" ;
	schema:description "Servicing, repairing, adjusting, or testing machines, devices, moving parts, and equipment that operate on mechanical principles." ;
	schema:bestRating "5" .

<#K702b06> # Writing or Composing
    a schema:DefinedTerm ;
	schema:termCode "K702b06" ;
	schema:name "Writing or Composing" ;
	schema:description "Writing or composing original material using symbols such as letters of the alphabet or musical notation to communicate thoughts and ideas in a readable or audible form." ;
	schema:bestRating "5" .

<#K703a01> # Judging Quality
    a schema:DefinedTerm ;
	schema:termCode "K703a01" ;
	schema:name "Judging Quality" ;
	schema:description "Assessing the value, importance or quality of materials, products, services or people." ;
	schema:bestRating "5" .

<#K703a02> # Evaluating Information to Determine Compliance
    a schema:DefinedTerm ;
	schema:termCode "K703a02" ;
	schema:name "Evaluating Information to Determine Compliance" ;
	schema:description "Using relevant information and individual judgment to determine whether events or processes comply with laws, regulations or standards." ;
	schema:bestRating "5" .

<#K703a03> # Calculating
    a schema:DefinedTerm ;
	schema:termCode "K703a03" ;
	schema:name "Calculating" ;
	schema:description "Performing, interpreting, and reporting mathematical operations as part of work tasks." ;
	schema:bestRating "5" .

<#K703b01> # Making Decisions
    a schema:DefinedTerm ;
	schema:termCode "K703b01" ;
	schema:name "Making Decisions" ;
	schema:description "Choose the best solution based on the analysis of information and the evaluation of potential results." ;
	schema:bestRating "5" .

<#K703b02> # Thinking Creatively
    a schema:DefinedTerm ;
	schema:termCode "K703b02" ;
	schema:name "Thinking Creatively" ;
	schema:description "Generating innovative or creative ideas to develop or design new application, products, including artistic contributions." ;
	schema:bestRating "5" .

<#K703b03> # Developing Objectives and Strategies
    a schema:DefinedTerm ;
	schema:termCode "K703b03" ;
	schema:name "Developing Objectives and Strategies" ;
	schema:description "Define and establish medium to long-term objectives, and determine strategies and actions to achieve them." ;
	schema:bestRating "5" .

<#K703b04> # Applying New Knowledge
    a schema:DefinedTerm ;
	schema:termCode "K703b04" ;
	schema:name "Applying New Knowledge" ;
	schema:description "Keep up-to-date on relevant theorical and technical knowledge and apply them at work." ;
	schema:bestRating "5" .

<#K703b05> # Examining and Diagnosing
    a schema:DefinedTerm ;
	schema:termCode "K703b05" ;
	schema:name "Examining and Diagnosing" ;
	schema:description "Assessing the human, animal, technical, or scientific dimensions of a problem through examination or diagnostic testing in order to determine its root cause and appropriate intervention (excluding all forms of interviews)." ;
	schema:bestRating "5" .

<#K703b06> # Managing Resources
    a schema:DefinedTerm ;
	schema:termCode "K703b06" ;
	schema:name "Managing Resources" ;
	schema:description "Determining, acquiring, monitoring and controlling any kind of resources and overseeing the spending of money." ;
	schema:bestRating "5" .

<#K703b07> # Planning and Organizing
    a schema:DefinedTerm ;
	schema:termCode "K703b07" ;
	schema:name "Planning and Organizing" ;
	schema:description "Developing specific goals and plans to prioritize and organize tasks to get the work done." ;
	schema:bestRating "5" .

<#K703b08> # Scheduling Work and Activities
    a schema:DefinedTerm ;
	schema:termCode "K703b08" ;
	schema:name "Scheduling Work and Activities" ;
	schema:description "Scheduling events, programs, and activities, as well as the work of others." ;
	schema:bestRating "5" .

<#K704a01> # Communicating with Coworkers
    a schema:DefinedTerm ;
	schema:termCode "K704a01" ;
	schema:name "Communicating with Coworkers" ;
	schema:description "Sharing or providing information or advice to management, supervisors, co-workers and subordinates on work related topics." ;
	schema:bestRating "5" .

<#K704a02> # Coordinating the Work and Activities of Others
    a schema:DefinedTerm ;
	schema:termCode "K704a02" ;
	schema:name "Coordinating the Work and Activities of Others" ;
	schema:description "Getting members of a group to work together to accomplish tasks." ;
	schema:bestRating "5" .

<#K704a03> # Facilitating Group Discussion
    a schema:DefinedTerm ;
	schema:termCode "K704a03" ;
	schema:name "Facilitating Group Discussion" ;
	schema:description "Encouraging exchanges by facilitating participation in group interviews and discussions to improve dialogue, decision making or problem solving." ;
	schema:bestRating "5" .

<#K704a04> # Interpreting the Meaning of Information for Others
    a schema:DefinedTerm ;
	schema:termCode "K704a04" ;
	schema:name "Interpreting the Meaning of Information for Others" ;
	schema:description "Translating or explaining what information means and how it can be used." ;
	schema:bestRating "5" .

<#K704a05> # Protecting and Enforcing
    a schema:DefinedTerm ;
	schema:termCode "K704a05" ;
	schema:name "Protecting and Enforcing" ;
	schema:description "Responding to public safety, security and cybersecurity needs, and promoting and ensuring compliance to rules, standards or laws to protect the general population from all kinds of significant danger (excluding medical treatments)." ;
	schema:bestRating "5" .

<#K704a06> # Communicating with Persons Outside Organization
    a schema:DefinedTerm ;
	schema:termCode "K704a06" ;
	schema:name "Communicating with Persons Outside Organization" ;
	schema:description "Sharing or exchanging information with people outside the organization, representing the organization to customers, the public, government or other external sources." ;
	schema:bestRating "5" .

<#K704a07> # Establishing and Maintaining Interpersonal Relationships
    a schema:DefinedTerm ;
	schema:termCode "K704a07" ;
	schema:name "Establishing and Maintaining Interpersonal Relationships" ;
	schema:description "Developing respectful, constructive, and cooperative working relationships with others, and maintaining them over time." ;
	schema:bestRating "5" .

<#K704a08> # Selling or Influencing Others
    a schema:DefinedTerm ;
	schema:termCode "K704a08" ;
	schema:name "Selling or Influencing Others" ;
	schema:description "Convincing others to buy goods or services, or to change their minds or actions." ;
	schema:bestRating "5" .

<#K704a09> # Performing for or Working Directly with the Public
    a schema:DefinedTerm ;
	schema:termCode "K704a09" ;
	schema:name "Performing for or Working Directly with the Public" ;
	schema:description "Working or interacting directly with the public or performing for public audiences." ;
	schema:bestRating "5" .

<#K704a11> # Interviewing
    a schema:DefinedTerm ;
	schema:termCode "K704a11" ;
	schema:name "Interviewing" ;
	schema:description "Conduct formal interviews with individual or group to collect information or opinions (excluding interviews for the purpose of staffing or recruitment)." ;
	schema:bestRating "5" .

<#K704a12> # Assisting and Caring for Others
    a schema:DefinedTerm ;
	schema:termCode "K704a12" ;
	schema:name "Assisting and Caring for Others" ;
	schema:description "Providing personal assistance, medical attention, emotional support, or other care to customers, clients, or patients." ;
	schema:bestRating "5" .

<#K704b01> # Coaching and Developing Others
    a schema:DefinedTerm ;
	schema:termCode "K704b01" ;
	schema:name "Coaching and Developing Others" ;
	schema:description "Identifying the developmental needs of others and coaching, mentoring, or otherwise helping others to improve their knowledge or skills." ;
	schema:bestRating "5" .

<#K704b02> # Providing Consultation and Advice
    a schema:DefinedTerm ;
	schema:termCode "K704b02" ;
	schema:name "Providing Consultation and Advice" ;
	schema:description "Providing guidance and expert advice to management or other groups on technical, systems, or process related topics." ;
	schema:bestRating "5" .

<#K704b03> # Resolving Conflicts and Negotiating with Others
    a schema:DefinedTerm ;
	schema:termCode "K704b03" ;
	schema:name "Resolving Conflicts and Negotiating with Others" ;
	schema:description "Handling complaints, settling disputes, and resolving grievances and conflicts, or otherwise negotiating with others." ;
	schema:bestRating "5" .

<#K704b04> # Supervising Subordinates
    a schema:DefinedTerm ;
	schema:termCode "K704b04" ;
	schema:name "Supervising Subordinates" ;
	schema:description "Provide guidance and direction to subordinates, including the establishment of work outcomes for performance monitoring." ;
	schema:bestRating "5" .

<#K704b05> # Team Building
    a schema:DefinedTerm ;
	schema:termCode "K704b05" ;
	schema:name "Team Building" ;
	schema:description "Encouraging and building mutual trust, respect, and cooperation among team members." ;
	schema:bestRating "5" .

<#K704b06> # Training and Teaching
    a schema:DefinedTerm ;
	schema:termCode "K704b06" ;
	schema:name "Training and Teaching" ;
	schema:description "Identifying the educational needs of others, developing formal educational or training programs or classes, and teaching or instructing others." ;
	schema:bestRating "5" .

<#K704c01> # Staffing
    a schema:DefinedTerm ;
	schema:termCode "K704c01" ;
	schema:name "Staffing" ;
	schema:description "Recruiting, interviewing, selecting, hiring, and promoting employees in an organization (excluding non-recruitment interviews)." ;
	schema:bestRating "5" .

# FIM DO ARQUIVO
```

**Fields Description**

Each of the 312 attrubutes is represented using the same data structure described below:

* **schema:termCode** - Acronym
* **schema:name** - Name
* **schema:description** - Description
* **schema:bestRating** - Highest value

### WorkDNA.ttl

**File Location**

<User's POD>/KarreraAI/personas/main

**Description**

This file stores the **WorkDNA** attributes for the main persona.

**File Structure**

```ttl title="WorkDNA.ttl" linenums="1"
    @prefix dcterms:    <http://purl.org/dc/terms/> .
@prefix esco:       <http://data.europa.eu/esco/model#> .
@prefix schema:     <http://schema.org/> .
@prefix skos:       <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix dna:        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/.system/WorkDNA-Definitions.ttl> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/WorkDNA.ttl>
    a schema:DefinedTermSet ;

    # K101a01 - Information Ordering
    schema:hasDefinedTerm [
        a schema:DefinedTermSet ;
        schema:inDefinedTermSet <dna:#K101a01> ;
		schema:termCode "K101a01" ;
        schema:ratingValue "5" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;
    
    # K101a02 - Categorization Flexibility
    schema:hasDefinedTerm [
        a schema:DefinedTermSet ;
        schema:inDefinedTermSet <dna:#K101a02> ;
		schema:termCode "K101a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;
	
    # K101a03 - Deductive Reasoning
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101a03> ;
        schema:termCode "K101a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101a04 - Inductive Reasoning
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101a04> ;
        schema:termCode "K101a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101a05 - Fluency of Ideas
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101a05> ;
        schema:termCode "K101a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101a06 - Problem Identification
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101a06> ;
        schema:termCode "K101a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101b01 - Numerical Ability
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101b01> ;
        schema:termCode "K101b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101b02 - Mathematical Reasoning
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101b02> ;
        schema:termCode "K101b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101c01 - Memorizing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101c01> ;
        schema:termCode "K101c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101c02 - Multitasking
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101c02> ;
        schema:termCode "K101c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101c03 - Pattern Identification
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101c03> ;
        schema:termCode "K101c03" ;
		schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101c04 - Pattern Organization Speed
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101c04> ;
        schema:termCode "K101c04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101c05 - Perceptual Speed
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101c05> ;
        schema:termCode "K101c05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101d01 - Spatial Orientation
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101d01> ;
        schema:termCode "K101d01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101d02 - Spatial Visualization
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101d02> ;
        schema:termCode "K101d02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101e01 - Verbal Ability
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101e01> ;
        schema:termCode "K101e01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101e02 - Written Comprehension
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101e02> ;
        schema:termCode "K101e02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101e03 - Written Expression
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101e03> ;
        schema:termCode "K101e03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101f01 - Selective Attention
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101f01> ;
        schema:termCode "K101f01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101f02 - Form Perception
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101f02> ;
        schema:termCode "K101f02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K101f03 - General Learning Ability
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K101f03> ;
        schema:termCode "K101f03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102a01 - Trunk Strength
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102a01> ;
        schema:termCode "K102a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102a02 - Static Strength
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102a02> ;
        schema:termCode "K102a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102a03 - Dynamic Strength
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102a03> ;
        schema:termCode "K102a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102a04 - Explosive Strength
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102a04> ;
        schema:termCode "K102a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102b01 - Multi-Limb Coordination
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102b01> ;
        schema:termCode "K102b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102b02 - Gross Body Coordination
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102b02> ;
        schema:termCode "K102b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102b03 - Gross Body Equilibrium
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102b03> ;
        schema:termCode "K102b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102b04 - Body Flexibility
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102b04> ;
        schema:termCode "K102b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102b05 - Dynamic Flexibility
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102b05> ;
        schema:termCode "K102b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K102c01 - Stamina
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K102c01> ;
        schema:termCode "K102c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103a01 - Arm-Hand Steadiness
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103a01> ;
        schema:termCode "K103a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103a02 - Finger Dexterity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103a02> ;
        schema:termCode "K103a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103a03 - Manual Dexterity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103a03> ;
        schema:termCode "K103a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103b01 - Motor Coordination
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103b01> ;
        schema:termCode "K103b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103b02 - Rate Control
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103b02> ;
        schema:termCode "K103b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103b03 - Control of Settings
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103b03> ;
        schema:termCode "K103b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103b04 - Multi-Signal Response
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103b04> ;
        schema:termCode "K103b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103c01 - Reaction Time
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103c01> ;
        schema:termCode "K103c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103c02 - Speed of Limb Movement
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103c02> ;
        schema:termCode "K103c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K103c03 - Finger-Hand-Wrist Motion
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K103c03> ;
        schema:termCode "K103c03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104a01 - Auditory Attention
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104a01> ;
        schema:termCode "K104a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104a02 - Hearing Sensitivity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104a02> ;
        schema:termCode "K104a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104a03 - Speech Clarity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104a03> ;
        schema:termCode "K104a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104a04 - Speech Recognition
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104a04> ;
        schema:termCode "K104a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104a05 - Sound Localization
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104a05> ;
        schema:termCode "K104a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104b01 - Far Vision
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104b01> ;
        schema:termCode "K104b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104b02 - Near Vision
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104b02> ;
        schema:termCode "K104b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104b03 - Peripheral Vision
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104b03> ;
        schema:termCode "K104b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104b04 - Depth Perception
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104b04> ;
        schema:termCode "K104b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104b05 - Glare Tolerance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104b05> ;
        schema:termCode "K104b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104b06 - Night Vision
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104b06> ;
        schema:termCode "K104b06" ;
        schema:ratingValue "1" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104c01 - Colour Perception
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104c01> ;
        schema:termCode "K104c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104c02 - Smell
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104c02> ;
        schema:termCode "K104c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104c03 - Taste
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104c03> ;
        schema:termCode "K104c03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K104c04 - Touch
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K104c04> ;
        schema:termCode "K104c04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K201a01 - Leadership
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K201a01> ;
        schema:termCode "K201a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K201a02 - Charisma
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K201a02> ;
        schema:termCode "K201a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K201b01 - Concern for Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K201b01> ;
        schema:termCode "K201b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K201b02 - Collaboration
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K201b02> ;
        schema:termCode "K201b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K201b03 - Service Orientation
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K201b03> ;
        schema:termCode "K201b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K201b04 - Trust in Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K201b04> ;
        schema:termCode "K201b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K201b05 - Social Orientation
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K201b05> ;
        schema:termCode "K201b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202a01 - Adaptability
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202a01> ;
        schema:termCode "K202a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202a02 - Self-Control
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202a02> ;
        schema:termCode "K202a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202a03 - Stress Tolerance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202a03> ;
        schema:termCode "K202a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202a04 - Tolerance of Ambiguity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202a04> ;
        schema:termCode "K202a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202a05 - Resilience
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202a05> ;
        schema:termCode "K202a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202b01 - Self-Awareness
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202b01> ;
        schema:termCode "K202b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202b02 - Self-Confidence
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202b02> ;
        schema:termCode "K202b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202c01 - Active Learning
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202c01> ;
        schema:termCode "K202c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K202c02 - Continuous Learning
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K202c02> ;
        schema:termCode "K202c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K203a01 - Achievement
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K203a01> ;
        schema:termCode "K203a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K203a02 - Initiative
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K203a02> ;
        schema:termCode "K203a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K203a03 - Motivation
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K203a03> ;
        schema:termCode "K203a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K203a04 - Perseverance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K203a04> ;
        schema:termCode "K203a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K203a05 - Risk-Taking
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K203a05> ;
        schema:termCode "K203a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K203a06 - Competitiveness
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K203a06> ;
        schema:termCode "K203a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K203a07 - Independence
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K203a07> ;
        schema:termCode "K203a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K204a01 - Reliable
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K204a01> ;
        schema:termCode "K204a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K204a02 - Integrity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K204a02> ;
        schema:termCode "K204a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K204a03 - Being Responsible
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K204a03> ;
        schema:termCode "K204a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K205a01 - Having Judgement
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K205a01> ;
        schema:termCode "K205a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K205a02 - Analytical Thinking
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K205a02> ;
        schema:termCode "K205a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K205a03 - Attention to Detail
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K205a03> ;
        schema:termCode "K205a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K205b01 - Creativity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K205b01> ;
        schema:termCode "K205b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K205b02 - Innovativeness
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K205b02> ;
        schema:termCode "K205b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K205b03 - Entrepreneurial Spirit
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K205b03> ;
        schema:termCode "K205b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K301a01 - Realistic
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K301a01> ;
        schema:termCode "K301a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K301a02 - Investigative
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K301a02> ;
        schema:termCode "K301a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K301a03 - Artistic
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K301a03> ;
        schema:termCode "K301a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K301a04 - Social
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K301a04> ;
        schema:termCode "K301a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K301a05 - Enterprising
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K301a05> ;
        schema:termCode "K301a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K301a06 - Conventional
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K301a06> ;
        schema:termCode "K301a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K401a01 - Oral Communication: Active Listening
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K401a01> ;
        schema:termCode "K401a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K401a02 - Oral Communication: Oral Comprehension
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K401a02> ;
        schema:termCode "K401a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K401a03 - Oral Communication: Oral Expression
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K401a03> ;
        schema:termCode "K401a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K401b01 - Reading Comprehension
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K401b01> ;
        schema:termCode "K401b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K401b02 - Writing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K401b02> ;
        schema:termCode "K401b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K401c01 - Numeracy
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K401c01> ;
        schema:termCode "K401c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K401c02 - Digital Literacy
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K401c02> ;
        schema:termCode "K401c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K402a01 - Critical Thinking
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K402a01> ;
        schema:termCode "K402a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K402a02 - Learning and Teaching Strategies
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K402a02> ;
        schema:termCode "K402a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K402a03 - Decision Making
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K402a03> ;
        schema:termCode "K402a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K402b01 - Evaluation
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K402b01> ;
        schema:termCode "K402b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K402b02 - Requirements Analysis
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K402b02> ;
        schema:termCode "K402b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K402b03 - Systems Analysis
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K402b03> ;
        schema:termCode "K402b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K402b04 - Researching and Investigating
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K402b04> ;
        schema:termCode "K402b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K402b05 - Problem Solving
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K402b05> ;
        schema:termCode "K402b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a01 - Equipment and Tool Selection
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a01> ;
        schema:termCode "K403a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a02 - Preventative Maintenance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a02> ;
        schema:termCode "K403a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a03 - Setting Up
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a03> ;
        schema:termCode "K403a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a04 - Operation and Control
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a04> ;
        schema:termCode "K403a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a05 - Operation Monitoring of Machinery and Equipment
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a05> ;
        schema:termCode "K403a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a06 - Troubleshooting
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a06> ;
        schema:termCode "K403a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a07 - Repairing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a07> ;
        schema:termCode "K403a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a08 - Quality Control Testing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a08> ;
        schema:termCode "K403a08" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a09 - Product Design
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a09> ;
        schema:termCode "K403a09" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K403a10 - Digital Production
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K403a10> ;
        schema:termCode "K403a10" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404a01 - Management of Financial Resources
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404a01> ;
        schema:termCode "K404a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404a02 - Management of Material Resources
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404a02> ;
        schema:termCode "K404a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404a03 - Management of Personnel Resources
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404a03> ;
        schema:termCode "K404a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404b01 - Operational Planning
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404b01> ;
        schema:termCode "K404b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404b02 - Projecting Outcomes
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404b02> ;
        schema:termCode "K404b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404b03 - Risk Management
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404b03> ;
        schema:termCode "K404b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404b04 - Strategic Planning
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404b04> ;
        schema:termCode "K404b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404b05 - Time Management
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404b05> ;
        schema:termCode "K404b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404c01 - Monitoring
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404c01> ;
        schema:termCode "K404c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404d01 - Change Management
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404d01> ;
        schema:termCode "K404d01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K404d02 - Crisis Management
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K404d02> ;
        schema:termCode "K404d02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K405a01 - Coordinating
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K405a01> ;
        schema:termCode "K405a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K405a02 - Instructing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K405a02> ;
        schema:termCode "K405a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K405a03 - Negotiating
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K405a03> ;
        schema:termCode "K405a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K405a04 - Persuading
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K405a04> ;
        schema:termCode "K405a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K405a05 - Social Perceptiveness
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K405a05> ;
        schema:termCode "K405a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K405a06 - Cross-Cultural Sensitivity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K405a06> ;
        schema:termCode "K405a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K405a07 - Managing Conversation
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K405a07> ;
        schema:termCode "K405a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K501a01 - Accounting
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K501a01> ;
        schema:termCode "K501a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K501a02 - Business Management
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K501a02> ;
        schema:termCode "K501a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K501a03 - Clerical
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K501a03> ;
        schema:termCode "K501a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K501a04 - Finance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K501a04> ;
        schema:termCode "K501a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K501a05 - Human Resources and Labour relations
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K501a05> ;
        schema:termCode "K501a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K501a06 - Sale and Marketing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K501a06> ;
        schema:termCode "K501a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K501a07 - Client Service
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K501a07> ;
        schema:termCode "K501a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K502a01 - Communications and Media
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K502a01> ;
        schema:termCode "K502a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K503a01 - Teaching
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K503a01> ;
        schema:termCode "K503a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K503a02 - Training, Mentoring and Coaching
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K503a02> ;
        schema:termCode "K503a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K504a01 - Hospitality
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K504a01> ;
        schema:termCode "K504a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K504a02 - Mental Health
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K504a02> ;
        schema:termCode "K504a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K504a03 - Personal Services
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K504a03> ;
        schema:termCode "K504a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K504a04 - Physical Health
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K504a04> ;
        schema:termCode "K504a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K504a05 - Recreation, Leisure and Fitness
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K504a05> ;
        schema:termCode "K504a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K504a06 - Veterinarian and Animal Care
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K504a06> ;
        schema:termCode "K504a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K505a01 - Military
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K505a01> ;
        schema:termCode "K505a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K505a02 - Law
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K505a02> ;
        schema:termCode "K505a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K505a03 - Public Affairs and Government Relations
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K505a03> ;
        schema:termCode "K505a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K505a04 - Public Safety and Security
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K505a04> ;
        schema:termCode "K505a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K506a01 - Manufacturing, Processing and Production
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K506a01> ;
        schema:termCode "K506a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K506a02 - Logistics
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K506a02> ;
        schema:termCode "K506a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K506a03 - Performance Measurement
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K506a03> ;
        schema:termCode "K506a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K506a04 - Technical Design
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K506a04> ;
        schema:termCode "K506a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K507a01 - Agriculture and Horticulture
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K507a01> ;
        schema:termCode "K507a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K507a02 - Forestry
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K507a02> ;
        schema:termCode "K507a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K507a03 - Geological Resources
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K507a03> ;
        schema:termCode "K507a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K507a04 - Livestock, Farm Animals & Wildlife
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K507a04> ;
        schema:termCode "K507a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K507a05 - Water Resources
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K507a05> ;
        schema:termCode "K507a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K508a01 - Biology
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K508a01> ;
        schema:termCode "K508a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K508a02 - Chemistry
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K508a02> ;
        schema:termCode "K508a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K508a03 - Geoscience
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K508a03> ;
        schema:termCode "K508a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K508a05 - Physics
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K508a05> ;
        schema:termCode "K508a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K509a01 - Arts
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K509a01> ;
        schema:termCode "K509a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K509a02 - Economics
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K509a02> ;
        schema:termCode "K509a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K509a03 - Humanities
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K509a03> ;
        schema:termCode "K509a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K509a04 - Library, Conservation, and Heritage
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K509a04> ;
        schema:termCode "K509a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K509a05 - Theology and Philosophy
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K509a05> ;
        schema:termCode "K509a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K510a01 - Building and Construction
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K510a01> ;
        schema:termCode "K510a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K510a02 - Computer, Technology and Information Systems
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K510a02> ;
        schema:termCode "K510a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K510a03 - Electrical and Electronics
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K510a03> ;
        schema:termCode "K510a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K510a04 - Mechanics and Machinery
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K510a04> ;
        schema:termCode "K510a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K510a05 - Telecommunications
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K510a05> ;
        schema:termCode "K510a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K510a06 - Vehicle, Machinery and Equipment Operations
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K510a06> ;
        schema:termCode "K510a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K511a01 - Languages
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K511a01> ;
        schema:termCode "K511a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K511a02 - Mathematics
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K511a02> ;
        schema:termCode "K511a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601a01 - Consequence of Error
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601a01> ;
        schema:termCode "K601a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601a02 - Freedom to Make Decisions
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601a02> ;
        schema:termCode "K601a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601a03 - Frequency of Decision Making
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601a03> ;
        schema:termCode "K601a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601a04 - Impact of Decisions
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601a04> ;
        schema:termCode "K601a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601b01 - Automation
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601b01> ;
        schema:termCode "K601b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601b02 - Precision
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601b02> ;
        schema:termCode "K601b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601b03 - Structured versus Unstructured Work
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601b03> ;
        schema:termCode "K601b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601b04 - Tasks Repetition
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601b04> ;
        schema:termCode "K601b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601c01 - Pace Determined by Speed of Equipment
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601c01> ;
        schema:termCode "K601c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601c02 - Time Pressure
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601c02> ;
        schema:termCode "K601c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601c03 - Type of Work Schedules
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601c03> ;
        schema:termCode "K601c03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601c04 - Work Week Duration
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601c04> ;
        schema:termCode "K601c04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K601d01 - Competition
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K601d01> ;
        schema:termCode "K601d01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a01 - Dangerous Locations
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a01> ;
        schema:termCode "K602a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a02 - Fire, Steam, Hot Surfaces
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a02> ;
        schema:termCode "K602a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a03 - Flying Particles, Falling Objects
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a03> ;
        schema:termCode "K602a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a04 - Hazardous Conditions
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a04> ;
        schema:termCode "K602a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a05 - Hazardous Equipment, Machinery, Tools
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a05> ;
        schema:termCode "K602a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a06 - High Places
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a06> ;
        schema:termCode "K602a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a07 - Radiation
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a07> ;
        schema:termCode "K602a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a08 - Cramped Work Space, Awkward Positions
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a08> ;
        schema:termCode "K602a08" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602a09 - Skin Injury
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602a09> ;
        schema:termCode "K602a09" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602b01 - In an Enclosed Vehicle or Equipment
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602b01> ;
        schema:termCode "K602b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602b02 - In an Open Vehicle or Equipment
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602b02> ;
        schema:termCode "K602b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602b03 - Indoors, Environmentally Controlled
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602b03> ;
        schema:termCode "K602b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602b04 - Indoors, Not Environmentally Controlled
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602b04> ;
        schema:termCode "K602b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602b05 - Outside, Exposed to Weather
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602b05> ;
        schema:termCode "K602b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602b06 - K602b06
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602b06> ;
        schema:termCode "K602b06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602b07 - Physical Proximity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602b07> ;
        schema:termCode "K602b07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602c01 - Biological Agents
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602c01> ;
        schema:termCode "K602c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602c02 - Dangerous Chemical Substances
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602c02> ;
        schema:termCode "K602c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602c03 - Vibration
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602c03> ;
        schema:termCode "K602c03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602c04 - Sound and Noise
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602c04> ;
        schema:termCode "K602c04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602c05 - Extremely Bright or Inadequate Lighting
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602c05> ;
        schema:termCode "K602c05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602c06 - Extreme Temperatures
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602c06> ;
        schema:termCode "K602c06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602c07 - Odours
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602c07> ;
        schema:termCode "K602c07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602d01 - Specialized Safety Equipment
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602d01> ;
        schema:termCode "K602d01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K602d02 - Standard Safety Equipment
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K602d02> ;
        schema:termCode "K602d02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a01 - Bending or Twisting the Body
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a01> ;
        schema:termCode "K603a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a02 - Climbing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a02> ;
        schema:termCode "K603a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a03 - Crawling
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a03> ;
        schema:termCode "K603a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a04 - Crouching
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a04> ;
        schema:termCode "K603a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a05 - Handling Material Manually
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a05> ;
        schema:termCode "K603a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a06 - Keeping or Regaining Balance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a06> ;
        schema:termCode "K603a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a07 - Kneeling
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a07> ;
        schema:termCode "K603a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a08 - Making Repetitive Motions
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a08> ;
        schema:termCode "K603a08" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a09 - Sitting
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a09> ;
        schema:termCode "K603a09" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a10 - Standing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a10> ;
        schema:termCode "K603a10" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a11 - Walking and Running
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a11> ;
        schema:termCode "K603a11" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a12 - Reaching
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a12> ;
        schema:termCode "K603a12" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a13 - Stooping
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a13> ;
        schema:termCode "K603a13" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603a14 - Keyboarding
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603a14> ;
        schema:termCode "K603a14" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603b01 - Carrying
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603b01> ;
        schema:termCode "K603b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603b02 - Lifting
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603b02> ;
        schema:termCode "K603b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603b03 - Pulling
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603b03> ;
        schema:termCode "K603b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603b04 - Pushing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603b04> ;
        schema:termCode "K603b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603c01 - Speaking
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603c01> ;
        schema:termCode "K603c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K603c02 - Visual Acuity
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K603c02> ;
        schema:termCode "K603c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604a01 - Conflict Situations
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604a01> ;
        schema:termCode "K604a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604a02 - Contact with Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604a02> ;
        schema:termCode "K604a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604a03 - Coordinating or Leading Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604a03> ;
        schema:termCode "K604a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604a04 - Deal With External Customers
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604a04> ;
        schema:termCode "K604a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604a05 - Work with Work Group or Team
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604a05> ;
        schema:termCode "K604a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604a06 - Deal with Physically Aggressive People
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604a06> ;
        schema:termCode "K604a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604a07 - Dealing With Unpleasant or Angry People
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604a07> ;
        schema:termCode "K604a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604b01 - Electronic Mail
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604b01> ;
        schema:termCode "K604b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604b02 - Face-to-Face Discussions
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604b02> ;
        schema:termCode "K604b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604b03 - Written Communications
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604b03> ;
        schema:termCode "K604b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604b04 - Public Speaking
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604b04> ;
        schema:termCode "K604b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604b05 - Telephone
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604b05> ;
        schema:termCode "K604b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604b06 - Videoconference
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604b06> ;
        schema:termCode "K604b06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604c01 - Responsibility for Outcomes and Results of Other Workers
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604c01> ;
        schema:termCode "K604c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K604c02 - Responsible for Others' Health and Safety
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K604c02> ;
        schema:termCode "K604c02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701a01 - Getting Information
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701a01> ;
        schema:termCode "K701a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701a02 - Monitoring Processes, Materials, or Surroundings
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701a02> ;
        schema:termCode "K701a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701a03 - Document Use
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701a03> ;
        schema:termCode "K701a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701a04 - Information Synthesis
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701a04> ;
        schema:termCode "K701a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701a05 - Comparing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701a05> ;
        schema:termCode "K701a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701a06 - Analyzing Data or Information
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701a06> ;
        schema:termCode "K701a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701a07 - Developing Technical Instructions
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701a07> ;
        schema:termCode "K701a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701a08 - Clerical Activities
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701a08> ;
        schema:termCode "K701a08" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701b01 - Identifying Objects, Actions, and Events
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701b01> ;
        schema:termCode "K701b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701b02 - Estimating the Quantifiable Characteristics
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701b02> ;
        schema:termCode "K701b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701b03 - Inspecting Equipment, Structures, or Material
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701b03> ;
        schema:termCode "K701b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K701b04 - Processing Information
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K701b04> ;
        schema:termCode "K701b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a01 - Handling and Moving Objects
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a01> ;
        schema:termCode "K702a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a02 - Operating Vehicles, Mechanized Devices, or Equipment
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a02> ;
        schema:termCode "K702a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a03 - Constructing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a03> ;
        schema:termCode "K702a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a04 - Controlling Machines and Processes
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a04> ;
        schema:termCode "K702a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a05 - Manipulating - Operating
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a05> ;
        schema:termCode "K702a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a06 - Sorting
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a06> ;
        schema:termCode "K702a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a07 - Catering
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a07> ;
        schema:termCode "K702a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a08 - Performing Janitorial Services
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a08> ;
        schema:termCode "K702a08" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702a09 - Performing General Physical Activities
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702a09> ;
        schema:termCode "K702a09" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702b01 - Debugging and Reprogramming
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702b01> ;
        schema:termCode "K702b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702b02 - Artistic Designing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702b02> ;
        schema:termCode "K702b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702b03 - Electronic Maintenance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702b03> ;
        schema:termCode "K702b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702b04 - Interacting with Computers
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702b04> ;
        schema:termCode "K702b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702b05 - Mechanical Maintenance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702b05> ;
        schema:termCode "K702b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K702b06 - Writing or Composing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K702b06> ;
        schema:termCode "K702b06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703a01 - Judging Quality
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703a01> ;
        schema:termCode "K703a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703a02 - Evaluating Information to Determine Compliance
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703a02> ;
        schema:termCode "K703a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703a03 - Calculating
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703a03> ;
        schema:termCode "K703a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703b01 - Making Decisions
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703b01> ;
        schema:termCode "K703b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703b02 - Thinking Creatively
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703b02> ;
        schema:termCode "K703b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703b03 - Developing Objectives and Strategies
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703b03> ;
        schema:termCode "K703b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703b04 - Applying New Knowledge
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703b04> ;
        schema:termCode "K703b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703b05 - Examining and Diagnosing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703b05> ;
        schema:termCode "K703b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703b06 - Managing Resources
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703b06> ;
        schema:termCode "K703b06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703b07 - Planning and Organizing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703b07> ;
        schema:termCode "K703b07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K703b08 - Scheduling Work and Activities
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K703b08> ;
        schema:termCode "K703b08" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a01 - Communicating with Coworkers
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a01> ;
        schema:termCode "K704a01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a02 - Coordinating the Work and Activities of Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a02> ;
        schema:termCode "K704a02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a03 - Facilitating Group Discussion
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a03> ;
        schema:termCode "K704a03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a04 - Interpreting the Meaning of Information for Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a04> ;
        schema:termCode "K704a04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a05 - Protecting and Enforcing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a05> ;
        schema:termCode "K704a05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a06 - Communicating with Persons Outside Organization
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a06> ;
        schema:termCode "K704a06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a07 - Establishing and Maintaining Interpersonal Relationships
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a07> ;
        schema:termCode "K704a07" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a08 - Selling or Influencing Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a08> ;
        schema:termCode "K704a08" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a09 - Performing for or Working Directly with the Public
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a09> ;
        schema:termCode "K704a09" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a11 - Interviewing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a11> ;
        schema:termCode "K704a11" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704a12 - Assisting and Caring for Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704a12> ;
        schema:termCode "K704a12" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704b01 - Coaching and Developing Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704b01> ;
        schema:termCode "K704b01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704b02 - Providing Consultation and Advice
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704b02> ;
        schema:termCode "K704b02" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704b03 - Resolving Conflicts and Negotiating with Others
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704b03> ;
        schema:termCode "K704b03" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704b04 - Supervising Subordinates
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704b04> ;
        schema:termCode "K704b04" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704b05 - Team Building
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704b05> ;
        schema:termCode "K704b05" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704b06 - Training and Teaching
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704b06> ;
        schema:termCode "K704b06" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
        schema:status   "not validated"
    ] ;

    # K704c01 - Staffing
    schema:hasDefinedTerm [
        a schema:DefinedTerm ;
        schema:inDefinedTermSet <dna:#K704c01> ;
        schema:termCode "K704c01" ;
        schema:ratingValue "0" ;
		schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/memory/longterm/79a65b9a-7bd2-4605-ac8e-6a89d8ff720a.ttl> ;
		schema:validFrom "2025-04-24T153045Z"^^xsd:dateTime ;
    ] .
```

**Fields Description**

Each indicator is represented using the same data structure described below:

* **schema:inDefinedTermSet** - Link to the attribute definition in .WorkDNA-Definitions.ttl file
* **schema:termCode** - Acronym
* **schema:ratingValue** - Attribute values
* **schema:subjectOf** - Link to the memory file that last changed the attribute
* **schema:validFrom** - Timestamp of the last change (Format: YYYY-MM-YYThhmmssZ)

### PAI.ttl

**File Location**

<User's POD>/KarreraAI/chatAI

**Description**

This file stores the list of CHATs created by the user.

**File Structure**

```ttl title="PAI.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <http://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/chatAI/PAI.ttl>
  a schema:CreativeWork ;
  schema:hasPart </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/chatAI/a3932b42-f7d5-4ec2-b3f2-95a9dac0b06a.ttl> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/chatAI/a3932b42-f7d5-4ec2-b3f2-95a9dac0b06a.ttl>
  a schema:Conversation ;
  schema:dateCreated "2025-03-14T16:39:28Z"^^xsd:dateTime ;
  schema:abstract "Experience exploration" ;
  schema:keywords "career-guidance" ;
  schema:creativeWorkStatus "Initiated" .
```

**Fields Description**

* **schema:hasPart** - List of links to all chats created by the user
* **schema:dateCreated** - Creation date timestamp (Format: YYYY-MM-DDThh:mm:ssZ)
* **schema:abstract** - chat titles
* **schema:keywords** - chat template. It can be one of the following values:
    * **WorkDNA Analysis** - Get insights about your professional competencies and career alignment
    * **Career Path Guidance** - Explore career opportunities and professional developmant strategies
    * **Project Collaboration** - Get advice on team formation, project management and collaborative workflows
    * **Learning & Development** - Personalized learning recommendations and skill development strategis
    * **General Professional Assistant** - General professional advice and platform guidance
    * **Career Interviewer** - Professional career interview to gather comprehensive information about your journey
* **schema:creativeWorkStatus** - AI chat status. It can be one of the following values:    
   * **Initiated** - Chat was initiated

### MSG.ttl

**File Location**

<User's POD>/KarreraAI/chatAI

**Description**

This file stores the content of the CHATs created by the user.

**File Structure**

```ttl title="MSG.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <http://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .
@prefix usr:     <https://id.inrupt.com/karrera51> .
@prefix ai:      <https://id.inrupt.com/KarreraAI> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/chatAI/a3932b42-f7d5-4ec2-b3f2-95a9dac0b06a.ttl>
  a schema:Conversation ;
  schema:abstract "Experience exploration" ;
  schema:hasPart <#m0>, <#m1> , <#m2> .

<#m0>
  a schema:Message ;
  schema:sender <ai:> ;
  schema:recipient <usr:> ;
  schema:datePublished "2025-03-14T16:40:08Z"^^xsd:dateTime ;
  schema:text "Hi Silvia, can you tell us more about your experience in etnoarqueologia? What inspired you to pursue this field of study?" ;
  schema:creativeWorkStatus "Pending" .

<#m1>
  a schema:Message ;
  schema:sender <usr:> ;
  schema:recipient <ai:> ;
  schema:datePublished "2025-03-14T16:40:14Z"^^xsd:dateTime ;
  schema:text "Working with Brazilian indian culture was always a fascinating subject" ;
  schema:creativeWorkStatus "Pending" .

<#m2>
  a schema:Message ;
  schema:sender <ai:> ;
  schema:recipient <usr:> ;
  schema:datePublished "2025-03-14T16:40:20Z"^^xsd:dateTime ;
  schema:text "It sounds like your work with Brazilian indigenous cultures has been a significant part of your etnoarqueologia research. Have you had the opportunity to collaborate with indigenous communities directly in your research, or is your work more focused on analyzing and interpreting existing data?" ;
  schema:creativeWorkStatus "Pending" .
```

**Fields Description**

* **schema:hasPart** - List of links to all messages created by the user
* **schema:sender** - Sender WebID
* **schema:recipient** - Recipient WebID
* **schema:datePublished** - Publushing date timestamp (Format: YYYY-MM-DDThh:mm:ssZ)
* **schema:text** - Message content
* **schema:creativeWorkStatus** - Message status. It can be one of the following values:
    * **Pending** - Message was not sent to AI extraction process queue
    * **Processing** - Message was sent to AI extraction process queue
    * **Finished** - Message was processed by AI extraction process

### PI-history.ttl

**File Location**

<User's POD>/KarreraAI/personas/main

**Description**

This file description.

**File Structure**

```ttl title="PI-History.ttl" linenums="1"
  schema
```

**Fields Description**

* **schema:hasPart** - 

### PI.ttl

**File Location**

<User's POD>/KarreraAI/personas/main

**Description**

This file stores the Personal Information (PI) profile for the main persona, containing comprehensive personal, professional, educational, and interest-related data.

**File Structure**

```ttl title="PI.ttl" linenums="1"
PREFIX :       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/PI.ttl#>
PREFIX id:     <https://id.inrupt.com/>
PREFIX schema: <http://schema.org/>
PREFIX pi:     </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/PI.ttl#>
PREFIX xsd:    <http://www.w3.org/2001/XMLSchema#>
PREFIX esco:   <http://data.europa.eu/esco/model#>
PREFIX skos:   <http://www.w3.org/2004/02/skos/core#>

id:karrera51 a schema:Person ;
    schema:address           pi:location ;
    schema:id               "a7bcfbf7-92bd-4cbe-96e9-2ee737970e26" ;
    schema:name             "Karrera Boa Ideia" ;
    schema:taxID             "CPF" ;
    schema:award             <#5a76042d-489f-4c46-8ebc-4ec5037e2a7c> ;
    schema:birthDate        "2000-10-20"^^xsd:date ;
    schema:description      <#ba67321f-ab5b-4b38-8d65-8e6d9da6a020> ; #Biography generated by AI agent
    schema:email            "conta51@karrera.ai";
    schema:jobTitle         <#77268671-1cf3-4cc8-92c3-0d9598935c7b> ; #Current Job. The code comes from Karrera Ocuppation Database
    schema:hasOccupation     <#9853d312-e078-46a3-a296-034aac1a78fa> ,
                            <#c42a6385-876b-4ac0-92ec-4c74a6197091> ; #Past Jobs. The code comes from Karrera Ocuppation Database
    schema:hasCredential    <#c160b433-0709-4bfa-92c6-30a3e9cc224e> ,
                            <#af443277-c582-4e41-98c5-9cbf5e570447> ,
                            <#99480e94-308a-4fb4-a128-61c3b79adfa0> ;
    schema:image            </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/avatar.jpg> ;
    schema:knows            </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/.person-index.ttl> , 
                            </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/.organization-index.ttl> ;
    schema:knowsAbout       <#bd22ed83-213d-4bae-b9c3-67121733e071> , #Hobby
                            <#07c2737f-f25b-4cc9-b1f6-263a883efa73> , #Skill
                            <#aa4d5c58-c3a0-43f3-b22f-f8a7bb07be8b> ; #Interests
    schema:knowsLanguage    <#4781712a-f51f-4fad-9251-1e5915f429e3> ,
                            <#90ed5f03-9dbe-43a2-8d25-ba68d13086c7> ,
                            <#ebc96cc3-d561-4983-bee7-b4a4f59948b8> ;
    schema:workExample      </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/.project-index.ttl> , 
                            <#56a59ced-53d7-4a28-8017-4ef6b26327bd> , #MusicAlbums
                            <#744f1a37-7b5c-4c42-ba95-d6dc0a0a19eb> , #MusicRecordings
                            <#3abd8b65-53b4-49fe-b245-4d166a68ffb5> , #Seasons
                            <#ac11efbf-d651-4d00-b029-1d3e68d9ae2e> , #Movies_ID
                            <#fa17e4de-98b0-468b-81dd-dce226b5c405> , #Episodes_ID
                            <#4faa1717-34f3-4cd0-8591-d06e0286b819> , #PodcastEpisodes 
                            <#49e895a8-4f18-4490-b3eb-47dee4123177> , #Articles_ID
                            <#f5a5b57f-ae9f-4fca-911d-667d64816c8e> ; #Books_ID
    schema:sameAs           </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/WorkDNA.ttl> ;
    schema:identifier       </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/personas/main/CCIH.ttl> . 

pi:location  a                  schema:PostalAddress ;
        schema:addressCountry   "Brazil";
        schema:addressLocality  "Cotia";
        schema:addressRegion    "São Paulo";
        schema:subjectOf        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom        "2025-07-30T12:00:00.000Z"^^xsd:dateTime .

<#4781712a-f51f-4fad-9251-1e5915f429e3> 
    a schema:Language ;
    schema:name "English" ;
    schema:additionalProperty   [
                                a schema:PropertyValue ;
                                schema:name "Proficience Level" ;
                                schema:value "Fluent"
                                ] .

<#90ed5f03-9dbe-43a2-8d25-ba68d13086c7>
    a schema:Language ;
    schema:name "Spanish" ;
    schema:additionalProperty   [
                                a schema:PropertyValue ;
                                schema:name "Proficience Level" ;
                                schema:value "Beginner"
                                ] .

<#ebc96cc3-d561-4983-bee7-b4a4f59948b8>
    a schema:Language ;
    schema:name "Portuguese" ;
    schema:additionalProperty   [
                                a schema:PropertyValue ;
                                schema:name "Proficience Level" ;
                                schema:value "Mother Language"
                                ] .

<#07c2737f-f25b-4cc9-b1f6-263a883efa73>
        a                           skos:Concept , esco:Skill;

        schema:proficiencyLevel    "20%";
        schema:alternateType       "knowledge";
        schema:startDate           "2015"^^xsd:date ;
        schema:name                "Project Management" ; #This name is how the knowledge was found in user documentation
        skos:prefLabel             "Project Management" ; #This name comes from Karrera Capabilities database
        schema:id                  "123456" ; #ID from Karrera Capabilities Database
        schema:url                 <http://data.europa.eu/esco/skill/7111b95d-0ce3-441a-9d92-4c75d05c4388> ;
        schema:subjectOf           </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/ee4b0c1d-0624-426c-ac18-7073647a4edf.ttl> ;
        schema:validFrom           "2025-04-27T12:00:00.000Z"^^xsd:dateTime .

<#c42a6385-876b-4ac0-92ec-4c74a6197091>
a       skos:Concept , esco:Occupation ;
        schema:name       "Infrastructure Manager" ; #This name is how the occupation was found in user documentation
        schema:id         "20012.0.0045" ;
        schema:startDate  "2010"^^xsd:date ;
        schema:endDate    "2015"^^xsd:date ;
        schema:worksFor   "Dresdner Bank" ;
        schema:description "Restructured the technology department, leading a team of 18 professionals responsible for support services to internal clients, voice and data, IT infrastructure; supporting business processes and the development of applications. Was responsible for the department’s budget process and the annual monitoring of expenses pertaining to the bank’s technology department." ;
        schema:url        <https://noc.esdc.gc.ca/OaSIS/OaSISOccProfile?code=21222.00&version=2023.0> ;
        schema:subjectOf  </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom  "2025-04-27T12:00:00.000Z"^^xsd:dateTime ;
        skos:prefLabel    "information technology (IT) infrastructure engineering manager" . #This name is taken from Karrera database

<#77268671-1cf3-4cc8-92c3-0d9598935c7b>
        a                 skos:Concept , esco:Occupation ;
        schema:name       "Senior Project Manager" ; #This name is how the occupation was found in user documentation
        schema:id         "21222.0.0039" ;
        schema:startDate  "2015"^^xsd:date ;
        schema:endDate    ""^^xsd:date ;
        schema:worksFor   "SocialTech Inc." ;
        schema:description "- Led product for flagship social app, growing DAU 40% in 18 months. - Shipped major video features adopted by 70% of users. - Managed 5 PMs and 30-engineer squad." ;
        schema:url        <https://noc.esdc.gc.ca/OaSIS/OaSISOccProfile?code=21222.00&version=2023.0> ;
        schema:subjectOf  </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom  "2025-04-27T12:00:00.000Z"^^xsd:dateTime ;
        skos:prefLabel    "Technical Project Manager" . #This name is taken from Karrera database

<#c160b433-0709-4bfa-92c6-30a3e9cc224e>  a  schema:EducationalOccupationalCredential , esco:Qualification ;
        schema:educationalLevel    "Bachelor degree" ;
        schema:startDate           "1987-01-01"^^xsd:date ;
        schema:endDate             "1992-12-30"^^xsd:date ;
        schema:recognizedBy        <a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/organization/c160b433-0709-4bfa-92c6-30a3e9cc224e.ttl> ;
        schema:name                "Mechanical Engineering" ; #This name comes from Karrera database
        schema:subjectOf           </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom           "2025-07-30T12:00:00.000Z"^^xsd:dateTime .

<#af443277-c582-4e41-98c5-9cbf5e570447>  a  schema:EducationalOccupationalCredential , esco:Qualification ;
        schema:educationalLevel    "Master degree" ;
        schema:startDate           "2008-01-01"^^xsd:date ;
        schema:endDate             "2008-12-30"^^xsd:date ;
        schema:recognizedBy        <a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/organization/af443277-c582-4e41-98c5-9cbf5e570447.ttl> ;
        schema:name                "MBA Tecnologia da Informação" ;
        schema:subjectOf           </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom           "2025-07-30T12:00:00.000Z"^^xsd:dateTime .

<#99480e94-308a-4fb4-a128-61c3b79adfa0>  a  schema:EducationalOccupationalCredential , esco:Qualification ;
        schema:educationalLevel    "Technical Course" ;
        schema:startDate           "2010-01-01"^^xsd:date ;
        schema:endDate             "2010-06-30"^^xsd:date ;
        schema:recognizedBy        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/organization/99480e94-308a-4fb4-a128-61c3b79adfa0.ttl> ;
        schema:name                "Financial Market Trader" ;
        schema:subjectOf           </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom           "2025-07-30T12:00:00.000Z"^^xsd:dateTime .

<#ba67321f-ab5b-4b38-8d65-8e6d9da6a020>
        a                          schema:Text ;
        schema:alternateName       "Biography" ;
        schema:text                "Carlos Fucci, a seasoned technology executive with 31 years of experience, has had a distinguished career in various leadership roles. With a strong educational background from Poli Usp, Escola De Engenharia Mauá, and Financial Market Trader Course, he has developed a unique blend of technical expertise and business acumen.\n\nThroughout his career, Carlos has worked with prominent organizations such as Cpqi, Pricewaterhousecoopers, Interactive Brokers, Royal Bank Of Scotland, Banco Dresdner, Banco Merrill Lynch, Jpmorgan, and Wittel Comunicações. His extensive experience in ITIL and Mcafee (Endpoint Security and Web Filtering) has enabled him to drive strategic initiatives and deliver results-driven solutions.\n\nAs a seasoned professional with a wealth of knowledge and expertise, Carlos is well-positioned to continue making significant contributions to the technology industry. Notably, his early experience as a Cyber Security Manager at MUFG played a crucial role in shaping his career. In this role, he successfully cleared audit issues, demonstrating his ability to overcome specific challenges.\n\nCarlos has also led notable projects, such as the successful migration of Banco Dresdner's office systems. As Technology Executive and CIO, he was responsible for overseeing the project's execution and ensuring its success. His experience in this area highlights his leadership skills and ability to drive complex initiatives forward.\n\nOverall, Carlos' unique blend of technical expertise, business acumen, and leadership abilities make him a valuable asset to any organization seeking innovative solutions and strategic guidance." ;
        schema:subjectOf           </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom           "2025-07-30T12:00:00.000Z"^^xsd:dateTime .

<#9853d312-e078-46a3-a296-034aac1a78fa>
        a                 skos:Concept , esco:Occupation ;
        schema:name       "CISO" ;
        schema:id         "20012.0.0026" ;
        schema:startDate  "2016"^^xsd:date ;
        schema:endDate    "2024"^^xsd:date ;
        schema:worksFor   "MUFG" ;
        schema:description "Responsible for managing a team of Cybersecurity specialists. I handle requests from US and Japan teams to ensure standards and controls are aligned with the company's global strategy. In this last year we have already eliminated around 22 audit issues that were not addressed for over 5 years. New controls related to Vulnerability Management, Identity Management and Configuration Management were implemented. All Security Policies were revised to cover Resolution 4,893 of Brazilian Central Bank and LGPD (“Lei Geral de Proteção de Dados”). These are some of the applications we use to support our environment: Splunk (Core and Enterprise Security), Varonis, McAfee (Endpoint Security and Web Filtering), Imperva (WAF and DAM), Cyberark and Qualys." ;
        schema:url        <https://noc.esdc.gc.ca/OaSIS/OaSISOccProfile?code=20012.00&version=2023.0> ;
        schema:subjectOf  </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom  "2025-07-30T12:00:00.000Z"^^xsd:dateTime ;
        skos:prefLabel    "Cybersecurity Manager" .
       
<#56a59ced-53d7-4a28-8017-4ef6b26327bd>
        a                   schema:MusicAlbum ;
        schema:author       <https://id.inrupt.com/karrera51> ;
        schema:name         "2020 Best Songs" ;
        schema:dateCreated  "2020-02-20"^^xsd:date ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/approved/23648efe-cefa-400a-8f0f-93aa544f1694.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime .

<#744f1a37-7b5c-4c42-ba95-d6dc0a0a19eb>
        a              schema:MusicRecording ;
        schema:author  <https://id.inrupt.com/karrera51> ;
        schema:name    "Festa de Arromba" ;
        schema:inAlbum  <#56a59ced-53d7-4a28-8017-4ef6b26327bd> ;
        schema:dateCreated  "2001-02-20"^^xsd:date ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime .

<#3abd8b65-53b4-49fe-b245-4d166a68ffb5>
        a              schema:Season ;
        schema:author  <https://id.inrupt.com/karrera51> ;
        schema:name    "Wandinha: Temporada 2" ;
        schema:dateCreated  "2025-08-06"^^xsd:date ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom    "2025-08-24T153045Z"^^xsd:dateTime .

<#ac11efbf-d651-4d00-b029-1d3e68d9ae2e>
        a              schema:Movie ;
        schema:author  <https://id.inrupt.com/karrera51> ;
        schema:name    "O Poderoso Chefão" ;
        schema:dateCreated  "1972-07-07"^^xsd:date ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime .

<#fa17e4de-98b0-468b-81dd-dce226b5c405>
        a              schema:Episode ;
        schema:author  <https://id.inrupt.com/karrera51> ;
        schema:name    "Mais desgosto" ;
        schema:dateCreated  "2025-02-06"^^xsd:date ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime .

<#4faa1717-34f3-4cd0-8591-d06e0286b819>
        a              schema:PodcastEpisode ;
        schema:author           <https://id.inrupt.com/karrera51> ;
        schema:name             "Podcast Conexão Servidor - EP#02 - Automação no INSS: avanços, desafios e impactos" ;
        schema:episodeNumber    "02" ;
        schema:url              <https://www.youtube.com/watch?v=cyt1kRGR2WQ&t=12s> ;
        schema:dateCreated      "2025-02-06"^^xsd:date ;
        schema:subjectOf        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom        "2025-04-24T153045Z"^^xsd:dateTime .

<#49e895a8-4f18-4490-b3eb-47dee4123177>
        a              schema:Article ;
        schema:author       <https://id.inrupt.com/karrera51> ;
        schema:name         "Estudo sobre as Diversidades de Gêneros" ;
        schema:url          </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/artifacts/RelatorioAvaliacaodeRisco.docx> ;
        schema:dateCreated  "2025-02-06"^^xsd:date ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime .

<#f5a5b57f-ae9f-4fca-911d-667d64816c8e>
        a              schema:Book ;
        schema:author       <https://id.inrupt.com/karrera51> ;
        schema:name         "A Volta ao Mundo em 80 Dias" ;
        schema:isbn         "9791041946525" ;
        schema:dateCreated  "2025-02-06"^^xsd:date ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime .

<#5a76042d-489f-4c46-8ebc-4ec5037e2a7c>
        a            esco:Qualification , schema:Text ;
        schema:name  "Nobel Prize in Physics" ;
        schema:recognizedBy "Nobel" ;
        schema:dateCreated  "2009-08-08"^^xsd:date ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime .

<#bd22ed83-213d-4bae-b9c3-67121733e071>
        a                     schema:Thing ;
        schema:alternateType    "Hobbies" ;
        schema:name             "Play Guitar" ;
        schema:subjectOf        </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom        "2025-04-24T153045Z"^^xsd:dateTime .

<#aa4d5c58-c3a0-43f3-b22f-f8a7bb07be8b>
        a                     schema:Thing ;
        schema:alternateType  "Interests" ;
        schema:name           "Global Warming" ;
        schema:subjectOf    </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/memory/a708ffc7-1268-44fd-9ba8-093f0d52c9fd.ttl> ;
        schema:validFrom    "2025-04-24T153045Z"^^xsd:dateTime .
```

**Fields Description**

* **Core Personal Information:**

    * **schema:id** - Unique identifier for the persona
    * **schema:name** - Full name of the person
    * **schema:birthDate** - Date of birth (YYYY-MM-DD format)
    * **schema:email** - Primary email address
    * **schema:taxID** - Tax identification number type. (In Brazil we will use CPF)
    * **schema:image** - Link to profile avatar image
    * **schema:sameAs** - Link to WorkDNA data file
    * **schema:identifier** - Link to CCIH indicators file

* **Location Information:**

    * **schema:address** - Reference to postal address object containing:

        * **schema:addressCountry** - Country name
        * **schema:addressLocality** - City name
        * **schema:addressRegion** - State/region name
        * **schema:validFrom** - Timestamp when address became valid (YYYY-MM-DDThh:mm:ssZ format)

* **Professional Information:**

    * **schema:jobTitle** - Current occupation (linked to detailed occupation object)
    * **schema:hasOccupation** - Previous employment history (multiple entries linked to detailed occupation object)
    * **schema:hasCredential** - Educational qualifications and certifications
    * **schema:workExample** - Portfolio items including projects, publications, and creative works (Creative works use appropriate schema.org types: MusicAlbum, Article, Book, etc.)
    * **schema:award** - Honors and recognitions received

* **Skills & Knowledge:**

    * **schema:knowsLanguage** - Language proficiencies with skill levels
    * **schema:knowsAbout** - Skills, hobbies, and interests
    * **schema:description** - Biography and professional summary

* **Social & Network Data:**

    * **schema:knows** - Links to person and organization indexes (.person-index.ttl and .organization-index.ttl)

* **System Integration:**
    
    * **schema:subjectOf** - References to narrative memory files throughout (provides audit trail)
    * **schema:validFrom** - Timestamp of last update (Format: YYYY-MM-DDThhmmssZ)

### item.ttl

**File Location**

<User's POD>/KarreraAI/narrative/item/<status>

The item is stored in a differente folder depending on its status. It can be oen of the following:
    * **approved** - Items that are waiting for revision/approval
    * **discarded** - Items that were discarded
    * **pending** - Items approved. They are now part of Long-term memories

**Description**

This file is used to store a memory item. The content of the item file is a small set of a **PI.ttl** file

**File Structure**

```ttl title="item.ttl" linenums="1"
@prefix dcterms:    <http://purl.org/dc/terms/> .
@prefix esco:       <http://data.europa.eu/esco/model#> .
@prefix schema:     <http://schema.org/> .
@prefix skos:       <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix pi:         </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/11c741e6-3f7c-4919-9334-8d3118ae6bec.ttl#> .

<https://id.inrupt.com/futika>
        a                     schema:Person; 
        schema:hasCredential  <#2859d4d6-0404-4f0c-9b8e-96478c043075> .

<#2859d4d6-0404-4f0c-9b8e-96478c043075>
        a                           esco:Qualification , schema:EducationalOccupationalCredential;
        schema:additionalProperty  [ a              schema:PropertyValue;
                                     schema:name:   "Nivel de Conhecimento";
                                     schema:value:  "1"
                                   ];
        schema:educationalLevel    "Bachelor degree" ;
        schema:startDate           "2001"^^xsd:date ;
        schema:endDate             "2005"^^xsd:date ;
        schema:recognizedBy        "UC Berkeley" ;
        schema:name                "Economics";
        schema:subjectOf           </a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/narrative/item/pending/11c741e6-3f7c-4919-9334-8d3118ae6bec.ttl>;
        schema:status              "pending" .
```

**Fields Description**

Since the item is a small set of a PI.ttl file, the content is explained on PI.ttl section.

### organization.ttl

**File Location**

<User's POD>/KarreraAI/relationship/organization

**Description**

This file is used to store Organization information.

**File Structure**

```ttl title="organization.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <http://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/organization/99480e94-308a-4fb4-a128-61c3b79adfa0.ttl>
        a                     schema:Organization ;
        
        schema:id             "99480e94-308a-4fb4-a128-61c3b79adfa0" ;
        schema:legalName      "Saint Paul Escola de Negócios" .
```

**Fields Description**

* **schema:id** - Organization ID. It is a UUID to guarantee the id is unique
* **schema:legalName** - Organization legal name

### person.ttl

**File Location**

<User's POD>/KarreraAI/relationship/person

**Description**

This file is used to store Person information. It can be a small PI.ttl.

**File Structure**

```ttl title="person.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <http://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/relationship/person/fdad4928-35a7-45dd-ae24-198bd8264b45.ttl>
        a                     schema:Person ;
        schema:id             "fdad4928-35a7-45dd-ae24-198bd8264b45" ;
        schema:name           "Ester Lima" .
```

**Fields Description**

* **schema:id** - Person ID. It is a UUID to guarantee the id is unique
* **schema:name** - Person name

### project.ttl

**File Location**

<User's POD>/KarreraAI/relationship/project

**Description**

This file is used to store projects information.

**File Structure**


```ttl title="project.ttl" linenums="1"

  The file format is under contruction

```

**Fields Description**

!!! note "Under Construction"

    File content is Under Construction
