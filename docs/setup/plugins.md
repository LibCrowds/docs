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

!!! warning "Important"

    Some plugins import Flask modules in a deprecated manner, causing warnings when launching the server.
	The issue is related to several calls in the `__init__.py` files in PyBossa plugins that import Flask submodules in a deprecated manner. These warnings should be patched in a future update, but a temporary fix is obtained with the following:

	Flask extension import statements such as
	```
	import flask.ext.plugins
	```
	should be replaced with
	```
	import flask_plugins
	```
	Affected files include:
	```
	pybossa/plugins/pybossa_lc/__init__.py
	pybossa/plugins/pybossa_lc_email/__init__.py
	pybossa/plugins/pybossa_z3950/__init__.py
	pybossa/plugins/pybossa_lc/api/projects.py
	pybossa/plugins/pybossa_lc/api/categories.py
	pybossa/plugins/pybossa_lc/api/admin.py
	```

	Additionally, the following warning may be observed when calling `python run.py`:
	```
	WARNING: Couldn't create 'PyZ3950.PyZ3950_parsetab'. [Errno 20] Not a directory: '/home/vagrant/pybossa-env/lib/python2.7/site-packages/mollyZ3950-2.04_molly1-py2.7-linux-x86_64.egg/PyZ3950/PyZ3950_parsetab.py'
	<type 'exceptions.ImportError'>
	('No module named ext.z3950',)
	No module named ext.z3950
	Z39.50 plugin disabled
	```
	Again, a temporary fix for this is obtained with the following:
	```
	pip uninstall mollyZ3950
	wget https://files.pythonhosted.org/packages/6a/34/8176b841926a2add20524a9f74c307ac5fe6e33e9f4af12a58e6f7223982/mollyZ3950-2.04-molly1.tar.gz
	pip install mollyZ3950-2.04-molly1.tar.gz
	pip uninstall Flask-Z3950
	pip install Flask-Z3950
	```
	in combination with changing `flask.ext.*` for `flask_*` in
	```
	/home/vagrant/pybossa-env/lib/python2.7/site-packages/flask_z3950/view.py
	```
---

The next step is [Configuring PYBOSSA](/setup/configuring-pybossa).
