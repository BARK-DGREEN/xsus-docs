---
layout: default
title: Testing Continuity Emails
nav_order: 1
parent: Testing
---

We only trigger purchase or attempted purchase emails for first box orders. So continuity ATB carts should only get reservation confirmation/cancellation emails.

Logic: ATB reservation/cancellation emails are triggered by the `atb_cart:batch_trigger_emails` rake task. The rake task picks up carts where the `customer_updated_at` cart option is at least 30 minutes ago *AND* the cart’s `last_email_triggered_at` cart option precedes the `customer_updated_at` timestamp *OR* is `nil`. (if you already triggered the email once before, the `last_email_triggered_at` has to be older than the `customer_updated_at`)

If you want to tests triggering a reservation success email:
```
    cart = Shopping::Cart.find(XXX)
    cart.options[:customer_updated_at]=30.minutes.ago
    cart.options[:last_email_triggered_at]=nil
    cart.save!
    Scheduled::AtbCartBatchTriggerEmailsWorker.new.perform
```

If you want to test triggering a reservation cancellation email, be sure to change the `customer_updated_at` value before you change the status of the cart to `canceled` because once it’s `canceled` the cart becomes `locked`, and you can’t make any more changes to it.

````rb
    cart = Shopping::Cart.find(XXX)
    cart.options[:customer_updated_at]=30.minutes.ago
    cart.options[:status]=”canceled”
    cart.save!
    Scheduled::AtbCartBatchTriggerEmailsWorker.new.perform
````