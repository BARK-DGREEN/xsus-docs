---
layout: default
title: Featured Collections Default Images
nav_order: 2
parent: Scripts
---

settings_with_errors = []
  settings = MonthlyAddonSetting.where(month: [10], year: 2022)
  settings.each_with_index do |setting, index|
    puts "processing setting at index #{index}"
    images = setting.images
    images.each do |image|
      begin
        url = image.image.url
        new_url = url.sub('development', 'review')
        image.image = URI.parse(new_url).open
        image.save!
      rescue StandardError => e
        settings_with_errors << [setting.id, image.id, e.message]
      end
    end
  end

  collections_with_errors = []
  collections = FeaturedCollection.where(month: [10], year: 2022)
  collections.each_with_index do |collection, index|
    puts "processing collection at index #{index}"
    images = [
      collection.carousel_banner,
      collection.atb_background_image_desktop,
      collection.atb_background_image_mobile,
      collection.atb_logo_image
    ]
    images.each do |image|
      next unless image.present?

      begin
        url = image.image.url
        new_url = url.sub('development', 'review')
        image.image = URI.parse(new_url).open
        image.save!
      rescue StandardError => e
        collections_with_errors << [collection.id, image.id, e.message]
      end
    end
  end