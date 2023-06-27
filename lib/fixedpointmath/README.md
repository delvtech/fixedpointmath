# fixed point lib

## Number format

Internally Elfpy conducts all operations using 18-decimal fixed-point precision integers and arithmetic.
Briefly, this means our representation for unity, "one", is `1 * 10 ** 18`, which would be `1.0` when cast to a float.

This can lead to confusion when additionally dealing with standard Python floats and ints.
As such, we have purposefully constrain support for mixed-type operations that include the FixedPoint type.
Due to a lack of known precision, operations against Python floats are not allowed (e.g. `float * FixedPoint` will raise an error).
However, operations against `int` are allowed.
In this case, the `int` _argument_ is assumed to be "unscaled", i.e. if you write `int(8) * FixedPoint(8)` we will scale up the first variable return a `FixedPoint` number that represents the float `64.0` in 18-decimal FixedPoint format.
So in this example the internal representation of that operation would be `64*10**18`.
If you cast FixedPoint numbers to ints or floats you will get "unscaled" representation, e.g. `float(FixedPoint(8.0)) == 8.0` and `int(FixedPoint(8.528)) == 8`.

If you want the integer scaled representation, which can be useful for communicating with Solidity contracts, you must ask for it explicitly, e.g. `FixedPoint(8.52).scaled_value == 8520000000000000000`.
Conversely, if you want to initialize a FixedPoint variable using the scaled integer representation, then you need to instantiate the variable using the `scaled_value` argument, e.g. `FixedPoint(scaled_value=8)`.
In that example, the internal representation is `8`, so casting it to a float would produce a small value: `float(FixedPoint(scaled_value=8)) == 8e-18`.

To understand more, we recommend that you study the fixed point tests and source implementation.