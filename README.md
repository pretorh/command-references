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


## Encryption

### GPG

#### Extending expiration date

Get the key's code: `gpg --list-keys`  
Start interactive edit: `gpg --edit-key CODE`  

```
key 0
expire
...
key 1
expire
...
save
```

[source](http://www.g-loaded.eu/2010/11/01/change-expiration-date-gpg-key/)

#### Exchanging keys

Export:
`gpg --armor --export <CODE>` (For secret keys: `gpg --armor --export-secret-keys <CODE>`)

Import:
`gpg --import <file>`

[source](https://www.gnupg.org/gph/en/manual/x56.html)
