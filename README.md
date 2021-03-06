# catbox-mongodb

MongoDB adapter for [catbox](https://github.com/hapijs/catbox)

Note: the module has been deprecated and archived due to low usage. The last publish version is known it work well but that may change in the future as breaking changes of catbox are introduced. If you rely on this module, consider forking it and creating your own alternative (it is very little code). You can also ask to take over and the module will be moved to your personal account to maintain.

**catbox-mongodb** serializes values to BSON using MongoDB driver, therefore following data types are supported for this adapter: Object, Array, Number, String, Date, RegExp.


## Installation
> The lastest `catbox-mongodb` version `4.x` works only with **hapi v17 and v18**

Install `catbox-mongodb` via NPM. Remember that `catbox-mongodb` requires its parent module [`catbox`](https://github.com/hapijs/catbox):

```
npm install catbox catbox-mongodb
```

---

Do you use **hapi v16 or lower**? Install `catbox-mongodb` version `3.x` with a compatible version of `catbox`:

```
# for hapi v16 (or lower)
npm install catbox@9 catbox-mongodb@3
```


## Options
`catbox-mongodb` accepts the following options:

- `uri` - the [MongoDB URI](https://docs.mongodb.com/manual/reference/connection-string/), defaults to `'mongodb://127.0.0.1:27017/?maxPoolSize=5'`
- `partition` - the MongoDB database for cached items


## Usage
Sample catbox cache initialization :

```JS
const Catbox = require('catbox');

const cache = new Catbox.Client(require('catbox-mongodb'), {
    uri: 'your-mongodb-uri', // Defaults to 'mongodb://127.0.0.1:27017/?maxPoolSize=5'
    partition: 'cache-users'
})
```

Or configure your hapi server to use `catbox-mongodb` as the caching strategy (code snippet uses hapi `v17`):

```js
const Hapi = require('hapi')

const server = new Hapi.Server({
    cache : [{
        name: 'mongodb-cache',
        engine: require('catbox-mongodb'),
        uri: 'your-mongodb-uri', // Defaults to 'mongodb://127.0.0.1:27017/?maxPoolSize=5'
        partition: 'cache-posts'
    }]
});
```

For hapi `v18` you need a slightly different config:

```js
const Hapi = require('hapi')
 
const server = new Hapi.Server({
    cache : [{
        name: 'mongodb-cache',
        provider: {
          constructor: require('catbox-mongodb'),
          options: {
            uri       : 'your-mongodb-uri', // Defaults to 'mongodb://127.0.0.1:27017/?maxPoolSize=5'
            partition : 'cache'
          }
        }
    }]
});
```
