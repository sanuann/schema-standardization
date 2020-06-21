# Introduction

??? example "Tl;DR - Advantages of the current schema representation"
    - Rich contexts for a questionaire with JSON-LD rather than a "flat" csv
    - A single source of curated assessments from [ReproNim](https://github.com/ReproNim)
    - Each Item (i.e question), Activity (i.e questionaire), and Protocol (i.e set of questionaire)
    provides unique and persistent identifiers.
    - Versions of a given questionaire can be tracked (e.g., PHQ-9, PHQ-8)
    - Allows, supports, and tracks internationalization (e.g. ABCD requires Spanish and English forms)
    - Implementation agnostic – the schema can be used by several software
    - Still a linked data graph that can be validated using [SHACL](https://www.w3.org/TR/shacl/)

Cognitive and clinical assessments are used throughout neuroscience. Despite many efforts
([Cognitve Atlas](https://www.cognitiveatlas.org/), [Cognitive Paradigm Ontology](http://www.cogpo.org/),
[OOve]( ??? )) there is little consistency exists in assessment data acquisition or response
representation across studies. Each project tends to use its own schema, format and data collection
tool (paper, form, ...). This highlights the need for harmonization across projects. However,
harmonizing data after acquisition is resource intensive. Currently, the NIMH Data Archive (NDA)
enforces harmonization during data submission and this approach can create a mismatch between
collected and submitted data.

Reverse engineering the NDA data dictionaries to their original assessments using a tool like
Brainverse can be tedious. Thus to enforce consistency at the data acquisition stage, we created
a standard schema and a set of reusable common assessments. The schema extends and modifies the
[CEDAR metadata representation]( ??? ).

Using JSON-LD, we represent:

-   `Items` - elements of individual assessments, e.g a single question in a questionaire
-   `Activities` - individual assessments that contains a set of `Items`, e.g a whole questionaire
    with a set of questions
-   `Protocols` - collections of activities performed by a participant, e.g a set of questionaire used in a study.

Each `Item`, `Activity`, and `Protocol` provides unique and persistent identifiers

An implementation of the schema can specify:

-   scoring logic, how the total score to the responses on a questionaire should be computed
-   visibility, whether a given item or activity should be displayed to the user,
-   user interface rendering options.

This schema :

-   allows internationalization (i.e having the same questionaire in multiple languages),
-   is implementation agnostic (no matter if the app used to render the questionaire is written in javascript, python...),
-   tracks variations in assessments (e.g., PHQ-9, PHQ-8).

This open and accessible schema library with appropriate conversion (e.g., to RedCap) and data
collection tools (e.g., [MindLogger](https://mindlogger.org/), LORIS, RedCap) enables more consistent
acquisition across projects, with results being harmonized by design.
