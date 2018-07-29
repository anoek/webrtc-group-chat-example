About this fork
=====

This fork is intended for use only with audio so video support was removed
because I have no intentions to test and support it. Also I don't have
a webcam.

Second, HTTPS support was added because without it this demo was working for
Firefox users only (which allows `getUserMedia` for insecure hosts). Now support
should be much broader, tested Chrome and Firefox on Mac, Chrome on Android.
From now on `client.html` and signaling server should be hosted on SSL enabled
domain.

3rd, some issues were fixed (but some deprecation issues are still there).

About
=====

This is a "simple", but complete example of how to utilize WebRTC to do peer to
peer voice chatting between two or more people.

### Server Side 
This example uses node.js and socket.io to create a "Signaling Server", which
runs on (or near) your web server to manage who should talk to who. The purpose
of the signaling server is to relay information between peers while you are
setting them up to talk directly to each other.


### Client Side
Included is `client.html` which contains all of the logic to connect to the
signaling server, join a virtual group chat channel, connect with peers, and
stream audio to all party members using the raw WebRTC API.


Running
=======

### Node.js signaling server
You'll need to install `node.js` as well as the `express` and `socket.io` libraries:
```
npm install
```

Then simply run the signaling server:
```
node signaling-server.js
```

### Web server
You'll also probably want to host `client.html` on a web server somewhere. You'll need
to edit `client.html` and change `YOUR_HTTPS_DOMAIN` to be the hostname or IP of the signaling server.

Note: you cannot file locally or AFAIK host signaling server and `client.html`
on different hosts.


### Running the sample
Now navigate to wherever you stuck `client.html` and you should be presented with
a dialog asking permission to access your microphone / webcam. Once accepted,
you should see a local stream appear on the page. Now open up the same page in
another browser, on the same computer or another, and watch as the magic of WebRTC takes
effect and both images and audio samples mysteriously move from one browser to the other.
Repeat with as many browsers as you dare.


Note: At the time of writing this, only firefox and chrome support WebRTC,
however both browsers support this on Windows, Linux, Mac, and Android, so lots
of fun can be had pointing everyones' phones, tablets, and laptops at that `client.html`
and bogging down your network with audio traffic.


Using things other than jQuery, node.js, and socket.io
=============================================
The choice of node.js and socket.io is based purely on my familiarity with them
and the fact that their fairly easy to understand even if you aren't familiar
with them. However, you can use any mechanisms you want for your signaling system, you
just need a way to exchange ICE candidates and session descriptions between
clients.

The use of jQuery is even less important, I just like using it for DOM
manipulation, and we only do that to add and remove the <audio>
elements in this demo. We don't use it at all for anything WebRTC specific in
this example.

Adapter.js
==========
You'll see `client.html` use `adapter.js`. This "library" just normalizes the
WebRTC API, which will only be necessary while WebRTC is making its way through
the standards process. Once everything is standardized and functions are
de-prefixed in the browsers, this won't be necessary anymore.
