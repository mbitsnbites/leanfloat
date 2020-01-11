# LeanFloat Specification (DRAFT)

## Abstract

*This section is non-normative.*

LeanFloat is a simplified version of **[IEEE754]**.

This work is licensed under **[CCBY4]**.

## 1. Introduction

TBD

## 2. Formats

Only binary floating-point formats are considered by the LeanFloat
specification. Decimal floating-point formats are not supported.

### 2.1 Encoding

The encoding in memory is the same as in IEEE 754, with the following
exceptions:

* Denormal numbers are interpreted as zero. I.e. when the biased exponent is
  zero, the value is +/- 0, regardless of the value of the significand field.
* All NaNs are interpreted as quiet NaNs. I.e. when all bits of the exponent
  field are zero and the significand field is non-zero, the value is qNaN.

Note: In the tables below, the *Significand bits* field denotes the number
of *implicit* bits. The in-memory representation uses one less bit for the
significand, since the most significant significand bit is implicitly 1.

### 2.1.1 Standard formats

The following standard binary floating-point formats are supported:

| Name      | Common name         | Significand bits | Exponent bits | Exponent bias |
| --------- | ------------------- | ---------------- | ------------- | ------------- |
| binary16  | Half precision      | 11               | 5             | 15            |
| binary32  | Single precision    | 24               | 8             | 127           |
| binary64  | Double precision    | 53               | 11            | 1023          |
| binary128 | Quadruple precision | 113              | 15            | 16383         |

A conforming implementation must support at least one of these standard
formats.

### 2.1.2 Non-standard formats

*This section is non-normative.*

The following binary floating-point formats, which are not specified in the
IEEE 754 standard, are recognized by the LeanFloat specification with the sole
purpose of providing a common definition:

| Name      | Common name         | Significand bits | Exponent bits | Exponent bias |
| --------- | ------------------- | ---------------- | ------------- | ------------- |
| binary8   | Quarter precision   | 4                | 4             | 7             |
| bfloat16  | Brain float         | 8                | 8             | 127           |

None of the non-standard formats need to be supported by a conforming
implementation.

## 3. Denormal numbers

A denormal number is one where the biased exponent is zero (all exponent field bits are zero), and the significand field is non-zero (i.e. at least one bit is set).

Whenever a denormal number is used as an input to a floating-point operation, it is treated as the value zero. The sign bit is preserved, so that a denormal value can be interpreted as either +0 or -0.

Whenever a floating-point operation produces a result that would be a denormal value, it shall instead produce the value zero. The sign bit is preserved, so that the return value can be either +0 or -0.

## 4. Rounding

TBD

## 5. Exceptions

TBD

## A. References

**[IEEE754]**<br>"IEEE 754-2019 - IEEE Standard for Floating-Point Arithmetic", URL: [https://standards.ieee.org/content/ieee-standards/en/standard/754-2019.html](https://standards.ieee.org/content/ieee-standards/en/standard/754-2019.html)

**[CCBY4]**<br>"Creative Commons Attribution 4.0 International", URL: [https://creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/)