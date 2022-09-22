---
layout: default
title: Cheatsheets
nav_order: 2
has_children: true
---

# Cheatsheets

Data setup to make sub exempt from U-DD (Tailored, litebox and custom billing subs are all exempt from adding U-DD to ATB as of 3/26/20)

## To make sub tailored:

````
    sub = Subscription.find(230) 
    sp = SubscriptionPreference.create!(subscription_id: sub.id, preferences: { treats: { "lamb": "never" }, toys: { "plush": "more" }, chews: nil })
    sub.reload
````

## To get a cart in a state where it has a sold out state 

1. Log into admin from the RA.
2. Monthly Addon_settings
3. Go to the SKU you want to set to sold out state and select edit monthly addon 
4. Scroll to the bottom of the product sku
5. Set the sell to QTY to Zero
6. Then save your changes
7. Head to monthly_addons find the specific sku and select ATB 
8. This launches the sub, the SKU should now be updated and show sold out

## To expire addons for a sub in bulk via console

````
    sub = Subscription.find(xx)
    month = 1
    year = 2021
    ma = MonthlyAddon.where(subscription_id: sub.id, month: month, year: year)
    expiration = 1.day.ago
    ma.each do |addon|
      addon.update(expires_at: expiration)
    end
````

## Make your account in an RA admin
````
    user = User.find_by_email("atb_test@example.com")
    user.password = "Puppies!"
    role = Role.find_by(name: 'Tech')
    role.permissions << Permission.all
    role.save
    user.beta_roles << role
    user.save
````