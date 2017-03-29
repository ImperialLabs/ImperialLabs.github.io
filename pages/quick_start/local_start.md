---
title: Step By Step - Local
keywords: 'getting_started, quick start'
last_updated: 'March 29, 2017'
tags:
  - step-by-step
  - framework
sidebar: framework_sidebar
permalink: local_start.html
folder: quick_start
---

# SLAPI: Step By Step Guide

## Ruby Install and Run

There are several ways to do this locally, this is the quickest options. The rake tasks will generate a bot.local.yml for you at `./config/bot.local.yml`

**Note** All files in the `./config` are ignored by git and docker builds with the exception of `bot.yml` and `environments.yml`.

-   Option 1: Use rake to quick bootstrap (Config Creation, Clean Dev Files, and Run Local Prod)

    ```bash
    export SLACK_TOKEN=xoxb-XXXXXXXXXXXX-TTTTTTTTTTTTTT
    bundle install --binstubs --path vendor/bundle
    bundle exec rake local
    ```
-   Option 2: Create a config and Start Bot
    -   Create the following config at `./config/bot.local.yml`

        ```yaml
        adapter:
          type: slack
          token: $SLACK_TOKEN

        # Bot ConfigFile
        bot:
          name: slapi

        # Admin Settings
        admin: # Future Feature
          users:

        # Help Settings
        help:
          level: 1
          dm_user: false

        plugins:
          location: '../../config/plugins/'
        ```

    -   Run the following rake command

        ```bash
        bundle exec rake run:local_prod
        ```

## Next Steps

Go to the [Common Start](https://imperiallabs.github.io/common_start.html) for more

{% include links.html %}
