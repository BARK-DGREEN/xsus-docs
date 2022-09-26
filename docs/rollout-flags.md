---
layout: default
title: Rollout Flags
nav_order: 5
---
# Rollout Flags 

We use these to be able to toggle features on/off as well as run A/B tests. 

## Creating A Rollout Flag In Dev

- Create YourFlagConstraint.rb file by extending `BaseConstraint` in app/constraints

```rb
class YourConstraint < BaseConstraint
  def initialize(request)
    super(
      request: request, # The actual HTTP request rails object from the controller. 
      feature_key: :xsus_new_flag_name, # Flag name, always prefixed with "xsus_". 
      param_override: "NEW_FLAG_NAME" # Force param
    )
  end
end
```
***Note:*** You'll now have access to this object in your controllers and concerns.

1. Create and instance variable based on the rollout flag
    - `@atb_eats_v2 = AtbEatsV2Constraint.matches?(request)`
2. Add instance variable to page data
    - `page_data[:atb_eats_v2] = @atb_eats_v2`
3.  Add to the relevant js file if necessary 
    - `isEatsV2: window.pageData.atbEatsV2`
    - this gets the page data variable from step 3 and assigns it to a js variable
4. If working with .erb files, be sure to add it as a local variable to partials. 

[Reference commit from Jon on Eats v2 project from late 2021/early 2022](https://github.com/barkbox/barkbox-rails/pull/12270/commits/e982233e8855b5bde21d9ae57af7a6569fb95d59).

## Rollout Flag Related Commands 

Turn flag on:

- `$rollout.activate(:xsus_your_flag_name)`

Turn flag off: 

- `$rollout.deactivate(:xsus_your_flag_name)`

[Import Flags To GCP RA](https://xsus-docs.vercel.app/cheatsheets/gcp-cli-cheatsheet.html#import-flags): 

- `gcp-cli review rake review_app:import_rollout_flags -a barkbox-rails-review-PR_NUMBER`




