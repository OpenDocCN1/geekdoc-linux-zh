# Rewrite Rules

# 231

the contents class w shows that robin is indeed in the list. Next we need ClassTest the address@hawk, which returns “Not in class w.” Again, a glance at the content of class w that hawk is not in the class. Finally, testing the address craig returns “Wrong format because the address is not in the format user@host. Using symbols, variables, classes, and literals, patterns can be constructed to match any type of e-mail address.

The patterns used in the ClassTest ruleset are realistic, but the templates are contrived. An address goes into a rule and an address comes out. Clearly, the strings found it, in class w, and Wrong format are not legitimate addresses. In the next section we look at how real templates are constructed and how they operate.

# Conditional Syntax

Before we leave the topic of pattern matching, the use of conditional syntax in rewrite rules defines a mention. The “if” ($?) “else” ($) syntax can legally be used in rewrite rules. In reality the $7 symbol ($) is never used in a rewrite rule. The pattern matching of a rewrite rule, by its very nature, is already a conditional. Adding an “if” to an existing conditional test would just increase the complexity of an already complex syntax. The “else” symbol ($) is sometimes used, but it is used as more of an “or” symbol—e.g., this $1 can be read as “this or that.”

Avoid using the conditional syntax in rewrite rules. Every rule starts with a conditional test. It is better to use two rules, each of which does one thing, and then to try to combine multiple tests in a single rule.

# Transforming the Address

The template field, from the right-hand side of the rewrite rule, defines the format used for rewriting the address. It is defined with the same things used to define the pattern: literals, variables, and special symbols. Literals in the transformation are written into the new address exactly as shown. Variables are expanded and then written. The symbols perform special functions. Each symbol that can be used in a template and its purpose are shown in Table 8.4.

![](bbox=[0.933, 0.465, 0.983, 0.503])

![](bbox=[0.933, 0.526, 0.983, 0.545])