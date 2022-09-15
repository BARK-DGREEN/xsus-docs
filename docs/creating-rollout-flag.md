---
layout: default
title: Creating A Rollout Flag
nav_order: 2
---

1. Create constraint in app/constraints
2. add instance var to figure out rollout flag
    - `@atb_eats_v2 = AtbEatsV2Constraint.matches?(request)`
3. add to page data
    - `page_data[:atb_eats_v2] = @atb_eats_v2`
4. if doing fun javascript things, add to the relevant js file
    1. `isEatsV2: window.pageData.atbEatsV2`
    2. this gets the page data variable from step 3 and assigns it to a js variable
5. if doing ERB things, which you most likely are, be sure to add it as a local variable to partials

[Reference commit from Jon on Eats v2 project from late 2021/early 2022](https://github.com/barkbox/barkbox-rails/pull/12270/commits/e982233e8855b5bde21d9ae57af7a6569fb95d59)