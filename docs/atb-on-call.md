---
layout: default
title: ATB On Call
nav_order: 3
---

## Quick Links
- [ATB On-Call Calendar](https://docs.google.com/spreadsheets/d/1nZurt7LJ3bP7kgx2xorzMmAvRQ5agztjqayMI1RVL6g/edit#gid=0)
- [ATB On-Call Periscope Monitoring Dashboard](https://app.periscopedata.com/app/barkbox/1005055/ATB-On-Call)
- [ATB On-Call Sumo Logic Dashboard](https://www.google.com/url?q=https://bark.us2.sumologic.com/ui/%23/dashboardv2/YNKu1O5jIRIpEax6xBwN0iZYiWEFdsiOOXIRKofWmONfgBE8LHxk3HgdHVxW&sa=D&source=editors&ust=1663869586502244&usg=AOvVaw1ek6d8P_7LyY3HfDLqR8tT)

# On Call RunBook 

Please be looking in 

### Request: This subscription had an item mysteriously removed from their cart
Possible steps to investigate: 

- Find the cart in the dash above by adding sub id to the filters and .
- Look for the cart here: barkbox.com/admin/shopping_carts/cart_id.
- Look for a line item with the ‘source_id’ of the item that has been allegedly removed.
- If only a sku is given, you can find the item id by searching by sku here.
- If the line item is a recurring item, ie source_type of ‘SubscriptionAddition’, you can search a subs subscription additions using the ‘Subscription Additions for a Subscription’ table in the dashboard, this time looking for an addition_id with the item id in question, and a non-null expires_at timestamp.
- Once you have the line item in question and it has a quantity of 0, check the updated_at timestamp.
- With the updated_at timestamp in mind, go to sumo, and search for “add_to_box/sub_id”, with sub id replaced by the sub id in question, and at around the time that the line item was updated.
- The search should return messages representing the sub in question’s activity on their ATB page during the time the line item was removed. 
- Look for an entry where you can see the quantity of the sku in question changing to 0.

### Request: Remove a line item from a sub
Steps to solve:
- Create a ticket detailing the request.
- Go to the sub’s page in admin.
- Click on the ‘Current Reserved ATB Cart’ in the side panel.
- Find the item in question and click ‘Remove’ next to the item.
