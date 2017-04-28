# cerebral-app-cache

## Install

```bash
npm install cerebral-app-cache
```


## API

```bash
var cerebralCache = require('cerebral-app-cache');
```


## .setup

```bash
setup: [
  set(props`token`, state`app.token`),
  set(props`domain`, state`app.model.domain`),
  oadaSetup,      //Calls oadaCache.setup
  cerebralSetup,  //Setup the state tree recursively
],

function oadaSetup({props, state}) {
  return oadaCache.setup(props.domain, props.token, tree);
};

function cerebralSetup({props, state}) {
  return recursiveSetup(domain, tree, keysArray, {state});
}
```


## .get

```bash
get: [
  set(props`token`, state`app.token`),
  set(props`domain`, state`app.model.domain`),
  createUrl,
  oadaGet, {
    success: [setAvailableData],
    error: [],
  },
]
```


## .put

```bash
put: [
  set(props`token`, state`app.token`),
  set(props`domain`, state`app.model.domain`),
  createBookmarksUrl,
  getPathFromUrl,
  prepareBookmarksUrl,
  oadaPut, {
    success: [
      set(state`${props`statePath`}.sync_status`, 'synced'),
    ],
    error: [
      set(state`${props`statePath`}.sync_status`, 'failed'),
    ],
  },
]
```


## .post

```bash
post: [
  generateNewId,
  set(props`token`, state`app.token`),
  set(props`domain`, state`app.model.domain`),
  createBookmarksUrl,
  getPathFromUrl,
  oadaPut, {
    success: [
      set(state`${props`statePath`}`, props`content`),
      set(state`${props`statePath`}.sync_status`, 'synced'),
    ],
    error: [],  //keep status 'new'
  },
],
```

