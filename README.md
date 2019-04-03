# Monash Data Fluency website

[![Build/Deploy Status](https://travis-ci.org/MonashDataFluency/data-fluency-website.svg?branch=master)](https://travis-ci.org/MonashDataFluency/data-fluency-website)

This is the source for the _Monash Data Fluency_ website.
 
# Quickstart

```bash
git clone --recurse-submodules https://github.com/MonashDataFluency/data-fluency-website
cd data-fluency-website
# For hugo v0.41, currently used version
brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/b1e187384baf6b50960ceed7d0964c151d14eada/Formula/hugo.rb

# brew install hugo
# sudo apt-get install hugo

hugo server
```

To update the site:

* Edit the Markdown in `content` (and possibly files in `static` or `config.toml`)
* Check that the site builds and looks correct by locally running `hugo server`.
* `git commit` your changes and `git push`.

Deployment to the live site at [monashdatafluency.github.io](https://monashdatafluency.github.io/) happens automatically, via Travis CI.

# Detail

## Dependencies

You'll need [Hugo](https://gohugo.io/getting-started/installing/).

## Cloning
```bash
git clone --recurse-submodules https://github.com/MonashDataFluency/data-fluency-website.git
```

## Editing

```bash
hugo server

# or if you want to see pages marked as drafts
# hugo server -D
```

* Content is in `content/`
* Images and CSS are in `static/`
* Some theme customization and overrides lives in `layouts/`

### Updating for past / new events

We want past events to automatically appear as a list of 'posts' at the bottom of the events page. To do this:

* Create a new page in the `content/events` folder (eg `launch-workshop-20-mar-2018.md`). Include the date at the end of the file as shown.
* Copy the content for the past event on `content/events/_index.md` into the new page dedicated to the past event.
* Replace the content on `content/events/_index.md` with info about any upcoming events.

### Deploying your changes
Commits pushed to the master branch are deployed to the live site automatically. You can monitor the build and 
deployment process on [Travis CI](https://travis-ci.org/MonashDataFluency/data-fluency-website.svg?branch=master).


## Custom template features

### In config.toml

```toml
# Hide the site title in the top navigation area
show_title_in_navigation = false

# list Sections here (by filename minus .md) that you want to exclude from the front page navigation
hide_sections_in_main_menu =  ["intro_to_python"]
```

### In pages

Adding the [tag](https://gohugo.io/variables/page/#page-level-params) `no_sidebar` to a page hides the sidebar 
listing all pages in that section, for that page.

## Manual building and deployment
Normally, deployment of the live site will happen automatically with every commit pushed to the `master` branch - 
you don't need to do anything but wait until the site goes live. You can monitor the build and deployment process on 
[Travis CI](https://travis-ci.org/MonashDataFluency/data-fluency-website.svg?branch=master).

If for some reason you need to build and deploy the live site manually, do:
```bash
# This builds the static pages, commits and pushes to the Github pages site (using the 'public' git submodule).
# It doesn't commit or push any changes to your Markdown source - do that yourself.

./deploy.sh
```

