This always displays **This test is successful** because the expression is true when `test_expression` is a nonnull string. If `expr= "foobar"` is changed to `expr=""` or `expr=" "`, however, then the text within the if-endif block will never be part of the output.

The following is an example of a string equality test:

```
```xml
<|-->#set var="quicksearch" value="yes" --<|>
<|-->#if expr="${quicksearch} = yes" --<|>
  Quick search is requested.
<|-->#endif --<|>
```
```

The variable called **quicksearch** is being set with the value **yes** and is later being compared with **yes**. Because the set value and the comparison value are equal, the '''Quick search is requested''' line is the output. If you require more-complex flow control constructs, use the following forms:

```
```xml
<|-->#if expr="test_condition1" --<|>

<|-->#elif expr="test_condition2" --<|>

<|-->#else --<|>

<|-->#endif --<|>
```
```

The `clif` directive enables you to create an `else-if` condition. For example:

```
```xml
<|-->#if expr="${HTTP_USER_AGENT} = /MSIE/" --<|>

  <|-->#set var="browsetest" value="IE" --<|>
  <|-->#include file="vbcs.html" --<|>
<|-->#elif expr="${HTTP_USER_AGENT} = /Lynx/" --<|>

  <|-->#set var="browsetest" value="Lynx" --<|>
  <|-->#include file="simple-html.html" --<|>
<|-->#else --<|>
```
```