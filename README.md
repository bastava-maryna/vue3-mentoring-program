# vue3-mentoring-program

## Project Setup with Vite

```sh
npm init vite@latest
cd <project-name>
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Storybook

```sh
npx storybook@latest init
npm run storybook
```

1. Additionally install eslint-plugin-storybook

```sh
npm install --save-dev eslint-plugin-storybook
```

Inside .eslintignore file add
`!.storybook`
Add plugin:storybook/recommended to the extends section of .eslintrc configuration file
`"extends": ["plugin:storybook/recommended"]`

### ESLint

```sh
npm install --save-dev eslint eslint-plugin-vue @vue/eslint-config-typescript @rushstack/eslint-patch
```

`eslint-plugin-vue` is an official ESLint plugin for vue.

`@rushstack/eslint-patch` in order to work around a known limitation in ESLint.

1. Create a `.eslintrc.js` file in your projects root directory
2. Add at the beginning of file:
   `require("@rushstack/eslint-patch/modern-module-resolution")`
3. Add required configuration options.
4. Add script in package.json:
   `"lint": "eslint . --ext .vue,.js,.jsx,.cjs,.mjs,.ts,.tsx,.cts,.mts --fix --ignore-path .gitignore"`
5. Configure ESLint in WebStorm to use its code hint:
   `Settings > Languages & Frameworks > JavaScript > Code Quality Tools > ESLint` (using Automatic ESLint configuration or Manual ESLint configuration).

### Prettier

```sh
npm install --save-dev eslint-config-prettier prettier
```

`eslint-config-prettier` to turn off all rules that are unnecessary or might conflict with Prettier.

1. Make modifications to .eslintrc.js:
   make sure to put `"prettier"` last to `"extends"` section, so it gets the chance to override other configs.
2. Create a `.prettierrc.js` file and add rules to override the defaults 3. Add script in package.json:
   `"format": "prettier .  --write"`
3. Configure Prettier in WebStorm to use its format function:
   `Settings > Languages & Frameworks > JavaScript > Prettier` (using Automatic ESLint configuration or Manual ESLint configuration).
   It is recommended to check an item `Run on save` for files in the settings page, so that the code can be automatically formatted through Prettier when Command + S.
   If not check the above configuration, you need to format the code through Command + Option + Shift + P.

### Tailwindcss

Install tailwindcss and its peer dependencies, then generate your tailwind.config.js and postcss.config.js files.

```sh
npm install --save-dev tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

1. Add the paths to all of your template files in your tailwind.config.js file.
   `/** @type {import('tailwindcss').Config} */
   export default {
   content: [
   "./index.html",
   "./src/**/*.{vue,js,ts,jsx,tsx}",
   ],
   theme: {
   extend: {},
   },
   plugins: [],
   }`
2. Add the @tailwind directives for each of Tailwind’s layers to ./src/style.css file.
   `@tailwind base;
 @tailwind components;
 @tailwind utilities;`
3. Delete `import "./assets/main.css"` from ./src/main.ts and add `import "./assets/tailwind.scc"`
4. Instead @storybook/addon-postcss install @storybook/addon-styling(although it also depreceted)

```sh
npm install -save-dev @storybook/addon-styling
```

Add in .storybook/main.ts
`{ 
   name: "@storybook/addon-styling", 
   options: {
     postCss: true,
    },
},`

with storybook/postcss it was:
`   {
name: '@storybook/addon-postcss',
options: {
cssLoaderOptions: {
importLoaders: 1,
},
postcssLoaderOptions: {
implementation: require('postcss'),
},
},
},` 5. Add storybook-addon-vue-slots to enable using Vue slots inside Storybook's CSF files.

```sh
nmp install --save-dev storybook-addon-vue-slots
```

Add the storybook-addon-vue-slots to your plugins in storybook/main.ts file
`export default {
// ...
addons: [
// ...
"storybook-addon-vue-slots",
],
} satisfies StorybookConfig`

### vite-plugin-svg4vue

This plugin can transform SVG icon to vue component.

```sh
npm install --save-dev vite-plugin-svg4vue
```

1. Add to vite.config.mts
   `import { svg4VuePlugin } from 'vite-plugin-svg4vue'
export default defineConfig({
plugins: [
vue(),
svg4VuePlugin(),
],
})`
2. If you are using TypeScript, vite-plugin-svg4vue/client can be added to d.ts declaration file.
   `<reference types="vite-plugin-svg4vue/client" />`
3. controls:
   font-size, fill, stroke, width

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```
