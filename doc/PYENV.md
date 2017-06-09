# Pyenv and Pyenv-Virtualenv

pyenv lets you easily switch between multiple versions of Python. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

pyenv-virtualenv is a pyenv plugin that provides features to manage virtualenvs and [conda](https://conda.io/docs/using/envs.html) environments for Python on UNIX-like systems.

## Install Pyenv

Download and install Pyenv either [from the github](https://github.com/pyenv/pyenv#installation) or use homebrew.

`brew install pyenv`

Add to your .profile this line to automatically initialize pyenv

```bash
eval "$(pyenv init -)"
```

Download and install Pyenv either [from the github](https://github.com/pyenv/pyenv-virtualenv) or use homebrew.

`brew install pyenv-virtualenv`

Add to your .profile this line to automatically initialize pyenv

```bash
eval "$(pyenv virtualenv-init -)"
```

## Instructions

1. DirEnv will automatically handle creating, activating, and deactivating our python virtual environment as well as activating
