# Chapter 9

looks better, but keep in mind the fact that function, method, and class names are all treated in a case-insensitive manner: Mandate and Mandate will refer to the same entity.

Defined constants created with define() or const are generally identified by being written in UPPERCASE. Those created in the global scope with define() should be preceded by some distinctive sequence of characters to prevent them from colliding with other constants that may be defined else where (see the PHP manual for many examples of this practice). This isn’t necessary for class constants, as their names are already preceded by the name of the class (or self:: within the class definition).

Since the distinction is already built into PHP’s syntax, rules for distinguishing variable/property names from function/method names are unnecessary compared with other languages; but there is no such distinction between classes and functions. You can have a class named Foo and a function named Foo, and the only way to tell the difference is that $v = new Foo(); uses the class, and $v = Foo(); uses the function.

```
$v = Foo(); Foo(); // something else again—to wit, something that won’t even compile; constructors can’t be called statically, and static functions can’t be constructors
```

On grammatical grounds, classes, variables, and properties are best described with nouns or noun phrases. Use the same parts of speech you would use in a corresponding verbal description of what the code does. Arrays and other collections should be given names that are plurals ($children, $pages). Boolean-valued properties should have names starting with “is” or “has” or other means of denoting a predicate ($isValid, $can_be_deleted). Classes should be named with nouns (UserFactory, NonPlayerCharacter); abstract classes can be given the prefix Abstract_ or Abstract to prevent accidental attempts to create objects from them (AbstractCollection, Abstract_Document), while the construct FooFactory is a common convention for denoting classes that provide static methods returning new objects of class Foo. Functions and methods can be named with verbs (traversePath(), anneal(), be_wonderful()), allowing adjectives, adverbs, and occasionally nouns for naming constants (COLOR_GREEN, QUICKLY, GOLDEN_RATIO).

# Hacking the Grammar

Some rules about coding style can be enforced by turning a violation into a parse error. If you know what you are doing, you can edit the zend_language_parser.y and zend_language_scanner.l files and rebuild PHP.

If, for example, you want to rule out the possibility of using constructs such as if() : … endif;, then from the lex file you’d remove the patterns matching endif, endwhile, endfor, endforeach, enddeclare, and endswitch (all of which appear in the <ST_IN_SCRIPTING> context); and from the yacc file, the corresponding T_END* token declarations, and the production rules:

```
```
unticked_statement:
    T_IF (' expr ') ':' inner_statement_list new_elseif_list new_else_single T_ENDIF ';'

while_statement:
    ':' inner_statement_list T_ENDWHILE ';'

for_statement:
    ':' inner_statement_list T_ENDFOR ';'

foreach_statement:
    ':' inner_statement_list T_ENDFOREACH ';'
```
```