# Frontend Mentor - Product preview card component solution

This is a solution to the [Product preview card component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/product-preview-card-component-GO7UmttRfa). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

To run this project, use the following commands in the terminal or command prompt:

```bash
npm install
npm start
```

## Table of contents

- [Frontend Mentor - Product preview card component solution](#frontend-mentor---product-preview-card-component-solution)
  - [Table of contents](#table-of-contents)
  - [Overview](#overview)
    - [The challenge](#the-challenge)
    - [Links](#links)
  - [My process](#my-process)
    - [Built with](#built-with)
    - [HTML Implementations](#html-implementations)
      - [🔵 Embed `svg` directly into HTML](#-embed-svg-directly-into-html)
    - [Sass Implementations](#sass-implementations)
      - [🟢 Setup Sass project](#-setup-sass-project)
      - [🟢 Sass folder and file structure](#-sass-folder-and-file-structure)
      - [🟢 Implementing `rem` using Sass _function_](#-implementing-rem-using-sass-function)
      - [🟢 Implementing responsive layout media queries using _Mixin_](#-implementing-responsive-layout-media-queries-using-mixin)
    - [Useful Resources](#useful-resources)
  - [Author](#author)

**Note: Delete this note and update the table of contents based on what sections you keep.**

## Overview

### The challenge

Users should be able to:

- View the optimal layout depending on their device's screen size
- See hover and focus states for interactive elements

### Links

- Live Site URL: [Add live site URL here](https://your-live-site-url.com)

## My process

### Built with

- Semantic HTML5 markup
- SASS (SCSS) with BEM
- Flexbox
- Mobile-first workflow

### HTML Implementations

Using HTML structures from Grace Snow's Product Preview Page [^1].

#### 🔵 Embed `svg` directly into HTML

Embed `svg` code (_icon-cart.svg_ content) directly into HTML, so its `fill` color can be adjusted based on the button variants [^2].

Hide the `svg` with `aria-hidden = "true"` as it is a presentational icon [^3].

```html
<button class="btn btn--primary">
  <svg
    aria-hidden="true"
    width="15"
    height="16"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path ... />
  </svg>
  <span>Add to Cart</span>
</button>
```
> [!NOTE]
> This implementation is actually not necessary, but I just want to make some test with Sass.

### Sass Implementations

If you don't know about Sass, it is a stylesheet programming language made specific for CSS. It can do a lot more than normal CSS. More operations on variables, nesting selectors, create functions, etc. Read more [introduction to Sass](https://sass-lang.com/guide/).

#### 🟢 Setup Sass project

Sass is installed in the project using NPM, so you need to [install Node](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) first if you haven't done so.

In the root project folder, execute `npm init` to create Node configuration file (read more [beginner guide to using NPM](https://nodesource.com/blog/an-absolute-beginners-guide-to-using-npm)). This will create _package.json_ file in the root folder.

Add these list of packages to the project using NPM. Install it as dev dependencies using `npm install --save-dev [package-name]`:

- **sass**: Sass package.
- [**browser-sync**](https://www.npmjs.com/package/browser-sync): To serve the html in your local machine, similar to [Live Server VSCode Extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer).
- [**cpx2**](https://www.npmjs.com/package/cpx2): To copy html and image files.
- **npm-run-all**: Execute NPM script in parallel.
- [**postcss-cli**](https://www.npmjs.com/package/postcss-cli): Process CSS after build process.
- **autoprefixer**: Automatically add browser prefixes to CSS properties (_postcss_ plugin).
- **cssnano**: Compress CSS (_postcss_ plugin).

> [!NOTE]
> You can install them one by one, or install them all at once by listing all the package names separated by spaces. Example: `npm install --save-dev package1 package2 package3`.

Once installed, there will be this code in the _package.json_ file.

```json
...
"devDependencies": {
  "autoprefixer": "^10.4.21",
  "browser-sync": "^3.0.3",
  "cpx2": "^8.0.0",
  "cssnano": "^7.0.6",
  "npm-run-all": "^4.1.5",
  "postcss-cli": "^11.0.1",
  "sass": "^1.85.1"
}
```

Add these _NPM scripts_ code in the _package.json_ file:

```json
...
"scripts": {
  "watch:sass": "sass --watch src/scss:src --source-map-urls=relative",
  "build:sass": "sass src/scss:public --no-source-map",
  "copy": "cpx \"src/**/*.{html,jpg,png,svg}\" public",
  "serve": "browser-sync start --server src --files src",
  "postbuild": "postcss public/*.css -u autoprefixer cssnano -r --no-map",
  "start": "npm-run-all --parallel watch:* serve",
  "build": "npm-run-all build:* copy"
},
...
```

There are two main scripts that you can run:

- `start` (run using `npm run start` or just `npm start`), and
- `build` (run using `npm run build` ).

> [!TIP]
> As an alternative to typing the command manually in the command prompt, in VSCode you can show the _NPM Scripts_ panel inside the _Explorer_ panel by clicking the _three dots menu_ in the _Explorer_ title and check the _NPM Script_. Once the _NPM Scripts_ panel is shown you can just click the `run` button to run the script.

These are the breakdown of the scripts. The other 5 scripts are executed in the 2 main scripts.

- `"start": "npm-run-all --parallel watch:* serve"`

  This is used when developing the project. It executes these other 2 scripts in parallel:

  - `"watch:sass": "sass --watch src/sass:src --source-map-urls=relative"`

    Compile the `*.scss` files in the _src/scss_ directory to _src/style.css_. Also auto compile it if there are changes to the `*.scss` files.

  - `"serve": "browser-sync start --server src --files src"`

    Launch a local development server, for example: `http://localhost:3000/`.

  With these 2 scripts, when you make changes on the html or scss files and save it, the changes will be shown immediately on the browser.

- `"build": "npm-run-all build:* copy"`

  It is used to compile the files for deployment on the remote server. This script produces files in _/public/_ folder.

  It executes these other 3 scripts:

  - `"build:sass": "sass src/sass:public --no-source-map"`

    Compile the `*.scss` file at once, no need to watch the changes. The CSS output is in the public folder.

  - `"copy": "cpx \"src/\*_/_.{html,jpg,png,svg}\" public"`

    Copy all the `*.html` and the image files from the _/src/_ to the _/public/_ folder.

  - `"postbuild": "postcss public/*.css -u autoprefixer cssnano -r --no-map"`

    This script is run automatically after running the _build_ script. It adds browser prefixes to the CSS and then compress the CSS.

  > [!NOTE]
  > Even if I put the build script, I don't use the files in the _public/_ folder and put in the server, but I use the files in the _src/_ folder. The reason is to allow anyone to debug the Sass code.

#### 🟢 Sass folder and file structure

The Sass files are located in _/src/sass/_ folder.

It consists of:

- `style.scss`.
- Sass partial files (prefixed with an underscore "\_"). Example: `_base.scss`.

  The partial files are put inside multiple folders. The folder structure is called 7-1 pattern [^4]. There are 7 folders of which each has one or more than one Sass partial files inside. All these partial files are imported in the `style.scss`.

Each of the partial files has underscore "\_" as its prefix and will be skipped by the Sass compiler. There will be only one file that is compiled: `style.scss`, compiled to `style.css`.

```YAML
- public/
- src/
- sass/
  - base/
  - components/
  - layout/
  - pages/
  - themes/
  - abstracts/
  - vendors/
  - style.scss
- index.html
```

#### 🟢 Implementing `rem` using Sass _function_

If in the previous challenge I use [CSS variables to store `rem` unit](https://github.com/finkusuma-dev/fem-recipe-page/?tab=readme-ov-file#-css-variables-for-px-and-rem), in this challenge with Sass I created a functon to convert `px` to `rem`.

```scss
@function rem($value) {
  @return if(math.unit($value) == 'px', calc($value / 16px * 1rem), $value);
}
```

Using function is so much more convenient as you can just use it with the value in `px`.

```scss
.attribution {
  font-size: rem(11px);
}
```

Or use it with the variable.

```scss
.product-preview-card {
  border-radius: rem($spacing-100);
}
```

This function implements a false case where, if the value is not in pixels, it returns the original value without any conversion. This prevents unwanted results when we accidentally pass a variable with units other than pixels.

#### 🟢 Implementing responsive layout media queries using _Mixin_

With Sass it's easier to write media query. Sass has a feature called _mixin_. It enables to re-use styles to any part of the code.

I put all the code related with the responsive layout in the `_breakpoints.scss` partial.

```scss
// _breakpoints.scss

$breakpoints: (
  $medium: functions.rem(768px),
  $xxl: functions.rem(1440px),
);

@mixin media-up-to($breakpoint) {
  ...
}
```

To use the _mixin_, put `@include` followed by the _mixin_ name. This is an example of adding a tablet layout to `body` element.

```scss
body {
  @include media-up-to($medium) {
    min-height: 100vh;

    /* To center .container */
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
```

The compiled CSS result:

```css
@media (min-width: 48rem) {
  body {
    min-height: 100vh;
    /* To center .container */
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
```

### Useful Resources

- https://sass-lang.com.
- https://sass-guidelin.es.
- https://github.com/KittyGiraudel/sass-boilerplate/tree/master/stylesheets/base.
- https://getbootstrap.com/docs/5.0/layout/breakpoints/#available-breakpoints.
- https://www.scottohara.me/blog/2017/04/14/inclusively-hidden.html#hiding-content-visually.

## Author

- Github - [@finkusuma-dev](https://github.com/finkusuma-dev/)
- Frontend Mentor - [@finkusuma-dev](https://www.frontendmentor.io/profile/finkusuma-dev)
- Twitter - [@finkusuma_dev](https://www.twitter.com/finkusuma_dev)

---

[^1]: https://fedmentor.dev/posts/html-plan-product-preview/ - Grace snow's detailed step-by-step breakdown of the same challenge.
[^2]: https://web.dev/learn/design/icons#styling_icons - Styling svg.
[^3]: https://web.dev/learn/design/icons#icons_and_text - Presentational svg icon.
[^4]: https://sass-guidelin.es/#the-7-1-pattern - Sass files and folders pattern.
