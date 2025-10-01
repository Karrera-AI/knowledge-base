# SOLID

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
This is an excripted tar file that contains the whole **KarreraAi** folder content. It will be used as a source to restore user's data in case of file corruption and/or deletion.

**Creation Workflow Diagram**

![image info](./assets/BackupFlow.jpg)
