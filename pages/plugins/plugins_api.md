---
title: API Plugins
keywords: 'getting_started, plugins'
last_updated: 'March 27, 2017'
tags:
  - getting_started
  - plugins
sidebar: framework_sidebar
permalink: plugins_api.html
folder: plugins
---

# Overview

3rd and most advanced level of plugin. Can be managed by SLAPI or completely separate.

## API Plugin Basics

### Info Endpoint

This is an endpoint that SLAPI can query to get plugin information and commands to setup routing and the help list with.

Here is all the information the info endpoint can contain.

```json
{
    "help": {
        "arg01": "arg description",
        "arg02": "arg description"
    }
}
```

-   Required Info Items

    -   help: this is what we build the help list off of for `@bot help plugin`

### Command Endpoint

This is the endpoint that is posted to from the bot with the chat data

-   Endpoint is completely configurable, right now SLAPI only supports 1 to 1 config. (1 Endpoint to 1 Plugin)
-   JSON Payload from SLAPI:
```json
    {
        "chat":
        {
          "type":"message",
          "channel":"C77777MMM",
          "user":"U66666NNN",
          "text":"\u003c@U66666NNN\u003e plugin_name plugin_arg",
          "ts":"1484927050.000300",
          "team":"T88888BBB"
        },
        "command": "plugin_arg"
    }
```
-   Gives the option of just running the `plugin_arg` from `@bot plugin_name plugin_arg` or sorting through the entire data

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
    Image: 'SLAPI/SLAPIn-test:api' # Enter user/repo (standard docker pull procedures), you can also pull from a private repo via domain.com/repo
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
    -   plugin_name: same as the `plugin_name.yml`. See [api spec fixture config](https://github.com/ImperialLabs/SLAPI/blob/api_plugin/spec/fixtures/plugins/api.yml) for working example.
    -   Treat the `plugin_name` folder as a regular docker folder. See [api spec fixture directory](https://github.com/ImperialLabs/SLAPI/tree/api_plugin/spec/fixtures/plugins/api) for a working example.

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
Extensive breakdown of the API Type config options

-   See [here](https://imperiallabs.github.io/plugins_script.html#config-breakdown)) for General Config Options
-   See [here](https://imperiallabs.github.io/plugins_container.html#config-breakdown) for Docker/Container Specific Config Options

### API Config Options
-   Plugin Level: `plugin:`
    -   Type Setting; This lets SLAPI know the type of plugin being loaded
        -   `type: 'api'`
    -   Managed Setting; This will let SLAPI know if it's a plugin that it's suppose to start/manage
        -   `managed: true`; `true` for letting SLAPI know to manage the plugin or `false` to just let it be aware of it
    -   Build Setting; This will have SLAPI build from a Dockefile (see [here]() for more info)
    -   Mount Config Setting; Allows mounting the same config SLAPI uses to build plugin inside plugin container
        -   `mount_config: '/api/api.yml'` # Path to config inside container, Will check if not nil and will mount if this exists into
-   API Config Level (Nested Under Plugin): `api_config:`
    -   Endpoint Setting:
        -   `endpoint: '/endpoint'`; This is a configurable endpoint for the SLAPI to post the [json payload](#command-endpoint) to
        -   `url: 'http://localhost:4700'`; Only required for un-managed API setups. This lets the bot know the base URI for the plugin
        -   Header Config Level: SLAPI will iterate over any key value under this hash to create the headers for HTTParty to use, below are some common use examples
            -   `Content-Type: 'application/json'`; Just set the key/value exactly how you would for any header data. Right now only JSON is the supported content type or no content (ruby type hash)
            -   `Authorization: 'Token "token=sdf9u3jnf9sj3r"'`; You can pass any support Authorization type into this header.
-   Container Config Level (Nested Under Plugin): `config:`; This is for managed API plugins and configure the container
    -   Host Config Setting: `HostConfig:`; This is the most important and only require setting for a manged API Plugin
        -   Port Bindings: You can use any port (except SLAPI or Brain (Redis) ports), The `0.0.0.0` is required though or it will not be accessible by the bot
            ```yaml
            PortBindings:
              4700/tcp:
                -
                  HostIp: '0.0.0.0'
                  HostPort: '4700'
            ```



{% include links.html %}
