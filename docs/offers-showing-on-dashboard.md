---
layout: default
title: Offers Showing On Dashboard
nav_order: 2
---

Turn on flags:

````
    :show_atb_hotfix
    :atb_reduced_assortment 
    :atb_featured_collection_banner
````
Update the create_at for the sub to be more than 9 days
````
    sub = Subscription.find(id)
    sub.created_at = 10.days.ago
    sub.save!
````