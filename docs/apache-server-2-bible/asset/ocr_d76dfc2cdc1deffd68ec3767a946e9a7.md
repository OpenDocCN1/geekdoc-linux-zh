![](bbox=[0.17, 0.13, 0.58, 0.64])

**Figure 12-7:** CGI Web form-processing diagram.

# Looking at formwizard.pl

The *formwizard.pl* script implements this flow diagram. In the *formwizard.ini* configuration file, the *register.html* fields have these restrictions:

+   - The *name* field is required and set to be from 3 to 50 characters in length. The field value must be composed of characters ranging from a- to z and the period. If the field value passes the length and pattern tests, it is stored as a string in which each word starts with a capital letter.
+   - The *email* field is also required and it must be between 6 and 100 characters. Acceptable characters for an e-mail address are a to z, 0 to 9, dash (-), underscore (_), period, and the AT (@) symbol. The *email* pattern test is applied to the value of this field and if all (length, character set, and pattern) tests are passed by the value, it is stored in lowercase format.