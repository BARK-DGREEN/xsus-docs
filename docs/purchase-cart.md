---
layout: default
title: Purchase Cart
nav_order: 2
---
To purchase reserved carts individually, connect to the RA in console and run the following command (with the number in the parenthesis being the shopping cart ID which you can find at /admin/shopping_carts): 
```
    service = PurchaseReservedCartService.new(<cart_id>)
    service.perform!
```

## Gotchas:

- The subscription you are purchasing for will need to have an order for the atb month you are purchasing. So, for example, if the atb month is July, the sub will need to have an order with a scheduled_at date of `7-15-<year>`. If you only have one order and the `scheduled_at` timestamp is incorrect, you can update the order to have the appropriate timestamp.

- The items in the cart need to have inventory. If you visit the item page in admin, you should see the inventory counts in the panel to the left. To update the inventory you can run the following command:

`InventoryCount.where(item_id: item.id).update(warehouse_qty: {"PBKY"=>{"count"=>10000, "counted_at"=>"2021-06-08 06:00:23"}, "OIASKY"=>{"count"=>10000, "counted_at"=>"2021-06-08 07:10:00"}}). If the count has an ‘available’ property of 0 or less, you can update it with InventoryCount.where(item_id: <item_id>).update(available: 100)`

- If you encounter an error when you run the service, you should be able to run the service again after addressing the error/s, but you will first need to unlock the cart with `Shopping::Cart.find(<cart_id>).unlock!`

## -OR-

To purchase ALL reserved carts that are not first box reservations, run:

`gcp-cli review rake add_to_box:purchase_reserved_carts -a barkbox-rails-review-XXXXX`

***(Note: before attempting to purchase, make sure a subscription order is ‘scheduled’ in admin and the addons are expired in order for it to get picked up by the rake task)***

To purchase all reserved carts that are first box reservations, run:

`gcp-cli review rake add_to_box:purchase_reserved_carts_first_box -a barkbox-rails-review-XXXXX`

***(Note: before attempting to purchase first box carts, the subs created_at date has to be at least 30 minutes old for it to get picked up by the rake task)***

```
    sub=Subscription.find(xx)
    sub.created_at=30.minutes.ago
    sub.save!
```
