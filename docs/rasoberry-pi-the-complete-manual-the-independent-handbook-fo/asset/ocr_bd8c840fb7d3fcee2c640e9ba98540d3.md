# Find your IP address

**15** Before you start the web server running, you will need to check the following: * You have a folder set up called Mobile_Lights * In the Mobile_Lights folder is a Python file named mobile_Lights.py * Also within the Mobile_Lights folder are two folders, one named templates which stores the index HTML, file and another folder named static which contains the file styles.css

If everything checks out, then in the LX Terminal you can type sudo hostname -I. This will display the IP address of your Raspberry Pi – for example, 192.158.x.x. Make a note of it because this is the address you will enter into the web browser on your mobile device.

# Start the web server

**16** You have arrived at the point where you are ready to start the web server. Move to the Mobile_Lights folder by typing cd Mobile_Lights. Now run the Python mobile_Lights.py program by typing sudo python mobile_Lights.py. This starts up the web server, which is then ready to respond to the buttons that are pressed on the web page.

# Turn your lights on and off

**17** Grab your mobile device, smartphone or tablet and load the web browser. In the address bar enter the IP address that you noted down in Step 15. At the end of the address, add :5000/ – for example, 192.168.1.122:5000. The 5000 is the port number that is opened to enable the communication between your device and the Raspberry Pi. You will be presented with ON and OFF options, and you can now control the socket and whatever you have plugged in – kettle, radio, TV – all from your mobile device by simply pressing ON or OFF.

> “You will be presented with ON and OFF options to control the socket”

![](bbox=[0.02, 0.47, 0.92, 0.92])