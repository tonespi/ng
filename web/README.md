# ng

# Install pyenv

pyenv allows swapping versions of python. Prevents messing around with the system python install 

1. Install all required prerequisite dependencies:

```
sudo apt-get update; sudo apt-get install make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

2. Download and execute installation script:

```
curl https://pyenv.run | bash
```

3. Add the following entries into your ~/.bashrc file:

```
# pyenv
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"
```

4. Restart your shell:

```
exec $SHELL
```

5. Validate installation:

```
pyenv --version
```

6. Install python 3.10.7:

```
pyenv install 3.8.0
```

# Install poetry

Poetry is a tool for dependency management and packaging in Python. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you. Poetry offers a lockfile to ensure repeatable installs, and can build your project for distribution.

```
curl -sSL https://install.python-poetry.org | python3 -
```

# Install deps local

At this time, poetry will use the version of python active at time of install. This may cause issues when installng deps. If you get python version compatability errors even if you have the right version active with pyenv, you can get the poetry venv built using:

```
pyenv shell 3.10.7
poetry env use $(pyenv which python)
poetry install
```