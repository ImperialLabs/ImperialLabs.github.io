---
title: Step By Step - Docker
keywords: 'getting_started, quick start'
last_updated: 'March 29, 2017'
tags:
  - step-by-step
  - framework
sidebar: framework_sidebar
permalink: docker_start.html
folder: quick_start
---

# SLAPI: Step By Step Guide

## Docker Install & Run

There are several ways to do this via Docker, this is the quickest options. The rake tasks will generate a bot.local.yml for you at `./config/bot.local.yml`

**Note** All files in the `./config` are ignored by git and docker builds with the exception of `bot.yml` and `environments.yml`.

-   Option 1: If ruby and rake are installed

    ```bash
    export SLACK_TOKEN=xoxb-XXXXXXXXXXXX-TTTTTTTTTTTTTT
    rake docker
    ```
-   Option 2: If only Docker Machine & Compose is installed
    -   Create a config and Start Bot
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
        -   For Prebuilt: Run Docker Compose Up

            ```bash
            docker-compose -f docker-compose.yml up
            ```
        -   For Fresh Build: Run Docker Compose Up

            ```bash
            docker-compose -f slapi-build-compose.yml up
            ```

## Next Steps

Go to the [Common Start](https://imperiallabs.github.io/common_start.html) for more

{% include links.html %}
