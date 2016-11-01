# Grind

`grind` is a set of bash scripts to configure macOS machines.

## How to use it

Install the basic software for `grind` itself work.

```
$ ./grind bootstrap run
```

Load and execute the configurations/installation definitions, see bellow.

```
$ ./grind update run
```

## Definitions

All `grind` does is execute some functions in series defined in the `definitions` directory.
Here's an example of a definition:

```bash
do_run "brew install httpie"
  unless_file "/usr/local/bin/http"

do_run "brew install jq"
  unless_file "/usr/local/bin/jq"

do_run "brew install leiningen"
  unless_file "/usr/local/bin/lein"
```

### Definitions directory organization

First `grind` will load and execute whatever is in the `global` directory,
these are assumed to be definitions to be applied to any machine.

After that `grind` will load scripts from the `machines` directory, where it will try
to find a subdirectory with the machine name and from there load the scripts. These
definitions are specific for each machine you want to maintain.
