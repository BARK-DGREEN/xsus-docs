---
layout: default
title: Rails Console Cheatsheet
nav_order: 1
parent: Cheatsheets
---

# Rails Console Cheatsheet

`cmd + k` 
-   Clears the console.

`reload!`  
-   reloads code changes

`variable = _`  
-   Saves last executed thing in console and assigns it to [[variable]]

`ctrl + r`  
-   Reverse command search

Some other good ones for getting more info about your queries were:
`Benchmark.measure {|x| query }`  
`query.to_sql  
`query.explain`

`load "file_path_starting_at_users_folder"`
-    Loads file into console