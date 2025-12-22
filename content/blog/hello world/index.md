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

Hello 👋! As a fan of tech, I enjoy exploring new ways to learn about programming, design, and engineering.

My old Linktree-style site served its purpose, but I eventually outgrew it. I needed a dedicated space to document my projects and share what I'm learning in a more permanent way.

Here is how I built this blog using Zola and Pico CSS, and how I automated the whole thing with GitHub Pages.

## Why I chose Zola

I finally decided to expand my online presence with a blog. Static Site Generators (SSGs) build websites mostly in advance, making them ideal for blogs. Instead of generating pages on each visit, the site is built once and the files are uploaded. This results in faster, more secure, and easier to host websites.

I wanted an SSG that:

* Didn't require me to install an environment to use (so no Python, Node.js, etc)
* Is a single binary if possible
* Easy to build my own templates

This ruled out popular options like Gatsby, Astro, Jekyll, and Pelican, narrowing my choice to Hugo and Zola.

Hugo is the SSG heavyweight, but after some fiddling, I found its Go templating a bit unintuitive.

Zola clicked. It uses [Tera](https://keats.github.io/tera/docs/), which feels like Jinja2 (the engine I use in Flask). Since I was already comfortable with that syntax, the learning curve was small.

etting started is as simple as downloading the binary from [GetZola.org](https://www.getzola.org/) and following their initialization guide.

## Pico CSS for Styling

I've been exploring lightweight CSS frameworks for my projects. Lightweight CSS frameworks simplify styling by providing a customizable base of styles, saving time and effort.

Some of my favorites are:

* [MPV.css](https://andybrewer.github.io/mvp/)
* [Pico CSS](https://picocss.com/)
* [Pure.css](https://purecss.io/)
* [Sakura](https://oxal.org/projects/sakura/)
* [Simple.css](https://simplecss.org/)

I’ve experimented with several "classless" frameworks like MVP.css and Simple.css, but they often felt either too rigid or didn't quite match the vibe I wanted. I landed on Pico CSS. It’s clean, lightweight, and incredibly easy to customize. Changing a button color is just a single CSS variable tweak.

You can get started by grabbing the file directly or linking to their CDN. Check out [PicoCSS.com](https://picocss.com/) for the quick setup.

## Hosting on Github Pages

I had been hosting my Linktree-style personal site on [GitHub Pages](https://pages.github.com/), so I stuck with that. It's free, easy to use, and especially convenient if you've already using GitHub. A huge perk is using [GitHub Actions](https://github.com/features/actions) to automate the build. Every time I push code, an Action builds the site and deploys it. There are example GitHub Actions that can be [found on GitHub](https://github.com/marketplace/actions/zola-deploy-to-pages).

Here is the workflow configuration I used for Zola v0.20.0:

``` yaml
name: Zola on GitHub Pages

on: 
 push:
  branches:
   - main  # Trigger on pushes to the main branch (rename to master if that is what your main branch is called)

jobs:
  build:
    name: Publish site
    runs-on: ubuntu-latest
    steps:
    - name: Checkout main
      uses: actions/checkout@v4  # check out the repository code
    - name: Build and deploy
      uses: shalzz/zola-deploy-action@v0.20.0  # Uses Zola v0.20.0 to build the site
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}  # This token is automatically provided by GitHub for deployment
```

Just add this to a YAML file in the `.github/workflows` folder. I called my file `zola-build.yml`.

In your GitHub repository settings, set the Pages source to "Deploy from a branch" and point it to the `gh-pages` branch. The Action handles the heavy lifting: every time I push to main, it builds the site and pushes the static files to that deployment branch automatically.

![GitHub Pages settings: 'Deploy from a branch' configuration](deploy%20from%20a%20branch.webp)

After pushing your files to GitHub, the action should create a *gh-pages* branch, making your site public.

## Conclusion

Setting up this blog with Zola and Pico CSS has been smooth and rewarding. If you're exploring SSGs or lightweight CSS frameworks, I hope this helps!
