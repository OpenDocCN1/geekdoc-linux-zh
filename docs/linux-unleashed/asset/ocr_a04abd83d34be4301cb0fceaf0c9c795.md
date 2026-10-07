# ## Brackets, Bars, and Piles

As equations get more complicated, you will need to use more brackets and braces. You can generate brackets `([])`, braces `({})`, and parentheses `((()))` as needed using the `left` and `right` commands:

```
```
left { b over d+1} = left( alpha over {beta + gamma} )
```
```

This produces large braces, and parentheses are required to surround the terms. You can nest these, of course, with `geqn` adjusting the sizes properly. Braces can usually be bigger than brackets and parentheses.

For floor and ceiling characters, use the `left floor`, `right floor`, `left ceiling`, and `right ceiling` commands. For example:

```
```
left ceiling x over alpha right ceiling > left floor beta over 2 right floor
```
```

draws the equation with the proper vertical bars and ceiling and floor markers.

To create a pile of elements, use the reserved word `pile`. The following example shows the usage best:

```
```
X = left [ pile { a above b above c } right ]
```
```

This produces output with the three elements a, b, and c stacked vertically within big braces.

# ## Matrices

To make a matrix requires a little more work. You could probably make a matrix using the `pile` command, but if the elements are not of equal height, they will not line up. For that reason, use the keyword `matrix`. The general format is

```
```
matrix {
 ccol { elements }
 ccol { elements }
}
```
```

in which `ccol` produces centered columns. For left-adjusted columns, use `lcol`; `rcol` produces right-adjusted columns. The elements are specified individually. For example, the command

```
```
matrix {
 ccol { x sub 1 above y sub 1 }
 ccol { x sub 2 above y sub 2 }
}
```
```

produces the matrix

```
```
x^1 x^2
y^1 y^2
```
```