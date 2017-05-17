# Pyenv and Pyenv-Virtualenv

pyenv lets you easily switch between multiple versions of Python. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

pyenv-virtualenv is a pyenv plugin that provides features to manage virtualenvs and [conda](https://conda.io/docs/using/envs.html) environments for Python on UNIX-like systems.

## Install Pyenv

Download and install Pyenv either [from the github](https://github.com/pyenv/pyenv#installation) or use homebrew.

`brew install pyenv`

Download and install Pyenv either [from the github](https://github.com/pyenv/pyenv-virtualenv) or use homebrew.

`brew install pyenv-virtualenv`

## Instructions

1. install versions of python `pyenv install 2.7.11`

1. set the python version for the local directory `pyenv local 2.7.11`

1. create a virtualenv `pyenv virtualenv 2.7.11 querium`

1. activate virtualenv `pyenv activate querium`

1. deactivate current virtualenv `pyenv deactivate`

1. list virtualenvs `pyenv virtualenvs`

1. delete virtualenv `pyenv uninstall <env-name>`
