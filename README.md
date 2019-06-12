

# svelte-materialize-posts

This proyect is based on the youtube tutorial from @hidjou.

To implement MaterializeCSS in an Svelte3 project, we need to install __rollup-plugin-css-only__ to inject new CSS code coming from another libraries.

On _rollup.config.js_ file we need to include:

```js
plugins: [
    //.....
    css({output: 'public/extra.css'}),
    //.....
    ],
```
An then in the _App.svelte_ file:

```js
import "../node_modules/materialize-css/dist/css/materialize.min.css";
import "../node_modules/materialize-css/dist/js/materialize.min.js";
```
## Get started

Clone the repo

```bash
cd svelte-materialize-posts
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running.

## Deploying to the web

### With [now](https://zeit.co/now)

Install `now` if you haven't already:

```bash
npm install -g now
```

Then, from within your project folder:

```bash
now
```

As an alternative, use the [Now desktop client](https://zeit.co/download) and simply drag the unzipped project folder to the taskbar icon.

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public
```
