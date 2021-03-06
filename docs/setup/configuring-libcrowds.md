This page details all of the core LibCrowds settings. To edit them you can
begin by copying the settings template:

```bash
cd /path/to/libcrowds
cp local.config.js.tmpl local.config.js
```

## Required Settings

The following settings are all required for the application to run correctly.
They are given defaults in the settings template but should be edited
accordingly.

### annotations

A server that complies with the
[Web Annotation Protocol](https://www.w3.org/TR/annotation-protocol) is
required to handle the storage and retrieval of user tags and results data.

LibCrowds has been built for use with the
[Explicates](https://github.com/alexandermendes/explicates) server, which
complies with the standard protocol and has the additional search
functionality required for this application.

The [Setup](/setup/introduction) section contains details on setting up an
Annotation server, the base URL of which should then be added to the local
settings file, as below.

```js
config.explicates = {
  baseURL: 'http://127.0.0.1:3000'
}
```

### brand

The name of the platform.

```js
config.brand = 'My Brand'
```

### company

The company responsible for the platform.

```js
config.company = 'My Company'
```

### description

An SEO optimised description of the platform.

```js
config.description: 'My SEO optimised meta description'
```

### libcrowdsHost

The host where this application will be deployed

```js
config.libcrowdsHost: 'http://127.0.0.1:8080'
```

### pybossaHost

The host for all PYBOSSA API calls.

```js
config.pybossaHost: 'http://127.0.0.1:5000'
```

### tagline

Some inspiring tagline.

```js
config.tagline: 'My inspiring tagline'
```

## Optional Settings

The following can be added to the configuration file to enable additional
functionality.

### analytics

Add [Google Analytics](https://analytics.google.com) to the platform by
providing your tracking ID.

```js
config.analytics = {
  ua: 'UA-XXX-X'
}
```

This will enable
[event tracking](https://developers.google.com/analytics/devguides/collection/analyticsjs/events)
for the following events:

| Category        | Action          | Label                                    | Description                 |
|-----------------|-----------------|------------------------------------------|-----------------------------|
| Downloads       | {type}_{format} | Project name or AnnotationCollection IRI | Data file is downloaded     |
| Statistics      | view            | Project name                             | Project statistics viewed   |
| Contributions   | {project name}  | Collection name                          | Answer submitted            |
| Filters         | {filter value}  | Collection name                          | Main projects list filtered |
| Project Toolbar | {name}_shown    | Collection name                          | Project modal shown         |


Tracking these events can help to determine the content that your users are most
interested in. For example, monitoring the filters most used for a microsite can
help determine the types of project that should be prioritised for release at
a given time.

[Social interactions](https://developers.google.com/analytics/devguides/collection/analyticsjs/social-interactions)
will be tracked using the social media 'Share' buttons present on the site.
However, note that this reports button clicks and does not guarantee that the
user actually then went ahead and shared the page.

User IDs are used to track all registered and authenticated users.

### docs

Provide a URL to the platform's documentation that will be linked to from the
main footer and all admin dashboard pages.

```js
config.docs: 'http://docs.libcrowds.com'
```

If you want to use your own documentation site, please include the page
structure found in the original documentation's
[mkdocs.yml](https://github.com/LibCrowds/docs/blob/master/mkdocs.yml) file.
This is beacuse many of these paths are linked to from specific LibCrowds
admin pages.

### email

Add a contact email address to the main footer.

```js
config.email = 'me@example.com'
```

### facebook

Add a [Facebook app ID](https://developers.facebook.com/docs/apps/register) to
enable [Open Graph](https://developers.facebook.com/docs/sharing/opengraph)
integration.

```js
config.facebook = {
  appId: '1234567890'
}
```

### flarum

Enable [Flarum](http://flarum.org/) integration by adding the base `url` of
the forum, a master `apiKey`, the `sessionCookieDomain` and a random string as
the `salt` that is used to encrypt passwords.

The [flarum-ext-sso](https://github.com/fabwu/flarum-ext-sso) extension will
also need to be installed for your Flarum instance and the API key created
during this installation process should be used in the configuration
below.

```js
config.flarum = {
  url: 'http://community.example.com',
  sessionCookieDomain: '.example.com',
  apiKey: 'XXX-XXX-XXX',
  salt: 'super-secret-string',
  disableEmailConfirmation: true
}
```

Adding these settings will enable SSO and add the ability to link each
collection microsite to a particular forum topic.

!!! warning

    Beware that if SSO is enabled, then disabled, user's will not be able to
    access their forum accounts without resetting their passwords.


### footer

Add an additional list menu to the main footer.

```js
config.footer = {
  title: 'Newsletter',
  items: [
    { text: 'Sign up', url: 'http://mailchimp.signup.url' }
  ]
}
```

### github

Add a GitHub link to the main footer.

```js
config.githubUrl = 'https://github.com/github'
```

### https

Force HTTPS for all external requests.

```js
config.https = true
```

### sentry

Enable [Sentry](https://sentry.io/) error tracking.

```js
config.sentry = {
  public_key: '',
  private_key: '',
  project_id: ''
}
```

### social

A list of [social profile](https://developers.google.com/search/docs/data-types/social-profile)
links to add to the site's structured metadata.

```js
config.social = [
  'http://www.facebook.com/your-profile',
  'http://instagram.com/yourProfile',
  'http://www.linkedin.com/in/yourprofile',
  'http://plus.google.com/your_profile'
]
```

### twitter

Adds a twitter link to the main footer and enhances the platforms Twitter cards
with `twitter:site` meta tag.

```js
config.twitter = 'mytwitterhandle'
```

### disableProjectBuilder

Disable project building functions for non-admin users.

```js
config.disableProjectBuilder = true
```
