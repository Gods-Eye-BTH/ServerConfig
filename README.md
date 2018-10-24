# ServerConfig

This is the server configuration instructions and documentation repo.
API documentation can be found in the file [API_DOC.md](/API_DOC.md).

## Setting up a God's Eye Server

This set of instructions has been tested on ubuntu 18 but should work on most installs
(some steps may vary depending on your OS, feel free to contribute with instructions)

### Step 1: Server Requirements
You need to have a server that you can access over ssh and reach over port 80 (HTTP), 443 (HTTPS) and 1935 (RTMP).
Note that depending on how much you scale up this project it may require more processing
power.

### Step 2: Packages you need
 * Git
 * NodeJS version 10 or above
 * npm
 * ffmpeg
 * Nginx
 * Go (golang)
 * tmux (recommended for ease of use)
 * some form of service management like systemd, systemctl or use crontab


### Step 3: Installation
Install Git, ffmpeg, tmux, nginx, and Go from the package manager of your choice.
I suggest installing NodeJS and npm with [Node Version Manager](https://github.com/creationix/nvm)
for easy version handling and updating. Please note that nvm installs node in your home
directory and might not be optional for running node services.

Make a new folder and clone the Node Media Server into the folder:  
`mkdir streamserver && git clone https://github.com/illuspas/Node-Media-Server streamserver/`

Move to the newly created folder: `cd streamserver`

Install the required node modules: `npm install`

#### This part is a work in progress
**TODO**: Add intstructions for setting it up as a service

in a tmux run `node app.js`

**TODO**: Add nginx config to repo

now copy over the nginx config from this repo to your nginx.
You may need to customize it based on what you're already are running.

Install a SSL-TLS certificate from Let's Encrypt with [Certbot](https://certbot.eff.org/)
