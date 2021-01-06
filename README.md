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
- Start 11ty and begin to generate static site content
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
npm install bulma
```