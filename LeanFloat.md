# LeanFloat Specification (DRAFT)

## Abstract

*This section is non-normative.*

LeanFloat is a simplified version of the [IEEE Standard for Floating-Point Arithmetic (IEEE 754)](https://en.wikipedia.org/wiki/IEEE_754).

This work is licensed under a Creative Commons Attribution 4.0 International License.

## Introduction

TBD

### Formats

Only binary floating-point formats are considered by the LeanFloat
specification. Decimal floating-point formats are not supported.

#### Encoding

The encoding in memory is the same as in IEEE 754, with the following
exceptions:

* Denormal numbers are interpreted as zero. I.e. when the biased exponent is
  zero, the value is +/- 0, regardless of the value of the significand field.
* All NaNs are interpreted as quiet NaNs. I.e. when all bits of the exponent
  field are zero and the significand field is non-zero, the value is qNaN.

Note: In the tables below, the *Significand bits* field denotes the number
of *implicit* bits. The in-memory representation uses one less bit for the
significand, since the most significant significand bit is implicitly 1.

#### Standard formats

The following standard binary floating-point formats are supported:

| Name      | Common name         | Significand bits | Exponent bits | Exponent bias |
| --------- | ------------------- | ---------------- | ------------- | ------------- |
| binary16  | Half precision      | 11               | 5             | 15            |
| binary32  | Single precision    | 24               | 8             | 127           |
| binary64  | Double precision    | 53               | 11            | 1023          |
| binary128 | Quadruple precision | 113              | 15            | 16383         |

A conforming implementation must support at least one of these standard
formats.

#### Non-standard formats

*This section is non-normative.*

The following binary floating-point formats, which are not specified in the
IEEE 754 standard, are recognized by the LeanFloat with the sole purpose of
providing a common definition:

| Name      | Common name         | Significand bits | Exponent bits | Exponent bias |
| --------- | ------------------- | ---------------- | ------------- | ------------- |
| binary8   | Quarter precision   | 4                | 4             | 7             |
| bfloat16  | Brain float         | 8                | 8             | 127           |

None of the non-standard formats need to be supported by a conforming
implementation.

### Denormal numbers

TBD

### Rounding

TBD

### Exceptions

TBD
