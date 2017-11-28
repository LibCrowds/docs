Tests are written using [Jest](https://facebook.github.io/jest/) and run each
time a commit is pushed using [Travis CI](https://travis-ci.org/). Run the tests
with the following commands:

``` bash
# build (required for testing with nuxt components)
npm run build

# run lint
npm lint

# run unit tests
npm unit

# run all tests
npm test
```
