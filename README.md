[![](https://codecov.io/gh/delvtech/agent_0/branch/main/graph/badge.svg?token=1S60MD42ZP)](https://app.codecov.io/gh/delvtech/agent_0?displayType=list)
[![](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![](https://img.shields.io/badge/testing-pytest-blue.svg)](https://docs.pytest.org/en/latest/contents.html)
<br><a href="https://app.codecov.io/gh/delvtech/agent_0?displayType=list"><img height="50px" src="https://codecov.io/gh/delvtech/agent_0/branch/main/graphs/sunburst.svg?token=1S60MD42ZP"><a>

# [DELV](https://delv.tech) Agent 0

Agent 0 monorepo with the following subpackages:
- **agentz:** (Not Implemented) Bot specification, interface, tooling

- **fixedpointmath:** Fixed-point arithmetic package

- **holodrive:** (Not Implemented) Plotting, visualization, post-processing of blockchain data

- **hypercache:** (Not Implemented) Accesses data from the blockchain, decodes it, and delivers it as a queryable database

- **warpcore:** (Not implemented) Hyperdrive simulation engine (most of what is presently in elfpy)

This project is a work-in-progress. All code is provided as is and without guarantee.

Documentation can be found [here](https://elfpy.delv.tech).

## Install

Please refer to [INSTALL.md](https://github.com/delvtech/agent_0/blob/main/INSTALL.md).

## Build

Please refer to [BUILD.md](https://github.com/delvtech/agent_0/blob/main/BUILD.md).

## Deployment

TODO

## Testing

Testing is achieved with [py.test](https://docs.pytest.org/en/latest/contents.html). You can run all tests from the repository root directory by runing `python -m pytest`, or you can pick a specific test in the `tests/` folder with `python -m pytest tests/{test_file.py}`.

## Contributions

Please refer to [CONTRIBUTING.md](https://github.com/delvtech/agent_0/blob/main/CONTRIBUTING.md).
