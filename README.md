[![](https://codecov.io/gh/delvtech/fixedpointmath/branch/main/graph/badge.svg?token=n5y9GhZSYZ)](https://app.codecov.io/gh/delvtech/fixedpointmath?displayType=list)
[![](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![](https://img.shields.io/badge/testing-pytest-blue.svg)](https://docs.pytest.org/en/latest/contents.html)
<br><a href="https://app.codecov.io/gh/delvtech/fixedpointmath?displayType=list"><img height="50px" src="https://codecov.io/gh/delvtech/fixedpointmath/branch/main/graphs/sunburst.svg?token=n5y9GhZSYZ"><a>

# [DELV](https://delv.tech) FixedPoint Python repo

The FixedPoint arithmetic package provides a Python endpoint for simulationg FixedPoint arithmetic that follows standards established by the Ethereum Solidity community.


## Install

We are on [PyPI](https://pypi.org/project/fixedpointmath/):

`pip install fixedpointmath`

## Testing

Testing is achieved with [py.test](https://docs.pytest.org/en/latest/contents.html).

## Contributions

Please refer to [CONTRIBUTING.md](https://github.com/delvtech/fixedpointmath/blob/main/CONTRIBUTING.md).

## Documentation

This numeric representation is a noiseless alternative to floating point arithmetic.
Floating point rounding errors can be deteremental when precision matters, such as in the case of blockchain simulation.
The `FixedPoint` conducts all operations using 18-decimal fixed-point precision integers and arithmetic.

### Number format

This package supports 18-decimal fixed-point precision numbers for arithmetic.
Briefly, this means our representation for unity, "one", is `1 * 10 ** 18`, which would be `1.0` when cast to a float.
Unlike typical floats, a FixedPoint numeric always supports 18 decimal digits of precision, regardless of the scale of the number.

If you want the integer scaled representation, which can be useful for communicating with Solidity contracts, you must ask for it explicitly, e.g. `FixedPoint("8.52").scaled_value == 8520000000000000000`.
Conversely, if you want to initialize a FixedPoint variable using the scaled integer representation, then you need to instantiate the variable using the `scaled_value` argument, e.g. `FixedPoint(scaled_value=8)`.
In that example, the internal representation is `8`, so casting it to a float would produce a small value: `float(FixedPoint(scaled_value=8)) == 8e-18`.

If you cast FixedPoint numbers to ints or floats you will get an "unscaled" representation, e.g. `float(FixedPoint("8.0")) == 8.0` and `int(FixedPoint("8.528")) == 8`.

We have purposefully constrained support for mixed-type operations that include the FixedPoint type.
Due to a lack of known precision, operations against Python floats are not allowed (e.g. `float * FixedPoint` will raise an error).
However, operations against `int` are allowed.
In this case, the `int` _argument_ is assumed to be "unscaled", for example `int(8) * FixedPoint(8) == FixedPoint(int(8)) * FixedPoint(8) == FixedPoint(64)`.
The internal "scaled" representation would be `FixedPoint(64).scaled_value == 64 * 10**18`.

Warning! Using floating point as a constructor to FixedPoint can cause loss of precision. For example,

```
>>> FixedPoint(1e18)
FixedPoint("1000000000000000042.420637374017961984")
```

Allowing floating point in the constructor of FixedPoint will be removed in a future version of `fixedpointmath`.

### Computing with FixedPoint

The `FixedPoint` class abstracts away an internal integer representation and provides a suite of operations that act upon the class.
For example,

```python
>>> from fixedpointmath import FixedPoint
>>> float(FixedPoint(8.0))
8.0
>>> int(FixedPoint(8.528))
8
>>> int(8) * FixedPoint(8)
FixedPoint("64.0")
>>> 8.0 * FixedPoint(8)
TypeError: unsupported operand type(s): <class 'float'>
```

The last example throws a `TypeError` due to the lack of known precision between Python `float` and `FixedPoint`.
