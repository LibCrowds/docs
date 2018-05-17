This section explains how to download and install and instance of
LibCrowds locally, for testing or development. If you are interested in
deploying LibCrowds to a live server, see the
[Deployment](/setup/deployment.md) guide.

## Install VirtualBox, Vagrant and git

The easiest way to get started is by using
[VirtualBox](https://www.virtualbox.org/) and
[Vagrant](https://www.vagrantup.com/).

We will also need to install git, which is the version control system via which
both LibCrowds and PYBOSSA are distributed.

Follow the links below to download and run the appropriate installers for
your operating system.

1. [git](https://git-scm.com/downloads)
2. [VirtualBox](https://www.virtualbox.org/)
3. [Vagrant](https://www.vagrantup.com/)

## Download and run PYBOSSA

Once the above software is succesfully installed, open up a terminal and clone
PYBOSSA to your local machine:

```bash
git clone --recursive https://github.com/Scifabric/pybossa.git
```

Setup the PYBOSSA development environment:

```bash
cd pybossa
vagrant up
```

Run the PYBOSSA server:

```bash
vagrant ssh
python run.py
```

PYBOSSA should now be running (with the default theme) at
[http://127.0.0.1:5000](http://127.0.0.1:5000)

??? tip "Installing behind a web proxy"
    If you're installing from behind a web proxy then you will probably run
    into issues when attempting to start Vagrant, in which case you can try
    running these commands from the `pybossa` directory:

    ```bash
    # set environment variables using the command for your OS (Windows example shown)
    set VAGRANT_HTTP_PROXY=http://username:password@proxy_server:proxy_port
    set VAGRANT_HTTPS_PROXY=https://username:password@proxy_server:proxy_port

    # install the vagrant-proxyconf plugin
    vagrant plugin install vagrant-proxyconf
    ```

## Download and run Explicates

A server that complies with the
[Web Annotation Protocol](https://www.w3.org/TR/annotation-protocol) is
required to handle the storage and retrieval of user tags and results data.

LibCrowds has been built for use with the
[Explicates](https://github.com/alexandermendes/explicates) server, which
complies with the standard protocol and has the additional search
functionality required for this application.

Once the above software is succesfully installed, open up a terminal and clone
Explicates to your local machine:

```bash
git clone https://github.com/alexandermendes/explicates.git
```

Setup the Explicates development environment:

```bash
cd explicates
vagrant up
```

Run the Explicates server:

```bash
vagrant ssh
python run.py
```

Explicates should now be running at
[http://127.0.0.1:3000](http://127.0.0.1:3000)

??? tip "Installing behind a web proxy"
    If you're installing from behind a web proxy then you will probably run
    into issues when attempting to start Vagrant, in which case you can try
    running these commands from the `pybossa` directory:

    ```bash
    # set environment variables using the command for your OS (Windows example shown)
    set VAGRANT_HTTP_PROXY=http://username:password@proxy_server:proxy_port
    set VAGRANT_HTTPS_PROXY=https://username:password@proxy_server:proxy_port

    # install the vagrant-proxyconf plugin
    vagrant plugin install vagrant-proxyconf
    ```

## Download and run LibCrowds

The same process is followed to setup the LibCrowds development environment:

```bash
git clone https://github.com/LibCrowds/libcrowds.git
```

Setup the LibCrowds development environment:

```bash
cd pybossa
vagrant up
```

Run the LibCrowds server:

```bash
vagrant ssh
npm run dev
```

??? tip "Installing behind a web proxy"
    If you're installing from behind a web proxy then you will probably run
    into issues when attempting to start Vagrant, in which case you can try
    running these commands from the `libcrowds` directory:

    ```bash
    # set environment variables using the command for your OS (Windows example shown)
    set VAGRANT_HTTP_PROXY=http://username:password@proxy_server:proxy_port
    set VAGRANT_HTTPS_PROXY=https://username:password@proxy_server:proxy_port

    # install the vagrant-proxyconf plugin
    vagrant plugin install vagrant-proxyconf
    ```

LibCrowds should now be running, using the default settings, at
[http://127.0.0.1:8080](http://127.0.0.1:8080).

!!! info
    You must access the website at http://127.0.0.1:8080, rather than
    http://localhost:8080, otherwise it will not be possible to track the user
    session cookie.

However, if you attempt to open the site now you are likely to see an error
message as the two servers have not yet been configured to communicate properly
with each other, nor have we installed the required plugins.

---

The next step is to install the required [Plugins](/setup/plugins.md).
