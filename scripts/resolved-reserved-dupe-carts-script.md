---
layout: default
title: Resolve Reserved Dupe Carts
nav_order: 2
parent: Scripts
---

```rb
def resolve_reserved_dupe_carts(array_of_cart_ids)
  array_of_cart_ids.each do |cart_id|
    cart = Shopping::Cart.find(cart_id)

    cart.line_items.each do |li|
      li.quantity = 0 
      li.save!
    end

    cart.options["status"] = AtbCart::CANCELED_STATUS
    cart.options["cancelation_reason"] = "duplicate cart"
    cart.save!
  end 
end

array_of_cart_ids = [
  55958753,
  55926033,
  56002878,
  55975783,
  56038294,
  56022751,
  55879624,
  55887211,
  56123385,
  55900337,
  56059597,
  56002703,
  56016929,
  56133117,
  55942960,
  56031320,
  55988806,
  55885003,
  55952246,
  56013400,
  55891529,
  56003364,
  56003996,
  56112867,
  55954018,
  56071269,
  55928970,
  55930519,
  56098796,
  56089262,
  56119914,
  55256688,
  55949454,
  55973088,
  55976113,
  56056917,
  56071909
]
```