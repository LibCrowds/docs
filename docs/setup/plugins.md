Most of LibCrowds' custom functionality is handled via the core frontend
application. However, some functionality such as results analysis, can
only be dealt with effectively on the backend server, so we need to install a
few additional PYBOSSA plugins. The following page will guide you through the
steps required.

Navigate to your PYBOSSA root folder:

```bash
cd /path/to/pybossa
```

If you are running locally, enter the virtual machine:

```bash
vagrant ssh
```

Otherwise, if you're setting up a production server, activate your virtual
environement:

```bash
source pybossa/env/bin/activate
```

Now install the various plugins.

## pybossa-z3950

This plugin handles the communication with Z39.50 databases that is required
to use the platforms Z39.50 task presenter.

Install dependencies:

```bash
sudo apt-get install libxml2-dev libxslt-dev python-dev lib32z1-dev
```

Clone the plugin repo:

```bash
git clone https://github.com/alexandermendes/pybossa-z3950 pybossa/plugins
```

Install the plugin and return to root folder:

```bash
cd pybossa/plugins/pybossa-z3950
python setup.py install
cd ..
cp -r pybossa-z3950/pybossa_z3950 pybossa_z3950
cd /path/to/pybossa
```

## pybossa-lc-email

This plugin replaces the default email templates with custom LibCrowds
templates.

Clone the plugin repo:

```bash
git clone https://github.com/LibCrowds/pybossa-lc-email pybossa/plugins
```

Activate the plugin and return to root folder:

```bash
cd pybossa/plugins
cp -r pybossa-lc-email/pybossa_lc_email pybossa_lc_email
cd /path/to/pybossa
```

## pybossa-lc

This plugin handles various bits of LibCrowds-specific functionality, such as
results analysis, generation of Web Annotations and project management via
templates.

Clone the plugin repo:

```bash
git clone https://github.com/LibCrowds/pybossa-lc pybossa/plugins
```

Install the plugin:

```bash
cd pybossa/plugins/pybossa-lc
pip install -r requirements.txt
cd ..
cp -r pybossa-lc/pybossa_lc pybossa_lc
```

The plugins will be available after you restart the server.

---

The next step is [Configuring PYBOSSA](/setup/configuring-pybossa.md).
