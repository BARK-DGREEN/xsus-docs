---
layout: default
title: GCP CLI Cheatsheet
nav_order: 2
parent: Cheatsheets
---

# GCP CLI Cheatsheet

## Quick Links

- [Bark GCP CLI Repo](https://github.com/barkbox/gcp-cli)
- [Bark GCP CLI Docs](https://docs.barkco.xyz/workflows)
- [XSUS GCP CLI Docs](https://docs.google.com/document/d/1TGkvv3QTY2GOMgYrX5m2gSWBEVMsWlagchoHMrYDBII/edit)

## Commands 
Review App Console
- `gcp-cli review console -a barkbox-rails-review-PR_NUMBER`

Review App Logs 
- `gcp-cli review logs -a barkbox-rails-review-PR_NUMBER`

Import Flags
- `gcp-cli review rake review_app:import_rollout_flags -a barkbox-rails-review-PR_NUMBER`
