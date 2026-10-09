![](bbox=[0.17, 0.05, 0.82, 0.33])

Or if send a parameter of anything at all you will get surprising results:

![](bbox=[0.17, 0.45, 0.82, 0.74])

What we are doing here is using the string parameter argv[1] as a background colour code inside an HTML body tag. We change the Content-type specification to text/html and miraculously now our program is generating HTML content. A language being expressed inside another language. Web browsers understand a limited set of colour terms and colours can be also defined hexadecimal codes such as #FFFFFF (white) #FF0000 (red) #00FF00 (green) #0000FF (blue).