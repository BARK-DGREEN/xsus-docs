---
layout: default
title: Testing First Emails
nav_order: 2
---

We don’t trigger reservation confirmation or cancellation emails for atb first box carts, but instead only send them a purchase confirmation or failure emails.


***TODO: update this for GCP workflow***


`You will need to 1st log into Heroku with look for the RA and change the email dynos from 0>1 this will allow the emails to be triggered.`

***Logic:*** Purchase success/failure emails are triggered for `first_box` carts only and only trigger for subs that were created at least 30 minutes ago.

If you want to test a purchase success email:

1. Create new classic sub and assign ATB for first month
2. Expire the addons to be <30 minutes ago so you see countdown timer
3. Reserve item(s) and make sure shopping cart has `first_box value = true`
4. Update credit card to be `4111 1111 1111 1111` - so purchase doesn't fail
5. Make subs `created_at` date at least 30 minutes ago so the purchase rake task picks it up
6. Run first box purchase rake task and expect to receive an success billing email

````
    sub = Subscription.find(XXX)
    month = 10
    year = 2021
    ma = MonthlyAddon.where(subscription_id: sub.id, month: month)

    expiration = 30.minutes.ago
    ma.each do |addon|
      addon.update(expires_at: expiration, updated_at: Time.zone.now)
    end
````
````
    sub.created_at=30.minutes.ago
    sub.save!
````
````
    gcp-cli review rake add_to_box:purchase_reserved_carts_first_box -a barkbox-rails-review-XXXXX
````

If you want to test a purchase failure email, do all the same steps as above except on step 4, update the credit card in happier admin to be `4000 0000 0000 0341` so the purchase fails before you run the purchase rake task. 

***Note: Happier admin will give you an error saying it couldn’t save the credit card but it actually does save in recurly.***
