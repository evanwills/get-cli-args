# get-cli-args

`get-cli-args` is a simple tool for working with arguments passed to a NodeJS script using unix style long argument syntax (`--arg-name` or `--arg-name=arg-value`)

NOTE: Because of the way this is written, CLI arguments are available anywhere in the script.

It provides three versions of a function, each do exactly the same thing and accept the same two parameters (`arg` & `default_`)

The only difference is how they handle differences in type between the value passed when the script is called and the default value supplied wen getting the CLI value

* `cliArgs(arg, default_)` is the simplest and least strict. If the argument `arg` was passed when the script was called, it's value is returned. If not the default value (`default_`) is returned unless `default_` is undefined, in which case, `NULL` is returned.
* `cliArgsStrict(arg, default_)` works the same as `cliArgs()` but when the matching CLI argument is found, its type is compared to the default type. If the types match the CLI value is returned otherwise the default is returned. If no default is specified, then it behaves identically to `cliArgs()`
* `cliArgsStrict(arg, default_)` works the same as `cliArgsStrict()` but when the CLI argument type doesn't match the default type, an error is thrown.

## Argument names are standardised

When CLI arguments are processed and access, the argument name is standardised to lowercase alphabetical characters only. This limits the chance of human error when passing CLI arguments.

e.g. `--arg-name`, `--ARG_NAME` & `--argName` all get converted to _`argname`_

## Boolean arguments

When a CLI argument has no value, it is assumed to be boolean & `true`

e.g. `--stop-the-race` becomes `stoptherace` = `true` but 
  `--stop-the-race=false` becomes `stoptherace` = `false`

## Boolean and Number interpretation

When CLI arguments are processed, if the value can be converted to a boolean or number, they are.
e.g. _"true"_ & _"false"_ are converted to their boolean equivalents `true` & `false`
and  _"123"_ or _"4.56"_ are converted to numeric equivalents `123` & `4.56`

## White space in string values

By default, CLI arguments are space separated. If you need white space in your CLI arguments value, wrap the value in quotes.

e.g. `--suburb='North Sydey'` becomes `{suburb: "North Sydney"}`
