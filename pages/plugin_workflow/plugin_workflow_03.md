---
title: Plugin Info and Command Build
keywords: plugins
sidebar: framework_sidebar
permalink: plugin_workflow_03.html
simple_map: true
map_name: pluginmap
box_number: 3
folder: plugin_workflow
---

## Info Endpoint
* Perform data grab on info endpoint and parse
    * Example: Get pageduty info `https://localhost:8100/info`
    * Example Payload:
    ```json
       {
            "plugin": {
                "info":{
                    "name": "pagerduty",
                    "endpoint": "true",
                    "commandList": {
                        "on call": "Find out who's on call",
                        "on call next": "find out who's next to be on call",
                        "resolve": "resolve incident"
                }
            }
        }
    ```

## Build Command List

* Consumes data and stores into brain
* Builds default help command
    * `@framework help` just returns list of plugins
    * `@framework $plugin help` returns plugin help list
* Commands are assigned to ports
    * All pagerduty:$ command will route to 8100
    * `@framework pagerduty:on call` will route to https://localhost:8100
    * Example payload:
    ```json
        {
            "plugin": {
                "command": "on call",
                "fromUser": "dude_awesome"
                }
            }
        }
    ```


{% include links.html %}
