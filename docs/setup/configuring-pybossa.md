As LibCrowds relies on a PYBOSSA backend you will need to add the following to
PYBOSSA's `settings_local.py` file:

!!! tip
    See the [PYBOSSA documentation](http://docs.pybossa.com) for details of all
    other available settings.

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

!!! warning
    These settings are all required for the application to run correctly.

If you're following on from the [Installation](/setup/installation.md) guide,
you should now be able to open up
[http://127.0.0.1:8080](http://127.0.0.1:8080) and see your fully operational
LibCrowds instance.

To explore the and modify the LibCrowds settings, see
[Configuring LibCrowds](/setup/configuring-libcrowds.md).

!!! info
    You must access the website at http://127.0.0.1:8080, rather than
    http://localhost:8080, otherwise it will not be possible to track the user
    session cookie.