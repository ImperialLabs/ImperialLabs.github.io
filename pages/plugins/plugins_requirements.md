---
title: Plugins Requirements
keywords: 'getting_started, plugins'
last_updated: 'July 21, 2016'
tags:
  - getting_started
  - plugins
sidebar: framework_sidebar
permalink: plugin_requirements.html
folder: plugins
---

# Overview

In a effort to make the simplest expandable bot possible we have several options when it comes to utilizing plugins

# Minimum Requirements

## Script Based

The easiest and lowest entry point into creating a "plugin" for SLAPI.

Just a simple script you wish to run as a bot command.

It will write out the run: > portion into the appropriate file, mount, and run inside a container.

### Plugin Config

```yaml
plugin_name:
    type: script
    config:
        command: my_script # aka 'bot my_script $args'
        language: ruby
        # Using pagerduty get-oncall as example
        run: >
          #!/usr/bin/env ruby
          # -*- coding: UTF-8 -*-

          require 'httparty'

          API_TOKEN = 'GFd723tgwEbnDcvixPV1'.freeze

          response = HTTParty.get(
          'https://api.pagerduty.com/oncalls',
          headers: {
            'Content-Type' => 'application/json',
            'Accept' => 'application/vnd.pagerduty+json;version=2',
            'Authorization' => "Token token=#{API_TOKEN}"
          }
          )

          puts response.body
```

## Docker Based

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

## API Based

### Info Endpoint

**-==Under Review==-**

This is an endpoint the Framework (slapi) can query to get plugin information and commands to setup routing and the help list with.

Here is all the information the info endpoint can contain.

```json
{
    "info": {
        "command": "pagerduty",
        "commandOpts": {
            "on call": "will return who's on call",
            "on call for $schedule": "chef who's on call for a specifc schedule",
            "resolve": "resolve incident"
        }

    }

}
```

- Required Info Items

  - commandOpts: this is what we build the help list off of.

- Optional Info Items

  - command: This is an override for replacing the plugin command. The plugin name is used by default.

### Command Opts

Command Opts are built as follows

- `"optname": "opt description/usage"`

an example of this in use is

- `@bot help plugin`

```
    bot: plugin opts help
         opts: Description/Usage
         opt2: Description/Usage
```

{% include links.html %}
