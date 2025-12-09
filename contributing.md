# Comparative Judgement Research Consortium

This repository contains the files that run the [Comparative Judgement Research Consortium Website](https://hiddenharmshub.github.io/cj-research-consortium/)


## Contributing

This is a quick guide to editing the content of the website.

### The _config.yml file

The config file provides the link to the Jekyll template used to render the pages (we can make changes to this as we go - it currently uses a shared template but I will move it onto its own when we start making changes). 

The key thing in the config file is the *sidebar* section which lists all the pages to be linked from the menu. 

Each page is linked using the id in the header (see next section). To make expanding menus you can use the label/children keys as is shown in the example for Meetings. The pages for the drop down menu content don't need to live in a parent folder but they are in a `meetings` folder just to keep things organised.

```md
sidebar:
    - index
    - label: Meetings
      children:
        - 2024-january
        - 2024-september
        - 2025-january
        - 2025-april
    - resources
    - acknowledgements
```

### Individual pages

All of the pages are written in markdown with a `.md` suffix.

Each page must have a header at the top with up to three entries. The most complex header looks like this:

```md
---
id: index
title: Welcome
sidebar_label: Home
---
```

+ *id* is the name of the page (without the .md suffix) and is how the page is referred to in the config file
+ *title* is the H1 title for the page
+ *sidebar_label* is the string used to refer to the page in the sidebar menu

*id* and *title* must be provided. If no *sidebar_label* is provided then the title will also be used in the sidebar. Being able to change this can be useful when you want to have a longer title but a shorter entry in the menu.

The rest of the page should be written in GitHub markdown.

The website is setup to use auto page titles which means a `<h1>` header will be created using the *title* entry from the header of the file. This means any headers added to the page should start at level 2 with `##`. This setting can be turned off in the config file and if that is done a `<h1>` title can be added to each page with `#`.

## Bibliography related pages (Jekyll-Scholar)

The build workflow for the site includes the [Jekyll-scholar](https://github.com/inukshuk/jekyll-scholar) plugin.

This plugin automatically generates a bibliography page from the `references.bib` file in the `_bibliography` folder.

The settings for the jekyll-scholar plugin can be found in the `_config.yml` file under `scholar:`.

The current reference file is apa but modified to remove the DOI/URL from the main reference and instead replace it as a hyperlink.
The two files controlling this are `_styles/apa_hyperlinks.csl` and `_layouts/bibliography_entry.html`.

Entries can be grouped and ordered in different ways in te settings and also split into categories such as years using a filter string.
See the Jekyll-scholar readme for the options.

Entries in the bibtex file can also be accessed elsewhere on the site either as citations or references.
An example of this in action can currently be seen on the `new_articles.md` page.

Jekyll-scholar cannot be used in the default GitHub pages build workflow so a CI workflow is provided in `.github/workflows`.
This will require some changes to the pages setup when this PR is merged.

## Deployment

Every push to the main branch will trigger a new deployment of the website automatically. If you are doing work that is not ready to be deployed please ensure you use branches and only merge to main when it is ready to go live.
