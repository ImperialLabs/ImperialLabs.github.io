---
title: Brain Overview
keywords: getting_started, brain
last_updated: March 09, 2017
tags: [getting_started]
sidebar: framework_sidebar
permalink: brain_landing.html
folder: brain
---

## SLAPI Brain

The Brain is a Redis Server in a docker container managed by the bot.

See: [The Brain Class](https://github.com/ImperialLabs/slapi/blob/master/lib/brain/redis.rb) for more specific info

Docker Image Utilized: [Dockerhub](https://hub.docker.com/_/redis/) [Dockerfile/Version](https://github.com/docker-library/redis/blob/3f926a47370a19fc88d57d0245823758cbf19b2d/3.2/alpine/Dockerfile)

Docker Tag: redis:3-alpine

### Usage

**Note**: The brain can only be used at the library level by the bot itself.

#### Plugin Access

Plugins may access the Brain via API, we have gone the simplest route possible for brain access.

##### Save Key
-   Endpoint: `$bot_url/v1/save`
-   Type: Post
-   Params (All Required):
    -   plugin: $plugin_name (Utilized as Hash Name)
    -   key: $key_name
    -   value: $value to save

**Examples**

```bash
curl -X POST -d "plugin=hello&key=world&value='what a world'" http://localhost:4567/v1/save
```

##### Query Key
-   Endpoint: `$bot_url/v1/query_key`
-   Type: Get
-   Params (All Required):
    -   plugin: $plugin_name (Utilized as Hash Name)
    -   key: $key_name
-   Returns Key Value

**Examples**

```bash
curl -X GET -H "plugin: hello" -H "key: world" http://localhost:9292/v1/query_key
```

##### Query Hash
-   Endpoint: `$bot_url/v1/query_hash`
-   Type: Get
-   Params (All Required):
    -   plugin: $plugin_name (Utilized as Hash Name)
-   Returns Hash Keys

**Examples**

```bash
curl -X GET -H "plugin: hello" http://localhost:9292/v1/query_hash
```

##### Delete Key
-   Endpoint: `$bot_url/v1/delete`
-   Type: Post
-   Params (All Required):
    -   plugin: $plugin_name (Utilized as Hash Name)
    -   key: $key_name

**Examples**

```bash
curl -X POST -d "plugin=hello&key=world" http://localhost:4567/v1/delete
```

{% include links.html %}
