# Control lights with your Pi

# Add some style

**13** CSS is used to create and apply a bunch of style effects to the web page. Move back to the Mobile_Lights folder and create a new folder named `static`. This is where the CSS file is saved. Create another new text file and add the code below, which sets out the *style* for the web page. You can customise the colours of the buttons from line 20 onwards. Save the file as `style.css` in the `static` folder.

```
```
body {
position: absolute;
margin: 0;
top: 0;
right: 0;
bottom: 0;
left: 0;
font-family: Arial, sans-serif;
font-size: 18px;
text-align: center;
}
```
```
div {
display: block;
width: 100%;
height: 50%;
}
```
```
div.a {
width: 100%;
height: 100%;
display: block;
}
```
```
div.on {
background: black;
}
```
```
div.on a {
color: white;
}
```
```
div.off a {
color: black;
}
```
```
a:link, a:visited {
text-decoration: none;
}
```
```

# Putting it all together

**14** The final part of the setup is to write the Python script that combines the index.html and style.css files with the Energenie socket control code similar to the one used in Step 7.

Open IDLE and start a new window, add the following code and save into your Mobile_Lights folder, naming it `mobile_lights.py`. Line 4 uses the route() decorator to tell Flask the HTML template to use to create the web page. Lines 7 and 11 uses app.route(‘on’) and app.route(‘off’) to tell Flask the function to trigger when the URL is clicked. In line 15 the run() function is used to run the local web server for our application. The `_ _name__ == __main__` makes sure the web server only runs if the script is executed directly from the Python interpreter and not used as an imported module.

```
```
from Flask import Flask, render_template
from energecie import switch_on, switch_off

app = Flask(_name_)

@app.route('/')
def index():
    return render_template('index.HTML')

@app.route('on/')
def on():
    switch_on()
    return render_template('index.HTML')

@app.route('off/')
def off():
    switch_off()
    return render_template('index.HTML')

if _name_ == _main_:
    app.run(debug=True, host='0.0.0.0')
```
```

![](bbox=[0.4, 0.68, 0.94, 0.95])