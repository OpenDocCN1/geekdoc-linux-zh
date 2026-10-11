Exercise E: May I Have This Dance?

829

# EXERCISE E
May I Have This Dance?

+   1. Add a form to `index.tt` that creates a new student. The form should probably have `method="post"` and `action="/"`.

+   2. What happens when you POST invalid data? What should happen? Amend `post '/ '` to error sensibly when the POST parameters are invalid. Creating a form assists the user in providing the correct field names, but a script or test using `curl` is still likely to get it wrong. Use HTTP status codes to indicate errors. Remember that the 400 range means the user did something wrong, and the 500 range means the server (you) did something wrong.

+   3. In the user index, create links from each student’s name to the full URL for that student (for example, Bob should link to `http://0.0.0.0:3000/123`). Note that you can either omit everything before /123 (i.e., just use /123 as the URL, and let the browser behave correctly), or you can use Dancer’s `uri_for` function. The former option is defined as standard behavior for browsers to follow (that is, if the browser sees /123, it will assume the `http://0.0.0.0:3000` part), and the latter option will have to be performed in the route handler, because the templates will not be able to use `uri_for` in the current setup.

+   4. What happens to the new students when you restart the server process? Why?

+   5. What happens when you try to run it a second time? This method of writing Web applications is supposed to allow you to run the script as many times as is necessary to handle the amount of traffic to the site. Run the script with `-p 3001` and note the different URL reported to you by Dancer.

+   6. How will you ensure that, if two copies of the application are running at the same time, they will respond to the same URL with the same information? Tip: you will not be able to have an array @students any more, because this array will be unique to each application process, and it cannot be shared. You will have to store the student data externally, and have the script pass on data requests somehow.

+   7. Amend the application to store Students in a new MySQL database created for the purpose. The same three route handlers can be used for this; the only difference is how you fetch and how you store the students. The query parameters in `get '/ '` will become bind values in a MySQL query, instead of a loop. Dancer provides a `database` function that you can use to get a handle on your DBI connection, as long as you correctly configure your application.