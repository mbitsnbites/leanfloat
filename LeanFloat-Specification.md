# LeanFloat Standard for Binary Floating-Point Arithmetic (DRAFT)

## Abstract

*This section is non-normative.*

LeanFloat is a simplified version of **[IEEE754]**.

This work is licensed under **[CCBY4]**.

## 1. Introduction

An implementation that conforms to the LeandFloat specification must support
**[IEEE754]**, with the exceptions provided by this specification.

## 2. Formats

Only binary floating-point formats are considered by the LeanFloat
specification. Decimal floating-point formats are not supported.

### 2.1 Encoding

The encoding in memory is the same as in **[IEEE754]**, with the following
exception:

* All NaNs are interpreted as quiet NaNs. I.e. when all bits of the exponent
  field are 1 (one) and the significand field is non-zero, the value is qNaN.

Additionally, if subnormal numbers are not supported, subnormal numbers are
interpreted as zero by the LeanFloat system.

### 2.1.1 Standard formats

The following standard binary floating-point formats are supported:

| Name      | Common name         | Significand bits<br>(implicit) | Exponent bits | Exponent bias |
| --------- | ------------------- | ------------------------------ | ------------- | ------------- |
| binary16  | Half precision      | 11                             | 5             | 15            |
| binary32  | Single precision    | 24                             | 8             | 127           |
| binary64  | Double precision    | 53                             | 11            | 1023          |
| binary128 | Quadruple precision | 113                            | 15            | 16383         |
| binary256 | Octtuple precision  | 237                            | 19            | 262143        |

A conforming implementation shall support at least one of these standard
formats.

### 2.1.2 Non-standard formats

*This section is non-normative.*

The following binary floating-point formats, which are not specified in
**[IEEE754]**, are recognized by the LeanFloat specification with the sole
purpose of providing a common definition:

| Name      | Common name         | Significand bits<br>(implicit) | Exponent bits | Exponent bias |
| --------- | ------------------- | ------------------------------ | ------------- | ------------- |
| binary8   | Quarter precision   | 4                              | 4             | 7             |
| bfloat16  | Brain float         | 8                              | 8             | 127           |

None of the non-standard formats need to be supported by a conforming
implementation.

## 3. Subnormal numbers

A subnormal number is one where the biased exponent is zero (all exponent field
bits are zero), and the significand field is non-zero (i.e. at least one bit
is set).

The support for subnormal numbers is optional.

### 3.1 Treat subnormal numbers as zero

*This section only applies when subnormal numbers are not supported by the
implementation.*

Whenever a subnormal number is used as an input to a floating-point operation,
it shall be treated as the value zero. The sign bit is preserved, so that a
subnormal value can be interpreted as either +0 or -0, according to the sign
bit.

Whenever a floating-point operation produces a result that would be a subnormal
value according to **[IEEE754]**, it shall instead produce the value zero. The
sign bit is preserved, so that the return value can be either +0 or -0,
according to the sign of the result.

## 4. Rounding

All floating-point operations use the same rounding mode: Round to nearest,
ties to even.

## 5. Floating-point exceptions

Neither floating-point exceptions nor status flags to indicate the occurrence
of exceptional conditions are supported (e.g. no floating-point status
register is required to hold state related to floating-point exceptions).

Instead, qNaN is returned (and propagated) for invalid operations, and
infinity is returned (and propagated) for overflow conditions.

In particular:

* An invalid operation returns qNaN.
* Division by zero returns ±infinity.
* Overflow returns ±infinity.
* Underflow returns ±0.
* Inexact returns the correctly rounded result.

## A. References

**[IEEE754]** "IEEE 754-2019 - IEEE Standard for Floating-Point Arithmetic",
URL: [https://standards.ieee.org/content/ieee-standards/en/standard/754-2019.html](https://standards.ieee.org/content/ieee-standards/en/standard/754-2019.html)

**[CCBY4]** "Creative Commons Attribution 4.0 International",
URL: [https://creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/)
