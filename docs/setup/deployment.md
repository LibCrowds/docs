This guide explains how to deploy an instance of LibCrowds to a set of
servers with NGINX and supervisor.

Three servers are required, one for LibCrowds, one for PYBOSSA and one
for Explicates. The following page describes how to get all three set up.

## Domains

Before we begin, it is important to note that both LibCrowds and PYBOSSA
should be served from the same domain.

This is because LibCrowds uses SSR, so the PYBOSSA session cookie needs to be
shared with the LibCrowds server (rather than the client) and this will only
work properly if both applications are served from the same domain. Subdomains
are fine, so you can still run your applications on different servers.

If you don't do this, the application will still run but, as it will not be
possible to fully render certain pages on the server, you will see some
strange behaviour with users appearing to not be signed in when the
application first loads. You might also notice errors when attempting to
navigate directly to restricted pages (such as the various administration
dashboards).

With that in mind, let's setup our servers.

## PYBOSSA

Rather than replicating what has already been written, for details of how to
deploy PYBOSSA see the [PYBOSSA documentation](http://docs.pybossa.com).

## LibCrowds

Starting with a fresh Ubuntu 16.04 server, run through the procedures below.

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
    it is possible that your server does not have enough memory. You
    may want to consider upgrading the server or adding some swap space.

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

Your LibCrowds server should now be running at
[http://your.domain.com](http://your.domain.com). However, we still need to
configure the Annotations server.

## Explicates

Starting with a fresh Ubuntu 16.04 server, run through the procedures below.

## Install Python

Explicates requires [Python](https://www.python.org/) >= 2.7 to run.

Update and upgrade the package index:

```bash
sudo apt-get update
sudo apt-get upgrade
```

Install Python:

```bash
sudo apt install python
```

Install some additional dependencies:

```
sudo apt install python-virtualenv python-dev python-setuptools python-pip
```

## Install git

Explicates is distributed under version control using
[git](https://git-scm.com/), install it by running:

```bash
sudo apt-get install git-core
```

## Download and build Explicates

Run the following commands to clone the Explicates repository into
`/var/www/explicates`:

```bash
mkdir /var/www
git clone https://github.com/alexandermendes/explicates /var/www/explicates
```

Enter the directory:

```bash
cd /var/www/explicates
```

Create and enter a virtual environment:

```bash
virtualenv env
source env/bin/activate
```

Install Explicates:

```bash
pip install -r requirements.txt
```

Copy the configuration template (see
[Configuring Explicates](/setup/configuring-explicates.md) for details
of how to edit this file):

```bash
cp settings.py.tmpl settings.py
```

!!! warning "Important"

    You will need to edit the `SERVER_NAME` setting now to point to the location
    of your server (e.g. annotations.example.com). It is required to build
    IDs outside of the request context and this is first done when the database
    is created below.

Copy the alembic configuration template:

```bash
cp alembic.ini.tmpl alembic.ini
```

## Seting up the database

Explicates is backed by a [PostgreSQL](https://www.postgresql.org/) database.

Install dependencies:

```bash
sudo apt-get install postgresql postgresql-server-dev-all python-psycopg2 libpq-dev
```

Add a database user:

```bash
sudo -u postgres createuser -d -P explicates
```

Enter the password `tester` when prompted.

!!! info

    If you choose a different password you should also edit the database
    path in `settings.py` and `alembic.ini`.

Create the database:

```bash
sudo -u postgres createdb explicates -O explicates
```

Populate the database:

```bash
python /var/www/explicates/bin/db_create.py
```

To check that everything has gone OK so far, you should now be able to
type `python run.py` and see some messages that let you know the develpoment
server is running (then press CTRL+C to quit).

## Setting up NGINX

To setup [NGINX](https://www.nginx.com/resources/wiki/), first install it:

```
sudo apt-get install nginx
```

Remove the default server configuration:

```bash
sudo rm -r /etc/nginx/sites-available/default
```

Edit a new server configuration file:

```bash
vim /etc/nginx/sites-available/explicates
```

Copy in the following and save the file:

```nginx
server {
  listen 80 default_server;
  listen [::]:80 default_server;

  # Change this to match your domain
  server_name annotations.example.com;

  client_body_buffer_size 10K;
  client_header_buffer_size 1k;
  client_max_body_size 10m;
  large_client_header_buffers 2 1k;

  gzip             on;
  gzip_comp_level  2;
  gzip_types       text/plain application/json application/ld+json;
  gzip_min_length  1000;
  gzip_proxied     expired no-cache no-store private auth;

  location / {
    expires -1;
    include uwsgi_params;
    uwsgi_pass unix:/tmp/explicates.sock;
  }
}
```

Enable the Explicates configuration:

```bash
ln -s /etc/nginx/sites-available/explicates /etc/nginx/sites-enabled/explicates
```

Restart the NGINX server:

```bash
sudo service nginx restart
```

## Setting up uWSGI

To setup [uWSGI](https://uwsgi-docs.readthedocs.io/en/latest/), first install it:

```bash
pip install -U uwsgi
```

Edit a new server configuration file:

```bash
vim /var/www/explicates/explicates.ini
```

Copy in the following and save the file:

```bash
[uwsgi]
socket = /tmp/explicates.sock
chmod-socket = 666
chdir = /var/www/explicates
pythonpath = ..
virtualenv = /var/www/explicates/env
module = run:app
cpu-affinity = 1
processes = 2
threads = 2
buffer-size = 65535
```

## Setting Up Supervisor

Supervisor is used to run Explicates in the background and restart it when the
server boots up.

```
sudo apt-get install supervisor
```

Edit a new Supervisor program configuration:

```bash
vim /etc/supervisor/conf.d/explicates.conf
```

Copy in the following and save the file:

```conf
[program:explicates]
command=/var/www/explicates/env/bin/uwsgi /var/www/explicates/explicates.ini
directory=/var/www/explicates
autostart=true
autorestart=true
log_stdout=true
log_stderr=true
logfile=/var/log/explicates.log
logfile_maxbytes=10MB
logfile_backups=2
```

Restart supervisor:

```bash
sudo service supervisor stop
sudo service supervisor start
```

Your Annotation server should now be running at
[http://your.domain.com](http://your.domain.com).

## Security

There are lots of potential steps that you could take to secure your servers.
Running through all of the options here is outside the scope of this guide,
but here are some quick wins for the LibCrowds and Explicates servers
(details might need to be modified a bit for the PYBOSSA server).

### Firewall

UFW, or Uncomplicated Firewall, is an easy way to manage a frontend firewall.

Install it:

```bash
sudo apt-get install ufw
```

Deny incoming and allow outgoing by default:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Allow connections:

```bash
sudo ufw allow ssh
sudo ufw allow 22/tcp
```

Check the rules:

```bash
ufw status
```

You should see the following output:

```bash
To                         Action      From
--                         ------      ----
22                         ALLOW       Anywhere
80                         ALLOW       Anywhere
443                        ALLOW       Anywhere
22 (v6)                    ALLOW       Anywhere (v6)
80 (v6)                    ALLOW       Anywhere (v6)
443 (v6)                   ALLOW       Anywhere (v6)
```

If the rules do indeed appear as above, enable the firewall:

```bash
sudo ufw enable
```

## Secure Sockets Layer (SSL)

[Let's Encrypt](https://letsencrypt.org) provide free SSL certificates. Use
the [Certbot](https://certbot.eff.org/) client to set them up for your
operating system.

After following the Certbot guide, above, you can setup a scheduled task
to automatically renew the certificates.

Edit a new daily task:

```bash
vim /etc/cron.daily/certrenew
```

Copy in the following and save the file:

```
certbot renew
```

Make the file executable:

```bash
chmod +x /etc/cron.daily/certrenew
```

Your certificate should now be checked for renewal daily.

---

The next step is to install the required LibCrowds
[Plugins](/setup/plugins.md).
