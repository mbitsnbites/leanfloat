# LeanFloat

[LeanFloat Specification (DRAFT)](LeanFloat-Specification.md)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/)

## About

LeanFloat is a simplified version of the [IEEE Standard for Floating-Point Arithmetic (IEEE 754)](https://en.wikipedia.org/wiki/IEEE_754).

For most intents and purposes it is compatible with the IEEE 754 standard, but with the following simplifications:

* [Subnormal numbers](https://en.wikipedia.org/wiki/Denormal_number) are not
  supported (they are treated as zeros).
* Only a single [rounding mode](https://en.wikipedia.org/wiki/IEEE_754#Rounding_rules)
  is supported: [Round to nearest, ties to even](https://en.wikipedia.org/wiki/Rounding#Round_half_to_even)
  (a.k.a. RTNE).
* Signaling [NaNs](https://en.wikipedia.org/wiki/NaN) (sNaN) are not
  supported. All NaNs are treated as quiet NaNs (qNaN).
* Floating-point [exceptions](https://en.wikipedia.org/wiki/IEEE_754#Exception_handling)
  are not supported. The default return value for an operation that would
  signal an exception is returned (e.g. sqrt(-1) returns qNaN).
* Decimal floating-point formats (e.g. [decimal64](https://en.wikipedia.org/wiki/Decimal64_floating-point_format))
  are not supported.

## Motivation

There are a number of driving motivations behind LeanFloat:

* Many existing systems, in particular SIMD/vector systems, do not fully
  support IEEE 754, but instead a subset that is equal to or very similar to
  LeanFloat. Yet, no proper common definition of this subset exists.
* Floating-point functionality is becoming increasingly popular in domains
  where full IEEE 754 compliance is neither necessary nor suitable (or even
  possible) due to hardware constraints. The LeanFloat specification aims to
  provide a least common denominator that can be targeted by such systems.
* For areas such as education and hobby and open source development where
  time and/or hardware constraints can be a limiting factor (e.g. if the
  target hardware is an FPGA with limited logic resources), LeanFloat can make
  floating-point functionality possible if a fully compliant IEEE 754
  implementation would not be feasible.
* It is common for software programs to configure the FPU in a mode that is
  very similar to LeanFloat (e.g. disable subnormal numbers and floating-point
  exceptions), for the purpose of improved performance and/or compatibility
  with systems where full IEEE 754 functionality is not available.

## Compatibility with IEEE 754

### Data interchange

Floating-point values produced by an IEEE 754 system can safely be used in a
LeanFloat system, and vice versa.

### Operations

Floating-point operations will behave identically on a LeanFloat system
compared to an IEEE 754 system, as long as:

* The IEEE 754 system uses the default rounding configuration.
* No subnormal numbers are part of the floating-point operations (see
  [Caveats](#caveats)).
* Floating-point exceptions are not used (see [Caveats](#caveats)).

## Caveats

A LeanFloat system is not 100% compatible with a fully compliant IEEE 754
system. In other words, software written against the IEEE 754 standard may not
produce the same result when running on a LeanFloat system (and vice versa).

For example:

* Software that needs to trap on floating-point exceptions (e.g. to catch
  division by zero or overflow) may not function properly.
* Since a LeanFloat system treats subnormal numbers as zeros, it has a slightly
  reduced numeric range. This can result in different computational results
  compared to an IEEE 754 system.
* Furthermore, the lack of support for subnormal numbers in a LeanFloat system
  voids some of the guarantees provided by an IEEE 754 system. For instance,
  the relationship A != B => A - B != 0 does not hold for small numbers in a
  LeanFloat system.

