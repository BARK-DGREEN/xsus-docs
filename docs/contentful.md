---
layout: default
title: Contentful
nav_order: 5
---
# [Contentful](https://be.contentful.com/login)

Contentful is a platform that allows Bark to easily build customizable content. It is a “headless CMS”, which means that the platform handles content creation and organization, while the client or server (in our case, the server) handles its rendering and presentation. 

In Contentful, the content is organized into different layers of “Content Models”. These are the building blocks of a page or section of a page. Engineers are responsible for creating, maintaining, and then utilizing these Content Models in barkbox-rails, or any other application that wants to make use of the content.

## Platform

- [Contentful](https://app.contentful.com/):
The primary “web app” for the platform, this is where Content Models and Platform configuration are managed.  Content creation can also be done here. 
Individual accounts must be provisioned from an admin [PROCESS TBD]
- [Compose](https://compose.contentful.com):
A more user-friendly content management application, this should especially be used when creating content for full-pages
- Access
You’ll need a CONTENTFUL_ACCESS_TOKEN, CONTENTFUL_SPACE_ID and a CONTENTFUL_PREVIEW_ACCESS_TOKEN in your .env file to get started. 

## Spaces

Spaces are Contentful’s version of environments. 
- “master” is the production environment. This should sparingly be used for testing
- Triple check you are working in “development” when creating new features, testing, or playing around

The current Space can be confirmed in the url (/development) in both applications, or the upper left corner of the web app (“development” will be in orange, “master” in green) and the little square in the left menu of the Compose app (less obvious). 
- Additionally, in the web app the “Space Home” top navigation item will be disabled in any environment that isn’t “master”

## Is it a good candidate for Contentful?

- Components have native styling - implementing Contentful components starts at the design phase (a lot like Bark UI). 
- Components are designed to be generic and reusable as possible (which is why they don’t contain user information).
- If you need user information contained inside the component (not dictating if they see it) this is most likely not a good candidate for Contentful. 

## Planning

Build with reusability, flexibility, and composability in mind!
Before beginning, think about how the proposed design for your feature compares to existing Content Models, and try and find ways to utilize them. Many Content Models function as building blocks, so use that to your advantage! 
If subtle differences exist between an existing model and the design, work with designers to see if the changes are actually needed. If they are, consider if an enhancement can be added to the similar Content Model, rather than creating a new one

For new Content Models:
Break it down into small parts where possible. 
Building blocks > god objects
Name things generically. Even if you have only one specific use case in mind, try and use naming that doesn’t make a Content Model feel beholden to one page or purpose
Avoid including business logic when possible. Consider leveraging [personalizations](https://docs.google.com/document/d/1VHyda-Vyi3pksdRZtzXwwFy9Be3P7NvvBbQGZTO9LKA/edit#heading=h.bmo0ejkcajox) where possible to support conditional business cases
Documentation for usage can be found [here](https://docs.google.com/document/d/1VHyda-Vyi3pksdRZtzXwwFy9Be3P7NvvBbQGZTO9LKA)
Be aware of resource nesting depth. Using building blocks is the ideal, but having too deep of a tree can have performance impacts

## Components, Content Models and Content

Existing Content Models are documented [here](https://docs.google.com/document/d/1VHyda-Vyi3pksdRZtzXwwFy9Be3P7NvvBbQGZTO9LKA)

Content Models have a 1:1 relationship with View Components in barkbox-rails. 
A View Component is an object-driven way to handle markup in modern Rails applications. They are well organized, easily testable, support previews, and more performant than partials. More information can be found in the official [guide](https://viewcomponent.org/)
A CMS Component is what we call a View Component that has a 1:1 relationship with a Content Model.
CMS Components are currently built under the `app/components/cms` directory
All components currently extend BaseComponent, which should house any generalized logic needed across all components.
The CMS Components themselves are user-agnostic and don’t contain any business logic or user information.
Each component will have a .rb Component file. A correspondingly named subdirectory in the `cms/` directory should be created to hold component-specific view (.erb), javascript (.js), and styling (.scss) files
Example: for a “Section” Content Model, you would make section_component.rb for class SectionComponent, section_component.html.erb , section_component.scss, SectionComponent.js. Naming must match
If a front-end file has no utility, it can be removed. E.g. if there’s no custom js, you do not need a .js file

## Generator

For simplicity, a rails generator has been created specifically for CMS Component creation
`rails g bark_component component_name_here --cms`
`rails g bark_component foo_bar --cms` will create:
foo_bar_component.rb
foo_bar_component/foo_bar_component.html.erb
foo_bar_component/foo_bar_component.scss
specs/…/foo_bar_component_spec.rb
test/components/previews/cms/foo_bar_component_preview.rb
Adding the optional `--js` flag will also create 
foo_bar_component/FooBarComponent.js
In addition to file creation, it will also stub various methods and implementation details

# Development

Use the generator to quickly create new files
Build and test all changes in the “development” space.
Cms_Concern.rb has the method ( fetch_contentful_entries() ) you’ll use to fetch from Contentful. 
fetch_contentful_entries() will provide you with the most recent entry of a component. 
Locally the default environment this method pulls from is the dev environment. 
To pull content from master, put export CONTENTFUL_ENVIRONMENT='master' into your .env file.
Currently we are wanting to make only one request to Contentful for data per page. 
This action should get all the components from Contentful needed to render a page. 
We can use business logic to dictate which version of a page a user sees (EX: a Super Chewer page vs Barkbox page). 
We can use the PersonalizationContainer to choose which version of a component a user sees. 
You can fetch a component by providing an entry_id which will attempt to fetch a specific component that has the corresponding id. 
You can also fetch a component by providing a content_type which will fetch all components of the matching type (in order of most recently published).

## Kill Switches

We Utilize two layers of kill-switches, depending on what you’re adding. 

We have a master Contentful rollout flag toggle to kill all Contentful fetching. 
We want a rollout flag to be able to toggle Contentful fetches on each page. 
This is so that just that portion of traffic can be disabled. 
EXAMPLE: Dashboard can be turned off without impacting Landing Pages
This helps manage issues on a smaller scale, for example problems on the 
Each page generally has a corresponding contentful_presenter file which handles the separation of the cms_entry object into various components.  

## Failed Fetches/Mocks

The Fetch to Contentful might fail. 

A common pattern is to provide a MockEntry object to the a Contentful Presenter - this can ensure the user always sees a component in the location you want should your fetch request fail. 

Consider failure cases (no active Contentful entry found; API errors; Contentful API needs to be shut off due to performance concerns; etc.)
What happens to your feature?
Does the user see nothing? 
Do you need a hardcoded fallback?
Link to fallback mock example
Consider how to handle missing fields in a Contentful entry. 
Make sure the page doesn’t 500. 
Avoid relying exclusively on validations within Contentful - they help provide a better content creator experience, but the application should handle missing content gracefully
Leverage View Component preview functionality to create previews for your individual components
Example and instructions coming soon

## PersonalizationContainer

Audience criteria are currently dictated by UTM Params. 
We can build out other audience criteria (EX: based on the subscription model).
We are now able to handle multiple criterias. 
As in the audience must have all matching corresponding UTM params. If you want to say they have at least one UTM Parameter - you’ll want multiple PersonalizationContainers. 
You have the choice of providing a ‘default’ option which all users will see unless they have a matching UTM Param. 

# Review/Deployment

Get a review for your new Content Type or any changes to existing Content Types, in addition to any code changes. 
Changes should be reviewed during standard code review. 
We encourage having a sanity check when moving changes from the “development” space to the “master” space to ensure everything was transferred correctly
Should we have a designated reviewer or reviewers, similar to code owners in github?
For QA, be sure to test edge cases. 
Test it with all expected values, and without any values. 
Test what happens when Contentful does not provide a response, errors, or is turned off. 
Confirm the UX in Contentful is configured in a user-friendly way
Move changes to master when they are ready to go live
Be careful not to introduce breaking changes due to being out of sync with a code deploy. Ex: don’t rename a field that is being used in production. Instead, create  a new field, copy the old values to the new field (manually or via a script), update the code to use it, deploy the code, and then remove the old field



