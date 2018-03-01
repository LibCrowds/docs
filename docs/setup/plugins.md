Most of LibCrowds' custom functionality is handled via the frontend
application. However, as some functionality, such as results analysis, can
only  be dealt with effectively on the backend server, we need to install a
few additional PYBOSSA plugins.

## pybossa-z3950

This plugin handles the communication with Z39.50 databases that is required
to use the platforms Z39.50 task presenter.

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

Install dependencies:

```bash
sudo apt-get install libxml2-dev libxslt-dev python-dev lib32z1-dev
```

Clone the plugin repo:

```bash
git clone https://github.com/alexandermendes/pybossa-z3950 pybossa/plugins
```

Install the plugin:

```bash
cd pybossa/plugins/pybossa-z3950
python setup.py install
cd ..
cp -r pybossa-z3950/pybossa_z3950 pybossa_z3950
```


## pybossa-lc

This plugin handles various bits of LibCrowds-specific functionality, such as
results analysis, generation of Web Annotations and project management via
templates.

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
