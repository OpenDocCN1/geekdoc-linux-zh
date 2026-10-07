# synchronized

The synchronized modifier is used to control access to critical code in multithreaded programs. Multithreading is an extensive topic in its own right and is covered in Chapter 7.

# Modifiers and Features

Not all modifiers can be applied to all features. Top-level classes may not be protected. Methods may not be transient. Static is so general that you can apply it to free-floating blocks of code.

Table 3.2 shows all the possible combinations of features and modifiers. Note that classes here are strictly top-level (that is, not inner) classes. (Inner classes are covered in Chapter 6.)

TABLE 3.2 All Possible Combinations of Features and Modifiers
| Modifier | Class | Variable | Method | Constructor | Free-Floating Block |
|---|---|---|---|---||
| public | yes | yes | yes | yes | no |
| protected | no | yes | yes | yes | no |
| (default)* | yes | yes | yes | yes | yes |
| private | no | yes | yes | yes | no |
| final | yes | yes | yes | no | no |
| abstract | yes | no | yes | no | no |
| static | no | yes | yes | no | yes |
| native | no | no | yes | no | no |
| transient | no | yes | no | no | no |
| volatile | no | yes | no | no | no |
| synchronized | no | no | yes | no | yes |

*Default is not a modifier; it is just the name of the access if no modifier is specified.