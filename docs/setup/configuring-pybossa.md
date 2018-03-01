LibCrowds relies on a PYBOSSA backend that needs to be configured as follows.

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
  'tags',
  'templates
]

# Additional user fields
USER_INFO_PUBLIC_FIELDS = [
  'announcements',
  'templates'
]

# Additional project fields
PROJECT_INFO_PUBLIC_FIELDS = [
  'tags',
  'template_id',
  'volume_id'
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

# The following settings are used in emails sent from the server-side
CONTACT_EMAIL = 'info@libcrowds.com'
BRAND = 'LibCrowds'

# Database details for Z39.50 projects
Z3950_DATABASES = {
    'loc': {
        'host': 'z3950.loc.gov',
        'db': 'Voyager',
        'port': '7090'
    }
}
```

!!! tip
    See the [PYBOSSA documentation](http://docs.pybossa.com) for details of all
    other available settings.

## Optional settings

The settings below can be added to PYBOSSA's `settings_local.py` file to help
with various administration tasks, such as checking for invalid templates, or
triggering analysis of all empty results.

These settings are optional as they will modify the database and there are
instances when that is undesirable, such as when migrating to a new version
of the application. However, unless you have a specific reason for excluding
them, it is recommended that they are also added to PYBOSSA's
`settings_local.py` file.

```python
# The user ID used to make automated announcements
ANNOUNCEMENT_USER_ID = 1

# Extra tasks to run when the application is started or restarted
EXTRA_STARTUP_TASKS = {
    'check_for_invalid_templates': True,
    'populate_empty_results': True,
    'reanalyse_all_results': True,
    'remove_bad_volumes': True
}
```

If you're following on from the [Local Installation](/setup/introduction.md)
or [Deployment](/setup/deployment.md) guides,
you should now have a fully operational LibCrowds instance.

---

To explore the core LibCrowds settings, see
[Configuring LibCrowds](/setup/configuring-libcrowds.md).
