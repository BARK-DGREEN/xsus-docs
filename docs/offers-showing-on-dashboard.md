---
layout: default
title: Offers Showing On Dashboard
nav_order: 5
---

1. Turn on flags:

```rb
    $rollout.activate(:show_atb_hotfix)
    $rollout.activate(:atb_reduced_assortment)
    $rollout.activate(:atb_featured_collection_banner)
```

2. Update the `create_at` for the sub to be more than 9 days.

```rb
    sub = Subscription.find(id)
    sub.created_at = 10.days.ago
    sub.save!
```