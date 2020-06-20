# Introduction

Cognitive and clinical assessments are used throughout neuroscience. Despite many efforts ([Cognitve Atlas](https://www.cognitiveatlas.org/), [Cognitive Paradigm Ontology](http://www.cogpo.org/), [OOve]( ??? )) there is little consistency exists in assessment data acquisition or response representation across studies. Each project tends to use its own schema, format and data collection tool (paper, form, ...). This highlights the need for harmonization across projects. However, harmonizing data after acquisition is resource intensive. Currently, the NIMH Data Archive (NDA) enforces harmonization during data submission and this approach can create a mismatch between collected and submitted data.

Reverse engineering the NDA data dictionaries to their original assessments using a tool like Brainverse can be tedious. Thus to enforce consistency at the data acquisition stage, we created a standard schema and a set of reusable common assessments. The schema extends and modifies the [CEDAR metadata representation]( ??? ).

Using JSON-LD, we represent:

-   `Items` - elements of individual assessments, e.g an single question in a questionaire
-   `Activities` - individual assessments, e.g a whole questionaire
-   `Protocols` - collections of activities performed by a participant, e.g a set o questionaire that was used in a study.

An implementation of the schema can specify:

-   scoring logic, how the total score to the responses on a questionaire should be computed
-   branching logic,
-   user interface rendering options.

This schema :

-   allows internationalization (i.e having the same questionaire in multiple languages),
-   is implementation agnostic (no matter if the app used to render the questionaire is written in javascript, python...),
-   tracks variations in assessments (e.g., PHQ-9, PHQ-8).

This open and accessible schema library with appropriate conversion (e.g., to RedCap) and data collection tools (e.g., [MindLogger](https://mindlogger.org/), LORIS, RedCap) enables more consistent acquisition across projects, with results being harmonized by design.

<!-- ## Need for Standardizing assessments
  - Harmonize large projects
    - ABCD
    - CONP
- Collaborations: ABCD, Healthy Brain Network, LORIS/CONP -->

## Advantages of current representation

- Rich contexts with JSON-LD
  - Redcap uses CSVs to represent forms
- Single source of curated assessments from [ReproNim](https://github.com/ReproNim)
- Each Item, Activity, and Protocol provide unique and persistent identifiers
- Variations can be tracked (e.g., PHQ-9, PHQ-8)
- Allows, supports, and tracks internationalization (ABCD requires Spanish and English forms)
- Implementation agnostic – schema can be used by several software
- Still a linked data graph and can be validated using [SHACL](https://www.w3.org/TR/shacl/)

## Schema

We have defined 3 different types of schema

-   [Protocol](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Protocol)
-   [Activity](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Activity)
-   [Item](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Field)

### Schema overall structure

- protocol directory structure: name the directory in the `CamelCase` naming convention. It contains the following:
  - `protocolName_schema` : schema to define the protocol
  - `protocolName_context` : context to define keys used specific to the protocol schema
- activity directory structure: name the directory with name of activity in the CamelCase naming convention. It contains the following:
  - `/items`: directory containing the jsonld files for individual items of the activity schema
    - `item_1`
    - ...
  - `activityName_schema` : schema to define the activity
  - `activityName_context` : context to define keys used specific to the activity schema
  - sub-activity jsonld schemas (if any)

Note: All schema and context files above are saved without a `.jsonld` files extension.

The generic keys are defined in the generic context file (contexts/generic)
