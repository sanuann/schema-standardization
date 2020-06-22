# Testing your schema and collecting data

First, make sure your syntax is in correct jsonld format. Test all files with `@context` from command line:

```
npm install -g jsonlint
grep -r --exclude-dir=node_modules --exclude-dir=ui --exclude-dir=.github "@context" . \
   | cut -d: -f1 | xargs -I fname jsonlint -q fname
```

Or test individual files on the [json linter website](`https://jsonlint.com/`).

Then you can view your schema by pointing the reproschema user interface to the path to your protocol: `http://schema.repronim.org/ui/#/?url=PATH_TO_PROTOCOL_SCHEMA`

For example: [https://schema.repronim.org/ui/#/?url=https://raw.githubusercontent.com/sensein/covid19/master/protocol/Covid19_schema](https://schema.repronim.org/ui/#/?url=https://raw.githubusercontent.com/sensein/covid19/master/protocol/Covid19_schema).
