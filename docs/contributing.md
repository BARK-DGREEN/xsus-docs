---
layout: default
title: Contributing to the Docs
nav_order: 1
---

To contribute to the glory that is Cross-Sell/Upsell/CRM Docs, simply clone [this repo]() to your local machine and follow these steps:

## To Create New Documentation
1. create a new markdown (`.md`) file in the `/docs` directory
2. add the following [frontmatter](https://jekyllrb.com/docs/front-matter/): 
````
---
layout: default
title: ${TITLE}
nav_order: ${IMPORTANCE}
---
```
3. replace `${TITLE}` with a proper title
4. replace `${IMPORTANCE}` according to the following scale:
    - 1 for the utmost important documentation that is a must-know
    - 2 for regular documentation
    - 3 for documentation related to troubleshooting
5. commit the changes with a meaningful commit message and push your changes
6. the documentation site *should* automatically update.
    - if it doesn't, do not panic! 
    - just ask @dylan in slack, he should be helpful in these kinds of situations
    - if that doesn't work, then you are allowed to panic, but not at the disco

## To Edit Existing Documentation
1. locate the doc you would like to edit under the `/docs` directory
2. make all the necessary edits and save your changes
3. commit the changes with a meaningful commit message and push your changes
4. ???
5. watch doc site go brrrrrr
6. doc site is updated!
    - see steps above if it doesn't update