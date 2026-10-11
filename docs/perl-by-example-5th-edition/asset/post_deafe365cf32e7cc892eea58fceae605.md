
number is 124 does not actually exist, while the resource where the ID was 123 did exist. In the first example, the URL that returned 404 was requesting a different resource from the URL that returned the representation of a student.

In the query string example, the **same** resource was being requested with a different set of query parameters. The student index was being requested in both cases. The index resource always exists, and if your query matches no students, then an empty index is returned. That is to say, the **representation** of the index resource with the query ?name=x is just representing a resource with no items in it. But the index resource still exists. An empty set is different from a set that does not exist at all.

So a query string does not affect which **resource** is being requested, but a different path does.

### E.1.4 POST

It was mentioned that a POST request can be made to create a new resource under a given resource. That means that if we want to make a new student, we would probably want to post the data to the index resource. Since the index resource always exists, all we have to do is allow it to handle POST requests and define what it should do when it receives one.

We know that a POST request should create a new resource, but how would it know the values with which to create this student? Well, the third form of parameterization, one that was not mentioned previously, is in the **body** of the request. When an HTTP request is made, it sends a verb and a URL, along with certain other information like the **Host**, **Accept**, and **User-Agent** headers we saw in our *curl* request earlier. For certain requests¹ it can also send a **body**, which is essentially everything else. POST parameters are sent in the body.

As usual, the following example is abridged. It lists the new route handler to go into *Example.pm*. It can be added anywhere, but it is recommended to organize them based on the route they handle. Since this is *post* /*, it makes sense to put it after the handler for *get* /*.

**EXAMPLE 1.9**

(Example.pm (abridged))

```perl
1  post '/'=> sub {
2    my $student = Student->new(
3      name       => params->{name},
4      idnumber   => params->{id},
5      major      => params->{major},
6      courses    => [ split /,/, params->{courses} ]
     );
7    push @students, $student;
8    redirect '/';
     };
```

1. In fact, a body can be sent for any request, but it doesn't always make sense to do so, and so sometimes the body may be ignored.

### EXPLANATION

- 1. The POST handler for '/' is defined. It uses the same principle as the GET handler; that is, the verb, then the path, then the code ref that handles it.
- 2. The variable Student is defined as a new Student object.
- 3. The Student object is constructed with parameters in a very similar manner to how the initial Students were created. This time, each constructor parameter is retrieved from the POST body. Once again, Dancer puts parameters into the hashref retrieved by params. The name property of the new Student is the name parameter from the POST body.
- 4. The idnumber for the new Student is the id parameter from the POST body. It is often tempting to write a loop that does these lines automatically, but that is not recommended. Over time, the names of the POST parameters and the names of the properties in the Student class may drift apart, meaning the automatic code eventually becomes manual code, or riddled with ifs. Being able to have a different set of POST parameter names from the set of fields on the class, is often very valuable.
- 5. The courses will be received in the POST body as a set of comma-separated values. An anonymous array ref is created containing the result of splitting this parameter by comma.
- 6. The new Student object is pushed onto the array of Student objects.
- 7. Dancer provides the redirect function, which sets the status to 302 Found and the Location header to the provided URL. In this case, it will cause the browser to send a GET request to the index page instead, effectively reloading the page with the new data.

Restarting the application now will allow you to send POST requests to the index page to create new students. Normally this would be done with a form on the page, but that has not been written yet. Instead, we can issue curl requests again:

**EXAMPLE E.10**

```bash
$ curl -X POST -d 'name=Jill' -d 'id=124' -d 'major=math' -d 'courses=topology,matrices,calculus,perl' 0.0.0.0:3000
```

**EXPLANATION**

- 1. curl is used to send a POST request (-X POST) to our running application. Each -d provides a key=value pair to the POST body, and curl combines these and sends an appropriately formatted request. The new Student is created with idnumber of 124, name of Jill, major of math, and with courses becoming the array of four values, topology, matrices, calculus, and perl.

Having run this curl request, refreshing the index page in the browser will produce output similar to Figure E.6.

![](img/8556abcb353c0991f12099420ec28735_857_0.png)

**Figure E.6** After running the POST request with *curl*, the response to the URL *http://0.0.0.0:3000* now contains three students, rather than two.

Having done this, it may also be noted that the URL that previously returned 404, *http://0.0.0.0:3000/124*, now returns the new student, *Jill*.

Sometimes, in the wild, you will see the query string used to create a resource. This is a bad idea; a page in the browser should be able to be refreshed. The browser will warn if this involves sending *POST* data again, but it is assumed that the query string is safe. The reverse is true; if *POST* is used to query a resource like the student index we just made, the browser will assume it is unsafe and warn the user when refleshing. These behaviors are defined by the HTTP and URI standards, so by contradicting the standards, Web sites cause themselves and their users issues. That is why our student index uses a *GET* request with a query string to fetch students, and a *POST* request with body data to create students.

A good way to remember the difference is to ask yourself whether it would make sense for a user to copy the URL from the browser and send it to a friend, in order to share the information. If so, it is probably a *GET* request and should be either the path or the query string of the URL. If not, you are probably creating a resource and you want to *POST* the data.

Remember, it is not only humans with Web browsers that will send requests to your application. Scripts (for example, search indexes) are going to make assumptions based on the standardized meaning of URLs and HTTP verbs.

## EXERCISE E
### May I Have This Dance?

- 1. Add a form to `index.tt` that creates a new student. The form should probably have `method="post"` and `action="/"`.

- 2. What happens when you POST invalid data? What should happen? Amend `post '/ '` to error sensibly when the POST parameters are invalid. Creating a form assists the user in providing the correct field names, but a script or test using `curl` is still likely to get it wrong. Use HTTP status codes to indicate errors. Remember that the 400 range means the user did something wrong, and the 500 range means the server (you) did something wrong.

- 3. In the user index, create links from each student’s name to the full URL for that student (for example, Bob should link to `http://0.0.0.0:3000/123`). Note that you can either omit everything before /123 (i.e., just use /123 as the URL, and let the browser behave correctly), or you can use Dancer’s `uri_for` function. The former option is defined as standard behavior for browsers to follow (that is, if the browser sees /123, it will assume the `http://0.0.0.0:3000` part), and the latter option will have to be performed in the route handler, because the templates will not be able to use `uri_for` in the current setup.

- 4. What happens to the new students when you restart the server process? Why?

- 5. What happens when you try to run it a second time? This method of writing Web applications is supposed to allow you to run the script as many times as is necessary to handle the amount of traffic to the site. Run the script with `-p 3001` and note the different URL reported to you by Dancer.

- 6. How will you ensure that, if two copies of the application are running at the same time, they will respond to the same URL with the same information? Tip: you will not be able to have an array @students any more, because this array will be unique to each application process, and it cannot be shared. You will have to store the student data externally, and have the script pass on data requests somehow.

- 7. Amend the application to store Students in a new MySQL database created for the purpose. The same three route handlers can be used for this; the only difference is how you fetch and how you store the students. The query parameters in `get '/ '` will become bind values in a MySQL query, instead of a loop. Dancer provides a `database` function that you can use to get a handle on your DBI connection, as long as you correctly configure your application.
