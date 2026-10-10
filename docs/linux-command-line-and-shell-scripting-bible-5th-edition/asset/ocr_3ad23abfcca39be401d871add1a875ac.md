# Chapter 22: Advanced gawk

Here's a simple example demonstrating this format:

```
$ cat data4
10
5
13
50
34
$ gawk '{if ($1> 20) print $1}' data4
50
34
$
```

Not too complicated. If you need to execute multiple statements in the if statement, you must enclose them with braces:

```
$ gawk '{
> if ($1> 20)
> {
> x = $1 * 2
> print x
> }
}' data4
100
68
$
```

Be careful that you don't confuse the if statement braces with the braces used to start and stop the program script. The gawk program can detect missing braces and will produce an error message if you mess up:

```
$ gawk '{
> if ($1> 20)
> {
> x = $1 * 2
> print x
> }' data4
gawk: cmd. line:7: (END OF FILE)
gawk: cmd. line:7: parse error
$
```

The gawk if statement also supports the else clause, allowing you to execute one or more statements if the if statement condition fails. Here's an example of using the else clause:

```
$ gawk '{
> if ($1> 20)
> {
> x = $1 * 2
> print x
> } else
> {
> x = $1 / 2
> print x
```