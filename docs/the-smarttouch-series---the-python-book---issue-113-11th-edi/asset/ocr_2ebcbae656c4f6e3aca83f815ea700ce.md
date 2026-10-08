between (% %). This time we're creating a loop; inside the loop we'll be able to access any property we have of that object and print it out. In this template we're going to create an `<li>` element for each tweet we received and display the user's profile picture and text of the tweet (Fig 04). In our template we can access properties using either dot notation (.) or with square brackets ([ ]). They behave largely the same; the [ ] notation will check for an attribute on the dictionary or object defined whereas the . notation will look for an item with the same name. If either cannot find the parameter specified, it will return undefined. If this occurs, the template will not throw an error; it will simply print an empty string. Keep this in mind if your template does not render the expected data: you've probably just mis-defined the property you're trying to access. Unlike traditional Python, we need to tell the template where the for loop and if/else statements end, so we do that with {% endfor %} and {% endif %}.

# **13** Flask filters

Sometimes, when parsing in JSON, Python can generate erroneous characters that don't render particularly well in HTML. You may notice that after `tweet['text']` there is `|forceescape`. This is an example of a Flask filter; it allows us to effect the input before we render — in this case it's escaping our values for us. There are many, many different built-in filters that come included with Flask. Your advisor recommends a full reading of all the potential options.

# **14** Wrapping up

That's pretty much it for templating with Flask. As we've seen, it's insanely quick and easy to build and deploy dynamic sites. Flask is great tool for any Python developer looking to run a web service. Although we've used Twitter to demonstrate Flask's power, all of the techniques described here can be used with any third-party service or database resource. Flask can work with other rendering engines, such as Handlebars (which is superb), but Jinja2 still needs to be present to run Flask and conflicts can occur between the two engines. With such great integration between Flask and Jinja2, it makes little sense to use another engine outside of very specific circumstances.

```
```
tweetRequestParams = {
    "oauth_consumer_key": consumer_key,
    "oauth_nonce": helpers.nonce(),
    "oauth_signature_method": "HMAC-SHA1",
    "oauth_timestamp": int(time.time()),
    "oauth_version": "1.0",
    "oauth_token": session[oauth_token],
    "user_id": session[user_id],
    "count": str(count)
}
```
```

```
```
tweetRequest = helpers.sign_request(tweetRequestParams, "GET",
"https://api.twitter.com/1.1/statuses/user_timeline.json", consumer_secret,
session["oauth_secret"])

tweetRequestParams["oauth_signature"] = tweetRequest

makeRequest = urllib2.Request("https://api.twitter.com/1.1/statuses/
user_timeline.json?count=" + tweetRequestParams["count"] + "&user_id=" 
+ tweetRequestParams["user_id"])

del tweetRequestParams["user_id"], tweetRequestParams["count"]

makeRequest.add_header("Authorization", helpers.create_oauth_
headers(tweetRequestParams))

try:
    httpResponse = urllib2.urlopen(makeRequest)
except urllib2.HTTPError, e:
    return e.read()
```
```

```
```
{% if data %}
<ul id="tweets">
{% for tweet in data %}
<li>
<div class="image">
<img src="{{ tweet['user']['profile_image_url_https']
}}" alt="User Profile Picture">
</div>
<div class="text">
>{{{{ tweet['text']|forceescape }}}}</div>
</li>
{% endfor %}
</ul>

{% else %}
><p>We didn't get any tweets :()</p>
{% endif %}
```
```