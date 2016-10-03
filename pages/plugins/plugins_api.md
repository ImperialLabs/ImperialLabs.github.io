---
title: API Plugins
keywords: 'getting_started, plugins'
last_updated: 'October 3, 2016'
tags:
  - getting_started
  - plugins
sidebar: framework_sidebar
permalink: plugins_api.html
folder: plugins
---

# Overview

In a effort to make the simplest expandable bot possible we have several options when it comes to utilizing plugins

# Minimum Requirements

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
