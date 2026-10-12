# Control lights with your Pi

# Find your IP address

+   **15** Before you start the web server running, you will need to check the following:
+   * You have a folder set up called \_Mobile\_Lights
+   * In the Mobile\_Lights folder is a Python file named mobile\_lights.py
+   * Also within the Mobile\_Lights folder are two folders: one named templates which stores the index.HTML file and another folder named static which contains the file style.css

If everything checks out, then in the LX Terminal you can type sudo hostname -I. This will display the IP address of your Raspberry Pi – for example, 192.168.35.8. Make a note of it because this is the address you will enter into the web browser on your mobile device.

# Start the web server

+   **16** You have arrived at the point where you are ready to start the web server. Move to the Mobile\_Lights folder by typing cd Mobile\_Lights. Now run the Python mobile\_lights.py program by typing sudo python mobile\_lights.py. This starts up the web server, which is then ready to respond to the buttons that are pressed on the web page.

# Turn your lights on and off

+   **17** Grab your mobile device, smartphone or tablet and load the web browser. In the address bar enter the IP address that you noted down in Step 15. At the end of the address, add :5000 – for example, 192.168.1.122:5000. The 5000 is the port number that is opened to enable the communication between your device and the Raspberry Pi. You will be presented with ON and OFF options, and you can now control the socket and whatever you have plugged in – kettle, radio, TV – all from your mobile device by simply pressing ON or OFF. Have fun!

> “You will be presented with ON and OFF options to control the socket”

![](bbox=[0.08, 0.57, 0.98, 0.92])

Above You need to get the folder names correct so that files are saved properly