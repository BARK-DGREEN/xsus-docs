---
layout: default
title: Expire All Addons For A Sub
nav_order: 2
parent: Scripts
---

## To make sub tailored:

```rb
    sub = Subscription.find(230) 
    sp = SubscriptionPreference.create!(subscription_id: sub.id, preferences: { treats: { "lamb": "never" }, toys: { "plush": "more" }, chews: nil })
    sub.reload
```