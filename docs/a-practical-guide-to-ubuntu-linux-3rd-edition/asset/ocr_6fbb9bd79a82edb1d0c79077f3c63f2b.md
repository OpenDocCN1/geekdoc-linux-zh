To see how type maps work, create the following files in /var/www:

```
$ cat /var/www/index.html.en
<html><body><h1>He\110</h1></body></html>
$ cat /var/www/index.html.fr
<html><body><h1>Bonjour</h1></body></html>
```

```
$ cat /var/www/index.html.var
URI: index.html.en
Content-Language: en
Content-type: text/html; charset=ISO-8859-1

URI: index.html.fr
Content-Language: fr
Content-type: text/html; charset=ISO-8859-1
```

If your browser’s preferred language is set to English (en), it will display the **Hello** page when you browse to http://localhost/index.html.var. If your browser’s preferred language is set to French (fr), it will display the **Bonjour** page. (With the MultiViews option turned on, as it is by default, the browser displays the correct page when you browse to http://localhost. See the next section.) You can change the default language in Firefox by selecting **Edit\>Preferences** from the menubar, clicking the **Advanced** icon and then the **General** tab, and finally clicking **Choose** from the **Languages** frame. Select a language from the **Select a language** to add combo box, if necessary, and then move the preferred language to the top of the list. In the example, the **charset** assignments are not necessary. However, they would be helpful if you were sending pages using different encodings such as English, Russian, and Korean.

Type maps are used for more than selecting among different languages. Instead of matching **Content-Language** as in the preceding example, the map could match **Content-type** and send jpeg or png images depending on how the browser’s preferences are set.

# MultiViews

When you set the MultiViews option on a directory, Apache attempts to deliver the correct page when a requested resource does not exist. The following lines in the **sites-avaiable/default** file set MultiViews for the document root ( /):

```
<Directory /var/www/>
    Options Indexes FollowSymlinks MultiViews
...
```

To see how MultiViews work, remove the /var/www/index.html.var type map file that you created in the preceding section. Now browse to http://localhost. The proper language page is displayed, but why?

When a browser sends Apache a request for a directory, Apache looks for a file named **index.html** in that directory. In the example, Apache does not find the file. If MultiViews is enabled, as it is by default, Apache looks for files named **index.html**.*.