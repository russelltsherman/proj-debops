# DirEnv: an environment switcher for the shell.

It knows how to hook into bash, zsh, tcsh and fish shell to load or unload environment variables depending on the current directory. This allows project-specific environment variables without cluttering the "~/.profile" file.

Before each prompt, direnv checks for the existence of a ".envrc" file in the current and parent directories. If the file exists (and is authorized), it is loaded into a bash sub-shell and all exported variables are then captured by direnv and then made available to the current shell.

Because direnv is compiled into a single static executable, it is fast enough to be unnoticeable on each prompt. It is also language-agnostic and can be used to build solutions similar to rbenv, pyenv and phpenv.

## Install

Mac OS X Using Homebrew

```bash
brew install direnv
```

activate direnv on shell load

### BASH

Add the following line at the end of the `~/.bashrc` file:

`eval "$(direnv hook bash)"`

Make sure it appears even after rvm, git-prompt and other shell extensions that manipulate the prompt.

### ZSH

Add the following line at the end of the `~/.zshrc` file:

`eval "$(direnv hook zsh)"`

reload your terminal session before continuing
