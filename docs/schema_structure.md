# Schema structure

We have defined 3 different types of schema

-   [Protocol](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Protocol)
-   [Activity](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Activity)
-   [Item](https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Field)

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
