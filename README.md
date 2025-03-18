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

To run the script, run it on command prompt. There are two main scripts that you can run:

- `start` (run using `npm run start` or just `npm start`), and
- `build` (run using `npm run build` ).

> [!TIP]
> As an alternative to typing the command manually in the command prompt, in VSCode you can show the _NPM Scripts_ panel inside the _Explorer_ panel by clicking the _three dots menu_ in the _Explorer_ title and check the _NPM Script_. Once the _NPM Scripts_ panel is shown you can just click the `run` button to run the script.

These are the breakdown of the scripts. The 5 other scripts are executed in the 2 main scripts.

- `"start": "npm-run-all --parallel watch:* serve"`

  This is used when developing the project. It executes these 2 other scripts in parallel:

  - `"watch:sass": "sass --watch src/scss:src --source-map-urls=relative"`

    Compile the `*.scss` files in the _src/scss_ directory to _src/style.css_. Also auto compile it if there are changes to the `*.scss` files.

  - `"serve": "browser-sync start --server src --files src"`

    Launch a local development server, for example: `http://localhost:3000/`.

  With these 2 scripts, when you make changes on the html or scss files and save it, the changes will be shown immediately on the browser.

- `"build": "npm-run-all build:* copy"`

  It is used to compile the files for deployment on the remote server. This script produces files in _/public/_ folder.

  It executes these 3 other scripts:

  - `"build:sass": "sass src/scss:public --no-source-map"`

    Compile the `*.scss` file at once, no need to watch the changes. The CSS output is in the public folder.

  - `"copy": "cpx \"src/\*_/_.{html,jpg,png,svg}\" public"`

    Copy all the `*.html` and the image files from the _/src/_ to the _/public/_ folder.

  - `"postbuild": "postcss public/*.css -u autoprefixer cssnano -r --no-map"`

    This script is run automatically after running the _build_ script. It adds browser prefixes to the CSS and then compress the CSS.

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
