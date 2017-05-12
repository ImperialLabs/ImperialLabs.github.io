---
title: Container Plugin
keywords: 'getting_started, plugins'
last_updated: 'March 30, 2017'
tags:
  - getting_started
  - plugins
sidebar: framework_sidebar
permalink: plugins_container.html
folder: plugins
---

# Overview

The 2nd level of plugins is a completely containerized container using docker.

## Container Plugin Basics

You have several options when it comes to containers. We are utilizing the [Docker API](https://github.com/swipely/docker-api#containers) Library and anything under `config:` will be passed without any alteration into the Container Creation.

### Data From Chat

SLAPI will break down commands from chat in a couple different ways so you can utilize them in plugins.

-   Simple Data - Default Toggle - Chat Text Breakdown
    -   SLAPI breaks the text into an array based on spaces
        -   The following `@bot say hello world` becomes
            -   **Note**: File would be saved in `./config/plugins/say.yml` for this example
            -   Dropped from Exec Data: `@bot`
            -   Plugin Name: `say`
            -   ARG 01: `hello`
            -   ARG 02: `world`
    -   The exception to this rule is items in `" "` **double quotes**, it will ignore the spaces for those items and consider anything in **double quotes** as a single arg
        -   The following `@bot say "hello world"` becomes
            -   **Note**: File would be saved in `./config/plugins/say.yml` for this example
            -   Dropped from Exec Data: `@bot`
            -   Plugin Name: `say`
            -   ARG 01: `hello world`
    -   So taking this knowledge, this would function like doing
        -   `docker exec -it say hello world`
    -   This is why having an Entrypoint inside the container is very important.
        -   Having the Entrypoint `bash /scripts/say.sh`
        -   Would make having the entire exec above look like `bash /scripts/say.sh hello world`
-   Advanced Data - Configurable Toggle - Full JSON Payload
    -   The following JSON payload is passed into the container Exec

        ```json
        {
          "type":"message",
          "channel":"C77777MMM",
          "user":"U66666NNN",
          "text":"\u003c@U66666NNN\u003e say hello world",
          "ts":"1484927050.000300",
          "team":"T88888BBB"
        }
        ```

### Minimum Requirements

This is the baseline, the absolute minimum to configure to use a container based plugin.

-   Example of file `on_call.yml`
-   Pulls from DockerHub

```yaml
plugin:
  type: docker
  config:
    image: 'username/plugin'
```

### Managed
Setting up container plugins as managed means SLAPI will maintain that plugin completely, it will manage the configuration via the `plugin_name.yml` file and start/stop the plugin with SLAPI

### Un-Managed
Setting up an Un-Managed container plugin means SLAPI will only execute against that plugin but will not manage configuration or starting/stoping of that plugin

**Requirements**
To utilize an un-managed plugin, it will need to be running on the same Dockerhost as the other SLAPI plugins (managed or un-managed) so it can exec commands against that container

### All Available Options

All the options you can set when using a container.

-   Example of file `schedules.yml` **Note**: This needs to be accessed for formatting, changes made as they are found
-   See [Config Breakdown](#config-breakdown) Section for explanations of settings

```yaml
plugin:
  type: container
  managed: true
  listen_type: passive
  message_data: true
  mount_config: '/schedules/config/schedules.yml'
  config:
    Image: 'slapi/schedules'
    Labels:
      arg01: "arg01 does this"
      arg02: "arg02 does this"
    Cmd:
    Entrypoint:
    Env:
      - API='1u3042034'
      - SERVICE='123490ijkd'
    HostConfig:
      PortBindings:
        8080/tcp:
          -
            HostIp: '0.0.0.0'
            HostPort: '8080'
```

## Config Breakdown
Extensive breakdown of the Container Type config options

-   See [here](https://imperiallabs.github.io/plugins_script.html#config-breakdown) for General Config Options

### Docker/Container Config Options
-   **Plugin Level**: `plugin:`
    -   **Type Setting**
        -   Required: Yes
        -   This lets SLAPI know the type of plugin being loaded
        -   Default: `nil`
        -   Setting:

            ```yaml
            type: 'container'
            ```

    -   **Listen Type Setting**
        -   Required: No
        -   This lets SLAPI know if the container being used is a one time run (build, run, print output, delete) or a persistent plugin (build, start, forward exec data, print output)
        -   SLAPI will recognize `active` for persistent/active plugin or `passive` for disposable run at exec plugins
        -   Default: `passive`
        -   Setting:

            ```yaml
            listen_type: 'passive'
            ```

    -   **Managed Setting**
        -   Required: No
        -   This will let SLAPI know if it's a plugin that it's suppose to start/manage
        -   `true` for letting SLAPI know to manage the plugin or `false` to just let it be aware of it
        -   Default: `true`
        -   Setting:

            ```yaml
            managed: true
            ```

    -   **Build Setting**
        -   Required: No
        -   This will have SLAPI build from a Dockefile
        -   `true` to be a from Dockerfile or `false` to pull image
        -   Default: `false`
        -   Setting:

            ```yaml
            build: true
            ```

    -   **Mount Config Setting**
        -   Required: No
        -   Allows mounting the same config SLAPI uses to build plugin inside plugin container
        -   Path configured is for container side only, it will mount the current plugin config to the container under that path for the plugin to use
        -   Default: `nil`
        -   Setting:

            ```yaml
            mount_config: '/container/container.yml'
            ```

-   **Container Config Level** - All of these settings are nested under
-   **Note**: This is for Managed Container plugins only

    ```yaml
    Plugin:
       config:
    ```

    -   **Image Setting**
        -   Required: Yes
        -   Set `user/repo` to pull from Dockerhub, use 3rd party/private but entering the entire url (e.g.; `domain.com/repo`), or use local build with just simple `repo` name
        -   Default: `nil`
        -   Setting:

            ```yaml
            Image: 'slapi/schedules'
            ```

    -   **Label Setting**
        -   Required: No
        -   Labels are what SLAPI uses to build out the help list for `@bot help` & `@bot help plugin`
        -   `Labels: #nested hash`; You can enter the labels here or inside the container See [here](https://github.com/ImperialLabs/slapi/blob/master/examples/Dockerfile) for Dockerfile example or below for config example
        -   Default: `nil`
        -   Setting:

            ```yaml
            Labels:
              arg01: "description"
              arg02: "description"
            ```

    -   **Entrypoint Settings**
        -   Required: No
        -   If you wish to override the container entrypoint
        -   Default: Image Default or `nil`
        -   Setting:

            ```yaml
            Entrypoint: /path/to/script.sh
            ```

    -   **Environment Settings**
        -   Required: No
        -   Sets exported environment variables inside plugin container
        -   `Env: # nested array`; List of environment variables, see below for example
        -   Default: `nil`
        -   Setting:

            ```yaml
            Env:
              - API='1u3042034'
              - SERVICE='123490ijkd'
            ```

    -   **Host Config Setting**
        -   All of these settings are nested under (see below) and these directly affect the container

            ```yaml
            Plugin:
              config:
                HostConfig:
            ```

            -   **Port Bindings Setting**
                -   Required: No
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
