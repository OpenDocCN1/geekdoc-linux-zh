![](bbox=[0.0, 0.0, 1.0, 0.5])

# # Customizing web content with Tampermonkey
## Monkey Business

Even small changes in a web page can improve the browsing experience. Your preferred web browser provides all the tools you need to inject JavaScript to adapt the page. You just need a browser with its debugging tools, some knowledge of scripting, and the browser extension **Tampermonkey**.
By Reinhard E. Vogelmaier

The browser has become a very important component for interacting with the Internet. In recent years, browsers have evolved from being just a tool for interacting with static HTML to a comprehensive part of the infrastructure. The modern browser is a kind of operating system within the operating system, with a complete SDK for JavaScript, HTML, and CSS, along with features such as a visual debugger, a code inspector, options for network and performance monitoring, and much more. One interesting feature is that you can modify pages already loaded into the browser with your own scripts. The ability to customize web pages is useful for:
* quick bug fixes for intranet applications,
* fixing annoying behaviors of websites or web applications,
* implementing security features for users in the enterprise,
* adding convenient new features to publicly available websites, such as
automation tools or similar functionalities, and
* providing easy access to AI-based tools.

This flexibility and power push the browser far beyond its original role of simply rendering HTML.

**Before I Start...**

This article is intended for educational purposes only. My goal is to show you the power of the described technologies. All information you will find here is already available on the Internet – links are provided at the end of this article. As with many tools used for programming, these tools can also be used for illegal activities. If you decide to experiment, it is up to you to obey all applicable laws and treat any websites in a way that is compliant with their intended use.

**Welcome to the DOM**

One very exciting feature of today's web is the connection between the HTML document and the scripts contained in the document itself. You can consider this construct as similar to the chicken-and-egg question: The document contains the script and the script can modify the document, including the script itself. The technology that allows this is the DOM (Document Object Model) [1] [2]. When a web page is loaded, the browser constructs a DOM tree, which is a hierarchical representation of the document's content. This tree structure allows for efficient selection, addition, removal, and modification of elements on the web page. The DOM is not tied to any programming language; however, JavaScript is commonly used to interact with the DOM.

Style sheets (CSS) also are part of the DOM. A style sheet describes how the document will be displayed in the browser (the font, the colors, and so forth). The most interesting feature of the browser is that the user can inject code into the DOM. This code can interact with the HTML and CSS part of the document. This feature opens a world of possibilities.