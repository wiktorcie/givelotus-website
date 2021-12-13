# GiveLotus.org made with Vue, NuxtJS and Vuetify

Pushes to master will deploy to https://givelotus.netlify.app/

Features:

- seo optimized (100% at google lighthouse)
- dark mode
- internationalization with nuxt-i18n
- SSR, SPA and UWA modes (https://recurse.me/posts/choosing-a-nuxt-mode.html)
- responsive

## Installation (tested on node >14)

```
yarn
```

## Run Development

```
yarn dev
```

## Build for CDN (SSR)

```
yarn generate
```

##  SPA/UWA

In nuxt.config.js add line:

```
mode: "universal"
```

or

```
mode: "spa"
```

and remove:

```
target: 'static',
```

then

```
yarn start
```

Credits:

built with amazing awrora-starter https://github.com/ilhammeidi/awrora-starter
