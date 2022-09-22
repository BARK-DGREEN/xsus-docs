---
layout: default
title: Renewal Service
nav_order: 5
---
The renewal service looks for any users that have autoship items purchased and generates an add-on setting (if not already created) and an add-on offer of that SKU for the following month. 

## Steps before running the renewal service

Purchase a reserved cart, expire those addons then open a new console window and run the renewal service by typing:

`gcp-cli review rake add_to_box:renew_subscription_additions -a barkbox-rails-review-XXXXX`

***(The add-ons have to be expired before running the service because that’s how the script looks for what offers need adding)***

After that runs, you should see a monthly offer and setting created for the following month.

## Summary of change to ATB renewal service 12/29/20:
We never used to bill carts then run the renewal service on the same month that users reserve their items, but since we have been moving the billing date to be earlier and earlier in order to ship boxes out faster, we have to make changes to the renewal service in order to allow it to create new carts for the correct month.

***For example:*** How it used to work is people would reserve things for *JANUARY'S* box in December, and we would bill them early in the next month for January (either the 1st, 3rd or 5th historically). But now that we want to bill them *EARLIER in late December* instead, we need to update that renewal rake task logic to be date dependent. So after we bill them for January cart on say December 30th, and we run the renewal task shortly after on that same day, it should create an autoship cart for *FEBRUARY* instead of January.

So essentially the new logic is:

1. IF we run the renewal service anytime after the 10th of the month, it will create a new cart that is 2 months from the current month

2. IF we run the renewal service anytime between the 1-10th of the month, it will create a new cart that is 1 month from the current month

3. If it's after the 10th of the month (in December), the renewal task will not pick up any carts from that month and will only pick up reserved, failed or purchased ATB carts that are for the next month in January.
