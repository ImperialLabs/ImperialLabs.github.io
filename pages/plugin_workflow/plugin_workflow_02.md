---
title: Eval and Install
keywords: plugins
sidebar: framework_sidebar
permalink: plugin_workflow_02.html
simple_map: true
map_name: pluginmap
box_number: 2
folder: plugin_workflow
---

# Plugin Management System

## Pull and Build Plugins

- Evaluate plugin config for list of plugins

  - Check for source; dockerhub, dockerfile (local or git)
  - Pull or Build plugin

## Configure Plugins and Start

- Load plugin config and assign appropriate config to docker start command

  - Assign variables to their own `-e`

- Associate plugin name with port number, load into brain

  - i.e. `pagerduty == 8100`

- Start plugin (aka docker run)

{% include links.html %}
