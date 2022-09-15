---
layout: default
title: Signed Links
nav_order: 2
---

When a customer clicks on a product when viewing an ATB email, they’ll be able to view their ATB landing page or PDPs without having to log in. This is because we generate unique signed links for each customer to use. If you ever want to test signed links in a RA, run this in console:

````
gcp-cli review rails c -a barkbox-rails-review-XXXXX
````

Find the Sub Id and User number in Admin then add both ids to this script:

````
    sub = Subscription.find(XX)
    user = XXX 
    expires_at = (Time.zone.now + 1.month).change(day: 6, hour: 7).iso8601
    
    sig = RequestSignature.generate(
        strings: [sub.user.id, expires_at],
        controller: 'subscriptions',
        action: 'addon_new'
      )
````

Once this script has run add this script to the console and run:

`link = "https://pr-XXXXX.barkboxdev.com/#{SUB_ID}?expires_at=#{expires_at}&signature=#{sig}"`

There will be an output cut and paste this into the browser.  The ellipse will work
Example:  

`https://pr-XXXXX.barkboxdev.com/add_to_box/51?expires_at=2021-12-06T07:...`

This will take you to ATB main

To get a an unAuth link to take you to a PDP choose a sku add it to this script along with the sub_id in the console run:

`pdp_link = "hhttps://pr-XXXXX.barkboxdev.com/add_to_box/items/#{SKU}/?subscription_id=#{SUB_ID}&expires_at=#{expires_at}&signature=#{sig}"`


For PDP UnAuth link, paste adding a sku and the Sub id where indicated in the script

`"https://pr-XXXXX.barkboxdev.com/add_to_box/items/XXXXXXXX?subscription_id=#{XX}&expires_at=#{expires_at}&signature=#{sig}"`

into the console (with quotes) and copy the resulting output Paste the url into the browser

Copy the output without quotes and paste this into the URL, this will take you to the PDP you inputted for that sub.

***Note: This will set a `add_to_box_user_id` cookie in your session, which will allow you to revisit atb pages without special links. If you try to access a signature link for another subscription, you will have to delete your cookie first, or use a fresh incognito session.***
