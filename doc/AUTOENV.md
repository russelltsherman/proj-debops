# Autoenv: Directory-based Environments

Magic per-project shell environments. Very pretentious.

**Note: you should probably use direnv (direnv.net) instead. It is higher quality, and maintained.**

## What is it

If a directory contains a ``.env`` file, it will automatically be executed
when you ``cd`` into it.

This is great for...

- auto-activating virtualenvs
- project-specific environment variables
- making millions

You can also nest envs within each other. How awesome is that!?

When executing, autoenv, will walk up the directories until the mount point and execute all ``.env`` files beginning at the top.

## Usage

Follow the white rabbit::

```bash
echo "echo 'whoa'" > project/.env
cd project
```

## Install

Mac OS X Using Homebrew

```bash
brew install autoenv
```

activate autoenv on shell load

```bash
echo "source $(brew --prefix autoenv)/activate.sh" >> ~/.bash_profile
```

## Configuration

Before sourcing activate.sh, you can set the following variables:

- ``AUTOENV_AUTH_FILE``: Authorized env files, defaults to ``~/.autoenv_authorized``
- ``AUTOENV_ENV_FILENAME``: Name of the ``.env`` file, defaults to ``.env``
- ``AUTOENV_LOWER_FIRST``: Set this variable to flip the order of ``.env`` files executed

## Shells

autoenv is tested on:

- bash
- zsh
- dash
- fish is supported by `autoenv_fish <https://github.com/loopbit/autoenv_fish>`_
- more to come

## Alternatives

Direnv is an excellent alternative to autoenv, and includes the ability to unset environment variables as well.
It also supports the fish terminal.

`https://direnv.net <https://direnv.net>`_

## Disclaimer

Autoenv overrides ``cd``. If you already do this, invoke ``autoenv_init`` within your custom ``cd`` after sourcing ``activate.sh``.

Autoenv can be disabled via ``unset cd`` if you experience I/O issues with
certain file systems, particularly those that are FUSE-based (such as ``smbnetfs``).
