# 14.5 Plain Old Documentation—Documenting a Module

documents that can be represented in a number of ways. The UNIX man pages are an example of documentation that has been formatted with nroff instructions. It is now easy to embed a set of pod formatting instructions in your scripts to provide documentation in any of the four formats: text, HTML, LaTeX, or nroff.

The first line of the pod documentation starts with an equal sign (=). Each pod instruction starting with an equal sign is a formatting instruction for the pod translator. Each formatting instruction must be terminated with a blank line.

# EXAMPLE 14.26

(The standard Perl library, under the subdirectory Math.)

```
```
=head1 NAME

Math::BigFloat - Arbitrary length float math package

=head1 SYNOPSIS

use Math::BigFloat;

$f = Math::BigFloat->new($string);
```
```

+   - $f->fadd(NSTR) return NSTR addition
+   - $f->fsub(NSTR) return NSTR subtraction
+   - $f->fmul(NSTR) return NSTR multiplication
+   - $f->fdiv(NSTR[, SCALE]) returns NSTR division to SCALE places
+   - $f->fneg() return NSTR negation
+   - $f->fabs() return NSTR absolute value
+   - $f->fcmp(NSTR) return CODE compare undef, <0, =0, >0
+   - $f->fround(SCALE) return NSTR round to SCALE digits
+   - $f->fround(SCALE) return NSTR round to SCALE places
+   - $f->fnorm() return (NSTR) normalize
+   - $f->fsqrt([SCALE]) return NSTR sqrt to SCALE places

(Here is the documentation found at the end of the BigFloat.pm module in

```
```
=head1 DESCRIPTION
```
```

All basic math operations are overloaded if you declare your big floats as

```
```
$float = new Math::BigFloat "2.123123123123123123123123123123123123";

=over 2
```
```

```
```
=item number format
```
```

canonical strings have the form /([+]\d+E[+-]\d+/ . Input values can have inbedded whitespace.