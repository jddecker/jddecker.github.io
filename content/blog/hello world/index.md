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

I'd been toying with the idea of using a static site generator (SSG) for my personal website. [Jamstack](https://jamstack.org/generators/) has a ranked index of them.

I wanted an SSG that:

* Didn't require me to install an environment to use (so no Python, Node.js, etc)
* Is a single binary if possible
* Easy to build my own template

That ruled out popular options like Gatsby, Astro, Jekyll, and Pelican, leaving me with two top contenders: Hugo and Zola.

Hugo is the more popular of the two. I fiddled around with it for a bit, but didn't really care for the Go templating engine.

Zola just clicked better for me. It uses a templating engine called [Tera](https://keats.github.io/tera/docs/) that is similar to Jinja2. I'd used Jinja2 in some Flask projects before. Tera templates have their logic between tags with curly brackets with percent signs. For example:

`{% if foo %}<!-- Do some stuff -->{% endif %}`

You can output a variable's value with double curly brackets.

`{{ foo }}`

## Styling

I've been getting into smaller CSS frameworks. They make styling quick and easy. Some of my favorites are:

* [MPV.css](https://andybrewer.github.io/mvp/)
* [Pico CSS](https://picocss.com/)
* [Pure.css](https://purecss.io/)
* [Sakura](https://oxal.org/projects/sakura/)
* [Simple.css](https://simplecss.org/)

For this blog, I went with Pico.css. I like its solid default styling, plus it's easy to tweak colors if needed.

## Hosting

I've been hosting my Linktree-style personal site on GitHub Pages, so I stuck with that. A nice perk is that a GitHub Action can build and deploy the site on push. You can find it [here](https://github.com/marketplace/actions/zola-deploy-to-pages).

Here is an example of what it looks like:

``` yaml
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

Just drop this into a YAML file in `.github/workflows`. I called my file `zola-build.yml`.

Then set your Github Pages settings to *deploy from a branch* and set that branch to *gh-pages* and the *root* folder.

![Screenshot of the deploy from a branch setting](deploy%20from%20a%20branch.webp)

After you push your files to Github, then the action should create a branch called gh-pages and your site should be visible online.
