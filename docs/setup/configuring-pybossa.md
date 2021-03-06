LibCrowds relies on a PYBOSSA backend that needs to be configured as follows.

## Required settings

The settings below are all required for the application to run correctly and
should be added to PYBOSSA's `settings_local.py` file.

The following settings can be copied into your main configuration file
directly:

```python
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
  'project_filters',
  'templates',
  'annotations'
]

# Additional user fields
USER_INFO_PUBLIC_FIELDS = [
  'announcements',
  'templates'
]

# Additional project fields
PROJECT_INFO_PUBLIC_FIELDS = [
  'filters',
  'template_id',
  'volume_id'
]

# Avoid 404 errors when accessing URLs with or without a trailing slash
STRICT_SLASHES = False

# Allow projects to be published with no traditional task presenter
DISABLE_TASK_PRESENTER = True
```

These settings will need to be modified according to your environment, after
copying them into your main configuration file:

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

# Specify an SPA frontend
SPA_SERVER_NAME = 'http://127.0.0.1:8080'

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

# The base URL of your Explicates annoation server
WEB_ANNOTATION_BASE_URL = 'http://127.0.0.1:3000'
```

!!! tip
    See the [PYBOSSA documentation](http://docs.pybossa.com) for details of all
    other available settings.

---

If you're following on from the [Local Installation](/setup/introduction)
or [Deployment](/setup/deployment) guides,
you should now have a fully operational LibCrowds instance.

To explore the core LibCrowds settings, see
[Configuring LibCrowds](/setup/configuring-libcrowds).
