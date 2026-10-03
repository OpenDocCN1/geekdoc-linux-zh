value with a known system; it installs the Solaris software specified by the class file listed in the class file field.

```
#
#   @(#)rules 1.12 94/07/27 SMI
#
# The rules file is a text file used to create the rules.ok file for
# a custom JumpStart installation. The rules file is a lookup table
# consisting of one or more rules that define matches between system
# attributes and profiles.
#
# This example rules file contains:
#   o syntax of a rule used in the rules file
#   o rule_keyword and rule_value descriptions
#   o rule examples
#
# See the installation manual for a complete description of the rules file.
#
#
#######################################################################
# RULE SYNTAX:
#
# [!]rule_keyword rule_value [& [!]rule_keyword rule_value]... begin profile finish
#
#   "[ ]"  indicates an optional expression or field
#   "..."  indicates the preceding expression may be repeated
#   "&&"   used to "logically AND" rule_keyword and rule_value pairs together
#   "!"    indicates negation of the following rule_keyword
#
# rule_keyword      a predefined keyword that describes a general system
#                   attribute. It is used with the rule_value to match a
#                   system with the same attribute to a profile.
#
# rule_value  a value that provides the specific system attribute
#             for the corresponding rule_keyword. A rule_value can
#             be text or a range of values (NN-MM).
#             To match a range of values, a system's value must be
#             greater than or equal to NN and less than or equal to MM.
#
# begin       a file name of an optional Bourne shell script
#             that will be executed before the installation begins.
#             If no begin script exists, you must enter a minus sign(-)
#             in this field.
#
# profile     a file name of a text file used as a template by the
#             custom JumpStart installation software that defines how
#             to install Solaris on a system.
#
# finish      a file name of an optional Bourne shell script
#             that will be executed after the installation completes.
#             If no finish script exists, you must enter a minus sign (-)
#             in this field.
#
```