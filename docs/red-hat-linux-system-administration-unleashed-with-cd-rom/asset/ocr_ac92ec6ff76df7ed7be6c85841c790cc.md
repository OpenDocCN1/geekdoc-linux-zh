The following is an example of using the LoadModule and AddModule directives to add PHP3 support to Apache:

```
LoadModule php3_module    modules/libphp3.so

AddModule mod_php3.c
```

There is also a directive that will clear the list of active modules: the ClearModuleList directive. After clearing the modules list, you can add modules back into the list using the AddModule directive.

# Conditional Directives Based Upon Modules

Apache has a directive that you can use when you want to execute certain directives conditionally based upon whether or not a specific module has been loaded into Apache. This is called the IfModule directive. A test is passed to the IfModule directive, and the conditional directives contained within it are only processed if the result of the test is true. Here is the syntax:

```
<IfModule [!]module_name>
Directive
Directive
...
</IfModule>
```

If the test fails, any directives contained between the <IfModule> and the </IfModule> are ignored. The format for the test can be one of two things:

+   - module_name
+   - !module_name

In the first case, the directives within the <IfModule> are only processed if the specified module name is loaded into Apache. In the second case, the specified directives are only processed if the specified module is not loaded into Apache.

# Default Apache Modules

There are a number of modules that come with Apache by default. In this section, we will take a look at each module and briefly cover what each module does. Each module has routines that implement various features of Apache.