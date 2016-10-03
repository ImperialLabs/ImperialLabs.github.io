---
title: Script Based Plugins
keywords: 'getting_started, plugins'
last_updated: 'October 3, 2016'
tags:
  - getting_started
  - plugins
sidebar: framework_sidebar
permalink: plugins_script.html
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

{% include links.html %}
