
# Projects

## Control your Raspberry Pi-powered car

Control a toy car with a smartphone and the latest web technologies

### What you’ll need...

- A RasPi car, ready to go
- An internet connection
- A reasonably modern smartphone/tablet
- Pi car source code
- [github.com/shaunuk/picar](https://github.com/shaunuk/picar)

### Download and install the software

01

To get the LCD connectivity working, you can follow the steps from pages 64–65. Next we’ll need to find a home for our new project code – how about `/var/www/picar`? Type `sudo mkdir /var/www/picar` in the terminal to make the directory and then change into that directory: `cd /var/www/picar`

Now, to download the project using Git, type `sudo git clone https://github.com/shaunuk/picar` (if you haven’t got Git, install it with `sudo apt-get install git`).

This will download the custom software for driving the car, but we still need the web server and some other bits before we can start burning rubber...

![](img/59caadfa348382a5c408c25137901e27_133_0.png)

> Our code will send instructions to our car over twenty-millisecond apart. It will be very responsive to drive!

Now we have our fantastic Raspberry Pi-powered car all wired and charged, it’s time to make it come alive. We’re using the best web technologies that the JavaScript programming language offers, to harness the natural movement of your hand and wirelessly drive the vehicle. Each little movement will trigger an event that calculates what the car should do and then sends it over a socket connection.

Below All you need to finish off your project is access to a smartphone or tablet

### Download and install Node.js

02 Next we're using Node.js and its package tool, the Node package manager (npm). Type `sudo wget http://nodejs.org/dist/v0.18.21/node-v0.18.21-linux-arm-pi.tar.gz`. This will download a fairly recent version of Node.js – the version Raspbian has in its repositories is way too old and just doesn't work with the new technologies we're about to use. Extract the node package by typing: `sudo tar -xzvf node-v0.18.21-linux-arm-pi.tar.gz`

### Configure Node.js

03 To make it easy to run from everywhere, we will create symbolic links for Node and npm binaries. Type `sudo ln -s /var/www/node-v0.18.21-linux-arm-pi/bin/node /bin/node` and then `sudo ln -s /var/www/node-v0.18.21-linux-arm-pi/bin/npm /bin/npm`. Then, to get the extra modules, type `npm install socket.io node-socket.io adafruit-i2c-pwm-driver sleep-optimist`

![](img/59caadfa348382a5c408c25137901e27_134_0.png)

### Get to know the project

04 Now we have everything, you should see three files: the server (app.js), the client (socket.html) and the jQuery JavaScript library for the client. The server not only drives the servos, but it is a web server and sends the socket.html file and jQuery to the browser when requested – it's a really neat and simple setup and just right for what we're trying to achieve.

### Test the servos

05 Our handy little program (app.js) has a special mode just for testing. We use two keywords here: beta for servo 0 (steering) and gamma for servo 1 (motor control). Type `node app.js beta=300`. You should see the front wheels turn. Now the numbers need experimenting with. On our example, 340 was left, 400 was centre and 470 was right. Do the same for the motor by typing `node app.js gamma=400` and take note of the various limits of your car.

![](img/59caadfa348382a5c408c25137901e27_135_0.png)

> *We're using the best web technologies that the JavaScript programming language has to offer*

![](img/59caadfa348382a5c408c25137901e27_135_1.png)

### Configure sensible defaults

06 Now you know what your car is capable of we can set the defaults in app.js and socket.html. Edit app.js and find the section that says function emergencyStop(). Adjust the two numbers to your car's rest values. Then open socket.html and define your variables here.

### Going for a spin

07 We're almost ready to try it out, but you need to know the IP address of your Pi car, so type ifconfig at the terminal. Then fire up the app by typing node app.js. Now grab your nearest smartphone or tablet, making sure it's on the same network as your Pi. Open the web browser and go to http://[your IP address]:8080/socket.html. You should get an alert message saying 'ready' and as soon as you hit OK, the gyro data from your phone will be sent to the car and you'll come off!

### Full code listing

**socket.html**

```html
<html>
<head>
<script src="jquery-2.0.3.min.js"></script>
<script src="socket.io/socket.io.js"></script>
<meta name="viewport" content="user-scalable=no, initial-scale=1.0, maximum-scale=1.0" />
<script>
//------ Define your variables here
var socket = io.connect(window.location.hostname + ':8080');
var centerbeta = 400; //where's the middle?
var minbeta = 340; //right limit
var maxbeta = 470; //left limit
var multbeta = 3; //factor to multiply the
// raw gyro figure
var centergamma = 330;
var adjustmentgamma = 70; //what do we do to
// the angle to get to adjust
var mingamma = 250; //backwards limit
var maxgamma = 400; //forward limit
var multgamma = 1; //factor to multiply the
//raw gyro figure by to get the desired
//rate of acceleration
window.lastbeta='0';
window.lastgamma='0';
$(function() {
window.gyro = 'ready';
alert('Ready - Lets race !');
});
window.ondeviceorientation = function(event) {
var beta = Math.round((event.beta - centerbeta)*multbeta);
if (beta < minbeta) {
beta=minbeta;
}
if (beta > maxbeta) {
beta=maxbeta;
}
gamma = Math.round(event.gamma + adjustmentgamma)*multgamma;
//stop sending the same command more than once
send = 'N';
if (window.lastbeta != beta) { send = 'Y' }
if (window.lastgamma != gamma) { send = 'Y' }
window.lastbeta=beta;
window.lastgamma=gamma;
if (window.gyro == 'ready' && send=='Y') {
//don't send another command until ready...
window.gyro = 'notready';
socket.emit('fromclient', { beta: beta, gamma: gamma });
window.gyro = 'ready';
}
};
</script>
</head>
<body>
</body>
</html>
```

**app.js**

```javascript
//declare required modules
var http = require('http'),
createServer = http.createServer,
io = require('socket.io').listen(createServer(handler)),
fs = require('fs'),
Static = require('node-static'),
sys = require('sys'),
PwmDriver = require('adafruit-i2c-pwm-driver'),
sleep = require('sleep'),
argv = require('optimist').argv;
var pwm = new PwmDriver(0x40, '/dev/i2c-0');
//set pulse width
function setServerPulse (channel, pulse) {
var pulseLength;
pulseLength = 1000000;
pulseLength /= 60;
console.log('%d us per period', pulseLength);
pulseLength /= 4096;
console.log('%d us per bit', pulseLength);
pulse = 1000;
pulse /= pulseLength;
return pwm.setPWM(channel, 0, pulse);
}
//set pulse frequency
pwm.setPWFRFC(50);

//Make a web server on port 8080
var file = new Static.Server();
function handler(request, response) {
console.log('serving', file, request.url);
file.serve(request, response);
}

if (argv.beta) {
console.log('performing one off servo position move to:', argv.beta);
pwm.setPWMC(0, 0, argv.beta); //using direct i2c pwm module
pwm.stop();
return process.exit();
}
if (argv.gamma) {
console.log('performing one off servo position move to:', argv.gamma);
pwm.setPWMC(0, 0, argv.gamma); //using direct i2c pwm module
pwm.stop();
return process.exit();
}

//Fire up a web socket server
io.sockets.on('connection', function (socket) {
socket.on('fromclient', function (data) {
console.log('RECEIVED:', data.beta);
//Gamma: /*data.echo*/
'use strict';
data = '';
//using python adafruit module
//exec('/pi car/e1/ electronics.chrona.se/rpisb.php
//using direct i2c pwm module
pwm.setPWMC(0, 0, data.beta);
//using python i2c pwm module
clearInterval(lastAction);
//stop emergency stop timer
lastAction = setInterval(emergencyStop, 1000);
//set emergency stop timer
});
});

process.on('SIGINT', function () {
emergencyStop();
console.log('\n*gracefully shutting down from SIGINT (Ctrl-C)');
pwm.stop();
return process.exit();
});

function emergencyStop() {
//center front wheels
pwm.setPWMC(0, 400);
//stop motor
pwm.setPWMC(0, 330);
console.log('####EMERGENCY STOP - signal lost or shutting down');
}
```
