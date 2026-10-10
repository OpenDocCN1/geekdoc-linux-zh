a powerful object-orientation system, the capability to throw program exceptions, and the general style of writing that both languages borrowed from C. Borrowed from Perl is the "it should just work" mentality where ease of use is favored over strictness. As a result, you will find a lot of "there is more than one way to do it" in PHP.

# Entering and Exiting PHP Mode

Unlike PHP\'s predecessors, you embed your PHP code inside your HTML, as opposed to the other way around. Before PHP, many websites had standard HTML pages for most of their content, linking to Perl CGI pages to do back-end processing when needed. With PHP, all your pages are capable of processing and containing HTML.

Each .php file is processed by PHP that looks for code to execute. PHP considers all the text it finds to be HTML, until it finds one of four things:

+   - `<?php`
+   - `<?`
+   - `<%`
+   - `<script language="php">`

The first option is the preferred method of entering PHP mode because it is guaranteed to work.

After you are in PHP mode, you can exit it by using `?>` (for `<?php` and `<?`), `;%` for `<%>` or `</script>` (for `<script language="php">`). This code example demonstrates entering and exiting PHP mode:

```
In HTML mode
<?php
    echo "In PHP mode";
?>
In HTML mode
In <?php echo "PHP"; ?> mode
```

# Variables

All variables in PHP start with a dollar sign (\$). Unlike many other languages, PHP does not have different types of variable for integers, floating-point numbers, arrays, or Booleans. They all start with a \$, and are interchangeable. As a result, PHP is a weakly typed language, which means you do not declare a variable as containing a specific type of data; you just use it however you want to.