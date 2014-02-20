*This repository is a mirror of the [component](http://component.io) module [ramitos/match-route](http://github.com/ramitos/match-route). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/ramitos-match-route`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*
# match-route

Match a request against a object of routes

## installation

#### [component/component](https://github.com/component/component)

```bash
$ component install [--dev] ramitos/match-route
```

#### npm

```bash
$ npm install [--save/--save-dev] match-route
```

## example

```js
var mr = require('match-route'),
    assert = require('assert');

mr({
  method: 'PUT',
  url: '/user/admin?q1=3&q2=t'
}, {
  'get': {
    '/user/:id/age': 'some string',
    '/': true
  },
  'post': {
    '/user/:id/:age': 45
  },
  'put': {
    '/:type/:subtype': 'other string'
  },
  'delete': {
    '/user/:id': false
  }
}, function (value, route, params, query) {
  assert(route === '/:type/:subtype');
  assert(params.subtype === 'admin');
  assert(value === 'other string');
  assert(params.type === 'user');
  assert(query.q1 === '3');
  assert(query.q2 === 't');
});
```

## license

MIT