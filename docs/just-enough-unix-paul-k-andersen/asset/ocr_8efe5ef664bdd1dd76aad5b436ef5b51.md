# 28 TUTORIAL:
PROGRAMMING IN PASCAL

It is a good idea to keep a
Pascal book handy as you
read through this chapter.

Pascal was developed by Niklaus Wirth during the late 1960s and early 1970s for
teaching good programming style. It has since become one of the most popular com-
puter languages. Although Pascal is not a standard part of UNIX, it is found on many
UNIX systems.

In this chapter, you will see how to write, compile, and run Pascal programs. This is
not intended to teach you Pascal; for that, you should consult a standard text on Pas-
cal. Indeed, it is a good idea to keep a Pascal book handy as you read through this
chapter.

# 28.1 The hello.p Program

We will begin with the program shown in Listing 28-1, which prints a message on
the standard output.

Listing 28-1
The hello.p pro-
gram.

```
```
(* Traditional first Pascal program. *)
program HelloWorld(output);
begin
writeln('Hello, world!')
end.
```
```

Let's examine this program in more detail:

+   *   `(* Traditional first Pascal program. *)`
+       Any text appearing between (`*` and `*`) is a *comment* and is ignored by the compiler. Comments are included for the benefit of the programmer and anyone else who may read the program later.