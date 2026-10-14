
## 05 Assigning a namespace to the Flask app

Now we create an instance of the Flask class. This variable will be how we access all of the classes and properties associated with the Flask package. The __name__ property in this instance gives our Flask class an idea of the scope it's operating in.

## 06 Creating our first route

In order to authorise our user, we need to create an endpoint that they can visit to trigger the process. This is where Flask comes in handy. Using the routes decorator (@app.route()) we can determine paths that trigger functions or actions. The first endpoint we want to create is @app.route('/authenticate'). The function we declare immediately after the decorator will be executed when that endpoint is called. Note that although we've done so here, you do not need to name the function the same as the endpoint. Flask can deliver static files as well as use template rendering engines, but for the sake of brevity we're going to use return at the end of the function to deliver a simple text response showing our progress.

## 07 Creating a session with Flask

In order to maintain various properties and values specific to multiple users, we're going to be storing our values in Flask sessions. A Flask session is almost exactly the same as using a cookie to store values, but with sessions we've got a layer of cryptography to help keep user credentials secure. The values in our sessions behave just like a dictionary, so we can call all of the methods that dictionaries have. For example, we can call session.clear() if we want to log a user out of a service or restart the authentication process. We need to make sure that before we make any calls to our sessions, we've set our session key, otherwise we'll get an error. In this example we've chosen to insert the key just before app.run() so it will be set just before our server is executed. Like most keys, you must keep this key secret.

## 08 Preparing to authorise our app

Now we need to start
Data = getParameters(httpResponse.read())
    session['oauth_token'] = responseData['oauth_token']
    session['oauth_secret'] = responseData['oauth_token_secret']
    return redirect("https://api.twitter.com/oauth/authorize?oauth_token=" + session['oauth_token'])

@app.route('/authorised')
def authorised():
    if request.args.get('oauth_token', '') == session['oauth_token']:
        verifyRequestParams = {
            "oauth_consumer_key" : consumer_key,
            "oauth_nonce" : str(random.randint(1, 99999999)),
            "oauth_timestamp" : int(time.time()),
            "oauth_version" : "1.0",
            "oauth_token" : session['oauth_token']
        }
        signVerification = sign_request(verifyRequestParams, "POST", "https://api.twitter.com/oauth/access_token")
        verifyRequestParams['oauth_signature'] = signVerification
        verifyRequest = urllib2.Request("https://api.twitter.com/oauth/access_token", "oauth_verifier=" + request.args.get('oauth_verifier'))
        verifyRequest.add_header("Authorization", create_oauth_

## Flask is perfect for this project: defining routes and handling parameters is a piece of cake

In order to sign the request properly, we need to order the parameters of the request alphabetically, URL-encode them, concatenate them and then sign against them each time. This is where the headache of OAuth begins. Because we'll be doing this for most every request, we're going to write a convenience function that does all of this for us: sign_request().

## 09 Creating our signature

So, what's going on in our sign_request() function? First, we need to URL-encode the base URL of the request which we can do with urllib.quote(). Next, we create an ordered dictionary (OrderedDict) which sorts the parameters we've passed through to the function alphabetically according to the key value. This is crucial as each request must be signed with all of the parameters concatenated alphabetically in order to be valid. Next, we create the variable requestString to build the first part of our request body. This is made up of the method we'll be using for the request and the URL we'll be submitting to. We then iterate through the keys in the OrderedDict, concatenating and URL-encoding the key value pairs of the dictionary so we have something like key=value. Finally, we check whether or not we're at the last key in the dictionary; if we aren't then we'll append a '&' to the parameter string in preparation for the next one to follow. Ultimately, we'll have a string that will appear as GET&http%3A%2F%2Fapi.twitter.com%2Fetc%2F?key1=value1&key2=value2&key3=value3.

## 10 The signing key

Now we need to create a signing key for our signature. As the code shows, it's just our consumer_secret + oauth_secret with an ampersand in the middle. However, you may notice that we don't have an OAuth secret yet. That's okay: for this first signing request we don't need one. You may have noticed in our /authenticate endpoint that after we popped the session values, we reassigned session['oauth_secret'] to ''. This way we won't get a KeyError message when we try to sign our request. When we get our callback in our /authorised endpoint, we'll assign our session['oauth_secret'] for future requests.

### A little about oauth_nonce

Most of the values included in the OAuth headers and signing process are self-explanatory. However, one isn't so obvious in its purpose. OAuth_Nonce is a randomly generated value – often alphanumeric but as there is no defined convention, an integer between 1 and something large will serve its purpose. It exists so Twitter can check that it's not been sent the same request twice.

## 11 Hashing the key

Finally, we're ready to hash the key. Using Python's HMAC library, we pass our signing key, our result string (the concatenation of our escaped base URL and method with our parameters string) and from Python's hashlib library, the SHA1 hash function. This results in a binary buffer with our signature – that's great, but we can't send a buffer to Twitter's server. On the next line, we pass our hashed variable through to the binascii library to convert it to a Base64 value. Now we have our signature which we'll return to the function that called it.

## 12 Obtaining a request token

With Twitter API v1.1, we can no longer just request an access token to access user data. First, we need to obtain a request token and then exchange that for our first access token. We don't need the user to interact with anything at this point, so we can trigger this on the back-end and handle it ourselves. In the requestParams dictionary, we prepare the values we'll need to sign against and then submit these to Twitter to receive a request token. The oauth_callback field won't do anything right now, but it's where our app will redirect after we obtain our first access token. We want to point it to our route /authorised. On line 27 we pass the requestParams through to the sign_request method. We then add the signature returned to the requestParams that passed through to the signing function, as we'll be using these to build our authorisation headers next.

## 13 Building the OAuth authorisation headers

Much like when we sign our requests, we need to properly encode and format our authorisation headers, too. The main difference between sign_request() and create_auth_headers() is that the signature base string (the string we build to generate our SHA1 signature) is all of the variables joined with '&', whereas our auth headers are joined with ',' and prepended with the word 'Auth'. Other than that, the two serve the same purpose. Here we've separated the two out to emphasise the importance of the difference – if either of these two functions returns a malformed string, the request will fail. Using the urllib2 module, we can prepare the request we'll submit. Notice the second parameter of the request function on line 31. If we omit this parameter, the request method will be GET; if it is included – regardless of the content – it will be a POST request. The parameter's main function is to assign the body of a property of a request; it's a little clumsy, but it's something we'll need in a bit.

## 14 Making the first request

Once we've gotten the prepared auth headers back, we add them to the HTTP request and then call the open() method and wait for a response. If all has gone well, we should receive a string in the request response with our first auth token and auth secret. To save us having to individually parse the string for properties, the function getParameters() will split the string up and return a dictionary we can access. We'll then store these values in our session for later.

## 15 Redirecting the user

Now we have our first set of credentials, we can redirect our user to the Twitter authorisations screen to let them grant access to their data. Because we haven't sent anything to our client yet, we can use Flask's redirect() method to send our user to the Twitter authorisation view. This request is one of the few that we can use URL parameters to send tokens to Twitter.
