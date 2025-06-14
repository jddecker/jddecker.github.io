+++
title = "Hello World 👋"
description = "Learning to use Zola and setting up my blog"
date = 2025-03-17
draft = false

[extra]
og_image = "og.webp"
og_image_alt = "Stylized code image representing Jeffrey David Decker's website"
+++

![Stylized code image representing Jeffrey David Decker's website](code.webp)

After years of having a simple Linktree style website, I finally decided to expand my online presence with a blog using a static site generator. This post walks through my journey of choosing Zola, styling with Pico CSS, and deploying on GitHub Pages.

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

Using Zola is as easy as visiting [GetZola.org](https://www.getzola.org/) and following the instructions.

## Styling

I've been exploring lightweight CSS frameworks for my projects. These tools make styling websites quick and easy.

Some of my favorites are:

* [MPV.css](https://andybrewer.github.io/mvp/)
* [Pico CSS](https://picocss.com/)
* [Pure.css](https://purecss.io/)
* [Sakura](https://oxal.org/projects/sakura/)
* [Simple.css](https://simplecss.org/)

For this blog, I chose Pico CSS. I hadn't used it in a project yet, and it's one of the most popular lightweight frameworks out there. I had used MPV.css recently and liked it, but didn't feel like it fit this blog, and the default styles in Simple.css weren't really jibing with me for this project either. Pico CSS's clean default styles and ease of customization made it a good choice. Plus adjusting colors or layouts is straightforward when needed.

Pico CSS can be implemented by downloading the file or via their CDN. [PicoCSS.com](https://picocss.com/) has instructions.

## Hosting

I had been hosting my Linktree-style personal site on [GitHub Pages](https://pages.github.com/), so I stuck with that. A nice perk is that GitHub Actions can be used to build and deploy the site on a git push. You can find an example of the GitHub Action for building a Zola site [here](https://github.com/marketplace/actions/zola-deploy-to-pages).

This is an example of what it looks like when I wrote this article:

``` yaml
name: Zola on GitHub Pages

on: 
 push:
  branches:
   - main  # Trigger on pushes to the main branch

jobs:
  build:
    name: Publish site
    runs-on: ubuntu-latest
    steps:
    - name: Checkout main
      uses: actions/checkout@v4  # check out the repository code
    - name: Build and deploy
      uses: shalzz/zola-deploy-action@v0.20.0  # Uses Zola to build the site
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Just drop this into a YAML file in `.github/workflows`. I called my file `zola-build.yml`.

Then set your Github Pages settings to *deploy from a branch* and set that branch to *gh-pages* and the *root* folder. I couldn't find a way to have it build to a folder in the main branch and have the site work, but GitHub Pages allows you to put your static website files in a branch called *gh-pages* to have your site visible to the public.

![GitHub Pages settings: 'Deploy from a branch' configuration](deploy%20from%20a%20branch.webp)

After you push your files to Github, then the action should create a branch called gh-pages and your site should be visible online.

## Conclusion

Setting up this blog with Zola and Pico CSS has been smooth and rewarding. If you're exploring SSGs or lightweight CSS frameworks, I hope this helps!
