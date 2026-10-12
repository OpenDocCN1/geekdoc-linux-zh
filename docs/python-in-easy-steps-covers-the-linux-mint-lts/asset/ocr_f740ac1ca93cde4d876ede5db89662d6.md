![](bbox=[0.12, 0.08, 0.27, 0.23])

The examples in this chapter use the free Abyss Personal Edition web server available at www.aprelium.com Installed locally on your computer this can be addressed by the domain name localhost or by the IP address 127.0.0.1.

1 Ensure the web server is running and configured to execute Python scripts

![](bbox=[0.27, 0.38, 0.75, 0.45])

2 Next, start a new Python script by describing its generated output content type to be an HTML document
print( 'Content-type:text/html\r\n\n' )

![](bbox=[0.12, 0.54, 0.18, 0.61])

response.py

3 Now, add statements to output an entire web page including all its HTML markup tags

```
print('<!DOCTYPE HTML>\')
print('<html lang="en">\')
print('<head>\')
print('<meta charset="UTF-8">\')
print('<title>Python Response</title>\')
print('</head>\')
print('<body>\')
print('<h1>Hello From Python Online!</h1>\')
print('</body>\')
print('</html>\')
```

4 Finally, save the file in the web server’s HTML documents directory –