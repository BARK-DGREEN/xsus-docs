---
layout: default
title: Contributing to the Docs
nav_order: 1
---

# XSUS Docs

To contribute to the glory that is Cross-Sell/Upsell/CRM Docs, simply clone [this repo](https://github.com/BARK-DGREEN/xsus-docs) to your local machine and follow the steps below.

## Quick Links

- [XSUS Docs Repo](https://github.com/BARK-DGREEN/xsus-docs).
- [Bark Eng Docs](https://docs.barkco.xyz/applications).
- [Bark UI Docs](https://www.barkbox.com/bark-ui/utilities/typography#adjust-body-text-weight).
- [Just The Docs Docs](https://just-the-docs.github.io/just-the-docs/)

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

## If you want you doc to be a child of a parent doc

On the parent page, add this YAML front matter parameter:

- `has_children: true` (tells us that this is a parent page)

EXAMPLE
---
layout: default
title: UI Components
nav_order: 2
has_children: true
---

Here we’re setting up the UI Components landing page that is available at /docs/ui-components, which has children and is ordered second in the main nav.

### Child pages
On child pages, simply set the parent: YAML front matter to whatever the parent’s page title is and set a nav order (this number is now scoped within the section).

EXAMPLE
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
---

The Buttons page appears as a child of UI Components and appears second in the UI Components section.
