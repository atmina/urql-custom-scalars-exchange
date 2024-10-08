# @atmina/urql-custom-scalars-exchange

urql exchange to allow mapping of custom scalar types

## Example

```sh
yarn add @atmina/urql-custom-scalars-exchange
```

or

```
npm install --save @atmina/urql-custom-scalars-exchange
```

Define a custom scalar like `Json` in your schema via:

```gql
scalar Json
```

Download the introspection query from your endpoint. See the [urql docs](https://formidable.com/open-source/urql/docs/graphcache/schema-awareness/#getting-your-schema) for a script to download the schema from your endpoint.

Configure the exchange like so

```js
import customScalarsExchange from '@atmina/urql-custom-scalars-exchange';
import schema from '../schema.json';

const scalarsExchange = customScalarsExchange({
    schema: schema,
    scalars: {
        Json(value) {
            return JSON.parse(value);
        },
    },
});
```

Finally add the exchange to your urql client like so

```js
const client = createClient({
    url: 'http://localhost:1234/graphql',
    exchanges: [dedupExchange, scalarsExchange, fetchExchange],
});
```

## FAQ

### Should this exchange be listed before or after the cache exchange?

This exchange should be listed before any cache exchange. Cache exchanges
should represent the the data as returned by the endpoint.

## Local Development

This project uses [Corepack](https://nodejs.org/api/corepack.html). Run `corepack enable` to enable it if you haven't already.

Below is a list of commands you will probably find useful.

### `npm start` or `yarn start`

Runs the project in development/watch mode. Your project will be rebuilt upon
changes. TSDX has a special logger for you convenience. Error messages are
pretty printed and formatted for compatibility VS Code's Problems tab.

Your library will be rebuilt if you make edits.

### `npm run build` or `yarn build`

Bundles the package to the `dist` folder. The package is optimized and bundled
with Rollup into multiple formats (CommonJS, UMD, and ES Module).

### `npm test` or `yarn test`

Runs the test watcher (Jest) in an interactive mode. By default, runs tests
related to files changed since the last commit.

## Acknowledgements

This project was bootstrapped with [TSDX](https://github.com/jaredpalmer/tsdx).

This project is a fork of [Christian Lentfort's exchange](https://github.com/clentfort/urql-custom-scalars-exchange).
