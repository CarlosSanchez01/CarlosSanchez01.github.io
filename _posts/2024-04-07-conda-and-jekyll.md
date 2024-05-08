---
layout: post
title: "Creating a development environment with conda"
date: 2024-04-07 09:00:00 -0500
tags: conda ruby jekyll web
image:
  path: /assets/img/headers/conda.svg
  alt: conda logo in svg
  max-width: 740
  # height: 180
---

# Using conda to build a jekyll site

Start by setting a conda environment that includes ruby
I used [this website](https://s-canchi.github.io/2021-04-30-jekyll-conda/)
as a guide but as usual, it did not work as is...

The commands I made were:

```bash
conda create --prefix ./_conda
conda activate _conda
conda install -c conda-forge c-compiler compilers cxx-compiler
conda install -c conda-forge ruby
```

I do not get into details about [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/index.html) but the \_conda folder weight too much and I add it to the .gitignore.
Additionally, I want to keep this environment for future needs so I want to keep
an environment.yaml to obtain the same environment whenever is needed.

```bash
conda env export > environment.yaml
```

This way, if needed, I can recreate the environment with and update the environment if there are some updated dependencies with the commands:

```bash
conda env create -f environment.yaml
conda env update --file environment.yaml --prune
```

Okay, now we have jekyll installed, a Gemfile to track dependencies and bundle to orchestrate those.

Now from the [jekyll documentation](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/), we can run:

```bash
gem install bundler
bundle init
bundle install
bundle add jekyll
bundle config set --local path '_bundle'
bundle exec jekyll --version
```

This creates a jekyll scaffold with about.markdown, index.markdown, 404.html and
\_posts folder.

```bash
bundle exec jekyll new --force --skip-bundle .
bundle exec jekyll serve
```

This creates a jekyll scaffold with about.markdown, index.markdown, 404.html and
\_posts folder and then it serves the website locally with `bundle exec jekyll serve`.
You can visit it at http://127.0.0.1:4000.

From here, you’re ready to continue developing the site on your own. All of the normal Jekyll commands are available to you, but you should prefix them with `bundle exec` so that Bundler runs the version of Jekyll that is installed in your project folder.
