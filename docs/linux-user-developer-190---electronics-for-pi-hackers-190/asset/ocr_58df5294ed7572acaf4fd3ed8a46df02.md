on compression. Faster presets mean less efficient
but quicker premiere; there are options such as
verslow, slow, medium, fast and veryfast, with
more in between. The last two parameters define
t format and the output destination, RTMP when we
use it. The destination is the URL for
Twitch streaming, ending with our API key. You can get
t API key from Twitch: https://www.twitch.com/
YOURSERNAME/dashboard/settings/streamkey, read
the warning and click 'Show key'.

Now that we know all these parts do, it should
hopefully be easy to understand their purpose. Time to
stream with sound!

# Adding sound

FFmpeg makes simply adding audio to another
video, which is straightforward. Use the
command like this:

```
ffmpeg -hwaccel auto -thread_queue_size 512
-f alta -acodec aac -i input.mp4 -f video 0 -s 1280x720
-f dev/null -vcodec libx264,preset veryfast -pix_fmt
yuv420p -brate 4000k-bufsize 8000k -pix_fmt
acodec aac -b:a 128k -ar 44100 -bufsize 5000k
-preset veryfast -f flv -rtmp "https://live.twitch.tv/app/86945472"
YOUR_STREAM_KEY
```

You should be aware of a few things. If you are
adding audio to an input, you might need to re-encode
the audio that Twitch supports. One of the issues
it was that the stream was deynchronized, so
the audio was also de-synchronized during
live. If you find the constant rate is too high, try
to remove the "-f vrate" (option) if it's necessary in
the-video-command, but not here.

+   * The acanc parameter determines how many
channels the audio has. Usually mono, unless only
one channel is here. We use the 44100 sample rate, or
other rates 44.1kHz, which is CD format. If you want
wo stereo, increase the bitrate, as codec
dibrate appears less to here.

You might notice that the thread_queue_size
banner is set right before -i. If you expect
FFmpeg to lag or stutter, use it "like-
banner, but this only applies to the audio input
dideo. This method affects how FFmpeg handles
streams. If you're using a Raspberry Pi Zero, or
to put it up to 192, which might give me a smooth,
glitch-free stream, however there in parts of
the audio being silent, but any higher result would
to consume a lot of memory and
freezing the stream. As rule of thumb, if your audio
is intermittent, increase the number; if FFmpeg crashes,
ndecrease it.

![](bbox=[0.532, 0.153, 0.908, 0.353])

# Interfacing with Twitch chat

What if you want your viewers some control
through chat? Chat is actually based on
the Twitch messaging standard. However, if you have
an automated solution, it's unlikely you want to use
full-irc bot; most likely, you will want to
stream easily.

Download a sample chat script,
which is easy to tailor to your needs. Download
from https://github.com/lib-twitch/chat for a direct
direct. Install the irc chat library by
using pip install irc. You also need two
parameters for the OAuth token and the ID.
If you want to join Twitch chat, you can
geto https://www.twitch-apps.com, and
then clicking 'Connect to Twitch'. Getting the chat is
so easy: go to go to fill in three fields: the Name Field
can contain any, OAuth redirect you have
have://localhost, and you'll see chat 'Chat Bot'
the Application Category description. You'll see a page
where you can configure your client ID.

Now, you have an OAuth token of
your_oauth_token and ID of your client_id.
hhere is how you run the chat script.

```
python USERNAME_FOR_BOT_
client_id_oauth_token_USERNAME
```

Notice that the OAuth token (after the ID) doesn'nhaveave out: in front, it is enough provided by
tTwitch with oauth. After running the script, you get
nect "Connecting to irc.twitch.tv" message, followed by
"Joining as your_username" message. Typing topic
help to break out of the chat: the
bot should receive the command and respond, as
print something on the console. If the chat
does connect, check the client ID and OAuth token.
Once it works, congratulations - now you have a powerfult to interact with your viewers: Happy streaming!

■

www.linuxuser.com | 79