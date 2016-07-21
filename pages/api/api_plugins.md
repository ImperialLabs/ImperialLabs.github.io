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
    "plugin": {
        "info":{
            "name": "pluginname",
            "endpoint": "true",
            "commandList": {
                "command1": "Command Description",
                "command2": "Command Description",
                "command2": "Command Description"
            }
        }
    }
}
```


{% include links.html %}
