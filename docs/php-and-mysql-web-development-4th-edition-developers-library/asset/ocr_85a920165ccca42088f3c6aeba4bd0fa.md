as a transaction to make sure that all score modifications succeed as a unit or all are canceled if an error occurs.

# 9.2.1.1. Collecting Web Input in PHP

Before implementing the score_entry.php script, we must take a slight detour to discuss how input parameters work in PHP.The script needs to perform several different actions, which means that it must pass a status value from page to page so that the script can tell what it's supposed to do each time it's invoked. One way to do this is to pass parameters at the end of the URL. For example, we can add a parameter named action to the script URL like this:

```
http://localhost/gp/score_entry.php?action=value
```

Parameter values may also come from the contents of a form submitted by the user. Each field in the form that is returned by the user's browser as part of a form submission will have a name and a value.

PHP makes input parameters available to scripts through special arrays. Parameters encoded at the end of a URL and sent as part of a get request are placed in the $_GET superglobal array and $$_GET superglobal array. For parameters received in a post request (such as the contents of a form that has a method attribute value of post), the parameters are placed in the $_POST superglobal array and $$POST_VARS superglobal array.

The global arrays must be declared explicitly if you use them in contexts other than at the top level of your PHP scripts, such as within function definitions. The superglobal arrays are accessible in any scope without any special declaration. For simplicity, we'll use the $$_GET and $$_POST superglobal arrays.($$_GET_VARS and $$_POST_VARS are deprecated now, anyway).

$$_GET and $$_POST are associative arrays, with elements keyed to the parameter names. For example, an action parameter sent in the URL becomes available to a PHP script as the value of $$_GET['action']. Suppose that a form contains fields called name and address.When a user submits the form, the Web server invokes a script to process the form's contents. If the form is submitted as a get request, the script can find out what values were entered into the form by checking the values of the $$_GET['name'] and $$_GET['address'] variables. If the form is submitted as a post request, the variables will be in $$_POST['name'] and $$_POST['address'].

For forms that contain a lot of fields, it can be inconvenient to give them all unique names. PHP makes it easy to pass arrays in and out of forms. If you use field names such as x[0],x[1], and so forth, PHP will store them in $$_GET['x'] or $$_POST['x'], the value of which will itself be an array. If you assign the array value to a variable $x, the array elements are available as $x[0],$x[1], and so on.

In most cases, we won't care whether a parameter was submitted via get or post, so we can write a utility routine,script_param(), that takes a parameter name and checks both arrays to find the parameter value. If the parameter is not present, the routine returns NULL:

```
function script_param($name)
{
```