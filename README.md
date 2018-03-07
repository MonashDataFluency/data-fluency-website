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

## Building and deployment

```bash
# This builds the static pages, commits and pushes to the Github pages site (using the 'public' git submodule).
# It doesn't commit or push any changes to your Markdown source - do that yourself.

./deploy.sh
```
