# ServerConfig

This is the server configuration instructions and documentation repo.
API documentation can be found in the file [API_DOC.md](/API_DOC.md).

Instructions on how to stream to the server can be found in the file [STREAMING.md](/STREAMING.md)


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
and services you want to run. Please note that full paths are required.

Now place the .service files in `/etc/systemd/system/`

Reload so systemd can find your service `sudo systemctl daemon-reload`

Start the services: `sudo service <servicename> start` where <servicename> is the name of your service.

run the command `sudo service <servicename> status` to check if it is running properly

### Alternative step 4: other ways of running things

You can set up crontabs with the things you want to start when the system starts:
`@reboot <your command here>`

If you want a highly temporary setup you can just open a tmux and run a command in there
and then detach it. Please note that it will not start up after a reboot.

### Step 5: Nginx config

Your nginx config should be located in `/etc/nginx/sites-available/`
the default config file is called `default`.

edit this config (or if you have a custom config edit that one) to add
the location /stream/ as a reverse proxy for the Node Media Server. An example is
available in this repo under [nginx_config/default](/nginx_config/default).

Install a SSL-TLS certificate from Let's Encrypt with [Certbot](https://certbot.eff.org/)*

\* *Note that this only works with machines that has an external ip*

### Step 6: Dummy streams (optional)

The dummy streams works the same as regular streams but point to the localhost url instead
and the input can be either a camera or an mp4 video with h264 video and AAC audio.

Setting up regular streams is documented in the [STREAMING.md](STREAMING.md) file.

The streams can be automated to loop with a quick bash script or run as a always restarting systemd service.

### Step 7: Dummy api (optional)

If you want to run the dummy api on the server you'll need to setup your [GOPATH](https://golang.org/doc/code.html#GOPATH).  
Then install the go package gorilla/mux by running `go get github.com/gorilla/mux`.  

After that you need to set it up as a service. Unfortunately the service file for the
dummy API that is provided in this repo doesn't really work.

Configure your nginx to add the location /api/ as a reverse proxy for the api.
There is an example of this configuration in this repo under [nginx_config/default](/nginx_config/default).
