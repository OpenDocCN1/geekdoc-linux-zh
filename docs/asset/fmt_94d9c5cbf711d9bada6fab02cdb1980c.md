
## Create with Python

```python
expirySQL.close()
session['logging'] = False

return redirect('/logout')
```

```python
@app.route('/')
def index():
    return render_template('index.html')
```

Fig 02

If we manage to pass the tests far, then we've two-step verified our user — hooray! Surprisingly eh? Before we give us free reign from our service, we still need to get it right — we don't need anyone more and we don't want anyone else using it meticulously in the future.

```python
@app.route('/login', methods=['GET'])
def login():
    return render_template('login.html')
```

```python
@app.route('/check-user', methods=['POST'])
def check_user():
```

```python
@app.route('/logout')
def logout():
    return redirect('/logout')
```

```python
@app.route('/verify-code', methods=['GET'])
def verify_code():
    return render_template('verify.html')
```

```python
db.commit()
session['verified'] = True
```

```python
@app.route('/check-code', methods=['POST'])
def check_code():
    return 'check page'
```

```python
else:
    return redirect('/')
```

```python
expirySQL = db.cursor()
expirySQL.execute("DELETE FROM users WHERE code=%s", (codeCheck))
expirySQL.close()
```

## 01 Setting up dependencies

If you're looking to get a better understanding of programming games with Python and Pygame, we recommend copying the Python code in the tutorial into your own program. It's great practice and gives you a chance to tweak the elements of the game to see what fits a different ship shape, changing the difficulty or the ways the aliens behave. If it isn't already installed can install it from the terminal by typing:

```
sudo apt-get install python
```

## 02 Downloading the project

If you prefer using Git, a brilliant form of version control to easily store the game files and retain historical versions of your code, it should already be installed on your Pi. If not you can install it by typing:

```
sudo apt-get install git
```

As well as today for code, Git enables you to clone copies of other projects so you can work on, or use them. To clone Pygame, go to your home folder in the terminal `cd` - make a directory for your project space invaders and type

```
git clone https://github.com/raspiiv/spaceinvaders
```

## Resources

Raspbian: [www.raspberry.org/downloads](https://www.raspberry.org/downloads)

Python: [www.python.org/doc](https://www.python.org/doc)

Pygame: [www.pygame.org/docs](https://www.pygame.org/docs)
