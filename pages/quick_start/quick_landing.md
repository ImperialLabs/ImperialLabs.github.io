---
title: Step By Step - Landing
keywords: 'getting_started, quick start'
last_updated: 'March 29, 2017'
tags:
  - step-by-step
  - framework
sidebar: framework_sidebar
permalink: quick_landing.html
folder: quick_start
---

# SLAPI: Step By Step Guide

## Pre-requisites

-   Slack - This is a Slack Bot (Well Custom Integration for now)
-   Install [Ruby](https://imperiallabs.github.io/ruby_install.html) - v2.3 or later (If doing local install)
    -   Install [Bundler](https://imperiallabs.github.io/ruby_install.html#bundler)
-   Install [Docker](https://imperiallabs.github.io/docker_install.html) - v1.10 or later

## Get The Bot

Choose Install to Start (More options in the future)
-   [Repo Clone](#repo-clone)

### Repo Clone

Clone the bot repo:

```
git clone https://github.com/ImperialLabs/slapi.git
cd slapi
```

## Get a Key

-   Go to <https://slack.com/apps/manage/custom-integrations>
    -   Select Bots
        {% include image.html file="custom_integrations.png" %}
    -   Add Configuration:
        {% include image.html file="add_configuration.png" %}
    -   Enter Name and Add Integrations
        {% include image.html file="add_integration.png" %}
    -   Copy API Token
        {% include image.html file="api_token.png" %}

## Choose Install

-   Install [Locally](https://imperiallabs.github.io/local_start.html)
-   Install w/ [Docker](https://imperiallabs.github.io/docker_start.html)


{% include links.html %}
