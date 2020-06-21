# Schema structure

## Style guides

{==⚠️ Note: All schema and context files above are saved without a `.jsonld` files extension. ⚠️ ==}

We recomment that the name the `protocol` and `activities` directory follow the `CamelCase` naming convention.

## Overall structure

We have defined 3 different types of schema

-   [Protocol](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Protocol)
-   [Activity](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Activity)
-   [Item](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Field)

## Protocol

The protocol directory structure contains the following:

[TO DO]

## Activity

The activity directory structure contains the following:

-   `/items`: directory containing the jsonld files for individual items of the activity schema
    -   `item_1`
    -   `item_2`
    -   …
-   `activityName_schema` : schema to define the activity
-   `activityName_context` : context to define keys used specific to the activity schema
-   sub-activity jsonld schemas (if any)

The generic keys are defined in the generic context file (contexts/generic)