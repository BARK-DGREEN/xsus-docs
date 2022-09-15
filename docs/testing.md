---
layout: default
title: Testing
nav_order: 2
---
(slack `@Flower Queen` for any help w/ this)

***Note: RA’s should automatically have ATB data generated when they’re built but if for some reason it doesn’t, you can run this rake task to generate ATB data:***

`gcp-cli review rake review_app:atb_setup -a barkbox-rails-review-XXXXX`

## Data Setup (Assigning ATB items to a user account)
You need to create assignments so the user can see the addons from their dashboard view in the first place. How do dat? (***Note:*** *if you have ATB offers for your first month, you’ll need to enable the `first_box_atb` flag on the RA in order to see those on your dashboard*)


## Add-on Setting 
**What:**  One setting is created for every SKU being offered to any user for that month. For example, if you want to offer customers Double Deluxe for February and March, you’ll make two settings w/ the U-DD sku… one for the month of Feb and one for the month of March

**Where:** `/admin/monthly_addon_settings`

**How:** From the settings page, click the “New Monthly Addon Setting” button. Input all the information and save checking the “Featured?” box will ensure that product displays at the top of a users ATB landing page (*as the first product they see*).
The “sell to quantity” field will limit how many we can reserve before it shows as sold out to the user. 

## Add-on Offer

**What:** Every SKU that has an add-on setting created needs an add-on offer created for every user we want to offer that product to

**Where:** `/admin/monthly_addons`

**How:** From the offers page, click the **“New Monthly Addon”** button.  Input all the information and save. Make sure the expires at date isn’t in the past because the offer won’t display on the users ATB landing page if it is

## Users ATB Landing Page
**What:** This is where a user goes to purchase ATB

**Where:** `/add_to_box/sub_id`
**How:** You can navigate any user’s ATB landing page as an admin or logged in as the user. To easily find an ATB page to test, you can click on the “Add to Box Page” link that’s on the add-on offer page (`/admin/monthly_addons`) to be redirected to that user’s ATB landing page
