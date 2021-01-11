---

# partygamepicker [![Netlify Status](https://api.netlify.com/api/v1/badges/9e8ace6d-3a5d-4fb3-807f-34a612da37fd/deploy-status)](https://app.netlify.com/sites/partygamepicker/deploys) [![Node.js CI](https://github.com/hiddenroles/partygamepicker/workflows/Node.js%20CI/badge.svg?branch=main)](https://github.com/hiddenroles/partygamepicker/actions?query=workflow%3A%22Node.js+CI%22)



`partygamepicker` is a simple project for picking a party game out of the many available.
It is part of the broader [Hidden Roles project](https://hiddenroles.com).

The project could likely do with more options, so feel free to submit a pull request or an issue if you got ideas. See below for some rough inclusion criteria.

## Inclusion criteria

This is a simple idea for what's suitable for this list:
- Suited for casual play (e.g. not Diplomacy)
- Easy to learn (e.g. not Diplomacy)
- Good for a group of people, preferably 4 or more (6+ is even better)
- Easy to set up (e.g. doesn't need a server a-la CS:GO)
- Stable & working

## Development

This is my first [Svelte](https://svelte.dev) so it likely is terrible and breaks all sort of conventions. Apologies for that!
However, I have to say so far I like this Svelte business.


### Run locally

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). Any changes should be hot-reloaded.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

### Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).
