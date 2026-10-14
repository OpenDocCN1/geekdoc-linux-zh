
## 13 Sound configuration

Before configuring speech support for Navit, configure the external sound card. You have to stop the Broadcom module from loading and remove some Raspberry-Pi-specific ALSA (Advanced Linux Sound Architecture). To do this, sudo-edit /etc/modprobe and comment out (i.e. prefix with a #):

- snd-bcm2835

Then run:

- sudo rm /etc/modprobe.d/alsa*

Reboot for the changes to take effect. Use alsamixer to set the volume on the if it’s too quiet.

## 14 Download a voice

The speech synthesis software needs a voice and a proprietary binary. You can get both by completing the following steps:

- sudo mkdir -p /usr/share/mbrola/voices/
- wget http://www.tcts.fpms.ac.be/synthesis/mbrola/dba/en1/en1-980910.zip
- unzip en1-980910.zip
- sudo cp en1/en1 /usr/share/mbrola/voices
- wget http://www.tcts.fpms.ac.be/synthesis/mbrola/bin/raspberrypi/mbrola.tgz
- tar zxvf mbrola.tgz
- sudo mv mbrola /usr/local/bin/

## 15 Create speech script

Navit supports speech by running an external script and passing the text to speak as an argument. Create one using:

- cd /home/pi/.navit
- wget http://liamfraser.co.uk/lud/carpi/chime.wav
- touch speech.sh
- chmod +x speech.sh

Now edit speech.sh:

```
#!/bin/bash
aplay -r 44100 /home/pi/.navit/chime.wav
espeak -vmb-en1 -s 110 -a 150 -p 50 "$1"
```

Finally, test it with:

- ./speech.sh “Hello World”

## Full code listing

```
try:
    r = requests.get(api_req)
except requests.exceptions.RequestException as e:
    return errstr

return WeatherClient.usefuldata(r.json())

class CarLauncher:
    def __init__(self):
        pygame.init()
        pygame.mixer.quit() # Don't need sound
        screen_info = pygame.display.Info()
        self.screen = pygame.display.set_mode((screen_info.current_w,
                                               screen_info.current_h))
        pygame.display.set_caption('Car Launcher')
        self.titlefont = pygame.font.Font(None, 100)
        self.wfont = pygame.font.Font(None, 30)
        self.w_text = None # Weather Text

    def clean_background(self):
        background = pygame.Surface(self.screen.get_size())
        self.background = background.convert()
        self.background.fill((0, 0, 0))

        # Render title centered
        text = self.titlefont.render("CarPi Launcher", 1, (255, 255, 255))
        textpos = text.get_rect()
        textpos.centerx = self.background.get_rect().centerx
        self.background.blit(text, textpos)

        self.screen.blit(self.background, (0,0))
        pygame.display.flip()

    def main_menu(self):
        # btns maps Text -> Rectangles we can do collision detection on
        self.btns = {'Music' : None, 'NAV' : None, 'Weather' : None}

        item_num = 1
        for key in self.btns:
            text = self.titlefont.render(key, 1, (255,255,255))
            textpos = text.get_rect()
            max_width = self.background.get_rect().width / len(self.btns)
            center_offset = max_width * 0.5
            # This maps btns buttons just below the title
            textpos.centery = self.background.get_rect().centery / 2
            textpos.centerx = (max_width * item_num) - center_offset
            self.btns[key] = textpos
            self.screen.blit(text, textpos)
            item_num += 1

        pygame.display.flip()

    def select_rect(self, rect, text):
        # Colour red to green when clicked in green
        surface = pygame.Surface((rect.w, rect.h))
        surface.fill((0, 255, 0))
        # Now we have to draw the text over it again
        t = self.titlefont.render(text, 1, (255,255,255))
        surface.blit(t, (0,0))
        self.screen.blit(surface, rect)
        pygame.display.flip()
```

## Use Python with Pi

![](img/3b256f430f51c98f1315671f6e4eec19_171_0.png)

Above The Navit software comes with a host of options built into its menu hierarchy

![](img/3b256f430f51c98f1315671f6e4eec19_171_1.png)

Above The pympdtouchgui front-end for the music player is surprisingly featureful

## You will need to write your own launcher for CarPi

![](img/3b256f430f51c98f1315671f6e4eec19_171_2.png)

## Make it mobile

It is definitely best to put this project together in a clean workspace so that you can clearly see what you’re working with and ensure everything is correctly wired and soldered, but the point of the project is to make this setup portable so that you can put it in your car and use it on the road. You could install everything into a single, hand-made enclosure or customise a large bought one, or you could secure the various parts inside, for example, your glovebox or car doors. You’ll also need to power both the screen and your Pi with a power pack and ensure that the GPS antenna is fastened into a good spot for signal.

## 16 Configure Navit for speech

The last part is simple. Edit the Navit config file again (//etc/navit/navit.xml) and replace the following line:

```
<speech type="cmdline" data="echo 'Fix the speech tag in navit.xml to let navit say: %s' cps="15" />

...with:

<speech type="cmdline" data="/home/pi/.navit/speech.sh %s" cps="10" />
```

Now you can run Navit with DISPLAY=:0.0 navit and have fun experimenting.

## 17 Install the music player

MPD is the music player back-end and pympdotouchgui is the front-end that needs installing manually:

```
sudo apt-get install mpd ncmpcpp
wget http://www.spida.net/projects/software/pympdotouchgui/pympdotouchgui-0.320.tgz
tar zxvf pympdotouchgui-0.320.tgz
cd pympdotouchgui-0.320/
sudo python setup.py install
# Fix hard coded path in software
sudo ln -s /usr/local/share/pympdotouchgui/ /usr/share/pympdotouchgui
```

## 18 Copy music

Scp (secure copy protocol) was used here to copy music. First get the Pi’s IP address by running ip addr. Then

run sudo passwd to set a password for root. From a computer with music on, run:

```
scp -r music_folder root@pi_ip_address:/var/lib/mpd/music/
```

Then on the Pi, change the ownership of the music that you just copied:

```
sudo chown -R mpd:audio /var/lib/mpd/music
```

## 19 Update mpd music library

Ncmpcpp is a command line client for mpd. Type ncmpcpp and press U to update the library. Press 3 to browse the library and check the music is there, and press Q to quit. Pressing 1 will select the help screen if you want to do more.

## 20 Install awesome window manager

Now you will need to write your own launcher for CarPi, which will full-screen. To ensure every application is forced to full-screen, use awesome window manager in full-screen mode.

```
sudo apt-get install awesome
sudo rm /etc/alternatives/x-session-manager
sudo ln -s /usr/bin/awesome /etc/alternatives/x-session-manager
```

When changing the default x-session-manager, awesome will auto-started at boot instead of LXDE. If you reboot the Pi, awesome should then load up automatically.
