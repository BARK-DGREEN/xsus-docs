---
layout: default
title: Expire All Addons For A Sub
nav_order: 2
parent: Scripts
---

## Expire All Addons For A Sub

```rb
    sub = Subscription.find(xx)
    month = 1
    year = 2021
    ma = MonthlyAddon.where(subscription_id: sub.id, month: month, year: year)
    expiration = 1.day.ago
    ma.each do |addon|
      addon.update(expires_at: expiration)
    end
```