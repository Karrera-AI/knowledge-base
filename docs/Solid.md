# Solid

All user's information will be stored in a Solid POD. This structure will guarantee that the users's personal data are not stored in our servers and therefore prevent these information from being used without user's approval.

This data repository stores various aspects of an individual's professional and personal profile, career capital, and interactions, organized using a structured schema. The files are primarily .ttl (Turtle) files, which are a syntax for RDF (Resource Description Framework), indicating a graph-like data structure where relationships between entities are explicit.

## FOLDER STRUCTURE

The application data are stored using a folder struture as follows:

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
* .forum-index.ttl
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

**Description**

This file is used to define the **KarreraAi Data Structure** version. It will be used to check version and update the structure or reject the user depending on the situation.

**File Structure**

```ttl title=".version.ttl" linenums="1"
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix esco:    <http://data.europa.eu/esco/model#> .
@prefix schema:  <https://schema.org/> .
@prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

</a7bcfbf7-92bd-4cbe-96e9-2ee737970e26/KarreraAI/.system/.version.ttl>
        a                   schema:Dataset;
        dcterms:date        "YYYY-MM-DD"^^xsd:date;
        dcterms:hasVersion  "1.0";
        schema:description  "Este arquivo informa a versão do POD do usuário".
```
