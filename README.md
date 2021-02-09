# How to start and launch a new site using 11ty and Netlify
https://www.11ty.dev/docs/getting-started/

## 1. Create a new repo in github and clone to machine
- Name and set up any options such as licensing or .gitignore files
- Navigate to desired file save location in terminal and clone repo
```bash
$ git clone "https://github.com/devBoysal/Boysal-portfolio.git"
```
- Generate Json file and answer with default setup questions
```bash
$ npm init -y
```
(-y will answer yes to all setup question as a default)

## 2. Install 11ty
- Install 11ty package
```bash
$ npm i @11ty/eleventy
```
(i = install)

## 3. Create any placeholder files within root directory
- Create an index.md or index.html file for placeholder content

## 4. Run and initialise 11ty
- Start 11ty and begin to generate static site content (use this if you'd like to run a rebuild into _site)
```bash
$ npx eleventy
```

## 5. Serve a local host and listen for live changes
```bash
$ npx eleventy --serve
```

## 6. Exclude generated content from commit
- In the .gitignore file add:
```
# eleventy
_site
```
## 7. Push to Github
- Add, commit and push all work to github.

## Netlify

### Config Netlify
- Navigate to Netlify and add a new site
- Choose Repo for Netlify to host
- Observe your new domain hosted by netlify

## Adding layouts
- Add a templating language of your choice. I've used nunjucks.
- Place a directory at root level as `_includes`
- Add a document labelled as `.njk`
```
default-layout.njk
```

## Adding any other dependecies
```
$ npm install node-sass --save-dev
$ npm install bulma --save-dev
```
- This adds sass and bulma as dev dependencies

## Creating an assets directory to compile into _site
This directory will be the location of all the assets that will be buit by 11ty into _site
- Create an `assets` directory at the root level
- Create an `img` directory within 'assets' for any images for the site.
### Creating passthrough command for 11ty
11ty will need to know that these are the assets used for your site.
- In `.eleventy.js` add:
```js
module.exports = function(eleventyConfig)   {

    eleventyConfig.addPassthroughCopy("assets")
};
```
- This will tell 11ty to build the directory `assets` into _site

## Compiling Bulma
- Create a `sass` directory under 'assets'
- Create a `styles.scss` file within 'sass' directory
  - make sure to place `@charset "utf-8";` within 'styles.scss'
- Create a `css` directory under 'assets'
  - Place text below in `default-layout.njk` head
  ``` html
  <link rel="stylesheet" href="css/styles.css">
  ```
- Create a `styles.css` file under 'css' directory

From here, you can now import any styling you wish to use from node_modules/bulma/sass/*
To do this simply write:
- `@import "./node_modules/bulma/sass/utilities/_all.sass";` into `styles.scss`
  - make sure path to directory is correct
- this will now give you access to use bulma styling after you run a css build command.

### CSS build
- If your `package.json` file does not contain any scripts make sure to include these:
```js
"scripts": {
  "css-build": "node-sass --omit-source-map-url assets/sass/styles.scss assets/css/styles.css",
  "css-watch": "npm run css-build -- --watch",
  "start": "npm run css-watch"
}
```
This will create a `css-build` command which will run and compile the scss file into _site
- any time you make changes to `styles.scss` in 'assets' make sure to run: `npm run css-build`
This will build sass into `css` directory which will then be built into _site by 11ty when you run:
- `npx eleventy --serve` or;
- `npx eleventy`