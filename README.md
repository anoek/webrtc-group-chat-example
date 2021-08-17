About
=====

This is a "simple", but complete example of how to utilize WebRTC to do peer to
peer voice and video chatting between two or more people.

### Server Side 
This example uses node.js and socket.io to create a "Signaling Server", which
runs on (or near) your web server to manage who should talk to who. The purpose
of the signaling server is to relay information between peers while you are
setting them up to talk directly to each other.


### Client Side
Included is `client.html` which contains all of the logic to connect to the
signaling server, join a virtual group chat channel, connect with peers, and
stream video and audio to all party members using the raw WebRTC API.


Running
=======

### Node.js signaling server
You'll need to install `node.js` for the signaling server portion of this code to run.

Once node.js is installed, install the packages we need for this demo
```
npm install
```

Then simply run the signaling server:
```
npm run start 
```

### Running the sample
All modern browsers require webrtc stuff to be run over SSL, so this sample uses
a self signed certificate for the signaling server and host of client.html. Because
of this, you'll be presented with a certificate warning when you open the page, simply
click advanced to click accept and the browser should connect to your server.

Head to https://localhost:8080/ , or if you are accessing the server from another device,
simply replace `localhost` with the IP or hostname of the server (and click through all
of the certificate warning stuff.)

At this point you should be presented with a dialog asking permission to access
your microphone / webcam. Once accepted, you should see a local stream appear
on the page. Now open up the same page in another browser, on the same computer
or another, and watch as the magic of WebRTC takes effect and both images and
audio samples mysteriously move from one browser to the other.  Repeat with as
many browsers as you dare.


Note: At the time of writing this, only firefox and chrome support WebRTC,
however both browsers support this on Windows, Linux, Mac, and Android, so lots
of fun can be had pointing everyones' phones, tablets, and laptops at that `client.html`
and bogging down your network with audio/video traffic.


Using things other than jQuery, node.js, and socket.io
=============================================
The choice of node.js and socket.io is based purely on my familiarity with them
and the fact that their fairly easy to understand even if you aren't familiar
with them. However, you can use any mechanisms you want for your signaling system, you
just need a way to exchange ICE candidates and session descriptions between
clients.

The use of jQuery is even less important, I just like using it for DOM
manipulation, and we only do that to add and remove the <video>/<audio>
elements in this demo. We don't use it at all for anything WebRTC specific in
this example.
