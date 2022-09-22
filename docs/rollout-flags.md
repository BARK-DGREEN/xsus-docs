---
layout: default
title: Rollout Flags
nav_order: 5
---

# Rollout Flags 

## Creating A Rollout Flag In Dev

1. Create YourFlagConstraint.rb file by extending BaseConstraint in app/constraints
    - You'll now have access to this object in your controllers and concerns.
2. Create and instance variable based on the rollout flag
    - `@atb_eats_v2 = AtbEatsV2Constraint.matches?(request)`
3. Add instance variable to page data
    - `page_data[:atb_eats_v2] = @atb_eats_v2`
4. Add to the relevant js file if necessary 
    - `isEatsV2: window.pageData.atbEatsV2`
    - this gets the page data variable from step 3 and assigns it to a js variable
5. If working with .erb files, be sure to add it as a local variable to partials. 

[Reference commit from Jon on Eats v2 project from late 2021/early 2022](https://github.com/barkbox/barkbox-rails/pull/12270/commits/e982233e8855b5bde21d9ae57af7a6569fb95d59)
