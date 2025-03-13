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

Using HTML structures and classes from Grace Snow's Product Preview Page [^1].

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

If you didn't know about SASS, it is a stylesheet programming language made specific for CSS. It can do a lot more than normal CSS can do: more operations on variables, nesting selectors, create functions etc. You can read more [introduction to Sass](https://sass-lang.com/guide/).

#### 🟢 Setup Sass project

Sass is installed to the project using NPM, so you need to [install Node](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) first if you haven't done so.

In the root project folder, execute `npm init` to create Node configuration file (more [beginner guide to using NPM](https://nodesource.com/blog/an-absolute-beginners-guide-to-using-npm)).

Add these packages to the project using NPM. Install it as dev dependencies using `npm install --save-dev [package-name]`:

- **sass**: Sass package.
- **browser-sync**: To serve the html into your local machine, similar to [Live Server VSCode Extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer).
- **cpx2**: To copy html and image files.
- **npm-run-all**: Execute NPM script in parallel.

**Note**: You can install them one by one, or install them all at once by listing all the package names separated by a space, ex: `npm install --save-dev package1 package2 package 3`.

Once installed, there will be this code in the _package.json_ file (in the root project folder).

```json
...
"devDependencies": {
  "browser-sync": "^3.0.3",
  "cpx2": "^8.0.0",
  "npm-run-all": "^4.1.5",
  "sass": "^1.85.1"
}
```

Add these `NPM scripts` code in the _package.json_ file:

```json
...
"scripts": {
  "watch:sass": "sass --watch src/scss:src --source-map-urls=relative",
  "build:sass": "sass src/scss:public --no-source-map",
  "copy": "cpx \"src/**/*.{html,jpg,png,svg}\" public",
  "serve": "browser-sync start --server src --files src",
  "start": "npm-run-all --parallel watch:* serve",
  "build": "npm-run-all build:* copy"
},
...
```

There are two main scripts here that you can run:

- `start` (run using `npm run start` command or just `npm start`), and
- `build` (run using `npm run build` command ).

As an alternative to typing the command manually in the prompt, in VSCode you can show the _NPM Scripts_ panel inside the _Explorer_ panel by clicking the _three dots_ in the _Explorer_ title and check the _NPM Script_. Once the _NPM Scripts_ panel is shown you can just click the `run` button to run the script.

The 4 other scripts are executed inside the 2 main scripts:

- `start`: It is used when developing the project. It executes these 2 other scripts:

  - `watch:sass`: Compile the `*.scss` files in the _src/scss_ directory to _src/style.css_. Also auto compile it if there are changes to the `*.scss` files.
  - `serve`: Launch a local development server, ex: `http://localhost:3000/`.

  With these 2 scripts, when you make changes on the html or scss style files and save it, the changes will be shown immediately on the browser.

- `build`: It is used when compiling the files for deployment on the remote server. It executes the 2 other scripts:
  - `build:sass`:.
  - `copy`

### Useful Resources

- https://www.scottohara.me/blog/2017/04/14/inclusively-hidden.html#hiding-content-visually.
- https://sass-lang.com.
- https://sass-guidelin.es.

## Author

- Github - [@finkusuma-dev](https://github.com/finkusuma-dev/)
- Frontend Mentor - [@finkusuma-dev](https://www.frontendmentor.io/profile/finkusuma-dev)
- Twitter - [@finkusuma_dev](https://www.twitter.com/finkusuma_dev)

---

[^1]: https://fedmentor.dev/posts/html-plan-product-preview/ - Grace snow's product preview page.
[^2]: https://web.dev/learn/design/icons#styling_icons - Styling svg.
[^3]: https://web.dev/learn/design/icons#icons_and_text - Presentational svg icon.
