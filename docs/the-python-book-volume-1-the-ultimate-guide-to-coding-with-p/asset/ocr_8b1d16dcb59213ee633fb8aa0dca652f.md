# 16 Handling access

If the user grants our application access, they will be redirected to the callback URL we defined in step 12. The redirection will include URL parameters that are our access token and a token verifier string. The Twitter documents state that we should check the access token we received in the URL parameters is the same as the one we obtained moments ago. If all has gone well, Our /authenticate endpoint will have stored our token in the session dictionary. If our stored token and the one Twitter returned matches, we can prepare to exchange our access token (which currently only has restricted privileges) for a fully fledged access token with read/write permissions (depending on the permissions you requested when you first created the app).

# 17 Third (and final) token exchange

So, same as before: we prepare our parameters for submission with sign_request(), build our auth headers and then fire off our request. Just like when we first retrieved our request token, this is something that we can do in the background without user interaction. Providing everything has gone swimmingly, you will then be returned a fully authorised access token that you can start building your own requests with.

# 18 Fire up your server

As you can see, we have ended our flask.py file with:

```
if __name__ == '__main__':
    app.secret_key = 'r4nD0MCRypt0gr4ph1ck3y0f9535i0N'
    app.run(host='0.0.0.0', debug=True)
```

If we didn’t include any parameters in the run function then our server would run and be accessible at 127.0.0.1: 5000, but it wouldn’t be accessible to external machines – kind of defeats the point of having a server. By passing host='0.0.0.0', Flask will listen on any IP address it can for potential requests with a default port of 5000. debug=True is an error message beautifier that Flask includes. Rather than crashing our server, an error page will be delivered detailing what went wrong in place of our expected return.

```
headers(verifyRequestParams)
try:
    httpResponse = urllib2.urlopen(verifyRequest)
except urllib2.HTTPError, e:
    return e.read()

responseData = getParameters(httpResponse.read())
session['oauth_token'] = responseData['oauth_token']

return "Authorised " + session['oauth_token']

def getParameters(paramString):
    paramString = paramString.split('&')
    pDict = {}
    for parameter in paramString:
        parameter = parameter.split('=')
        pDict[parameter[0]] = parameter[1]
    return pDict

def sign_request(parameters, method, baseURL):
    baseURL = urllib.quote(baseURL, '')
    p = collections.OrderedDict(sorted(parameters.items(), key=lambda t: t[0]))
    requestString = method + "&" + baseURL + "&"
    parameterString = ""
    for idx, key in enumerate(p.keys()):
        paramString = key + "=" + urllib.quote(str(p[key]), '')
        if idx < len(p.keys()) - 1:
            paramString += "&"
        parameterString += paramString
    result = requestString + urllib.quote(parameterString, '')
    signingKey = consumer_secret + "&" + session['oauth_secret']
    print signingKey
    hashed = hmac.new(signingKey, result, sha1)
    signature = binascii.b2a_base64(hashed.digest())[:-1]
    return signature

def create_oauth_headers(oauthParams):
    oauthp = collections.OrderedDict(sorted(oauthParams.items(), key=lambda t: t[0]))
    headerString = "OAuth "
    for idx, key in enumerate(oauthp):
        hString = key + "=\"" + urllib.quote(str(oauthp[key]), '') + "\""
        if idx < len(oauthp.keys()) - 1:
            hString += ", "
        headerString += hString
    return headerString

if __name__ == '__main__':
    app.secret_key = 'r4nD0MCRypt0gr4ph1ck3y0f9535i0N'
    app.run(host='0.0.0.0', debug=True)
```

![](bbox=[0.72, 0.24, 0.85, 0.36])