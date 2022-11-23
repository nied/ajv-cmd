# ajv-cmd

Deref, Validate, Transpile, and Test JSON-Schema (.json) files using ajv.

### Setup

```bash
$ npm install -D ajv-cmd
$ ajv --help
```

Based off of [ajv-cli](https://ajv.js.org/packages/ajv-cli.html).

## Examples

### Pre-transpile all handler schemas

```bash
#!/usr/bin/env bash

function bundle {
  ajv validate ${1} --valid \
	--strict true --coerce-types array --all-errors true --use-defaults empty
  ajv transpile ${1} \
	--strict true --coerce-types array --all-errors true --use-defaults empty \
	-o ${1%.json}.js
}

for file in handlers/*/schema.*.json; do
  if [ ! -n "$(bundle $file | grep ' is valid')" ]; then
	echo "$file failed"
	exit 1
  fi
done
```
