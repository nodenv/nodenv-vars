# nodenv-vars

[nodenv][] plugin to set global and project-specific environment variables

[![Tests](https://img.shields.io/github/actions/workflow/status/nodenv/nodenv-vars/test.yml?label=tests&logo=github)](https://github.com/nodenv/nodenv-vars/actions/workflows/test.yml)
[![Latest GitHub Release](https://img.shields.io/github/v/release/nodenv/nodenv-vars?label=github&logo=github&sort=semver)](https://github.com/nodenv/nodenv-vars/releases/latest)
[![Latest Homebrew Release](<https://img.shields.io/badge/dynamic/regex?label=homebrew-nodenv&logo=homebrew&logoColor=white&url=https%3A%2F%2Fraw.githubusercontent.com%2Fnodenv%2Fhomebrew-nodenv%2Frefs%2Fheads%2Fmain%2FFormula%2Fnodenv-vars.rb&search=archive%2Frefs%2Ftags%2Fv(%3F%3Cversion%3E%5Cd%2B.*).tar.gz&replace=v%24%3Cversion%3E>)](https://github.com/nodenv/homebrew-nodenv/blob/main/Formula/nodenv-vars.rb)
[![Latest npm Release](https://img.shields.io/npm/v/@nodenv/nodenv-vars?logo=npm&logoColor=white)](https://www.npmjs.com/package/@nodenv/nodenv-vars/v/latest)

<!-- toc -->

- [Installation](#installation)
- [Usage](#usage)
- [Credits](#credits)

<!-- tocstop -->

## Installation

To install nodenv-vars, clone this repository into your
`$(nodenv root)/plugins` directory. (You'll need a recent version of nodenv
that supports plugin bundles.)

```console
mkdir -p $(nodenv root)/plugins
cd $(nodenv root)/plugins
git clone https://github.com/nodenv/nodenv-vars.git
```

## Usage

Define environment variables in an `.nodenv-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

```dotenv
HUBOT_CAMPFIRE_ACCOUNT=nodenv
HUBOT_CAMPFIRE_TOKEN=somerandomtoken
HUBOT_CAMPFIRE_ROOMS=some,campfire,rooms
```

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `HUBOT_CAMPFIRE_ROOMS`:

```dotenv
HUBOT_CAMPFIRE_ROOMS=$HUBOT_CAMPFIRE_ROOMS:some,extra,rooms
```

You may also have conditional variable assignments, such that a
variable will **only** be set if it is not already defined or is blank:

```dotenv
USER_ID?=OiNutter
```

In the above case, `USER_ID` will only be set if `$USER_ID` is
currently empty (i.e., if `[ -z "$USER_ID" ]` is true).

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `$(nodenv root)/vars` file will be set
first. Then variables specified in `.nodenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.nodenv-vars` file in the current directory are set last.

Use the `nodenv vars` command to print all environment variables in the
order they'll be set.

## Credits

Forked from [Sam Stephenson](https://github.com/sstephenson)'s
[rbenv-vars](https://github.com/rbenv/rbenv-vars) by [Will
McKenzie](https://github.com/oinutter) and modified for nodenv.

[nodenv]: https://github.com/nodenv/nodenv
