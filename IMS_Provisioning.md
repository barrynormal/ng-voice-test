
# IMS Provisioning Process documentation 

## Introduction

This document is split into two sections.

**Section 1**, 'Discovery', is designed to answer some questions regarding the required documentation. 

These are:
1. Who will be using this information? 
  * Internal/external/devs/ops etc...
  * Do these audiences interact? For example, who provides engineering with new request?
  * Relative levels of technical knowledge

2. The context into which this process fits
  * The nature of the issues raised by clients/users
  * How the system is connected to and updated
  * How tests can be performed to verify everything is as it should be
  * The relationship between this system and other ng-voice components
  * The full list of things managed by this (or similar) process

3. The best structure for the documentation
  * Do we need separate pieces for technical and non-technical audiences *(Probably not)*
  * How much can we rely on diagrams *(depends on level of complexity)*
  * To what extent is it possible to provide an example solution which will cover all cases? 
  * Related docs and processes to be linked  *(such as standards and other internal processes)*

**Section 2**, 'Basic structure', gives a first draft for the documentation. 

> **Note.** The ambition is to provide clarity. So, if a step by step walk through of any process can be supplied, it should be. Though always within context.


## 1. Discovery

### From Support team
As usual, first port of call would be an orientation call to discover any ongoing issues from the Support team. 
  * How could this process work better for you?

  * Details of incoming request - frequency, etc. Are there any triggers, like network load, etc?
  * Who makes these requests? Make sure to understand the full audience. Their needs and technical competence.
  * Describe the issue or issues as stated by users? Are there more than one? List them. Make sure to catch edge cases.
  * What is the resolution? Do you have a standard doc you send out?
  * How successful is the resolution?
  * Do you get repeat requests from same clients or does the first interaction solve the issue?

### From Engineering team
As usual, first port of call would be an orientation call to discover any ongoing issues from the Engineering team. 
  * How could this process work better for you?

1. Outline of the process of IMS Core supplementary service provisioning in detail. 

The goal of producing:
  * A diagram which outlines basic flow of data/requirements for the set up. This needs to be accurate but intelligible without being an engineer. 
> The goal of this diagram is to align all teams (internal and external) on the high level mental model of the product and process.

  * A more detailed diagram which focuses on clarifying where the problem areas are in this flow and indicates the appropriate solutions/documents.
> This will give engineers (internal and external) a reference point for their own implementation and any conversations needed to further clarify. eg: 'we get to step 4 and the connection is rejected'

  * A clear step by step flow for each participant. 
> This supplements the previous engineering diagram, outlines numbered steps, provides test scripts and examples for all use cases.


### From Operations team
As usual, first port of call would be an orientation call to discover any ongoing issues from the Ops team. 
  * How could this process work better for you?

Taking the engineering diagram and process, we can discuss higher level business processes which encapsulate the engineering. 

The result should be a clarification/enlargement of context for:
1. The high level engineering flow diagram
2. The Step-by-step engineering process


### From General research
Collect links and snippets to provide good descriptions of the various acronyms and technologies involved: HSS, SSD, Sh Interface, Diameter etc...


## 2. Basic structure

### Introduction
  * What is IMS Core Supplementary service provisioning ? 
  * Who should care, how this document helps.
  * How to use this doc.
> Possibly include simple definitions of key terms, like SSD and Sh Interface. Links would suffice.

### For everyone
Outline the process from high level, using a diagram (this is place holder!)

![ Provisioning Supplementary Services ng-voice ](images/hss.png)

> Could be the process is simple enough that only one diagram is required, with links to the relevant scripts and examples? 

### Walk through the process 
1. Subscriber makes request to CRM => However this happens 
  * link to 'make a request' 
  * (Q:At what point do we go from regular text in a form to XML?)

2. Exactly how does the request get to the Provisioning Proxy? 

3. How the XML docs are manipulated over Ut Interface. And by whom 
  * [Link to example structure with notes] 
  * [link to curl template with notes]
  * [link to URL formatting and how to find/grok the various fields, like IMPU_NUMBER]
 > Testing - how does this happen?

 
4. SSD Interface, access to it, how it translates to Sh Interface. Links to more info on Sh Interface/Diameter

### Show example, with notes:
  * Enabling Call Forwarding Unconditional (CFU)

```XML
<cp:rule
  xmlns:cp="urn:ietf:params:xml:ns:common-policy"
  xmlns:ss="http://uri.etsi.org/ngn/params/xml/simservs/xcap"
  id="unconditional">
  <cp:conditions/>
  <cp:actions>
    <ss:forward-to>
      <ss:target>tel:+<FORWARDING_NUMBER></ss:target>
      <ss:notify-caller>true</ss:notify-caller>
    </ss:forward-to>
  </cp:actions>
</cp:rule>
```
> (Note: For disabling, `<cp:conditions>` would include `<ss:rule-deactivated/>`)

#### Continue example to include :
* generated curl
* expected responses?
* testing process?
* other trouble-shooting based on data from Support team.
