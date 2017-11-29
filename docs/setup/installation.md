The following guide explains how to download and install and instance of
LibCrowds locally, for testing or development.

!!! info
    If you are looking for guidance on how to create or configure projects see
    the [Projects](/projects/getting-started.md) section.

## Introduction

LibCrowds is fundamentally a [Vue.js](https://vuejs.org/) Server-Side Rendered
(SSR) UI that incorporates various custom plugins and communicates with a
[PYBOSSA](https://github.com/Scifabric/pybossa) backend.
Therefore, we need to install, configure and run both an instance of LibCrowds
and an instance of PYBOSSA.

## Install VirtualBox, Vagrant and git

The easiest way to get instances of LibCrowds and PYBOSSA up and running
is by using [VirtualBox](https://www.virtualbox.org/) and
[Vagrant](https://www.vagrantup.com/).

We will also need to install git, which is the version control system via which
both LibCrowds and PYBOSSA are distributed.

Follow the following links to download and run the appropriate installers for
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

PYBOSSA (with the default theme) should now be available at
[http://127.0.0.1:5000](http://127.0.0.1:5000)

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

LibCrowds should now be running using the default settings at
[http://127.0.0.1:8080](http://127.0.0.1:8080).

However, if you open it up now you are likely to see an error message as the
two servers have not yet been configured to communicate properly with each
other.

The next step is [Configuring PYBOSSA](/setup/configuring-pybossa.md).
