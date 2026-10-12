Therefore, 2    is literally substituted by the preprocessor whenever the defined name T    occurs in the program.

The fact that the preprocessor performs a literal text substitution whenever the defined name occurs explains why you don’t usually want to end your #    statement with a semicolon. If you did, then the semicolon would also be substituted into the program whenever the defined name appeared. If you had defined P   as

Click here to view code image

#

and then written

r

the preprocessor would replace the occurrence of the defined name P   with 3    . The compiler would therefore see this statement as

Click here to view code image

r

after the preprocessor had made its substitution, which would result in a syntax error. A preprocessor definition does not have to be a valid C expression in its own right—just so long as wherever it is used the resulting expression is valid. For instance, the definition

#

is legitimate, even though what appears after L    is not a syntactically valid expression. You can use your definition of L    in a statement such as

×

to shift the contents of y to the left eight bits and assign the result to x. Of a much more practical nature, you can set up the definitions

#

#

and then write expressions such as

i

and

i

You can even include a #    statement for the equality test:

#

and then write the statement

Click here to view code image

i

thus removing the very real possibility of mistakenly using a single equal sign for the equality test, as well as improving the statement’s readability.