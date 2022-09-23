---
layout: default
title: Rails Console Cheatsheet
nav_order: 1
parent: Cheatsheets
---

# Rails Console Cheatsheet

## Commands

Clear the console.
- `cmd + k` 

Reload code changes
- `reload!`  

Save last executed thing in console and assigns it to [[variable]]
- `variable = _`  

Reverse command search
- `ctrl + r`  

Load file into console
- `load "file_path_starting_at_users_folder"`

Some other good ones for getting more info about your queries were:
`Benchmark.measure {|x| query }`  
`query.to_sql  
`query.explain`
