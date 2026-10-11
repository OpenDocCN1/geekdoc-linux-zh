
Let's click on *Options* and then *Add* to start configuring our first Recursive Grep payload.

![](img/ec25e59d75726b7041242a56d3376832_285_0.png)

Figure 127: Add Grep Extract

This will open a new window with a HTTP response that we can use to define the location of the item we want extracted. We do not want to use the “Set-Cookie” headers to extract the session value because the server sets multiple instances of the *phpMyAdmin* cookie and Burp will always use the first instance it finds. We need to scroll down in the HTTP response window to the set\_session hidden input field within the login form.

We will click and select the value of the input field. When we do this, Burp will automatically set the "Start after expression" and "End at delimiter" values defining the delimiters for the grep extract as shown below.

![](img/ec25e59d75726b7041242a56d3376832_286_0.png)

*Figure 128: Defining the Grep Extract for the Session*

We'll click *Ok* to save the extract and then define another extract by clicking *Add from Intruder > 2 > Options*.

This time we need to select the contents of the *token* field:

![](img/ec25e59d75726b7041242a56d3376832_287_0.png)

Again, we'll click Ok to save the second extract.

Now that we have our "Recursive Grep" payloads defined, we need to set our payloads by clicking the Payloads tab. We will be setting four payloads in total. There is a Payload set value for each position we marked and they match the positions sequentially. In other words, set one is for the session cookie, set two is for the session field, set three is the password field, and set four is for the token field.

Payload set one is the `phpMyAdmin` session cookie value. We need to select "Recursive Grep" for the type and then click on `From _L_session" value="` to `" />Log]` as our Payload Option.

![](img/ec25e59d75726b7041242a56d3376832_288_0.png)

*Figure 130: Setting Payload Values*

Payload set two is the `set_session` value. It needs to match the value of the `phpMyAdmin` cookie, so we will use the same settings as payload set one - "Recursive Grep" as the type and `From _L_session" value="` to `" />Log]` as our Payload Option.

Payload set three is the password value. We will configure it to use the "Simple list" payload type. As its name indicates, this payload type uses a simple list of strings. We can add values to the list by manually entering passwords in the text box and clicking Add. We will repeat this to enter several common passwords.

![](img/ec25e59d75726b7041242a56d3376832_289_0.png)

Figure 131: Entering Passwords

Finally, payload set four is the *token* value. We will use the "Recursive grep" payload type again and From [`.php` />*<input type="hidden" name="token" value="1" />* fieldset->) as our Payload Option.

![](img/ec25e59d75726b7041242a56d3376832_290_0.png)

We've performed a number of setup steps so let's review what we've done before starting the attack.

We should have four positions marked on the Positions tab: the values for the *phpMyAdmin* cookie and the POST body values for the *set_session*, *prma_password*, and *token* parameters.

![](img/ec25e59d75726b7041242a56d3376832_291_0.png)

Our payloads for set one and two are “Recursive grep” with the session extract payload. Our payload for set three is a “Simple list” with our weak passwords. Finally, our payload for set four is again “Recursive grep” but with the token extract payload.

![](img/ec25e59d75726b7041242a56d3376832_291_1.png)

Once we have verified these settings, we'll click the **Start attack** button. This presents the following message.

![](img/ec25e59d75726b7041242a56d3376832_292_0.png)

The demo version of intruder will work fine for this demonstration, so we'll click Ok to start the attack and send requests with each position we marked replaced with the respective payload values. Burp Suite will open a new window with the results:

![](img/ec25e59d75726b7041242a56d3376832_292_1.png)

If everything is configured correctly, one request will trigger a 302 response, which stands out from the other 200 responses. This entry also contains a “pmaAuth-1” cookie which seems to indicate a successful login. According to the output, Burp Suite was able to log in as root with a password of “root”. We can verify this manually in our browser:

![](img/ec25e59d75726b7041242a56d3376832_293_0.png)

*Figure 137: phpMyAdmin Console*

This example might appear somewhat unusual, but weak or predictable passwords are still far too common in the real world and this demonstration process will certainly work with more complex real-world examples.

We can use our access to phpMyAdmin to execute arbitrary SQL queries directly against the database. If we click on SQL, we can write our own SQL queries. We will cover SQL more in-depth later in this module but for now, we will enter "select * from webappdb.users;" as our query to retrieve all the data in the users table in the webappdb database.

![](img/ec25e59d75726b7041242a56d3376832_294_0.png)

Figure 138: Executing queries via phpMyAdmin

After clicking Go, we get the results of our query, including plaintext passwords.

![](img/ec25e59d75726b7041242a56d3376832_295_0.png)

*Figure 139: Viewing query results via phpMyAdmin*

Not only can we query the database and view table contents but we can also insert data into the database.

Let's create a new user by clicking *Show query* box and entering "insert into webappdb.users(password, username) VALUES ("backdoor", "backdoor")." This query will add a new user named "backdoor" with a password of "backdoor".

![](img/ec25e59d75726b7041242a56d3376832_296_0.png)

*Figure 140: Inserting a New Admin User*

Next, we'll click **Go** to run the query. The page will update and show "1 row inserted".

![](img/ec25e59d75726b7041242a56d3376832_296_1.png)

*Figure 141: Query Results*

We can verify the user was added by clicking Show query box, entering “select * from webappdb.users;”, and then clicking Go. This should return three records:

![](img/ec25e59d75726b7041242a56d3376832_297_0.png)

This is just a brief example of what we can do with access to phpMyAdmin and SQL queries. We will take this farther later in this module when we demonstrate SQL injection and leverage SQL query access into a shell on the server.

## 9.4.1.3 Exercises

- Use Burp Intruder to gain access to the phpMyAdmin site running on your Windows 10 lab machine.
- Insert a new user into the “users” table.

## 9.4.2 Cross-Site Scripting (XSS)

One of the most important features of a well-defended web application is data sanitization, a process in which user input is processed, removing or transforming all dangerous characters or strings. Unsanitized data allows an attacker to inject and potentially execute malicious code. When this unsanitized input is displayed on a web page, this creates a Cross-Site *Scripting* (XSS) vulnerability.

Once thought to be a relatively low-risk vulnerability, XSS today is both high-risk and prevalent, allowing attackers to inject client side scripts, such as JavaScript, into web pages viewed by other users.

There are three Cross-Site Scripting variants: stored, *reflected*, and DOM-based.

*Stored XSS attacks*, also known as *Persistent XSS*, occurs when the exploit payload is stored in a database or otherwise cached by a server. The web application then retrieves this payload and displays it to anyone that views a vulnerable page. A single Stored XSS vulnerability can therefore attack all users of the site. Stored XSS vulnerabilities often exist in forum software, especially in comment sections, or in product reviews.

*Reflected XSS attacks* usually include the payload in a crafted request or link. The web application takes this value and places it into the page content. This variant only attacks the person submitting the request or viewing the link. Reflected XSS vulnerabilities can often occur in search fields and results, as well as anywhere user input is included in error messages.

*DOM-based XSS attacks* are similar to the other two types, but take place solely within the page’s Document Object Model (DOM). We won’t get into many details at this point, but a browser parses a page’s HTML content and generates an internal DOM representation. JavaScript can programmatically interact with this DOM.

This variant occurs when a page’s DOM is modified with user-controlled values. DOM-based XSS can be stored or reflected. The key difference is that DOM-based XSS attacks occur when a browser parses the page’s content and inserted JavaScript is executed.

Regardless of how the XSS payload is delivered and executed, the injected scripts run under the context of the user viewing the affected page. That is to say, the user’s browser, not the web application, executes the XSS payload. Still, these attacks can have a significant impact resulting in session hijacking, forced redirection to malicious pages, execution of local applications as that user, and more. In the following sections, we will explore some of these attacks.

### 9.4.2.1 Identifying XSS Vulnerabilities

We can find potential entry points for XSS by examining a web application and identifying input fields (such as search fields) that accept unsanitized input which is displayed as output in subsequent pages.

Once we identify an entry point, we can input special characters, and observe the output to see if any of the special characters return unfiltered.

- 256 (Wikipedia, 2019). https://en.wikipedia.org/wiki/Data_validation
- 257 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-site_scripting
- 258 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-site_scripting#Persistent_(or_stored)
- 259 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-site_scripting#Non-persistent_(reflected)
- 260 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-site_scripting#Server-side_versus_DOM-based_vulnerabilities
- 261 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Document_Object_Model
