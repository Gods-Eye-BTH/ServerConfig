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
 * systemd (comes pre-installed on most distros, you could probably do something with crontab if you prefer that)


### Step 3: Installing Node Media Server
Install Git, ffmpeg, tmux, nginx, and Go from the package manager of your choice.
I suggest installing NodeJS and npm with [Node Version Manager](https://github.com/creationix/nvm)
for easy version handling and updating. Please note that nvm installs node in your home
directory and might not be optional for running node services.

Make a new folder and clone the Node Media Server into the folder:  
`mkdir streamserver && git clone https://github.com/illuspas/Node-Media-Server streamserver/`

Move to the newly created folder: `cd streamserver`

Install the required node modules: `npm install`


### Step 4: Set up services

Edit the example service configs provided in this repo to match your paths
and services you want to run.

Now place the .service files in `/etc/systemd/system/`

Start the services: `sudo service start <servicename>.service` where <servicename> is the name of your service.

### Step 5: Nginx config

now copy over the nginx config from this repo to your nginx.
You may need to customize it based on what you're already are running.

Install a SSL-TLS certificate from Let's Encrypt with [Certbot](https://certbot.eff.org/)

### Step 6: Dummy api (optional)

If you want to run the dummy api on the server you'll need to setup your [GOPATH](https://golang.org/doc/code.html#GOPATH).  
Then install the go package gorilla/mux by running `go get github.com/gorilla/mux`.  

Config and set up the service for the dummy api and then start it. Note that you also need
to make sure you have the api route configured in your nginx config
