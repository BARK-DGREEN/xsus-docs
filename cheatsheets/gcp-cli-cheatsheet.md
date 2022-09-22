---
layout: default
title: GCP ClI Cheatsheet
nav_order: 2
parent: Cheatsheets
---

# GCP ClI 

- [Repo](https://github.com/barkbox/gcp-cli)
- [Bark Docs](https://docs.barkco.xyz/workflows)
- [XSUS Docs](https://docs.google.com/document/d/1TGkvv3QTY2GOMgYrX5m2gSWBEVMsWlagchoHMrYDBII/edit)

## Commands 
#### Review App Console
`gcp-cli review console -a barkbox-rails-review-PR_NUMBER`
#### Review App Logs 
- `gcp-cli review logs -a barkbox-rails-review-PR_NUMBER`
	- If that doesn't work trying running `export CLOUDSDK_PYTHON_SITEPACKAGES=1` beforehand.
#### Import Flags
`gcp-cli review rake review_app:import_rollout_flags -a barkbox-rails-review-PR_NUMBER`
