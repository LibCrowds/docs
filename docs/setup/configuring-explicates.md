This page details the core settings for the Explicates Web Annotation server.
To edit them you can begin by copying the settings template:

```bash
cd /path/to/libcrowds
cp local.config.js.tmpl local.config.js
```

## Required settings

The settings below are required for the application to run correctly.

```python
# ** IMPORTANT: Uncomment the lines below in production **
ENV = 'production'
SERVER_NAME = 'annotations.example.com'

# CORS settings (defaults below)
# See https://flask-cors.readthedocs.io/en/latest/
CORS_RESOURCES = {
    r"/*": {
        "origins": "*",
        "allow_headers": [
            'Content-Type',
            'Content-Length',
            'Authorization',
            'If-Match',
            'Prefer',
            'Accept',
            'Slug'
        ],
        "max_age": 21600,
        "supports_credentials": True
    }
}
```

!!! tip
    See the Explicates settings template for details of all optional settings.
