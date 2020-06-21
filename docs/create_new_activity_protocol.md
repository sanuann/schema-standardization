# How can I create a new activity and protocol?

## Programmatic schema generation

Tool to convert redcap CSVs to our schema format. But it cannot be used to convert every
redcap-formatted table as some are customized redcap tables (for example the 100s that are in ABCD)
but does cover most cases. A template of the CSV and how to use the tool can be found
[here](https://github.com/sanuann/reproschema-builder)

## Manual schema generation

Fork the project and manually create the jsonld files according to the above directory structure.
(This process will be tedious for large questionnaires).

### Create an activity

Under the [`activities`](./activities) directory, create directory with name of activity in the
`CamelCase` naming convention.

Activity directory structure:

-   `/items` (directory) : contains the `jsonld` files for individual items of the activity schema
    -   `item_1`
    -   `item_2`
    -   …
-   `activityName_schema` : schema to define the activity
-   `activityName_context` : context to define keys used specific to the activity schema

Creating `activityName_schema` – use the keys defined in [`schemas/Activity`](./schemas/Activity).
If any other keys are used, then define them in `activityName_context`

For example,

```json
  {
  "@context": [ "https://raw.githubusercontent.com/ReproNim/reproschema/master/contexts/generic",
      "https://raw.githubusercontent.com/ReproNim/reproschema/master/activities/Wellbeing/Wellbeing_context"
  ],
  "@type": "reproschema:Activity",
  "@id": "Wellbeing_schema",
  "skos:prefLabel": "Wellbeing",
  "schema:description": " Wellbeing Voice tasks",
  "schema:schemaVersion": "0.0.1",
  "schema:version": "0.0.1",
  "preamble": {
      "en": "For each task, you should hit the record button before speaking and then stop once you are done speaking. You may hit play to hear what was recorded.",
      "es": "Para cada pregunta, debería hacer click sobre el botón antes de hablar y luego hacerlo de nuevo para parar de grabar. Luego puede tocar play para escuchar su respuesta."
  },
  "ui": {
      "addProperties": [
          {"isAbout": "share_data",
          "variableName": "share_data",
          "prefLabel": {"en": "Share Data"},
          "isVis": true,
          "allow": ["skipped", "dontknow"],
          ...
          },
          {"isAbout": "email",
          "variableName": "email",
          "isVis": "share_data === 1"
          },
          {"isAbout": "multipart_audio_check",
          "variableName": "multipart_audio_check",
          "isVis": true
          },
          {"isAbout": "free_speech_general_mood",
          "variableName": "share_data",
          "isVis": true
          },
          {"isAbout": "say_ah",
          "variableName": "say_ah",
          "isVis": true
          }
      ],
      "order": [
          "multipart_audio_check",
          "share_data",
          "email",
          "free_speech_general_mood",
          "say_ah"
      ],
      "shuffle": false
  }
}
```

Mandatory keys:

-  `@context` - [Array] Include the ReproNim generic context JSON-LD file along with the activity context.
-   `@type`- describes type of the schema.
-   `@id` - unique id for the schema. should be same as the filename.
-   `skos:prefLabel` - display name for the schema
-   `ui.addProperties` - defines the various properties of each item.
-   `variablename` - variable name used in `ui.order` for the items
-   `isAbout` - file name of the corresponding variable name
-   `ui.order` - [Array] defines the order in which the items appear in the activity

#### Create items

To create `item_x` in the items folder:

-   Use keys defined in [`schemas/Field`](./schemas/Field)
-   `@type`=`"https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Field"`
-   `responseOptions` – can be embedded or can point to a remote JSON-LD object.

### Create a protocol

-   Under the [`protocols`](./protocols) directory, create directory with name of protocol in the CamelCase naming convention.
-   protocol directory structure:
    -   `protocolName_schema` : schema to define the protocol
    -   `protocolName_context` : context to define keys used specific to the protocol schema

Creating `protocolName_schema` – use the keys defined in [`schemas/Protocol`](./schemas/Protocol).
If any other keys are used, then define them in `protocolName_context`

Description of some other keys:

-   `@context` – Array. Include the ReproNim generic context JSON-LD file along with the protocol context.

For example,

```json
{
  "@context": [
    "https://raw.githubusercontent.com/ReproNim/reproschema/master/contexts/generic",
    "https://raw.githubusercontent.com/ReproNim/reproschema/master/protocols/example/nda-phq_context"
  ]
}
```

-   `@type` = `"https://raw.githubusercontent.com/ReproNim/reproschema/master/schemas/Protocol"`
