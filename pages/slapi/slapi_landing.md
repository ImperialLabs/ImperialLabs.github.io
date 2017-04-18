---
title: SLAPI Overview
keywords: 'getting_started, framework'
last_updated: 'April 18, 2017'
tags:
  - getting_started
  - framework
sidebar: framework_sidebar
permalink: slapi_landing.html
folder: slapi
---

# SLAPI Overview

SLAPI Bot strives to accomplish is a truly code agnostic approach to utilizing Bots and ChatOps.

What does SLAPI Stand For? Simple Lightweight API Bot or Slack API Bot

## What makes SLAPI Different?

-   Code Agnostic
    -   If it runs on Linux (windows pending) or has an API endpoint, you can make it a plugin
-   Plugin system
    -   Scripts
        -   YAML Configuration, just block out your script and SLAPI will put it in a Language Supported container
        -   For more specifics and a list of supported Script Languages here [Script Plugins](https://imperiallabs.github.io/plugins_script.html)
    -   Containers
        -   Whether it's a Dockerfile, Dockerhub, or Private Registry. You can pull it down and use it with SLAPI
        -   For more information and expectations of Dockerized plugins check out [Container Plugins](https://imperiallabs.github.io/plugins_container.html)
    -   API
        -   API Endpoints welcome, we just require 2 specific endpoints for SLAPI to utilize any external service
        -   See [API Plugins](https://imperiallabs.github.io/plugins_api.html) for more information

## What does this look like?

SLAPI is currently a Slack only bot

{% include image.html file="SLAPI_Overview.png" %}

-   Diagram Breakdown
    -   User Interface
        -   General Users interact via Slack
    -   Bot
        -   Slack Client
            -   Handles all back and forth of User/Bot
        -   SLAPI Framework (Ruby and Sinatra Based)
            -   Initializes Client, Brain, and Plugins
            -   Creates API Interface for SLAPI
        -   Plugin management
            -   Loads `./config/plugin/*.yaml` files and creates plugins based on `Type`
        -   Brain
            -   Runs Redis in a Container and creates API endpoints to interact with the Redis Client
            -   See [here](https://imperiallabs.github.io/brain_landing.html) for more info on the Brain
    -   Internal Plugins
        -   Languages Exampled: Golang, Python, NodeJS; These are only a fraction of supported languages
        -   These plugins come in two flavors
            -   Script
                -   Simple Script that can be triggered by the bot via Chat
            -   Container/Docker
                -   For more complex Command Line style programs, several configurable options for type of data passed into plugin
    -   External Plugins
        -  Frameworks Exampled: Rails, Spark, Flask; Not limited to these, any API/Web Framework will work
    -   External Notifications
        -   Internal plugins containers can be configured to have ports binded to them to use for monitoring endpoints
        -   i.e.; Github Webhook Plugin that notifies room every time there is a PR or Merge.
{% include links.html %}
