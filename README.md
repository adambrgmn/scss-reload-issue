# Hugo Sass reload issue

With the config setup in this repo updates to the scss stylesheet will not propagate to the front end. Only a hard refresh will update the styles.

## Reproduce

- Clone this repo
- Make sure you have Hugo installed (in my case `Hugo Static Site Generator v0.62.2/extended darwin/amd64 BuildDate: unknown`)
- Run `hugo serve`

The reason (at least the way I understand it) the styles are not updated is because of this line `staticDir = ["static", "assets"]` in [`config.toml`](./config.toml).

If I remove that line (or change it to the default `["static"]`) the issue is resolved.

## Why `assets` as a static directory as well?

Good question! I wanted to write my new site with modern vanilla javascript and skip the bundling step (I want to keep webpack configs and dependencies to a minimum). And at the same time use `main.js` as an entrypoint with Hugo.

That way I can `import { capitalize } from './js/utils.js` and it will work as expected in modern browsers.

I could place `utils.js` in a the `/static` folder. But then I loose the "physical" connection between `main.js` and `utils.js`. Which I would like to keep.
