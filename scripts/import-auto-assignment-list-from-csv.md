---
layout: default
title: Import Auto Assign Skus From CSV
nav_order: 2
parent: Scripts
---

## CSV Schema
- row = collection, sku, size

- AtbAutoAssignmentListImporter.perform!("/Users/nickcocks/Documents/Barkbox-Rails/barkbox-rails/data/2022-08/Auto Assign Hard Coded Order - Auto Assign Importer File  (1).csv")

## Script

```rb
class AtbAutoAssignmentListImporter < CsvImporter
  def self.perform!(filepath) # "./data/2022-07/September Auto Assign  - Sheet1.csv"
    new(filepath).perform!
  end

  def initialize(filepath)
    @csv_array = convert_csv_to_hashes(filepath)
  end

  def perform!
    hashmap = {}

    @csv_array.each do |row_array|
      collection = row_array[:collection]

      if hashmap[collection].blank?
        hashmap[collection] = {
          small: [],
          medium: [],
          large: []
        }
      end

      case row_array[:size]
      when 'XS', 'XS/S', 'E/S', 'S'
        hashmap[collection][:small] << row_array[:sku]
      when 'M'
        hashmap[collection][:medium] << row_array[:sku]
      when 'M/L'
        hashmap[collection][:medium] << row_array[:sku]
        hashmap[collection][:large] << row_array[:sku]
      when 'L', 'XL'
        hashmap[collection][:large] << row_array[:sku]
      when 'OSFA'
        hashmap[collection][:medium] << row_array[:sku]
        hashmap[collection][:small] << row_array[:sku]
        hashmap[collection][:large] << row_array[:sku]
      end
    end

    hashmap
  end

  def convert_csv_to_hashes(csv_file)
    # given a csv object, will convert to array of hashes where each row is a hash
    CSV.open(csv_file, headers: true, header_converters: :symbol, skip_blanks: true)
       .to_a.map(&:to_hash)
       .reject { |row| row.values.all?(&:nil?) }
  rescue ArgumentError => e
    raise ArgumentError, "Error: #{e.message}. File must be a CSV."
  end
end
```