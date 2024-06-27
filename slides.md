---
theme: wordman
class: text-center
highlighter: shiki
lineNumbers: false
info: |

drawings:
  presenterOnly: true
defaults:
  layout: default
title: "Enhancing Code Quality and Velocity with ESLint: A Practical Approach"
monaco: false
layout: cover
mdc: true
transition: slide-left
favicon: ./favicon.png
---

<div class="flex items-center justify-center h-full w-full flex-col text-shadow text-white">
    <h1 class="text-8xl! text-shadow text-shadow-lg">Enhancing Code Quality and Velocity with ESLint</h1>
    <h2 class="text-6xl! text-shadow text-shadow-lg">A Practical Approach </h2>
</div>

---
layout: two-cols
---

![Driveway of a very fancy looking hourse](/airbnb-kc.png)

::right::
<div class="flex items-center justify-center" style="background: #1c2939; height: 436px;margin-top: 15px;">
    <img src="/eslint-homepage.png" alt="Screenshot of the eslint homepage" />
</div>

---
layout: image
image: /airbnb.png
---

---
layout: image
image: /airbnb.io_javascript_.png
---

---
layout: image
image: /eslint-npm.png
---

<span class="absolute" style="width: 300px; height: 60px; top: 370px; right: 35px;" v-mark.circle.red> </span>

---
layout: introduction
---

---
layout: image
image: /kcdc24_sponsorslide.jpeg
---

---
transition: view-transitition
---

<h1 class="text-8xl"> What is EsLint </h1>

<div class="flex items-center text-2xl" style="height: 75%; padding-left: 300px">
    <span style="view-transition-name: 'linter'">Static Code Analysis for &nbsp;</span>
    <v-switch childTag="span" tag="span">
        <template #0> JavaScript </template>
        <template #1> TypeScript </template>
        <template #2> React </template>
        <template #3> Vue </template>
        <template #4> Angular </template>
        <template #5> NodeJS </template>
    </v-switch>
</div>

---
transition: view-transitition
---

<h1 class="text-8xl"> What is EsLint </h1>

<div class="flex items-center text-2xl" style="height: 75%; padding-left: 300px">
    <span style="view-transition-name: 'linter'">Fix Code for &nbsp;</span>
    <v-switch childTag="span" tag="span">
        <template #0> JavaScript  </template>
    </v-switch>
</div>

---
transition: view-transitition
---

<h1 class="text-8xl"> What is EsLint </h1>

<div class="flex items-center text-2xl" style="height: 75%; padding-left: 300px">
    <span style="view-transition-name: 'linter'">Formatter for &nbsp;</span>
    <v-switch childTag="span" tag="span">
        <template #0> JavaScript </template>
    </v-switch>
</div>


---
---

# Why

<ul>
    <li style="padding: 1em 0">Reusable</li>
    <li style="padding: 1em 0">Extensible</li>
    <li style="padding: 1em 0">Consistency</li>
    <li style="padding: 1em 0">Catches Bugs Early</li>
</ul>

---
layout: center
---

<h1>Bug Cost Curve</h1>

<img src="/bug-cost-curve.png" class="m-a" style="width: 70%">

<span class="float-right"> * Source: "Trust me, bro" </span>




---
---

# Community and Ecosystem

<div class="flex items-center justify-center w-full h-90">
    <span class="text-2xl">more than <span class="text-5xl">40.000</span> Packages </span>
</div>

---
---

# Community and Ecosystem

<span class="text-4xl text-red">Your Library could Go Here</span>

---
layout: center
transition: view-transition
---

<h1 style="view-tranistion-name: 'eslint-version'"> ESLint v9.0.0 is out 🎉 </h1>

---
layout: center
transition: view-transition
---

<h1 style="view-tranistion-name: eslint-version"> ESLint v9.5.0 is out 🎉 </h1>

---
transition: view-transition
preload: false
---

[//]: # (fix transition)
<h1 style="view-tranistion-name: eslint-version"> ESLint v9.5.0 is out 🎉 </h1>

<ul v-motion v-motion-slide-top>
    <li>Externalize Formatter</li>
    <li>Flat Config</li>
</ul>


---
---

# Formatter - The Problem
<div class="flex full-w items-center justify-center h-90">
    <span class="text-4xl"> ESLint !== Prettier</span> 
</div>

---
---

# Formatter - The Solution

<a href='https://eslint.style/'>
    <img src="/eslint-stylistic.png">
</a>
---
---

# ESLint - Flat Config - The Problems

````md magic-move
```json
{
  "extends": ["eslint:recommended"],
}
```

```json
{
  "extends": ["eslint:recommended"],
  "rules": {
    "semi": "warn"
  }
}
```

```yml
---
extends:
- eslint:recommended
rules:
  semi: warn
```

```js
export default [
    {
        "extends": ["eslint:recommended"],
        "rules": {
            "semi": "warn"
        }
    }
];
```

```json
{
  "extends": ["eslint:recommended"],
  "root": true,
  "rules": {
    "semi": "warn"
  }
}
```

```json
{
  "extends": ["eslint:recommended"],
  "root": true,
  "rules": {
    "semi": "warn"
  },
  "overrides": [{
     "files": ["bin/*.js", "lib/*.js"],
     "excludedFiles": "*.test.js",
     "rules": {
       "quotes": ["error", "single"]
     }
  }]
}
```

```json
{
  "root": true,
  "rules": {
    "semi": "warn"
  },
  "overrides": [{
     "files": ["bin/*.js", "lib/*.js"],
     "excludedFiles": "*.test.js",
     "extends": ["eslint:recommended"],
     "rules": {
       "quotes": ["error", "single"]
     }
  }]
}
```
````

---
---

# ESLint - Flat Config - The Solution

````md magic-move

```js
export default [
    {
        files: ["**/*.js"],
        ignores: ["**/*.test.js"],
        rules: {
            "semi": "error",
            "no-unused-vars": "error"
        }  
    }
];
```

```js{*|5,13}
export default [
    {
        files: ["**/*.js", "**/*.cjs"],
        rules: {
            "semi": "error",
            "no-unused-vars": "error"
        }  
    },
    {
        files: ["**/*.js"],
        rules: {
            "no-undef": "error",
            "semi": "warn"
        }  
    }
];
```

```js
import customConfig from "eslint-config-custom";

export default [
    customConfig,
    {
        files: ["**/*.js", "**/*.cjs"],
        rules: {
            "semi": "error",
            "no-unused-vars": "error"
        }  
    },
    {
        files: ["**/*.js"],
        rules: {
            "no-undef": "error",
            "semi": "warn"
        }  
    }
];
```
````

---
layout: center
---

# Things to Cover!

---
---

# Codestyle Linting Rules

<ul>
    <li>Spacing</li>
    <li>Types</li>
    <li>Syntax</li>
</ul>

---
---

# Feature Linting Rules

<ul>
    <li>Libraries & Frameworks</li>
    <li>Typeaware Rules</li>
    <li>Potential Bugs</li>
</ul>

---
layout: center
---

<img src="/eslint-meme.png" class="w-100">

---
---

# The Worst ESLint Rules

1. [Prefer default exports](https://github.com/import-js/eslint-plugin-import/blob/main/docs/rules/prefer-default-export.md)
2. [No plus plus](https://eslint.org/docs/latest/rules/no-plusplus.html)
3. [Ban TS Comment](https://typescript-eslint.io/rules/ban-ts-comment)

---
transition: view-transition
---

# The Best ESLint Rules

1. no-restricted-syntax

---
transition: view-transition
---

# The Best ESLint Rules

1. no-restricted-syntax

```json
{
  "rules": {
    "no-restricted-syntax": [
      "error",
      {
        "selector": "TSEnumDeclaration",
        "message": "Enums were a mistake in the first place! Thanks for coming to my TED talk."
      }
    ]
  }
}
```

---
---

# Anthony Fu Config

````md magic-move
```sh
pnpm i -D eslint @antfu/eslint-config
```
```js
import antfu from '@antfu/eslint-config'

export default antfu({
  // Enable stylistic formatting rules
  // stylistic: true,

  // Or customize the stylistic rules
  stylistic: {
    indent: 2, // 4, or 'tab'
    quotes: 'single', // or 'double'
  },

  // TypeScript and Vue are auto-detected, you can also explicitly enable them:
  typescript: true,
  vue: true,

  // Disable jsonc and yaml support
  jsonc: false,
  yaml: false,

  // `.eslintignore` is no longer supported in Flat config, use `ignores` instead
  ignores: [
    '**/fixtures',
    // ...globs
  ]
})
```
```ts
export function antfu(
  options: OptionsConfig & TypedFlatConfigItem = {},
  ...userConfigs: SomeComplexTypeThatWasTooLongForThisSlide
): FlatConfigComposer<TypedFlatConfigItem, ConfigNames> {
  const {
    astro: enableAstro = false,
    autoRenamePlugins = true,
    componentExts = [],
    gitignore: enableGitignore = true,
    isInEditor = !!(process.env.JETBRAINS_IDE && !process.env.CI),
    jsx: enableJsx = true,
    react: enableReact = false,
    regexp: enableRegexp = true,
    solid: enableSolid = false,
    svelte: enableSvelte = false,
    typescript: enableTypeScript = isPackageExists('typescript'),
    unocss: enableUnoCSS = false,
    vue: enableVue = VuePackages.some(i => isPackageExists(i)),
  } = options
  ...
}
```
````

---
---

# Nuxt EsLint Config

---
---

# Qodana

---
layout: outro
url: https://wordman.dev/talk/2024/eslint-kcdc
---
