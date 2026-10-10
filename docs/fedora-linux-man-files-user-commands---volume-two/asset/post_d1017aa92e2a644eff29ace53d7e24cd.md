
# USAGE

Only the differences between GNU **eqn** and Unix eqn are described here.

GNU **eqn** emits Presentation MathML output when invoked with the -T\~MathML option.

GNU eqn sets the input token ... as three periods or low dots, rather than the three centered dots of classic eqn. To get three centered dots, write \textbf{cdots} or \textbf{cdot cdot cdot}.

Most of the new features of the GNU **eqn** input language are based on TeX. There are some references to the differences between TeX and GNU **eqn** below; these may safely be ignored if you do not know TeX.

# Controlling delimiters

If not in compatibility mode, **eqn** recognizes

```
    \textbf{delim on}
```

to restore the delimiters which have been previously disabled with a call to ‘\textbf{delim off}’. If delimiters haven’t been specified, the call has no effect.

# Automatic spacing

**eqn** gives each component of an equation a type, and adjusts the spacing between components using that type. Possible types are:

- ordinary
  an ordinary character such as ‘1’ or ‘x’;
- operator
  a large operator such as ‘$\hat{L}$’;
- binary
  a binary operator such as ‘+’;
- relation
  a relation such as ‘=’;
- opening
  a opening bracket such as ‘(’;
- closing
  a closing bracket such as ‘)’;
- punctuation
  a punctuation character such as ‘,cl;
- inner
  a subformula contained within brackets;
- suppress spacing
  that suppresses automatic spacing adjustment.

Components of an equation get a type in one of two ways.

# type $t$ $e$

This yields an equation component that contains~$e$ but that has type~$t$, where $t$ is one of the types mentioned above. For example, **times** is defined as

```
type "binary" \(mu
```

The name of the type doesn't have to be quoted, but quoting protects from macro expansion. **chartype** $t$ $text$ Unquoted groups of characters are split up into individual characters, and the type of each character is looked up; this changes the type that is stored for each character; it says that the characters in $text$ from now on have type~$t$. For example,

```
chartype "punctuation" .,;
```

would make the characters ‘.';’ have type punctuation whenever they subsequently appeared in an equation. The type~$t$ can also be **letter** or **digit**; in these cases **chartype** changes the font type of the characters. See the **Fonts** subsection.

# New primitives

# big $e$

Enlarges the expression it modifies; intended to have semantics like CSS ‘large’. In troff output, the point size is increased by~5; in MathML output, the expression uses `<mstyle mathsize='big'>`

$e$**1 smaller** $e$**2** This is similar to **over**; **smaller** reduces the size of $e$**1** and $e$**2**; it also puts less vertical space between $e$**1** or $e$**2** and the fraction bar. The **over** primitive corresponds to the TeX \over primitive in display styles; **smaller** corresponds to \over in non-display styles. **vcenter** $e$ This vertically centers $e$ about the math axis. The math axis is the vertical position about which characters such as ‘+cq’ and ‘−’ are centered; also it is the vertical position used for the bar of fractions. For example, **sum** is defined as

```
{ type "operator" vcenter size +5 (*S }
```

(Note that vcenter is silently ignored when generating MathML.) $e$**1 accent** $e$**2** This sets $e$**2** as an accent over $e$**1**. $e$**2** is assumed to be at the correct height for a lowercase letter; $e$**2** is moved down according to whether $e$**1** is taller or shorter than a lowercase letter. For example, **hat** is defined as

```
accent { "^" }
```

**dotdot**, **dot**, **tilde**, **vec**, and **dyad** are also defined using the **accent** primitive.

$e$**1 uaccent** $e$**2** This sets $e$**2** as an accent under $e$**1**. $e$**2** is assumed to be at the correct height for a character without a descender; $e$**2** is moved down if $e$**1** has a descender. **utilde** is pre-defined using **uaccent** as a tilde accent below the baseline. **split** $stexts$ This has the same effect as simply

```
text
```

but $text$ is not subject to macro expansion because it is quoted; $text$ is split up and the spacing between individual characters is adjusted. **nosplit** $text$ This has the same effect as $stexts$

but because text is not quoted it is subject to macro expansion; text is not split up and the spacing between individual characters is not adjusted. e oprime This is a variant of prime that acts as an operator on~e. It produces a different result from prime in a case such as A oprime sub 1: with oprime the~1 is tucked under the prime as a subscript to the~A (as is conventional in mathematical typesetting), whereas with prime the~1 is a subscript to the prime character. The precedence of oprime is the same as that of bar and under, which is higher than that of everything except accent and uaccent. In unquoted text a~^ that is not the first character is treated like oprime. special text e This constructs a new object from~e using a (1) macro named text. When the macro is called, the string 0s contains the output for~e, and the number registers 0w, 0h, 0d, 0skern, and 0skew contain the width, height, depth, subscript kern, and skew of~e. (The subscript kern of an object says how much a subscript on that object should be tucked in; the skew of an object says how far to the right of the center of the object an accent over the object should be placed.)

```
The macro must modify 0s so that it outputs the desired result with its origin at the current point, and increase the current horizontal position by the width of the object. The number registers must also be modified so that they correspond to the result. For example, suppose you wanted a construct that ‘cancels’ an expression by drawing a diagonal line through it. 
.EQ define cancel ‘special Ca’.EN .de Ca . ds 0s \ Z^*(0s^)\v^n(0du)\ iD¹ \n(0wu \n(0hu+\n(0du) \ v\n(0hu) ..
```

Then you could cancel an expression~e with cancel { e } Here’s a more complicated construct that draws a box round an expression:

```
.EQ define box ‘special Bx’ .EN .de Bx . ds 0s \ Z^\h*1n^*(0s^)\Z^\
.\v\n(0du+1n^\D¹ \n(0wu+2n 0^\D¹ 0 \n(0hu-\n(0du-2n^\D¹ -\n(0wu-2n 0^)\D¹ 0 \n(0hu+\n(0du+2n^ ^\h^n(0wu+2n) . nr 0w +2n . nr 0d +1n . nr 0h +1n ..
```

space n A positive value of the integer~n (in hundredths of an em) sets the vertical spacing before the equation, a negative value sets the spacing after the equation, replacing the default values. This primitive provides an interface to groff’s \& escape (but with opposite sign). This keyword has no effect if the equation is part of a pic picture.

# Extended primitives

col n { ... }

```
ccol n { ... } lcol n { ... } rcol n { ... } pfile n { ... } cpile n { ... } lpile n { ... }
```

rpile n { ... } The integer value~n (in hundredths of an em) increases the vertical spacing between rows, using groff’s \& escape (the value has no effect in MathML mode). Negative values are possible but have no effect. If there is more than a single value given in a matrix, the biggest one is used.

# Customization

When eqn is generating troff markup, the appearance of equations is controlled by a large number of parameters. They have no effect when generating MathML mode, which pushes typesetting and fine motions downstream to a MathML rendering engine. These parameters can be set using the set command.

```
`set p n`
```

This sets parameter `p` to value `n`; `n` is an integer. For example,

```
`set x_height 45`
```

says that eqn should assume an x-height of 0.45~ems.

Possible parameters are as follows. Values are in units of hundredths of an em unless otherwise stated. These descriptions are intended to be expository rather than definitive.

- **minimum_size**
  eqn doesn’t set anything at a smaller point-size than this. The value is in points.
- **fat_offset**
  The `fat` primitive emboldens an equation by overprinting two copies of the equation horizontally offset by this amount. This parameter is not used in MathML mode; instead, fat text uses `<mstyle mathvariant='double-struck'>`
- **over_hang**
  A fraction bar is longer by twice this amount than the maximum of the widths of the numerator and denominator; in other words, it overhangs the numerator and denominator by at least this amount.
- **accent_width**
  When `bar` or `under` is applied to a single character, the line is this long.

Normally, `bar` or `under` produces a line whose length is the width of the object to which it applies; in the case of a single character, this tends to produce a line that looks too long.

- **delimiter_factor**
  Extensible delimiters produced with the `left` and `right` primitives have a combined height and depth of at least this many thousandths of twice the maximum amount by which the sub-equation that the delimiters enclose extends away from the axis.
- **delimiter_shortfall**
  Extensible delimiters produced with the `left` and `right` primitives have a combined height and depth not less than the difference of twice the maximum amount by which the sub-equation that the delimiters enclose extends away from the axis and this amount.
- **null_delimiter_space**
  This much horizontal space is inserted on each side of a fraction.
- **script_space**
  The width of subscripts and superscripts is increased by this amount.
- **thin_space**
  This amount of space is automatically inserted after punctuation characters.
- **medium_space**
  This amount of space is automatically inserted on either side of binary operators.
- **thick_space**
  This amount of space is automatically inserted on either side of relations.
- **x_height**
  The height of lowercase letters without ascenders such as `x`.
- **axis_height**
  The height above the baseline of the center of characters such as `+` and `.`. It is important that this value is correct for the font you are using.
- **default_rule_thickness**
  This should set to the thickness of the `ru` character, or the thickness of horizontal lines produced with the `D` escape sequence.
- **num1**
  The `over` command shifts up the numerator by at least this amount.
- **num2**
  The `smallover` command shifts up the numerator by at least this amount.
- **denom1**
  The `over` command shifts down the denominator by at least this amount.
- **denom2**
  The `smallover` command shifts down the denominator by at least this amount.
- **sup1**
  Normally superscripts are shifted up by at least this amount.
- **sup2**
  Superscripts within superscripts or upper limits or numerators of `smallover` fractions are shifted up by at least this amount. This is usually less than sup1.
- **sup3**
  Superscripts within denominators or square roots or
