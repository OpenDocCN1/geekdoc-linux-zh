# 21 Install the requirements for your launcher

The launcher is going to use a weather API combined with location data from the GPS receiver to give weather updates when requested. The nicest HTTP API for Python is requests, which you can install by doing the following:

```
sudo apt-get install python-pip
sudo pip install requests
```

# 22 Write the launcher code

Creating the code itself is pretty self explanatory, but you can use our ready-made version by downloading the CarPi package from FileSilo.co.uk and extracting carlauncher/carlauncher.py.

![](bbox=[0.12, 0.57, 0.3, 0.68])

# 23 Start the launcher automatically

Sudo-edit /etc/xdg/awesome/rc.lua and move awful.layout.suit.max.fullscreen to the top of the layouts list. Add the following to the bottom of the file:

```
awful.util.spawn_with_shell("/home/pi/carlauncher/carlauncher.py")
```

Now reboot again and the launcher should come up automatically.

![](bbox=[0.12, 0.7, 0.3, 0.86])

# 24 Future improvements

There are a number of improvements that could be made to the base project at this point:

+   - Make the launcher switch between applications rather than start them again each time
+   - Make the launcher look better aesthetically with icons
+   - Use Mopidy instead of MPD so you can use Spotify
+   - Further Navit configuration to make it more featureful
+   - An SSD or USB flash drive for storage to make things quicker

# Full code listing

```
def reset(self):
    self.clean_background()
    self.main_menu()
    self.render_weather()

def execute(self, path):
    os.system(path)
    # os.system blocks so by the time we get here application
    # has finished
    self.reset()

def render_weather(self):
    if self.w_text == None:
        return
    # Get y starting at the bottom of the nav button
    margin = 10
    y = self.btns['NAV'].bottomleft[1] + margin
    for t in self.w_text.split("\n"):
        line = self.wfont.render(t.rstrip(), 1, (255,255,255))
        line_rect = line.get_rect()
        line_rect.centerx = self.background.get_rect().centerx
        line_rect.y = y
        self.screen.blit(line, line_rect)
        y += margin + line_rect.height
    pygame.display.flip()

def handle_events(self, events):
    for e in events:
        if e.type == QUIT:
            sys.exit(0)
        elif e.type == MOUSEBUTTONDOWN:
            pos = pygame.mouse.get_pos()
            # Check if it collides with any of the buttons
            for btn_text, rect in self.btns.items():
                if self.select_rect(rect, btn_text)
                    if btn_text == "NAV":
                        self.execute("/usr/bin/navit")
                    elif btn_text == "Music":
                        self.execute("/usr/local/bin/pympd touchgui")
                    elif btn_text == "Weather":
                        self.w_text = WeatherClient.update()
                        # Reset will render weather if string is populated
                        self.reset()

def loop(self):
    clock = pygame.time.Clock()
    self.reset()
    while 1:
        self.handle_events(pygame.event.get())
        # 5 fps is plenty
        clock.tick(5)

if __name__ == "__main__":
    cl = CarLauncher()
    cl.loop()
```