before. Note the addition of the json module: we’ll be using that later as we start handling Twitter data. Having Flask use a rendering engine is super-simple. Flask comes packaged with the Jinja2 template rendering engine, so we’ve nothing to install – we just need to import the package into the project. We can do this by adding render_template to the end of our from flask import […] statement.

# **03  Our first template**

Now that we have a rendering engine, we need to create some templates for it to use. In the root of our project’s folder, create a new folder called templates. Whenever we try to render a template, Flask will look in this folder for the template specified. To get to grips with templating, we’ll rewrite some of our authentication logic to use a template, rather than manually requesting endpoints. In templates, create an index.html file. You can treat this HTML file like any other – included in the resources for this tutorial an index.html that includes all of the necessary head tags and <DOCTYPE> declarations for this file.

# **04  Rendering our template**

In server.py, let’s create a route for '/' to handle the authorisation process.

```
`@app.route('/')`
`def home():`

`    if not 'oauth_token' in session:`
`        session.clear()`
`        session['oauth_secret'] = '`
`            session['oauth_token'] = '`
`    return render_template('index.html')`
```

It’s a simple function: all we want to do is check whether or not we have an oauth_token already and create those properties in the Flask session so we don’t throw an error if we try to access it erroneously. In order to send our generated template in response to the request, we return render_template('index.html').

# **05  Template variables**

We can choose to send variables to our template with render_template('index.html', variableOne=value, variableTwo=value) but in this instance we don’t need to as each template has access to the request and session variables.

```
`{% if session['oauth_token'] != "" %}`
`    <!>Already Authorised<!>`
`    <div class="dialog">`
`        <!>Hello, you’ve authenticated<!> Let’s <a href='/get-tweets'>get some tweets<!>`
`    </div>`
`{% else %}`
`    <!>Authorisation required<!>`
`    <div class="dialog">`
`        <!>We need to <a href='/authenticate'>authenticate<!>`
`    </div>`
`{% endif %}`
```

The BSD-licensed Flask is easy to set up and use – check out the website for more info

![](bbox=[0.37, 0.43, 0.88, 0.54])

```
`from flask import Flask`
`app = Flask(__name__)`

`@app.route('/')`
`def hello():`
`    return 'Hello World!'`

`if __name__ == '__main__':`
`    app.run()`
```

# And Easy to Setup

```
`$ pip install Flask`
`$ python hello.py`
`* Running on http://localhost:5000/`
```

# Interested?

+   › Download latest release (0.10)
› Read the documentation or download as PDF and zipped HTML
› Join the mailinglist
› Fork it on github
› Add issues and feature requests