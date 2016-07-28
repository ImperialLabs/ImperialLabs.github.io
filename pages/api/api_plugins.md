---
title: API Requirements for Plugins
keywords: getting_started, api
last_updated: July 21, 2016
tags: [api]
sidebar: framework_sidebar
permalink: api_plugins.html
folder: api
---

## Framework to Plugin Payloads

```json
{
    "plugin": {
        "name":{
            "command": "somecommand",
            "commandData": "data after command",
            "channel": "channelid",
            "fromUser": "username",
            "mentionedUser": "username"
        }
    }
}
```

## Plugin Info Endpoint Payload

In order to build out Command and Help info, the following endpoint will need to exist to consume data from (port is just example, can be configured to whatever)

`curl -i https://localhost:8000/info`

```json
 {
    "info":{
        "command": "pluginname",
        "endpoint": "true",
        "commandOpts": {
            "opt1": "Command Description",
            "opt2": "Command Description",
            "opt2": "Command Description"
        }
    }
}
```


{% include links.html %}
