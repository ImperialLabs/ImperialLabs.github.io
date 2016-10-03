---
title: Container Plugin
keywords: 'getting_started, plugins'
last_updated: 'October 3, 2016'
tags:
  - getting_started
  - plugins
sidebar: framework_sidebar
permalink: plugins_container.html
folder: plugins
---

# Overview

In a effort to make the simplest expandable bot possible we have several options when it comes to utilizing plugins

# Minimum Requirements

## Docker/Container Based

Plugin that is built and completely contained inside a Docker Container

### Plugin Config

```yaml
plugin_name:
    type: docker
    managed: true # Docker only setting
    config:
        image: 'username/plugin' # Required
        tag: latest # Latest used by default, can override
        ports: # Choose which port(s) you want the plugin to respond on
          - 8080
          - 50000
        env: # List of environment variables
            - API='1u3042034'
            - SERVICE='123490ijkd'
```

{% include links.html %}
