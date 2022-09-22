---
layout: default
title: Create Admin Account
nav_order: 2
parent: Scripts
---

## Make your account in an RA admin

```rb
    user = User.find_by_email("atb_test@example.com")
    user.password = "Puppies!"
    role = Role.find_by(name: 'Tech')
    role.permissions << Permission.all
    role.save
    user.beta_roles << role
    user.save
```