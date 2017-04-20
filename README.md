## Watchman

Watchman is a machine learning network that has learned to recognize violence in video. It can be dropped in place with an existing IP camera system as an added level of security against violent events.

Its app notification system gives real-time alerts of events it detects as violent and logs video clips of the altercations for later viewing.

## Setup
Watchman is designed to leverage IP connected cameras, smartphones, and simple installation to make video classification simple to install.

### Server
The server hosts the classification network and the notification system. The network has been pre-trained and runs automatically with the server, but a few requirements are needed to run the system. Make sure you have Python2.7 and Tensorflow installed on the system that will host the server. On Linux, it's as simple as [this](https://www.tensorflow.org/get_started/os_setup):

```markdown
$ sudo apt-get install python-pip python-dev
$ pip install tensorflow
```

To set up the system, set your camera connections in the connections.conf configuration file as such:

```markdown
cam1:192.168.200.3
cam1pword:password1

cam2:192.168.200.5
cam2pword:password2
```

Then it's a simple matter of running the watchman.py script as such:

```markdown
$ python watchman.py
```
The script will automatically connect to the IP cameras listed in configuration file and begin classification.


In order to set up the notification server, make sure you have Node.js, Yarn, PM2 installed on the server.

Node.js installation:
```markdown
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
sudo apt-get install -y nodejs
```
Yarn installation:
```markdown
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install yarn
```
PM2 installation:
```markdown
$ npm install pm2 -g
```
Finally, install dependencies for this project using Yarn and run the application.

```markdown
$ yarn install
$ yarn startserver
```
All the endpoints will be available through http://localhost:8080

### App

Download the iOS app [here](https://github.com/iWatchman/iWatchman-iOS), installation instructions for which can be found 
[here](https://github.com/iWatchman/iWatchman-iOS/blob/master/README.md)

### Using Watchman

Under normal use, the server will send push notifications to the user's device when it detects events in the video feed.

![App Notification](assets/watchman_notification.png)

The user has the ability to pull up a list view of the logged videos. Selecting one will load a detail view of the video, allow the user to view the video by tapping it. This is shown in the following images:

![App Listview](assets/watchman_listview.png)

![App Detailview](assets/watchman_detailview.png)

![View Video](assets/watchman_viewvideo.png)
