+++
title = "Hello World 👋"
description = "Learning to use Zola and setting up my blog"
date = 2025-03-17
draft = false

[extra]
og_image = "og%20code.webp"
og_image_alt = "Showing computer code slightly blurred and at an angle"
+++

![Showing computer code slightly blurred and at an angle](code.webp)

I had been playing around with the idea of using a static site generator (SSG) on my personal website. [Jamstack has an index with popularity for them here.](https://jamstack.org/generators/)

I was mostly after an SSG that:

* Didn't require me to install an environment to use (so no Python, Node.js, etc)
* Is a single binary if possible
* Easy to build my own template

This ruled out a lot of popular SSGs such as Gatsby, Astro, Jekyll, Pelican, and many more, but left me with two very popular generators: Hugo and Zola.

Hugo appears to be the more popular of the two. I fiddled around with it for a bit, but didn't really care for the Go templating engine.

Zola seemed to click a bit better. It uses a templating engine called [Tera](https://keats.github.io/tera/docs/) that is similar to Jinja2. I had used Jinja2 in a few Flask projects. Tera templates have their logic between tags with curly brackets with percent signs. For example:

`{% if foo %}<!-- Do some stuff -->{% endif %}`

While outputting the value of a variable has a shortcut of doing two curly brackets.

`{{ foo }}`

## Styling

I've been becoming a fan of smaller CSS frameworks to be able to style websites quickly and to get up and going without much effort. Some of my favorites are:

* [MPV.css](https://andybrewer.github.io/mvp/)
* [Pico.css](https://picocss.com/)
* [Pure](https://purecss.io/)
* [Sakura](https://oxal.org/projects/sakura/)
* [Simple](https://simplecss.org/)

For this blog, I ended up using Pico.css. Like that it has good default styling, but also lets you change around the colors very easily if you would want.

## Hosting

I've been hosting my Linktree clone of a personal website on Github Pages and decided to continue doing that. Something that is nice is that there is a Github action that will do the building and deploy the website on a push. You can find it [here](https://github.com/marketplace/actions/zola-deploy-to-pages).

Here is an example of what it looks like:

```
name: Zola on GitHub Pages

on: 
 push:
  branches:
   - main

jobs:
  build:
    name: Publish site
    runs-on: ubuntu-latest
    steps:
    - name: Checkout main
      uses: actions/checkout@v4
    - name: Build and deploy
      uses: shalzz/zola-deploy-action@v0.20.0
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
