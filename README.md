# one-liners
Collection of commands for various stuff


## Parsing

### JSON

#### Pretty printing
`python -m json.tool`

[source](https://pascalprecht.github.io/2014/07/10/pretty-print-json-in-vim/)

#### Print nested JSON

`python -c 'import sys, json; j = json.load(sys.stdin); j = j["field"]["NestedField"]; print json.dumps(j, indent=4)'`

ex: `echo '{"test":{"abc": "def", "ghi": 5}}' | python -c 'import sys, json; j = json.load(sys.stdin); j = j["test"]["abc"]; print json.dumps(j, indent=4)'`

[source](http://www.cambus.net/parsing-json-from-command-line-using-python/)
