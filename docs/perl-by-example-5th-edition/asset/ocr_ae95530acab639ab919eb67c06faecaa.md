# EXPLANATION

+   1  The scalar $animal is assigned the value "dog". The name animal is stored in the symbol table along with a reference to its value dog.
+   2  The scalar $dog is assigned the string "Lady".
+   3  The variable ${animal} evaluates to Lady. This is a symbolic reference. $animal, one variable, is evaluated to dog. The first dollar sign causes dog to become $dog, and references its underlying value, "Lady". One variable has referenced another.
+   4  $animal will be evaluated to its value, dog. The dollar sign, prepended to the result of the evaluation leaves $dog="Lassie" as the statement.
+   5  The value of ${animal}; that is, $dog is Lassie, is printed.
+   6\-8  Now we will define an array, a hash, and a subroutine.
+   9\-11  The symbolic references are given the names of variables.
+   12  By preceding the symbolic reference with an @ sign, Perl will retrieve the values stored in the array @letters.
+   13  Now we get the first element in @letters using the symbolic reference.
+   14  The subroutine is called using the symbolic reference. This is one of the rare times you will use & to call a subroutine.

# EXAMPLE 12.17

```
use feature qw(say);
$perm1="readonly";
$perm2="read/write";
$perm3="execute";

foreach $n (1..3) {
  $attr = "perm". $n;
  say "$attr is ${$attr}";
}

(Output)
perm1 is readonly
perm2 is read/write
perm3 is execute
```

# EXPLANATION

+   1  Here is a case where the variables are numbered. (This is a technique used in Shell programming for dealing with numbered files, such as foo1, foo2, and foo3. Here, it would be much better to use a hash or an array since strict will complain. Symbolic references cannot be lexically scoped.)
+   2  The foreach loop will iterate through the numbers 1, 2, 3.
+   3  The value of the number, $n, is appended to the string perm and then assigned to the variable $attr. The value of $attr is the name of variable perm1 (first time through the loop) and when used as a symbolic reference, ${attr} evaluates to the string "readonly" that was assigned to $perm1 on line 1. The next time through the loop, $attr will be perm2, and so forth.