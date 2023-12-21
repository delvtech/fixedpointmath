# Build

## Building subpackages and uploading to pypi

1. Within a subpackage, make sure the version is updated in `pyproject.toml`.
2. Install prerequisites:

```bash
python -m pip install --upgrade pip
python -m pip install --upgrade build twine
```

3. Update the version number in the lib/<package>/pyproject.toml. Packages use standard semver.

4. Build the distribution within the subpackage. For example, to build the `fixedpointmath` package,

```bash
python -m build
```

5. Upload to pypi. The below command will ask for a username and password.

```bash
python -m twine upload --repository pypi dist/*
```

TODO figure out how to expand access across one current account (currently `fixedpointmath` is published under `slundquist`)
