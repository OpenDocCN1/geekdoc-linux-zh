feature helps you to find the element in the DOM you want to change.

# ## Test Your Code

The browser SDK helps you test your code. Consider the “Hello, World” example. Open the SDK by pressing F12. Once the SDK is open, click on the Console tab. In the console, you can now enter the code you want to test. Start typing in the program from Listing 2. As you type in the line `const btn = document.create(‘element’‘button’);`, you will notice (after you enter the dot after `document`) that the SDK offers you autocompletion, which is very helpful. Once you finish the definition of the button, you can explore what you created using JavaScript or insert the newly created button on the web page using the line: `‘document.body.appendChild(btn);’` (Figure 4). Newly created button will pop up on the web page.

# ## 3D Furniture Models

Modeling your home can be a little tricky. You will find some excellent open source programs that will help you, such as Blender. But also, many furniture vendors provide 3D models of their products. IKEA, for example, offers a lot of products as 3D models together with an online tool to visualize them.

If you explore the DOM for these pages, you will find that a little JavaScript program (Listing 5) is used to open a 3D file with the extension .gltb – a royalty-free method of encoding 3D data. A tool such as Blender can easily use this data to help you model your home. Look at the web page of an IKEA product with 3D modeling and you will discover that the *View in 3D* button calls a script that contains, as a parameter, the 3D model you would like to download.

With this information, you can easily download the model. You can then import the model directly into Blender.

However it is not very convenient to have to right-click on the HTML area of the SDK in order to find out the URL of the .gltb file. A little user script can assist you. You know the name of the function and can search for it in the DOM with the help of the function `document.querySelector`. Once you find the function, you just need to use the URL in its parameters to discover where to get the 3D model.

![](bbox=[0.36, 0.09, 0.93, 0.33])

**Figure 4: Executing the JavaScript example in the console.**

Now that you know how to get the URL of the 3D model, you just need to create a clickable button that will let you download this URL (Figure 5). You can use the JavaScript function `‘create(‘element’‘button’ )’` for this step. The user script that performs this miracle is available on GitHub [8]. I recommend that you download the script and read it carefully – you will learn a lot from a very short bit of code.

# ## Cybersecurity

Downloading a user script you found on the Internet into Tampermonkey can be quite dangerous. As I have mentioned before, the user scripts you install can run on every page you load into your browser. Every script can control all communication between your browser and the contacted servers. They act on your behalf and can do things on your behalf that you might not even notice.

Obviously, the same holds for every extension you install into your browser. Therefore, it is important to only install scripts you trust, as well as to install only browser extensions you trust. Extensions should only be installed from the official distribution of your browser provider.

You will find statements on the Internet telling you that tools such as Tampermonkey allow people with no coding experience to use powerful

scripts. That is not a good idea at all. Install user scripts only if you completely understand what these scripts are doing. Do not use scripts that contain code you do not fully understand. Script code performing harmful operations on your behalf could be obfuscated in a way that is difficult to perceive unless you look carefully and know what you are looking at. The most secure scripts are those you develop and test yourself. The same suggestion holds for extensions.

Instead of trusting the scripts on the distribution site of your browser, why not create your own extension? It is easier than you might think. You can write the code in JavaScript, just as you do with user scripts.

You could also choose to use Tampermonkey in a sandbox for development purposes, once you have developed a robust user script, and then convert the whole application to the form of an extension.

BTW: I hope you do not perform online banking with your regular browser and instead use a specially hardened browser for this purpose.

```
**Listing 5: Fetching 3D Models**
`<script type="application/json" id="pip-xz-viewer-model">`  
`{  "productId":"<productId>",`  
`"productName":"<productName>",`  
`"url":"<URL 3D Model1>"}`  
`</script>`
```