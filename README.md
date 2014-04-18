# nodenv-vars

This is a plugin for [nodenv](https://github.com/OiNutter/nodenv)
that lets you set global and project-specific environment variables
before spawning Node processes.

## Installation

To install nodenv-vars, clone this repository into your
`~/.nodenv/plugins` directory. (You'll need a recent version of nodenv
that supports plugin bundles.)

    $ mkdir -p ~/.nodenv/plugins
    $ cd ~/.nodenv/plugins
    $ git clone https://github.com/OiNutter/nodenv-vars.git

## Usage

Define environment variables in an `.nodenv-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

    HUBOT_CAMPFIRE_ACCOUNT=nodenv
    HUBOT_CAMPFIRE_TOKEN=somerandomtoken
    HUBOT_CAMPFIRE_ROOMS=some,campfire,rooms

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `HUBOT_CAMPFIRE_ROOMS`:

    HUBOT_CAMPFIRE_ROOMS=$HUBOT_CAMPFIRE_ROOMS:some,extra,rooms

You may also have conditional variable assignments, such that a
variable will **only** be set if it is not already defined or is blank:

    USER_ID?=OiNutter

In the above case, `USER_ID` will only be set if `$USER_ID` is
currently empty (i.e., if `[ -z "$USER_ID" ]` is true).

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.nodenv/vars` file will be set
first. Then variables specified in `.nodenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.nodenv-vars` file in the current directory are set last.

Use the `nodenv vars` command to print all environment variables in the
order they'll be set.

## Version History

**1.0.0** (April 18, 2014)

* Initial public release. (Copied from [rbenv-vars](http://github.com/sstephenson/rbenv-vars))

## License

&copy; 2014 Will McKenzie. Released under the MIT license. See
`LICENSE` for details.
