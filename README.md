# LeanFloat

LeanFloat is a simplified version of the [IEEE Standard for Floating-Point Arithmetic (IEEE 754)](https://en.wikipedia.org/wiki/IEEE_754).

For most intents and purposes it is compatible with the IEEE 754 standard, but with the following simplifications:

* [Denormal numbers](https://en.wikipedia.org/wiki/Denormal_number) are not supported (they are treated as zeros).
* Only a single [rounding mode](https://en.wikipedia.org/wiki/IEEE_754#Rounding_rules) is supported: [Round to nearest, ties to even](https://en.wikipedia.org/wiki/Rounding#Round_half_to_even) (a.k.a. RTNE).
* Signaling [NaNs](https://en.wikipedia.org/wiki/NaN) (sNaN) are not supported. All NaNs are treated as quiet NaNs (qNaN).
* Floating point [exceptions](https://en.wikipedia.org/wiki/IEEE_754#Exception_handling) are not supported. The default return value for an operation that would signal an exception is returned (e.g. sqrt(-1) returns qNaN).

## Specification

[LeanFloat Specification (DRAFT)](LeanFloat.md)

## Motivation

TBD

## Caveats

TBD

## Compatibility with IEEE 754

TBD

