
# fnsearch 391

Another simple filter expression is one that tests the value of a particular attribute.
The following command finds objects with ages less than 17.

```
$ fnsearch composite-name "age < 17"
```

String values are indicated by enclosing the string in single quotes. For example,
The following command finds all red objects.

```
$ fnsearch composite-name "color == 'red'"
```

Note that the double quotes ("") in this example are not part of the filter expression.
Instead, they prevent the shell from interpreting the white space and single quotes that
are part of the expression.

# Logical Operators

You can compose simple filter expressions by using the logical operators and, or, and
not, as shown in the following example.

```
$ fnsearch composite-name "age >= 35 and user_citizen"
```

You can use parentheses to group expressions, as shown in the following example.

```
$ fnsearch composite-name "not (make == 'olds' and year == 1973)"
```

The precedence of operators is as follows, in order of increasing precedence:

- or.
- and.
- not.
- Relational operators.

The logical operators and or or or are left-associative.

# Relational Operators

You can use the following relational operators to compare an attribute to a supplied
value:

```
== true if at least one value of the attribute is equal to the supplied value.
!= true if none of the attribute's values are equal to the supplied value.
< true if at least one value of the attribute is less than the supplied value.
<= true if at least one value of the attribute is less or equal to the supplied value.
> true if at least one value of the attribute is greater than the supplied value.
>= true if at least one value of the attribute is greater than or equal to the supplied value.
~ true if at least one value of the attribute matches the supplied value
according to some context-specific approximate matching criterion.
This criterion must subsum strict equality.
```

Comparisons and ordering are specific to the syntax or rules of the attribute being
tested.

# Displaying Selected Attributes

By default, the fnsearch command displays the names and all of the attributes of each object matching the search criteria. You can restrict the list of attributes by using the -a command-line option. In the following example, only the color and shape attributes of small objects are displayed.

```
% fnsearch composite-name -a color -a shape "size = 'small'"
```

The format of an attribute identifier is taken to be FN_ID_STRING(an ASCII string) by default. To name an attribute identifier that is an OID or a DCE UUID, prefix the attribute name by -0 or -u.

- -0 The identifier format is FN_ID_ISO_OID, an ASN.1, dot-separated, integer list string.
- -U The identifier format is FN_ID_DCE_UUID, a DCE UUID in string form.

The following examples show the -0 and -U attributes.

```
% fnsearch composite-name -a 0 2.5.4.0 "shoe_size = 9"
% fnsearch composite-name -a -U 0006aa46-5e97-105f-9828-8190285baa77
"blowing_avg > 200"
```

# Filter Arguments

You can replace some place of a filter expression with a substitution token which is a percent sign (%) followed by a single character. The value of this portion of the expression is then given in a filter argument that follows the filter expression, in much the same way as is in print(f). The available substitution tokens are:

- %a Attribute.
- %s String.
- %i Identifier.
- %v Attribute value.

> Note — The only syntax currently supported for %v is fn_attr_syntax_ascii.

For example, you could write the following command

```
% fnsearch composite-name "color == 'red'
```

as

```
% fnsearch composite-name "%a == 'red"
```

or or

```
% fnsearch composite-name "%a == %s" color red
```

Substitution tokens are helpful for writing shell scripts when the values of the filter arguments will be generated at runtime.

By default, the identifier of an attribute, such as the color attribute above, is taken to be FN_ID_STRING(an ASCII string). Substitution tokens enable the use of OSI OIDs and DCE UUIDs instead. Prefix the filter argument by -O or -U, with the same meaning as in the -a command-line option:

- -O The identifier format is FN_ID_ISO_OID_STRING, ASN. 1, dot-separated, integer list string.
- -U The identifier format is FN_ID_DCE_UUID, a DCE UUID in string.

For example:
`fnsearch composite-name "%a -O 2.5.4.0`

and
`fnsearch composite-name "%a"=='red' -U 0006aa46-5e97-105f-9288-81902baa77

# Wild-card Strings

A wild-circleded string is a sequence of alternating wild-card specifiers and strings. The wild-card specifier is denoted by the asterisk (*) and means 0 or more occurrences of any character.

Use wild-carded strings to specify substring matches. The following are some examples of wild-carded strings and their meanings.

- * Any string.
- '*tom*' The string tom.
- '*harv*' Any string starting with harv.
- '*ing' Any string ending with ing.
- '*a''*b' Any string starting with a and ending with b.
- '*jo***ph***ne*' Any string starting with jo and containing the substring ph, and containing the substring ne in the portion of the string following ph, and ending with er.

- %s* Any string starting with the string supplied as a filter argument.
- '*bix***s Any string starting with bix and ending with the string supplied as a filter argument.

# Extended Operations

Extended operators are predicates (functions that return true or false) that you can freely mix with other operators in a filter expression. You specify an extended operation by giving the operation name as a quoted string, followed by an argument in parentheses. The following three extended operations are currently defined:

- 'name' (Wildcardedstring) true if the object matches the supplied wild-carded string.
- 'reftype' (Identifier) true if the reference type of the object is equal to the supplied identifier.
- 'addrtype' (Identifier) true if any of the address types in the reference of the object are the supplied identifier.

The following example shows a search for objects whose names start with bill and who have IQ attributes over 80.

```
% fnsearch composite-name 'name'('bill*') and IQ > 80
```

# Grammar of Filter Expressions

The complete grammar of filter expressions is given below. It is based on the grammar defined by the X/Open Federated Naming (XFN) specification
FN_search_filter(t3N).

String literals in this grammar are enclosed in double quotes; the quotes are not themselves part of the expression. Use braces for grouping; brackets for optional elements. An unquoted asterisk (*) signifies 0 or more occurrences of the preceding element, a plus sign (+) signifies one or more occurrences.

```
FilterExpr ::= [Expr]
```

```
RelOp ::= "=" | "!=" | "<" | "<=" | ">" | ">=" | ".-
Attribute ::=Char*
      |%a
```

```
Value ::=Integer
      WildcardedString
      |%v
```

```
WildcardedString ::= :=
      ""
      |String
      {String "**"}+ [String]
      |("** String+) + [""]
```

(that is, an alternating sequence of String and \*)

```
String ::="*" Char |*"
      |%s
```

```
Ext ::="name" (WildcardedString ")
      |"retype" (Identifier")
      |"addrtype" (Identifier")
```

```
Identifier ::="*" Char |*"
      |%i **
```

```
Char ::=an element of the Portable Character Set (ASCII)
| a character in the repertoire of a string representation

**Note** - If the filter expression is empty, it evaluates to true (all objects satisfy it).

If the identifier in any subexpression of the filter expression does not exist as an attribute of an object, then the innermost logical expression containing that identifier evaluates to false.

# **Exit Status**

+    0 Operation was successful.
 1 Operation failed.

# **Attributes**

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwns |

# **See Also**

printf(1), FN_search_control_t(3N), FN_search_filter_t(3N), fn_attr_ext_search(3N), fn_attr_search(3N), attributes(5), fns(5)

# **fnunbind** — Unbind the Reference from an FNS Name

# **Synopsis**

```
/usr/bin/fnunbind composite-name
```

# **Description**

fnunbind unbind the Federated Naming Service (FNS) reference of composite-name.

For example, the following command unbinds the reference to which the name user/jsmith/fs was bound.

```
castle% fnbind user/jsmith/fs/
```

> **Note** - An fnunbind on a name of a context fails because such a context cannot be unbound unless it is first destroyed with the fdestroy command.
