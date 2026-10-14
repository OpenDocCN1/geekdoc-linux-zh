
## 16 Handling access

If the user grants our application access, they will be redirected to the callback URL we defined in step 12. The redirection will include URL parameters that are our access token and a token verifier string. The Twitter documents state that we should check the access token we received in the URL parameters is the same as the one we obtained moments ago. If all has gone well, Our /authenticate endpoint will have stored our token in the session dictionary. If our stored token and the one Twitter returned matches, we can prepare to exchange our access token (which currently only has restricted privileges) for a fully fledged access token with read/write permissions (depending on the permissions you requested when you first created the app).

## 17 Third (and final) token exchange

So, same as before: we prepare our parameters for submission with sign_request(), build our auth headers and then fire off our request. Just like when we first retrieved our request token, this is something that we can do in the background without user interaction. Providing everything has gone swimmingly, you will then be returned a fully authorised access token that you can start building your own requests with.

## 18 Fire up your server

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

![](img/3b256f430f51c98f1315671f6e4eec19_118_0.png)

![](img/3b256f430f51c98f1315671f6e4eec19_119_0.png)

## Part one: Program a Space Invaders clone

Write your own RasPi shooter in 300 lines of Python

### Resources

Raspbian: www.raspberrypi.org/downloads

Python: www.python.org/doc

Pygame: www.pygame.org/docs

When you're learning to program in a new language or trying to master a new module, experimenting with a familiar and relatively simply project is a very useful exercise to help expand your understanding of the tools you're using. Our Space Invaders clone is one such example that lends itself perfectly to Python and the Pygame module – it's a simple game with almost universally understood rules and logic. While the Invaders inspired shooter demands...

meander their way down the screen towards you, it's your job to pick them off while dodging their random fire. When one wave is conquered, another faster, more aggressive wave appears. We've tried to use many features of Pygame, which is designed to make the creation of games and interactive applications easier. We've extensively used the Sprite class, which saves dozens of lines of extra code in making collision detection simple and updating the screen and its many actors a single-line command. We hope you agree that this is an exciting game to play and a great tool to learn more about Python and Pygame, but our sensory system is far from overloaded here. Don't worry, as that will be covered in the next tutorial, as adding animation and sound effects to our game to give it the spit and polish any self-respecting Space Invaders-inspired shooter demands...

## 01 Setting up dependencies

If you're looking to get a better understanding of programming games with Python and Pygame, we strongly recommend you copy the Pivaders code in this tutorial into your own program. It's great practice and gives you a chance to tweak elements of the game to suit you, be it a different ship image, changing the difficulty or the ways the alien waves behave. If you just want to play the game, that's easily achieved too, though. Either way, the game's only dependency is Pygame, which (if it isn't already) can be installed from the terminal by typing:

```
sudo apt-get install python-pygame
```

## 02 Downloading the project

For Pivaders we've used Git, a brilliant form of version control used to safely store the game files and retain historical versions of your code. Git should already be installed on your Pi, if not, you can acquire it by typing:

```
sudo apt-get install git
```

As well as acting as caretaker for your code, Git enables you to clone copies of other people's projects so you can work on them, or just use them. To clone Pivaders, go to your home folder in the terminal [cd ~], make a directory for the project [mkdir pivaders], enter the directory [cd pivaders] and type:

```
git pull https://github.com/russ78/pivaders.git
```
