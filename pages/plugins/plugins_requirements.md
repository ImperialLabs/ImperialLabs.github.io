---
title: Plugins Requirements
keywords: getting_started, plugins
last_updated: July 21, 2016
tags: [getting_started, plugins]
sidebar: framework_sidebar
permalink: plugin_requirements.html
folder: plugins
---

## Overview

We refer to our plugins as "slapins" so you can just "slap it in".

In that context we do our best to make the entry point into plugin design as simplistic as possible.

## Minimum Requirements

### Info Endpoint

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

* Required Info Items
    * commandOpts: this is what we build the help list off of.
* Optional Info Items
    * command: This is an override for replacing the plugin command. The plugin name is used by default.

### Command Opts

Command Opts are built as follows
* `"optname": "opt description/usage"`

an example of this in use is

* `@bot help plugin`

```
    bot: plugin opts help
         opts: Description/Usage
         opt2: Description/Usage
```

{% include links.html %}
