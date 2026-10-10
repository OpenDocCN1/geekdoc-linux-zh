You'll notice in Table 19.1 that these directives don't include any password com-plexity directives. The complexity setting directives work a bit differently, using a concept called credits.

With credits you define one or more types of password requirements, such as uppercase letters, lowercase letters, numbers, or special characters, and then define how many of each type the user passwords must contain (for example, one uppercase letter, two lowercase letters, and one number). This system allows passwords to be any length, as long as the mandated types and quantities are present, and in any order. Table 19.2 shows the pwquality.so complexity directives.

# TABLE 19.2 The PAM password complexity directives

| Directive | Description |
| :--- | :--- |
| dcredit | Number of numeric characters |
| lcredit | Number of lowercase characters |
| ocredit | Number of special characters |
| ucredit | Number of uppercase characters |

The credit directives are somewhat odd in that you specify the values as negative num-bers. For example, to specify a complexity rule that requires at least one numeric character, two lowercase characters, and one uppercase character, you'd use the rule

```
password requisite pwquality.so dcredit=-1 lcredit=-2 ucredit=-1
```

The required characters can appear anywhere in the password, and there can be more than the specified minimum present in the password value.

# Restricting the Root Account

The root user account is important in that it has complete privileges over all aspects of the Linux system. It's imperative that you protect who can use the root user account and where they can use it from.

There are several security best practices for helping restrict just how the root user account is used on your Linux system. The following sections discuss some basic security ideas you should think about.