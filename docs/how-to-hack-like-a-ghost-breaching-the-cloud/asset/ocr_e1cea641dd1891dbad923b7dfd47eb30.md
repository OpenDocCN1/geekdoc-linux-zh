```
<h3>%s</h3>
</div>
""" % user_input

return render_template_string(template_str)
```

In this Python snippet, if we were to inject a valid template directive like {{8*2}} in the user_input variable, it would be evaluated to 16 by the render_template_string method, meaning the page would display the result 16. The tricky thing is that every template engine has its own syntax, so not all would evaluate it in this way. While some will let you read files and execute arbitrary code, others will not even let you perform simple multiplication.

That’s why our first order of business is to gather more information about this potential vulnerability. We need to figure out what language we are dealing with and which framework it is running.

# Fingerprinting the Framework

Since his presentation on SSTI at Black Hat USA 2015, James Kettle’s famous diagram depicting ways to fingerprint a templating framework has been ripped off in every article you may come across about this vulnerability, including here in Figure 6-4. To explore how it works, we’ll enter a few different expressions in our survey form to see how they’re executed.

![](bbox=[0.07, 0.53, 0.92, 0.88])

Figure 6-4: Different SSTI payloads to fingerprint the templating framework