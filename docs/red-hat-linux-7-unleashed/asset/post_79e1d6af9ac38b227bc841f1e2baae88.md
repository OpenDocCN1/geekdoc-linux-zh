
To install the new version of the `sendmail` executable, first stop the currently running daemon with the following command:

```
[root@gonzo src]# /etc/rc.d/init.d/sendmail stop
```

Then type this:

```
[root@gonzo src]# ./Build install
```

With everything in place, you can restart the new daemon with the following:

```
[root@gonzo src]# /etc/rc.d/init.d/sendmail restart
```

## sendmail.cf: The Configuration File

With the advent of V.8, `sendmail` has shipped with a quick and easy way to automatically create a `sendmail.cf` file for you. In fact, it is highly recommended that you do *not* create or modify any `sendmail.cf` files manually. You can safely skip this section if you aren’t interested in the gory details regarding the `sendmail.cf` file. (I discuss the easy way to configure `sendmail` in the next section.)

The `sendmail.cf` file provides `sendmail` with its brains, and because it’s so important, this section covers it in fairly executing detail. Don’t worry if you don’t understand everything in this section the first time through. It will make more sense upon rereading and after you’ve had a chance to play with some configuration files of your own.

`sendmail`’s power lies in its flexibility, which comes from its configuration file, `sendmail.cf`. `sendmail.cf` statements compose a cryptic programming language that doesn’t inspire much confidence at first glance (but C language code probably didn’t either, the first time you saw it). However, learning the `sendmail.cf` language isn’t very hard, and you won’t have to learn the nitty-gritty details unless you plan to write a `sendmail.cf` from scratch—a bad idea at best.

### General Form of the Configuration File

Each line of the configuration file begins with a single command character that indicates the function and syntax of that line. Lines beginning with a `#` are comments, and blank lines are ignored. Lines beginning with a space or tab are continuations of the preceding line, although you should usually avoid continuations.

Table 10.1 shows the command characters and their functions as well as an example of their usage. This table is split into three parts corresponding to the three main functions of a configuration file, which are covered later in the section “A Functional Description of the Configuration File.”

#### Table 10.1 *sendmail.cf* Command Characters

| Command Character | Command Syntax and Example | Function |
|---|---|---|
| `#` | `#` comments are ignored | A comment line. Always use lots of comments. |
| | `# Standard RFC822 parsing` | |
| `D` | `Dx string` | Defines a macro `x` to have the string value `string`. |
| | `DM mailhub.gonz o.gov` | |
| | `D({MacroName})value` | Defines long macro `{MacroName}` to have the value `value`, then referenced later with `\$({MacroName})`. |
| `C` | `D(Relay)mailhub.gonz o.gov` | |
| | `CX word1, word2, and so on` | Defines a class `X` as `word1`, `word2`, and so on. |
| `F` | `CWlocalhost myusername` | |
| | `FX/path/to/a/file` | Defines a class `X` by reading it from a file. |
| `H` | `Fw/etc/mail/host_aliases` | |
| | `H?mailerflag?name::template` | Defines a mail header. |
| | `H?F?From: $q` | |
| `O` | `OX option arguments` | Sets option `X`. Most command-line options can be set in *sendmail.cf*. |
| | `OL9 # sets the log level to 9.` | |
| `P` | `Pclass=nn` | Sets mail delivery precedence based on the class of the mail. |
| | `Pjunk=100` | |
| `V` | `Vn` | Tells V.8 *sendmail* the version level of the configuration file. |
| | `V3` | |
| `K` | `Knane class arguments` | Defines a key file (database map). |
| `M` | `Kuucphosts hash /etc/mail/uucphosts` | |
| | `Mname,field_1=value_1, ...,` | Defines a mailer. |
| | `Mprog,P=/bin/sh,F=1sD, @A@sh -c $u` | |
| `S` | `Sm` | Begins a new rule set. |
| | `S22` | |
| `R` | `Rlhs rhs comment` | Defines a matching/rewriting rule. |
| | `R+ S:>S22 call ruleset 22` | |

### A Functional Description of the Configuration File

A configuration file does three things. First, it sets the environment for `sendmail` by telling it which options you want set and the locations of the files and databases it uses.

Second, a configuration file defines the characteristics of the mailers (delivery agents or MTAs) that `sendmail` uses after it decides where to route a letter. All configuration files must define local and program mailers to handle delivery to users on the local host, most of them also define one or more SMTP mailers, and sites that must handle UUCP mail define UUCP mailers.

Third, a configuration file specifies rulesets that rewrite sender and recipient addresses and select mailers. All rulesets are user-defined, but some have special meaning to `sendmail`. Ruleset 0, for example, is used to select a mailer. Rulesets 0, 1, 2, 3, and 4 all have special meaning to `sendmail` and are processed in a particular order (see the section “The S and R Operators: Rulesets and Rewriting Rules” later in this chapter).

The following sections cover the operators in more detail, in the order in which they appear in Table 10.1.

### The D Operator: Macros

Macros are like shell variables. After you define a macro’s value, you can refer to it later in the configuration file and its value will be substituted for the macro. For example, a configuration file might have many lines that mention the hypothetical mail hub `mailer.gonzo.gov`. Rather than type that name over and over, you can define a macro `R` (for relay mailer) as follows:

```
DRmailer.gonzo.gov
```

When `sendmail` encounters an `$R` in `sendmail.cf`, it substitutes the string `mailer.gonzo.gov`.

Macro names can be more than one character. You could, for example, define `D(Relay)mailer.gonzo.gov` then refer to it later with `$(Relay)`

Quite a few macros are defined by `sendmail` and shouldn't be redefined except to work around broken software. `sendmail` uses lowercase letters for its predefined macros. Uppercase letters can be used freely. V.8 `sendmail`'s predefined macros are fully documented in section 5.1.2 of the SIQ.

### The C and F Operators: Classes

Classes are similar to macros but are used for different purposes in *rewriting rules* (see “The S and R Operators: Rulesets and Rewriting Rules” later in this chapter). As with macros, classes are named by single characters. Lowercase letters are reserved for `sendmail` and uppercase letters for user-defined classes. A class contains one or more words. For example, you could define a class `H` containing all the hosts in the local domain as follows:

```
CH larry moe curly
```

For convenience, large classes can be continued on subsequent lines. The following definition of the class `H` is the same as the preceding one:

```
CH larry
CH moe
CH curly
```

You can also define a class by reading its words from a file:

```
CF/usr/local/lib/localhosts
```

If the file `/usr/local/lib/localhosts` contains the words `larry`, `moe`, and `curly`, one per line, this definition is equivalent to the preceding two.

Why use macros and classes? The best reason is that they centralize information in the configuration file. In the preceding example, if you decide to change the name of the mail hub from `mailer.gonzo.gov` to `mailhub.gonzo.gov`, you have to change only the definition of the `$R` macro for the configuration file to work as before. If the name `mailer.gonzo.gov` is scattered throughout the file, you might forget to change it in some places. Also, if important information is centralized, you can comment it extensively in a single place. Because configuration files tend to be obscure at best, a liberal dose of comments is a good antidote to that sinking feeling you get six months later, when you wonder why you made a change.

### The H Operator: Header Definitions

You probably won’t want to change the header definitions given in the V.8 `sendmail` configuration files because they already follow accepted standards. Here are some sample headers:

- `H?D?Date: $a`
- `H?F?Recent-From: $q`
- `H?F?From: $q`
- `H?x?Full-Name: $x`

Note that header definitions can use macros, which are expanded when inserted into a letter. For example, the `$x` macro used in the preceding `Full-Name:` header definition expands to the full name of the sender.

The optional `?mailerflag?` construct tells `sendmail` to insert a header only if the chosen mailer has that mailer flag set (see “The M Operator: Mailer Definitions” later in this chapter).

Suppose the definition of your local mailer has a flag `Q`, and `sendmail` selects that mailer to deliver a letter. If your configuration file contains a header definition like the following one, `sendmail` inserts that header into letters delivered through the local mailer, substituting the value of the macro `$F`:

```
H?Q?X-Fruit-of-the-day: $F
```

Why would you use the `?mailerflag?` feature? Different protocols can require different mail headers. Because they also need different mailers, you can define appropriate mailer flags for each in the mailer definition and use the `?mailerflag?` construct in the header definition to tell `sendmail` whether to insert the header.

### The O Operator: Setting Options

`sendmail` has many options that change its operation or tell it the location of files it uses. Most of them can be given either on the command line or in the configuration file. For example, you can specify the location of the aliases file in either place. To specify the aliases file on the command line, you use the `-oA` option:

```
$ /usr/sbin/sendmail -oA/etc/aliases [other arguments...]
```

To do the same thing in the configuration file, you include a line like this:

```
OA/etc/aliases
```

Either use is equivalent, but options such as the location of the aliases file rarely change, and most people set them in `sendmail.cf`. The V.8 `sendmail` options are fully described in the SIQ.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_326_0.png)
