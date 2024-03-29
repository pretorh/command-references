# command references

This is a collection of command references and one-line commands for various stuff.

## Parsing

### JSON

#### Pretty printing
`python -m json.tool`

[source](https://pascalprecht.github.io/2014/07/10/pretty-print-json-in-vim/)

#### Print nested JSON

`python -c 'import sys, json; j = json.load(sys.stdin); val = j["field"]["nestedField"]; print(json.dumps(val, indent=4));'`

For example, to get value of the `test.abc` field (`"def"`) from the following json:
```
{
    "test": {
        "abc": "def",
        "ghi": 5
    }
}
```

```
echo '{"test":{"abc": "def", "ghi": 5}}' | \
python -c 'import sys, json; j = json.load(sys.stdin); val = j["test"]["abc"]; print(json.dumps(val, indent=4));'
```

[source](http://www.cambus.net/parsing-json-from-command-line-using-python/)

#### `jq`

can also use [jq](https://stedolan.github.io/jq/) to pretty print, extract data (`echo '{"test":{"abc": "def", "ghi": 5}}' | jq '.test.abc'` for same field)

## Encryption / Security

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

### ssh

#### Creating a new key

`ssh-keygen -t rsa -b 4096 -f ~/.ssh/dummy -C dummy`

Creates a file specified by `-f` using the comment (the last part in the `.pub` file) from `-C`

## Shell

- Bash: use `shopt -s globstar` for recursive globbing (`ls **/*.ts`)
- `ls *([2,3])` expands to the 2nd and 3rd matches only
- `!!` expands to the last command (ex `sudo !!` to rerun last command as `sudo`)
- `!git` expands to the last command that started with "git"
- `!!:2` expands to the 2nd argument to the last command (_argument_, so `ls -v ; echo !!:1` expands to `-v`)
- `!!:s/hello/bonjour` last command, but replace "hello" with "bonjour"

Source and more [zsh expansion](https://thevaluable.dev/zsh-expansion-guide-example/)

## System

### Create Linux swapfile

Create and enable now:
```
dd if=/dev/zero of=/tmp/swapfile bs=1024 count=524288
chown root:root /tmp/swapfile
chmod 0600 /tmp/swapfile
mkswap /tmp/swapfile
swapon /tmp/swapfile
```

Add to `fstab` if you want to use it after reboot:

`/tmp/swapfile none swap sw 0 0`

[source](http://www.cyberciti.biz/faq/linux-add-a-swap-file-howto/)

### Updating

- Arch: `pacman -Syu`. download download only: `pacman -Syuw --noconfirm`
- CentOS: `yum update`

### cleanup

remove package tarballs except for the latest 3 versions: `sudo paccache -rk3` (`paccache -vdk3` for a list of files)
