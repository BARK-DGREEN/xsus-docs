---
layout: default
title: Contributing to the Docs
nav_order: 1
---

# XSUS Docs

To contribute to the glory that is Cross-Sell/Upsell/CRM Docs, simply clone [this repo](https://github.com/BARK-DGREEN/xsus-docs) to your local machine and follow the steps below.

## Quick Links

- XSUS Docs Repo [here](https://github.com/BARK-DGREEN/xsus-docs).
- Bark Eng Docs [here](https://docs.barkco.xyz/applications).
- Bark UI Docs [here](https://www.barkbox.com/bark-ui/utilities/typography#adjust-body-text-weight).

## To Create New Documentation
1. Create a new markdown (`.md`) file in the `/docs` directory.
2. Add the following [frontmatter](https://jekyllrb.com/docs/front-matter/): 
````
---
layout: default
title: ${TITLE}
nav_order: ${IMPORTANCE}
---
```
3. Replace `${TITLE}` with a proper title
4. Commit the changes with a meaningful commit message and push your changes
5. The documentation site *should* automatically update.
    - if it doesn't, do not panic! 
    - just ask @dylan in slack, he should be helpful in these kinds of situations
