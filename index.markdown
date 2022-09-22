---
layout: default
title: Contributing to the Docs
nav_order: 1
---

# XSUS/CRM Docs

To contribute to the glory that is Cross-Sell/Upsell/CRM Docs, simply clone [this repo](https://github.com/BARK-DGREEN/xsus-docs) to your local machine and follow the steps below.

## Quick Links

- [XSUS Docs Repo](https://github.com/BARK-DGREEN/xsus-docs).
- [Bark Eng Docs](https://docs.barkco.xyz/applications).
- [Bark UI Docs](https://www.barkbox.com/bark-ui/utilities/typography#adjust-body-text-weight).

## To Create New Documentation
1. Create a new markdown (`.md`) file in the `/docs` directory.
2. Add the following [frontmatter](https://jekyllrb.com/docs/front-matter/): 

````
---
layout: default
title: ${TITLE}
nav_order: ${IMPORTANCE}
---
````

3. Replace `${TITLE}` with a proper title.
4. Commit the changes with a meaningful commit message and push your changes.

## Parent Pages
If you want you doc to be a child of a parent doc-
On the parent page, add this YAML front matter parameter:

- `has_children: true` (tells us that this is a parent page)

***For example:*** 
````
layout: default
title: Testing
nav_order: 2
has_children: true
````

Here we’re setting up the Testing landing page that is available at /testing/, which has children and is ordered second in the main nav.

### Child pages
On child pages, simply set the parent: YAML front matter to whatever the parent’s page title is and set a nav order (this number is now scoped within the section).

***For example:*** 
---
layout: default
title: Testing Amplitude
parent: Testing
nav_order: 2
---

The Testing Amplitude page appears as a child of Testing and appears second in the Testing section.

