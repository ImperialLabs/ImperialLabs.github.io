---
title: SLAPI Overview
keywords: 'getting_started, framework'
last_updated: 'July 21, 2016'
tags:
  - getting_started
  - framework
sidebar: framework_sidebar
permalink: slapi_landing.html
folder: framework
---

# SLAPI Overview (Pending Update)

SLAPI Bot (The ChatOps Framework) strives to accomplish is a truly code base agnostic approach to utilizing Bots and ChatOps.

What does SLAPI Stand For? Simple Lightweight API Bot or Slack API Bot (Though slack is only the first support chat system)

How is this different than other Bots?

-   No requirement to use same code base or import a specific library
-   Utilizes Docker as a package management system
-   Allows external API endpoints as plugins (if configured properly see Plugin Requirements)
-   Handles routing and plugin management within the framework

{% include image.html file="design_overview.png" %}

# Framework Overview

Breakdown of how the framework will be built out and communicate within itself

{% include image.html file="framework_overview.png" %}

{% include links.html %}
