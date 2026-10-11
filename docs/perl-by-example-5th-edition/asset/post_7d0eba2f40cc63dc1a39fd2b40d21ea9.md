
## EXAMPLE E.4 (CONTINUED)

```perl
my @students = (
    Student->new(
        name     => "Bob",
        idnumber => "123",
        major    => "math",
        courses  => [qw(calculus topology matrices)],
    ),
    Student->new(
        name     => "Jane",
        idnumber => "321",
        major    => "computer science",
        courses  => [qw(automata algorithms java)],
    )
);

get '/t' => sub {
    my $template_data = {
        students => \@students,
    };
    template 'index', $template_data;
};
1;
```

## EXPLANATION

1.  We are in the Example module, so we are going to define the *Example* package.
2.  As before, *Example.pm* will import the *syntax* group from Dancer to set up route handlers.
3.  This time we are also going to use the *Student* module we previously created.
4.  A lexically scoped array is created. The alternative (*our, like* $VERSION) is a package variable, but we don't want other modules to be able to affect our list of students. Route handlers in this part of the Dancer application (meaning, this file) will be able to interact with this array, but nobody else will. The array is populated with the same two students we used in the example script when we first saw *Student* in Chapter 14, “Bless Those Things!” (Object-Oriented Perl).
5.  The *get* handler is defined for the root path. An anonymous *subref* is defined to be run when the root path is requested.
6.  An anonymous hashref is created and assigned to the lexical variable $template_data.
7.  The hash key *students* is associated with the \@students array. When building data structures in Perl, we have to pass references to non-scalar data, so the \@students array is passed by reference.
8.  Dancer is instructed to render the *'index'* template when the root path is requested. This time, the new variable $template_data is also sent to the template. Within the template, the variable *students* will refer to the array reference we put into $template_data.

In order to use this new script, we are also going to have to change the template. Dancer is not going to magically know what to do with the template data we provided, after all.

## E.1.2 Templating

**Templating** is a manner of separating the way you **represent** a resource from the way you **produce** the resource. In our example, the list of students we are representing is directly defined inside the module. Every time we quit the application and restart it, the student data will be reset, because the program will be recompiled.

Alternatives to this include storing the data in a file, putting them in a database, or even storing them on somebody else's network! We could easily script our Web site to fetch data from a different Web site—that's how RSS readers work.

You can also represent a resource in different ways. In this case, we are going to assume we want to see the students in HTML form because we're going to assume we are using a browser. However, if we wanted to create an RSS feed of our students, we could use a different template with the same set of students to produce RSS-compliant XML. Or we could represent them as JSON. A Web-based RSS reader would **produce** resources by collecting them from somebody else's Web site; and it would **represent** them by repackaging them into HTML form.

So we really do want to be able to fetch the data in one place and represent it in a different place. This is something we simply couldn't do in the CGI days; in those days, you had to have a different script for different things—and CGI only provided HTML helpers!

Templating is a way of sending data to text files, and thus constructing the text files consistently based on the data we send them. We define a template, which contains the common factors like the header and footer HTML, plus the HTML we use to represent a resource, and into it we put the data items that make one resource different from another. In this example, templating is done with the `Template` module (see http://template-toolkit.org for more information), so we install that:

```
cpanm Template
```

Next, we need to change `config.yml` to say `template: "template_toolkit"`. The following is `config.yml` with comments removed for brevity. The reader is encouraged to read the comments in his own copy of the file. (This file is why we installed the YAML module.)

## EXAMPLE E.5

*(config.yml (abridged))*

```yaml
appname: "Example"
layout: "main"
charset: "UTF-8"
template: "template_toolkit"
```

## EXPLANATION

1.  YAML is a simple data definition language that uses key-value syntax. This line defines the name of the application as “Example”. Dancer generated this.
2.  Dancer supports layouts. This is basically a template that wraps up other templates. In CGI, we would have a *header.html* and a *footer.html*, but that was far too easy to break with mismatched tags. Having a wrapper is much easier. This application is configured to have a layout called “main”. This can be found in *views/layouts/main.tt*.
3.  HTTP specifies the charset that the resource is using. (Actually, it specifies the encoding, but calls it charset. This is an ancient mistake and it is too late to change it now.) Dancer is configured to encode everything with UTF-8, which is the preferred encoding these days.
4.  Dancer is configured to use the “*template_toolkit*” template system. Previously, it was the “*simple*” template system, but “*simple*” does not have loops, and we want to output an array of things.

When the Dancer application launches, the configuration is read from *config.yml*. This sets up Dancer with a default set of configuration, and in this case we are configuring the template system. There are many other configuration options, and you can even set it up so that it uses different values in different environments. This is the mechanism that allows us to put a Web site live without accidentally showing the users messy errors that are only useful to developers debugging the system.

Now that we’ve told it which template system to use, we turn our attention to the *views* directory. This contains all the templates, and is where Dancer will look if you don’t tell it to look elsewhere. **View** is the term we give to the concept of being able to display the same resource in different formats. There may be a *JSON* view, an *HTML* view, an *RSS* view, and so forth. To keep it simple, we’ll leave the structure as it is, but it is often beneficial to add subdirectories to *views*, one for each supported format.

The default *index.tt* can be opened to see the HTML that makes up the welcome page that was shown in the browser when the application was first run (Figure E.1). Part of this file uses the `<% %>` syntax of *Template::Toolkit*, which Dancer’s “*simple*” template system also uses, to output information like the Dancer version and the environment data on the right.

Now that we’re using *Template::Toolkit* properly (that’s what the *tt* stands for in *index.tt*) we can replace *index.tt* with other useful templates. The following example lists the new *index.tt*.

## EXAMPLE E.6

```html
<div id="page">
    <div id="content">
        <div id="header">
            <h1>Student List</h1>
        </div>
        <div id="students">
            [% FOREACH student IN students %]
            <h2>
                [% student.name %]
            </h2>
            <dl>
                <dt>ID</dt>
                <dd>[% student.idnumber %]</dd>
                <dt>Major</dt>
                <dd>[% student.major %]</dd>
                <dt>Address</dt>
                <dd>[% student.address %]</dd>
                <dt>Tuition</dt>
                <dd>[% student.tuition %]</dd>
                <dt>Course</dt>
                [% FOREACH course IN student.courses %]
                <dd>[% course %]</dd>
                [% END %]
            </dl>
            [% END %]
        </div>
    </div>
</div>
```

## EXPLANATION

1.  This file does not start with `<html>` or `<!DOCTYPE>`. Instead, it starts with `<div>`. The file will be imported into `views/layout/main.tt`, and so it only needs to contain the HTML specific to the student list page. It is `main.tt` that contains the `DOCTYPE` and `<html>` element. This allows us to create new pages while keeping a consistent theme and framing for them.
2.  By keeping some of the original HTML, the need to do many extra styling can be avoided. We will keep the `content` `div` and the `header` `div` inside it, and this will make the new page look similar to the old one.
3.  A new `div` is made whose `ID` is `students`. Later, we can style this with `CSS` if we want to.
4.  `Template::Toolkit` defines the `FOREACH` directive, which acts just like a `foreach` loop in Perl with a different syntax; for example, `IN` is used instead of the parentheses in Perl syntax. `Template::Toolkit` expects `students` to be an `arrayref` and iterates over it, assigning each element in turn to the `student` variable. `Dancer` configures `Template::Toolkit` with the `<% %>` syntax to identify template areas; everything else is output as plain text.
5.  This is the first line of the `FOREACH` loop body. It defines an `<h2>`. This line will be output once for each student in the `students` array.
