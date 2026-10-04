
```
HTTP_ACCEPT_ENCODING gzip
HTTP_creation_time 991008556
HTTP_REFERER http://localhost:8080/Folder1/Subfolder/method2/manage_edit
SERVER_PROTOCOL HTTP
SERVER_PORT 8080
PATH_INFO /Folder1/Subfolder/method2
HTTP_HOST localhost:8080
REQUEST_METHOD GET
PATH_TRANSLATED Folder1/Subfoldermethod2
SCRIPT_NAME -
SERVER_SOFTWARE Zope/2.3 (binary release, python 1.5.2) ZServer/1.1
HTTP_ACCEPT_LANGUAGE en
HTTP_ACCEPT_CHARSET no-8859-1;*.utf-8
HTTP_ACCEPT image/* -x-snapshot,image/jpeg,image/png,image/**
REMOTE_ADDR 127.0.0.1
```

The ability to display the entire REQUEST object is particularly useful when you are developing and debugging a Zope application. It also allows you to view the values of the CGI-defined query variables submitted by the client.

Table 4-6: Extract from a REQUEST

| Attribute Name | Explanation | Screen Output |
| --- | --- | --- |
| AUTHENTICATED_USER | The object of the user currently logged in. The user is "Anonymous User" if no user is logged in. | AUTHENTICATED_USER For example, manager |
| AUTHENTICATION PATH | Path of the acl_users folder in which the current user is defined. | AUTHENTICATION PATH /Test/Folder1 if the current user is defined in the acl_users folder in /Test/Folder |
| PARENTS | Returns highest folder-like object in the object hierarchy starting from the current document backward. PARENTS[-1] always refers to the root folder. | "PARENTS[0]['id']" "PARENTS[1]['title']" GWS_Training Zone |
| URL, URLO | Returns the full URL of the URL object requested by the client's web browser. | http://localhost:8080/Order1/Test/index.html |

Table 4-7: REQUEST Object Attributes

# Table 4-7: REQUEST Object Attributes (continued)

| Attribute Name | Explanation | Screen Output |
| --- | --- | --- |
| URL1 - URLn | The URL path to the object up to the nth object above it in the path. Used to create links to objects higher in the Zoe hierarchy. | URL1 URL2 | http://localhost:8080/Order/1 |
| BASE | Returns the base of the URL requested. | BASE BASE0 | http://localhost:8080 |
| BASE1 - BASEn | The URL path with n objects is added to the BASE. | BASE1 | http://localhost:2080/Order/1 |
| cookies | The result is the values set "REQUEST.cookies" as cookies in the form of a dictionary. | "REQUEST.cookies" | {''tree-s':'eljZTF23HANHPW/VYHUQUALYIEA','10','dpref_rows':'65'}\ |
| form | The result is the values "REQUEST.form" by a form in dictionary format. | "REQUEST.form['field']" | {''Field 1':'hello','myfield':'hello'} |
| has_key(name) | 1, if the specified variable name is contained in the REQUEST; 0, if the specified variable name is not contained in the REQUEST. | "REQUEST.has_key('URL0.has_key('URL9')" | 1 (because URL0 is contained in the REQUEST) 0 (because URL9 is not contained in the REQUEST) |
| set(name, value) | Sets a variable in REQUEST with the specified name and value. | "REQUEST.set('myvar','Content of myvar')" | None (has no result which can be evaluated) |
| get(name[,default]) | Retrieves a variable by name from REQUEST and optionally allows you to specify a default value if the variable is not set. | "REQUEST.get('myvar','')" | The value stored in myvar or empty string if myvar is not set |

## 4.3.4 The call Tag

The call tag works like the var tag, allowing you to carry variables, carry methods, and so on. except that it gets text and does not carry out text substitution.

For example, the following call displays no result on the screen and is therefore not very useful.

```
<html-call name="AUTHENTICATED_USER">
```

The tag is, however, very useful for methods whose results are not to be displayed. For example, many Python methods return None as sign that they have run successfully. If you don't want this message displayed in your document, use the call tag.

The call tag is also frequently used to set variables. For example, you should want to create a list in a DTML method, you could do the following:

```
<html-var expr="REQUEST.set('list', ['Schopenhauer', 'Freud'])">
```

The called method returns None and the var tag inserts this into the source text, "None" appears in the rendered output of the document. If you use the call tag instead, your list is generated without any text being added to the output, as follows:

```
<html-var expr="REQUEST.set('list', ['Schopenhauer', 'Freud'])">
```

To prove that the lists were actually created, you can display the REQUEST object using the dtml-var tag.
The call tag is very useful if you want certain actions to be carried out directly affecting the output of the document. For example, you want to add a new element to a list (easily done with the list's append method), and you want the list to be displayed immediately. Were we to use the var tag on its own, we would not be able to achieve the desired results because "None" is returned by the append method. The best thing to do is execute the append method using the call tag and then render the list using the var tag:

```
<html-var expr="list.append('Nietzsche')">
<html-var name="list">
```

The following text appears in the rendered output of your document:

['Schopenhauer', 'Freud', 'Nietzsche']

## 4.3.5 The if Tag

The tag is used for the conditional evaluation of source text, meaning that Zope DTML source code is executed only if a specific condition has been fulfilled. This condition is specified in the name or expr attribute of the opening tag. The value of the name or expression attribute is considered true if all the following criteria are met:

- 1. The result is zero.
- 2. The result is an empty string, list, or dictionary.
- 3. The result is not None.

Conversely, the value of the name or expression attribute is considered false if:

- 1. The result is zero.
- 2. The result is an empty string, list, or dictionary.
- 3. The result is not None.

The tag is a non-empty block that contains DTML code to be executed conditionally between its start and end tags. For example:

```
<dt-if name="title">
title of this object is: <dtml-var name="title">
```

Here, a check occurs (Line 1) to determine whether there a title that can be consulted. If one exists, the tag body (Line 2) is evaluated, and the object's title is retrieved. If the condition is not fulfilled, the instructions defined by the else tag are carried out. When specifying the name, it will result in a Zope error.

NOTE: When using the name, returns a false value if the name is not in the namespace. In an expression, specifying a name not in the namespace.

The above example illustrates only the most simple variant of the if. In fact, the tag can be used in four ways, as shown in Table 4-8.

### 4.3.5.1 The Else inside the if Tag

When inserted within the if tag, the else tag introduces the text to be processed if no condition above is fulfilled. We can extend the example as follows:

```
<dtml-if name="title">
title of this object is: <dtml-var name="title">
<dtml-else>
This object has no title.<br>
The Id of this object is: <dtml-var name="id">
</dtml-if>
```

Table 4-8: Using the if Tag

| if Use | Example |
| --- | --- |
| The start and end tags enclose the tag body. | <dt-if Condition>
>Tag Body
</dt-if> |
| The start and end tags enclose the tag body and an else tag. | <dt-if Condition>
>Tag Body
<dt-else>
>Instruction
</dt-if> |
| The start and end tags enclose the tag body as well as one or more elif tags. | <dt-if Condition>
>Tag Body
<dt-elif Condition>
>Instructions
</dt-if> |
| The start and end tags enclose the tag body, one or more elif tags, and an else tag. | <dt-if Condition>
>Tag Body
<dt-elif Condition>
>Instructions
<dt-else>
>Instructions
</dt-if> |

## 4.3.6 The elif Tag

Just as the else tags to be used to formulate alternative actions, you can use one or more elif tags with corresponding instructions to be carried out. The elif tag is non-empty and accepts the var and expr attributes just like the if tag.
The following structure is used:

```
1: <dt-if Condition1>
2: Code for condition1
3: <dt-elif Condition2>
4: Code for condition2
5: <dt-elif Condition3>
6: Code for condition3
7: </dt-if>
```
