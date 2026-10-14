```
expirySQL.close()
session["loggedin"] == False

return redirect('/logout')
```

If we manage to pass the tests so far, then we’ve two-step verified our user – hooray! Surprisingly easy, eh? Before we give our user free reign around our service, we still want to get rid of that token – we don’t need it any more and we don’t want to risk someone else using it maliciously in the future.

```
else:
    delSql = db.cursor()

    delSql.execute("""DELETE FROM verification WHERE code=%s"", (codeToCheck,))

    delSql.close()

    db.commit()

    session['verified'] = True

    return redirect('/')
else:
    return redirect('/verify?error=true')
```

And that’s it! Now we redirect our user to wherever we want them to be at the end of the process. In this instance we’re sending them back to our index page, which will render a success message and give the user a link to log out whenever they like – but they could be redirected to their user page, and so on.

# 09 Conclusion

In every web-based service, security is king. Users entrust more and more personal data and trends to services every day and it’s the responsibility of those services to maintain the privacy of that data as best they can. It’s no wonder that services such as Amazon, Google and Facebook have all implemented two-step verification across their services. With two-step authentication, a user can tie their account to one of the most personal things they own: their phone. With services like Twilio and some simple code, they contain people’s keys – or at least a part of them.

```
@app.route('/')
def index():
    return render_template('index.html')

@app.route('/login', methods=['GET'])
def login():
    return render_template('login.html')

@app.route('/check-user', methods=['POST'])
def checkUser():
    return "check user page"

@app.route('/logout')
def logout():
    return "logout page"

@app.route('/verify', methods=['GET'])
def twoStep():
    return render_template('verify.html')

@app.route('/check-code', methods=['POST'])
def checkCode():
    return "check code page"
```

```
verificationCode = generateVerificationCode(size=6)

ins = db.cursor()

expiration = int(time.time()) + expirationLength

sql = "INSERT INTO verification (code, expiration, username) VALUES ('%s', '%s', '%s')" % (verificationCode, expiration, request.form['username'])

ins.execute(sql)

ins.close()

db.commit()

session['user'] = request.form['username']
session['loggedin'] = True
```

```
@app.route('/check-code', methods=['POST'])
def checkCode():

if request.method == 'POST':
    codeToCheck = request.form['code']

    if not 'user' in session:
        return redirect('/login')
    else:
        cur = db.cursor()

        cur.execute("SELECT * FROM verification WHERE code = %s", (codeToCheck,))

        result = cur.fetchone()

        cur.close()

        if result is None:
            returnedUser = result[1]
            expirationTime = int(result[2])

            if returnedUser != session['user']:
                return redirect('/verify?error=true')
```