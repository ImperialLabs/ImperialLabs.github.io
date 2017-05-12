---
title: API Plugins
keywords: 'getting_started, plugins'
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
    headers: # Enter as normal HTTP headers, Key: Value
      Content-Type: # Set content type
      Authorization: # Use for tokens
  config:
    Image: 'SLAPI/slapin-test:api' # Enter user/repo (standard docker pull procedures), you can also pull from a private repo via domain.com/repo
    HostConfig:
      PortBindings:
        4700/tcp:
          -
            HostIp: '0.0.0.0'
            HostPort: '4700'
```

#### Dockerfile Build

This option will allow an API plugin to be managed and built from a Dockerfile.

-   Endpoints:
    -   info: provides help data about plugin; see [info endpoint](#info-endpoint) section for more info
    -   command: endpoint to pass all the plugin commands to, configurable see endpoint setting below (i.e. `@bot plugin_name do_something`)
-   Plugin Config Location: `config/plugins/plugin_name.yml`
    -   plugin_name: whatever name you wish your plugin to be accessed as. (i.e.; `@bot plugin_name`)
-   Docker File Location: `config/plugins/plugin_name/Dockerfile`
    -   plugin_name: same as the `plugin_name.yml`. See [api spec fixture config](https://github.com/ImperialLabs/slapi/blob/master/spec/fixtures/plugins/api.yml) for working example.
    -   Treat the `plugin_name` folder as a regular docker folder. See [api spec fixture directory](https://github.com/ImperialLabs/slapi/tree/master/spec/fixtures/plugins/api) for a working example.

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
    -   **Type Setting**
        -   This lets SLAPI know the type of plugin being loaded
        -   Default: `nil`
        -   Setting:

            ```yaml
            type: 'api'
            ```

    -   **Managed Setting**
        -   This will let SLAPI know if it's a plugin that it's suppose to start/manage
        -   `true` for letting SLAPI know to manage the plugin or `false` to just let it be aware of it
        -   Default: `false`
        -   Setting:

            ```yaml
            managed: true
            ```

    -   **Build Setting**
        -   This will have SLAPI build from a Dockefile
        -   `true` to be a from Dockerfile or `false` to pull image
        -   Default: `false`
        -   Setting:

            ```yaml
            build: true
            ```
    -   **Mount Config Setting**
        -   Allows mounting the same config SLAPI uses to build plugin inside plugin container
        -   Path configured is for container side only, it will mount the current plugin config to the container under that path for the plugin to use
        -   Default: `nil`
        -   Setting:

            ```yaml
            mount_config: '/api/api.yml'
            ```

-   **API Config Level** - All of these settings are nested  under

    ```yaml
    Plugin:
       api_config:
    ```

    -   **Endpoint Setting**
        -   This is a configurable endpoint for the SLAPI to post the [json payload](#command-endpoint) to
        -   Default: `nil`
        -   Setting:
            ```yaml
            endpoint: '/endpoint'
            ```
    -   **URL Setting**    
        -   Only required for un-managed API setups. This lets the bot know the base URI for the plugin
        -   Default: `nil`
        -   Setting:

            ```yaml
            url: 'http://localhost:4700'
            ```

    -   **Basic Auth Setting**
        -   If you wish to use basic auth, just configure it under `api_config`
        -   Default: `nil`
        -   Setting:

            ```yaml
            basic_auth:
              username:
              password:
            ```

    -   **Header Config Level** - All of these settings are nested under

          ```yaml
          Plugin:
             api_config:
               headers:
          ```
        -   SLAPI will iterate over any key value under this hash to create the headers for HTTParty to use, below are some common use examples
            -   **Content Type Setting**
                -   Just set the key/value exactly how you would for any header data. Right now only JSON is the supported content type or no content (ruby type hash)
                -   Default: `nil`
                -   Setting:
                    ```yaml
                    Content-Type: 'application/json'
                    ```
            -   **Authorization Setting**
                -   You can pass any support Authorization type into this header.
                -   Default: `nil`
                -   Setting:

                    ```yaml
                    Authorization: 'Token "token=sdf9u3jnf9sj3r"'
                    ```

-   **Container Config Level** - All of these settings are nested  under
-   **Note**: This is for managed Container plugins

    ```yaml
    Plugin:
       config:
    ```

    -   **Image Setting**
        -   Set `user/repo` to pull from Dockerhub, use 3rd party/private but entering the entire url (e.g.; `domain.com/repo`), or use local build with just simple `repo` name
        -   Default: `nil`
        -   Setting:

            ```yaml
            Image: 'slapi/schedules'
            ```

    -   **Host Config Setting**
        -   All of these settings are nested under (see below) and these directly affect the container

            ```yaml
            Plugin:
               config:
                 HostConfig:
            ```

            -   **Port Bindings Setting**
                -   You can use any port (except SLAPI or Brain (Redis) ports), The `0.0.0.0` is required though or it will not be accessible by the bot
                -   Default: `nil`
                -   Settings:

                    ```yaml
                    PortBindings:
                      8080/tcp:
                        -
                          HostIp: '0.0.0.0'
                          HostPort: '8080'
                    ```


{% include links.html %}
