# Vue 2 + TypeScript + Vite + Vuetify

<p align="center">
  <img src="https://user-images.githubusercontent.com/480173/157433906-7f7910d4-6430-49f4-857a-044945e71360.png" alt="logo" width="300" height="300" />
</p>

This is a [starter project](https://github.com/logue/vite-vue2-ts-starter) that uses [Vuetify](https://vuetifyjs.com/) as the UI framework. Please use scss version 1.32.12 due to a problem on the Vuetify side.

Vuetify3 version is [here](https://github.com/logue/vite-vuetify-ts-starter).

## Description

This template is for using Vue2 with TypeScript in Vite. Includes [vue-router](https://router.vuejs.org/) and [Vuex](https://vuex.vuejs.org/), [vue-property-decorator](https://github.com/kaorun343/vue-property-decorator).

In addition, [ESLint](https://eslint.org/), [Stylelint](https://stylelint.io/), and [Prettier](https://prettier.io/) are also included and are set to be executed automatically at runtime and commit. (Since these settings are set strictly, please relax yourself.)

Also, when the development server is executed, it is checked in real time by [vite-plugin-checker](https://github.com/fi3ework/vite-plugin-checker).

### Composition API

It also supports the [Composition API](https://composition-api.vuejs.org/). The installed VueRouter and Vuex are for Vue2, but you can use the functions (such as `useRouter()`, `useRoute()` and `useStore()`) for the composition API for Vue3.

Of course, Vuetify instance can also be accessed with `useVuetify()`. In the Composition API, you can handle it in the same way as `this.$vuetify` by entering `const vuetify = useVuetify();` in the `setup()` function.

It is possible to mix code written in Composition API and code written in vue-property-decolator, but it is not recommended to use them together in the same component. [^1]

As a limitation, Vue2's composition api cannot monitor the router with the watch function. In that case, monitor it by the following normal method:

```js
watch: {
  $route: {
    handler(to) {
      //
    },
    immediate: true,
  },
},
```

If you are thinking of supporting Vue2 and Vue3 both, consider introducing [vue-demi](https://github.com/vueuse/vue-demi).

### Vue i18n

If you want to use [vue-i18n](https://kazupon.github.io/vue-i18n/), please install [vue-i18n-composable](https://github.com/intlify/vue-i18n-composable) and call the instance with `useI18n()`.

In addition, the conventional method using `$t()` written in non composition-api can be used as it is.

### Teleport

Vue3 adds a mechanism called [`Teleport`](https://v3.vuejs.org/guide/teleport.html), which allows you to install vue components anywhere. This starter template is for vue2, but you can do the same with [vue2-teleport](https://www.npmjs.com/package/vue2-teleport).

However, you will need to manually load the component with `import Teleport from 'vue2-teleport';` wherever you want to use it.

#### Teleport JSON-LD Example

If you want to include [JSON-LD](https://json-ld.org/), enter as follows.

```vue
<template>
  <div class="container">
    ... Some Content
    <teleport to="head">
      <component :is="'script'" type="application/ld+json" v-text="jsonLd" />
    </teleport>
  </div>
</template>

<script>
import { defineComponent } from '@vue/composition-api';

import Teleport from 'vue2-teleport';

export default defineComponent({
  components: {
    Teleport,
  },
  setup() {
    const jsonLd = ref(
      JSON.stringfy({
        '@schema': 'https://json.schemastore.org/jsonld.json',
        '@context': 'http://schema.org',
        '@type': 'WebSite',
        name: 'Vite Vue2 Vuetify TypeScript Startar',
        url: 'https://github.com/logue/vite-vue2-vuetify-ts-starter',
        description: 'Vite Vue2 Vuetify TypeScript Demo Page',
      })
    );

    return {
      jsonLd,
    };
  },
});
</script>
```

JSON-LD is literally a `script`, so it can't be embedded directly, so it's a roundabout thing like this, but simple things like `meta` tags are reflected by simply inserting a tag.

Notice: For Vue3, `:as="'script'"` becomes `is="script"`.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=vue.volar) (and disable Vetur).

## Commands

| Command       | Description                                        |
| ------------- | -------------------------------------------------- |
| dev           | Start devserver.                                   |
| clean         | Clear devserver cache.                             |
| lint          | Run ESLint and prettier.                           |
| lint:style    | Run Stylelint.                                     |
| lint:markup   | Check vue markup.                                  |
| build         | Build for production.                              |
| build:analyze | Execute Bundle Analyzer                            |
| build:deploy  | Build for production without checking.             |
| build:clean   | Clear production build files.                      |
| preview       | Run the program generated by the production build. |

## Migrate from VueCli

It also works when migrating from VueCLI.

However, when importing a stylesheet with `@import`, it cannot be specified from the library directory. Must be specified from `~node_modules/`.

Also, if you used the .env file in the previous environment, you need to change the calling part from `process.env` to `import.meta.env` after installing [vite-plugin-env-compatible](https://github.com/IndexXuan/vite-plugin-env-compatible) separately.

## Troubleshooting

When adding or deleting files, an error may occur and even if the error is corrected, it may not be reflected in devserver. In that case, stop devserver and delete all the files in the `node_modules/.vite` directory. You can also run it with the `clean` command.

Due to [yarn issues](https://github.com/yarnpkg/berry/issues/4448), it may not work properly if the path contains non-ASCII characters (such as 日本語 or 한국어, 中文 etc.).

[^1]: <https://github.com/vuejs/composition-api/issues/136>
