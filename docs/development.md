# Development

LibCrowds is fundamentally a Vue.js Server-Side Rendered (SSR) UI that
communicates with a [PYBOSSA](https://github.com/Scifabric/pybossa) backend.

## Installation

Install [Node.js >=8.0.0](https://nodejs.org/en/), then:

``` bash
# install dependencies
npm install
```

You will also need to install an instance of
[PYBOSSA](http://docs.pybossa.com/).

## Configuration

See the [Configuration](/configuration/index.md) section for full details of how
to setup LibCrowds and PYBOSSA.

## Building

``` bash
# build for production with minification
npm run build

# run in production
npm start

# serve for development with hot reload at 127.0.0.1:8080
npm run dev
```

!!! warning
    You must access the website at http://127.0.0.1:8080, rather than
    http://localhost:8080, otherwise it will not be possible to track the user
    session cookie.
