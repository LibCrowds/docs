LibCrowds relies on a PYBOSSA backend that needs to be configured as follows.

## Plugins

Install the following plugins (the documentation for each explains how to
do this):

- [pybossa-z3950](https://github.com/alexandermendes/pybossa-z3950)
- [pybossa-lc](https://github.com/LibCrowds/pybossa-lc)

## Required settings

The following settings are all required for the application to run correctly.
They should be added to PYBOSSA's `settings_local.py` file:

```python
# Allow requests from LibCrowds
# (modify the origins according to your environment)
CORS_RESOURCES = {
  r"/*": {
    "origins": [
      "http://127.0.0.1:8080"
    ],
    "allow_headers": [
      'Content-Type',
      'Authorization',
      'X-CSRFToken'
    ],
    "supports_credentials": True
  }
}

# Additional category fields
CATEGORY_INFO_PUBLIC_FIELDS = [
  'tagline',
  'background',
  'license',
  'presenter',
  'forum',
  'presenter_options',
  'content',
  'published',
  'celebration',
  'volumes',
  'tags'
]

# Additional user fields
USER_INFO_PUBLIC_FIELDS = [
  'announcements',
  'templates'
]

# Additional project fields
PROJECT_INFO_PUBLIC_FIELDS = [
  'tags'
]

# The user ID used to make automated announcements
ANNOUNCEMENT_USER_ID = 1

# Avoid 404 errors when accessing URLs with or without a trailing slash
STRICT_SLASHES = False

# Specify an SPA frontend
SPA_SERVER_NAME = 'http://127.0.0.1:8080'

# Allow projects to be published with no traditional task presenter
DISABLE_TASK_PRESENTER = True

# Allow the session cookie to be shared with any subdomain of mydomain.com
SESSION_COOKIE_DOMAIN = 'mydomain.com'

# Flickr credentials (required for importing Z39.50 tasks)
FLICKR_API_KEY = 'your-key'
FLICKR_SHARED_SECRET = 'your-secret'
```

!!! tip
    See the [PYBOSSA documentation](http://docs.pybossa.com) for details of all
    other available settings.

## Optional settings

The settings below can be added to PYBOSSA's `settings_local.py` file to help
with various administration tasks such as reanalysing all results or
checking for empty templates.

```python
# The user ID used to make automated announcements
ANNOUNCEMENT_USER_ID = 1

# Extra tasks to run when the application is started or restarted
EXTRA_STARTUP_TASKS = {
    'reanalyse_all_results': False,
    'populate_empty_results': True,
    'check_for_missing_templates': True,
    'remove_bad_volumes': True
}
```

If you're following on from the [Installation](/setup/introduction.md) guide,
you should now be able to open up
[http://127.0.0.1:8080](http://127.0.0.1:8080) and see your fully operational
LibCrowds instance.

To explore the and modify the LibCrowds settings, see
[Configuring LibCrowds](/setup/configuring-libcrowds.md).

!!! info
    You must access the website at http://127.0.0.1:8080, rather than
    http://localhost:8080, otherwise it will not be possible to track the user
    session cookie.

