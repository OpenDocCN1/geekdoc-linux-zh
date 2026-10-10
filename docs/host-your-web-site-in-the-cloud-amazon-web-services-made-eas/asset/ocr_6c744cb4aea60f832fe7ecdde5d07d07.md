This handful of simple calls forms the foundation on which we can build very complex system architectures. We’ll take a look at some of the most common patterns in the next section. But first, let’s take a short detour and learn about a new and very useful data format known as JSON.

# ## Introducing JSON

Later in this chapter you’ll learn how to build message-based systems using Amazon SQS. Each process will pull a message from an SQS queue, process it, and quite possibly write it to another queue for further processing. We will want to be able to pass complex, structured data from process to process, so it makes sense to decide on a common data format. This format should be compact, simple to generate, and easy to process. Ideally, it would also be human-readable to simplify debugging.

Two good candidates are XML and JSON. We’ve already discussed XML, so you should know what it is and what it looks like.

Designed for lightweight data interchange, JSON (Java*Script* Object Notation) is a relatively new format. JSON is a text format, and it’s very clean and easy to read. Implementations of JSON are available for virtually every programming language, from ASP to Visual FoxPro.

PHP has had JSON support built in since version 5.2.0. The `json_encode` function returns the JSON representation of any PHP value. The `json_decode` function accepts this JSON representation and returns the PHP value.

The JSON encoding for integers and strings is trivial, and the encoding for arrays is nice and compact. For example, let’s create a multidimensional array in PHP and then print the JSON representation like so:

```
```
$values = array(1,"one",
                array(1, 2, 3),
                array(1, 2, array('a' => 'Uno', 'b' => 'Dos'))
);
print(json_encode($values) . "\n");
```
```

The above code will produce the following output:

> You can find more information on JSON at http://www.json.org/.