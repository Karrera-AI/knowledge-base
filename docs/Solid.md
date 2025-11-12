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

* **dcterms:date** - Last modified date

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
* **schema:datePublished** - Date and Time when the file was uploaded (Format: YYYY-MM-YYThhmmssZ) 
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
