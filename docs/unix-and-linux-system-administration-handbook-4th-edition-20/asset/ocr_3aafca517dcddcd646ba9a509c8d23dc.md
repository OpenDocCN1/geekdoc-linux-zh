# Chapter 20 Electronic Mail

Although Exim is as advertised as being easy to configure and is extensively documented, there is quite a learning curve for new users. The section "How Exim receives and delivers mail" in the specification document is essential reading for newcomers. It gives a good feel for the underlying concepts of the system.

When assigned a value, the Exim language's predefined options cause an action to occur. There are also about 120 predefined variables whose values may change as a result of one of the actions. These variables can be included in conditional statements.

The language for evaluating statements and the like may remind you of the reverse Polish notation used during the heyday of Hewlett-Packard calculators. Let's look at a simple example. In the line

```
acl_smtp_rcpt = ${if [25]$interface_part \ \
[acl_check_rcpt] [acl_check_rcpt_submit] }
```

acl_smtp_rcpt option, when set, causes an ACL to be implemented for each recipient (SMTP RCPT command) in the SMTP exchange. The value assigned to this option is either acl_check_rcpt or acl_check_rcpt_submit, depending on whether or not the Exim variable $interface_port has value 25.

We do not detail the Exim configuration language further, but refer you to its extensive documentation. In particular, pay close attention to the string section of the Exim specification.

# Exim configuration file

Exim's run-behavior is controlled by a single configuration file, usually called /usr/exim/configure. Its name is one of the required variables specified in the EDITIME file and compiled into the binary.

The supplied default configuration file, src/configure.default, is well commented and a good starting place for sites just setting up Exim. In fact, we recommend that you do not stray far from it until really understand the Exim paradigm and need to elaborate on the default configuration for a specific purpose. Exim works to support common situations and has sensible defaults.

It is also helpful to stick with the variable names used in the default config file because they are asked by the exim-users mailing list who will be answering your configuration questions.

exim prints a message to stderr and exits if you have a syntax error in your configuration file. It doesn't catch all syntax errors immediately, however because it does not expand variables until it needs to.

The order of entries in the configuration file is not quite arbitrary; the global configuration options section must be first and must exist. All other sections are optional and can appear in any order.