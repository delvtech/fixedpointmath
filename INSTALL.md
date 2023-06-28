# Install -- overview

Agent 0 has been tested with Python 3.9 and 3.10.

### 1. Install Pyenv

Follow [Pyenv install instructions](https://github.com/pyenv/pyenv#installation).

### 2. Clone Agent 0 repo

Clone the repo into a <repo_location> of your choice.
```bash
git clone https://github.com/delvtech/elf-simulations.git <repo_location>
```

### 3. Set up virtual environment

Here we use [venv](https://docs.python.org/3/library/venv.html) which is part of the built-in standard Python library. You can use another virtual environment package if you prefer, like [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv).

```bash
cd <repo_location>
pyenv install 3.10
pyenv local 3.10
python -m venv .venv
source .venv/bin/activate
```

### 4. Install agent_0

All individual subpackages can be installed from the outermost repo through `requirements.txt`

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m pip install -r requirements-dev.txt
```

An explanation of what the above steps do:
- `pyenv install 3.10` You should now see the correct version when you run `pyenv versions`.
- `pyenv local 3.10` This command creates a `.python-version` file in your current directory. If you have pyenv active in your environment, this file will automatically activate this version for you.
- `python -m venv .venv` This will create a `.venv` folder in your repo directory that stores the local python build & packages. After this command you should be able to type which python and see that it points to an executable inside `.venv/`.
- `python -m pip install -r requirements.txt` This installs the subpackages locally such that the install updates automatically any time you change the source code.
- `python -m pip install -r requirements-dev.txt` installs dev related packages such as pytest.

Alternatively, each subpackage in `lib` can be individaully installed through pip. For example, you can install `fixedpointmath` through pip as follows:
```bash
python -m pip install lib/fixedpointmath # Install from local file
python -m pip install 'fixedpointmath @ git+https://github.com/delvtech/agent_0.git/#subdirectory=lib/fixedpointmath' # Install from github
```


## Notes

You can test that everything is working by calling: `python -m pytest .`
