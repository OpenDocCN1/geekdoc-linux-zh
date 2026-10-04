And sure enough, a couple of seconds later, we receive an email with the results of the survey (see Figure 6-3).

![](bbox=[0.24, 0.15, 0.68, 0.25])

*Figure 6-3: Email reply from our normal survey submission*

The survey is working just fine, which means it's likely that it was indeed some special character in our payload that caused the page to crash the first time. To pin down which character, we replay the previous normal form entry, adding one special character from our payload at a time until we close in on the suspect: {{ (the double braces). We may very well be dealing with a server-side template injection (SSTI) since templates often rely on double braces.

# Server-Side Template Injection

In many web development frameworks, templates are simple HTML files annotated with special variables that get replaced at runtime with dynamic values. Here are some of those special variables used in various frameworks:

```
# Ruby templates
<p>
<%= @product %>
</p>
# Play templates (Scala/Java)
<p>
Congratulations on product @product
</p>
# Jinja or Django templates
<p>
Congratulations on product {{product}}
</p>
```

This separation between the frontend of a web project (visualization in HTML/JavaScript) and the backend (controller or model in Python/Ruby/Java) is the cornerstone of many development frameworks and indeed many team organizations. The fun begins when the template itself is built dynamically using untrusted input. Take the following code, for instance. It produces a dynamic template using the render_template_string function, which is itself built using user input:

```
--snip--
template_str = """
    <div>
        <h1>hello</h1>
```