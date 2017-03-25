---
title: API Plugins
keywords: 'getting_started, plugins'
last_updated: 'March 24, 2017'
tags:
  - getting_started
  - plugins
sidebar: framework_sidebar
permalink: plugins_api.html
folder: plugins
---

# Overview

3rd and most advanced level of plugin. Can be managed by Slapi or completely separate.

## API Plugin Basics

### Info Endpoint

This is an endpoint that Slapi can query to get plugin information and commands to setup routing and the help list with.

Here is all the information the info endpoint can contain.

```json
{
    "help": {
        "arg01": "arg description",
        "arg02": "arg description"
    }
}
```

- Required Info Items

  - help: this is what we build the help list off of for `@bot help plugin`

### Command Endpoint

This is the endpoint that is posted to from the bot with the chat data

### Config

We have enabled several config options for the API Plugin Type.

#### Un-Managed
Setup the plugin anywhere in this option, as long as there are two endpoints available to the bot.

-   Endpoints:
    -   info: provides help data about plugin; see [info endpoint](#info-endpoint) section for more info
    -   command: endpoint to pass all the plugin commands to, configurable see endpoint setting below (i.e. `@bot plugin_name do_something`)

```yaml
---
plugin:
  type: api
  api_config:
    url: 'http://localhost:4700'
    endpoint: '/endpoint'
    headers: # Enter as normal HTTP headers, Key: Value
      Content-Type: # Set content type
      Authorization: # Use for tokens
```

#### Managed

Works similar to a container plugin, but instead runs any execs via API calls.

-   Endpoints:
    -   info: provides help data about plugin; see [info endpoint](#info-endpoint) section for more info
    -   command: endpoint to pass all the plugin commands to, configurable see endpoint setting below (i.e. `@bot plugin_name do_something`)
-   Plugin Config Location: `config/plugins/plugin_name.yml`
    -   plugin_name: whatever name you wish your plugin to be accessed as. (i.e.; `@bot plugin_name`)

```yaml
---
plugin:
  type: api
  managed: true
  api_config:
    endpoint: '/endpoint'
    # headers: # Enter as normal HTTP headers, Key: Value
    #   Content-Type: # Set content type
    #   Authorization: # Use for tokens
  config:
    Image: 'slapi/slapin-test:api' # Enter user/repo (standard docker pull procedures), you can also pull from a private repo via domain.com/repo
    HostConfig:
      PortBindings:
        4700/tcp:
          -
            HostIp: '0.0.0.0'
            HostPort: '4700'
    Tty: true # Set true/false for container TTY
    RestartPolicy: # https://docs.docker.com/engine/reference/run/#/restart-policies---restart
     Name: on-failure # no|always|unless-stopped are valid options. on-failure requires MaximumRetryCount
     MaximumRetryCount: 2 # Max number of time to attempt to restart container/plugin before quitting
```

#### Dockerfile Build

This option will allow an API plugin to be managed and built from a Dockerfile.

-   Endpoints:
    -   info: provides help data about plugin; see [info endpoint](#info-endpoint) section for more info
    -   command: endpoint to pass all the plugin commands to, configurable see endpoint setting below (i.e. `@bot plugin_name do_something`)
-   Plugin Config Location: `config/plugins/plugin_name.yml`
    -   plugin_name: whatever name you wish your plugin to be accessed as. (i.e.; `@bot plugin_name`)
-   Docker File Location: `config/plugins/plugin_name/Dockerfile`
    -   plugin_name: same as the `plugin_name.yml`. See [api spec fixture config](https://github.com/ImperialLabs/slapi/blob/api_plugin/spec/fixtures/plugins/api.yml) for working example.
    -   Treat the `plugin_name` folder as a regular docker folder. See [api spec fixture directory](https://github.com/ImperialLabs/slapi/tree/api_plugin/spec/fixtures/plugins/api) for a working example.

```yaml
---
plugin:
  type: api
  managed: true
  build: true
  api_config:
    endpoint: '/endpoint'
    headers: # Enter as normal HTTP headers, Key: Value
      Content-Type: # Set content type
      Authorization: # Use for tokens
  config:
    HostConfig:
      PortBindings:
        4700/tcp:
          -
            HostIp: '0.0.0.0'
            HostPort: '4700'
    Tty: true # Set true/false for container TTY
    RestartPolicy: # https://docs.docker.com/engine/reference/run/#/restart-policies---restart
     Name: on-failure # no|always|unless-stopped are valid options. on-failure requires MaximumRetryCount
     MaximumRetryCount: 2 # Max number of time to attempt to restart container/plugin before quitting
```

#### Basic Auth

```yaml
---
plugin:
  type: api
  api_config:
    url: 'http://localhost:4700'
    endpoint: '/endpoint'
    headers: # Enter as normal HTTP headers, Key: Value
      Content-Type: # Set content type
    basic_auth:
      username:
      password:
```

## Config Breakdown
Extensive breakdown of the API config options


{% include links.html %}
