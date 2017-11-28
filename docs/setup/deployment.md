This page gives some guidance on how to deploy an instance of LibCrowds and
assumes that you are starting with a fresh Ubuntu server.

!!! info
    For details of how to deploy the PYBOSSA backend see the
    [PYBOSSA documentation](http://docs.pybossa.com).

## Install Node.js and npm

LibCrowds requires [Node.js](https://nodejs.org) >= 8.0.0 to run.

Update and upgrade the package index:

```bash
sudo apt-get update
sudo apt-get upgrade
```

Go to your home directory and retrieve the installation script:

```bash
cd ~
curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
```

Run the script:

```bash
sudo bash nodesource_setup.sh
```

Install Node.js and the `build-essential` package:

```bash
sudo apt-get install nodejs
sudo apt-get install build-essential
```

## Install git

LibCrowds is distributed under version control using
[git](https://git-scm.com/), install it by running:

```bash
sudo apt-get install git-core
```

## Download and build LibCrowds

Run the following commands to clone the LibCrowds repository into
`/var/www/libcrowds`:

```bash
mkdir /var/www
git clone https://github.com/LibCrowds/libcrowds /var/www/libcrowds
```

Enter the directory:

```bash
cd /var/www/libcrowds
```

Install LibCrowds' dependencies:

```bash
npm install
```

Copy the configuration template (see
[Configuring LibCrowds](/setup/configuring-libcrowds.md) for details
of how to edit this file):

```bash
cp local.config.js.tmpl local.config.js
```

Build the application:

```bash
npm run build
```

!!! tip
    If the installation or build process is getting killed before finishing
    it is possible that your don't have enough memory on the server and you
    may want to consider upgrading or adding some swap space.

## Setting up NGINX

To serve the site using [NGINX](https://www.nginx.com/resources/wiki/),
first install it:

```
sudo apt-get install nginx
```

Remove the default server configuration:

```bash
sudo rm -r /etc/nginx/sites-available/default
```

Edit a new server configuration file:

```bash
vim /etc/nginx/sites-available/libcrowds
```

Copy in the following and save the file:

```nginx
map $sent_http_content_type $expires {
    "text/html"                 epoch;
    "text/html; charset=utf-8"  epoch;
    default off;
}

server {
  listen 80 default_server;
  listen [::]:80 default_server;

  client_body_buffer_size 10K;
  client_header_buffer_size 1k;
  client_max_body_size 10m;
  large_client_header_buffers 2 1k;

  gzip             on;
  gzip_comp_level  2;
  gzip_types       text/plain application/xml text/css application/javascript;
  gzip_min_length  1000;
  gzip_proxied     expired no-cache no-store private auth;

  location / {
    expires $expires;
    proxy_redirect                      off;
    proxy_set_header Host               $host;
    proxy_set_header X-Real-IP          $remote_addr;
    proxy_set_header X-Forwarded-For    $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto  $scheme;
    proxy_read_timeout                  1m;
    proxy_connect_timeout               1m;
    proxy_pass                          http://127.0.0.1:8080;
  }
}
```

Enable the LibCrowds configuration:

```bash
ln -s /etc/nginx/sites-available/libcrowds /etc/nginx/sites-enabled/libcrowds
```

Restart the server:

```bash
sudo service nginx restart
```

## Setting Up Supervisor

Supervisor is used to run LibCrowds in the background and restart it when the
server boots up.

```
sudo apt-get install supervisor
```

Edit a new Supervisor program configuration:

```bash
vim /etc/supervisor/conf.d/libcrowds.conf
```

Copy in the following and save the file:

```conf
[program:libcrowds]
directory=/var/www/libcrowds
command=npm run start
autostart=true
autorestart=true
log_stdout=true
log_stderr=true
logfile=/var/log/libcrowds.log
logfile_maxbytes=10MB
logfile_backups=2
```

Restart supervisor:

```bash
sudo service supervisor stop
sudo service supervisor start
```

Your LibCrowds server should now be running at http://your.domain.com.


## Different Domains

It is important that the PYBOSSA instance is served from the same domain as
the LibCrowds instance. This is because the PYBOSSA session cookie needs to
be shared with the LibCrowds server and this will only work properly if both
applications are served from the same domain. Subdomains are fine, so you can
still run your applications on different servers.

If you don't do this, the application will still run but, as it will not be
possible to fully render certain pages on the server, you will see some
strange behaviour with users appearing to not be signed in when the
application first loads. You might also notice errors when attempting to
navigate directly to restricted pages (such as the various administration
dashboards).

You will also need to add `SESSION_COOKIE_DOMAIN = mydomain.com` to your
PYBOSSA settings file, see [Configuring PYBOSSA](configuration/pybossa.md).
