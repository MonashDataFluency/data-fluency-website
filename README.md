# Monash Data Fluency website

This is the source for the _Monash Data Fluency_ website.
 
To update the site, edit the Markdown and template overrides here,
commit and push, then run `/deploy.sh` to build and push the generated static HTML.

## Dependencies

You'll need  [Hugo](https://gohugo.io/getting-started/installing/).

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

## Building and deployment

```bash
# This builds the static pages, commits and pushes to the Github pages site (using the 'public' git submodule).
# It doesn't commit or push any changes to your Markdown source - do that yourself.

./deploy.sh
```

### Updating for past / new events

We want past events to automatically appear as a list of 'posts' at the bottom of the events page. To do this:

* Create a new page in the `content/events` folder (eg `launch-workshop-20-mar-2018.md`). Include the date at the end of the file as shown.
* Copy the content for the past event on `content/events/_index.md` into the new page dedicated to the past event.
* Replace the content on `content/events/_index.md` with info about any upcoming events.
