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

## Container Type Plugin

You have several options when it comes to containers. We are utilizing the [Docker API](https://github.com/swipely/docker-api#containers) Library and anything under `config:` will be passed without any alteration into the Container Creation.

### Data From Chat

SLAPI will break down commands from chat in a couple different ways so you can utilize them in plugins.

-   Simple Data - Default Toggle - Chat Text Breakdown
    -   SLAPI breaks the text into an array based on spaces
        -   The following `@bot say hello world` becomes
            -   **note** File would be saved in `./config/plugins/say.yml` for this example
            -   Dropped from Exec Data: `@bot`
            -   Plugin Name: `say`
            -   ARG 01: `hello`
            -   ARG 02: `world`
    -   The exception to this rule is items in `" "` **double quotes**, it will ignore the spaces for those items and consider anything in **double quotes** as a single arg
        -   The following `@bot say "hello world"` becomes
            -   **note** File would be saved in `./config/plugins/say.yml` for this example
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
        image: 'username/plugin' # Required
```

### All Available Options

All the options you can set when using a container.

-   Example of file `schedules.yml` **Note**: This needs to be accessed for formatting, changes made as they are found

```yaml
plugin:
  type: container
  managed: true # Choose True or False for SLAPI management
  listen_type: passive # Choose passive or active.
  message_data: true # True/False to accept the message data from who sent a message
  mount_config: '/schedules/config/schedules.yml' # Path to config inside container, Will check if not nil and will mount if this exists into container
  config:
    Image: 'slapi/schedules' # Enter user/repo (standard docker pull procedures), you can also pull from a private repo via domain.com/repo
    Labels:
      arg01: "arg01 does this"
      arg02: "arg02 does this"
    Cmd: # if you wish to override the container command
    Entrypoint: # if you wish to override the container entrypoint
    Env: # List of environment variables
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
        -   This lets SLAPI know the type of plugin being loaded
        -   Setting:

            ```yaml
            type: 'container'
            ```

    -   **Listen Type Setting**
        -   This lets SLAPI know if the container being used is a one time run (build, run, print output, delete) or a persistent plugin (build, start, forward exec data, print output)
        -   SLAPI will recognize `active` for persistent/active plugin or `passive` for disposable run at exec plugins
        -   Setting:

            ```yaml
            listen_type: 'passive'
            ```

    -   **Managed Setting**
        -   This will let SLAPI know if it's a plugin that it's suppose to start/manage
        -   `true` for letting SLAPI know to manage the plugin or `false` to just let it be aware of it
        -   Setting:

            ```yaml
            managed: true
            ```

    -   **Build Setting**
        -   This will have SLAPI build from a Dockefile
        -   `true` to be a from Dockerfile or `false`(default) to pull image
        -   Setting:

            ```yaml
            build: true
            ```

    -   **Mount Config Setting**
        -   Allows mounting the same config SLAPI uses to build plugin inside plugin container
        -   Path to config inside container, Will check if not nil and will mount if this exists into
        -   Setting:

            ```yaml
            mount_config: '/container/container.yml'
            ```

-   **Container Config Level** - All of these settings are nested  under

    ```yaml
    Plugin:
       config:
    ```

-   **Note**: This is for managed Container plugins
    -   **Image Setting**
        -   Set `user/repo` to pull from Dockerhub, use 3rd party/private but entering the entire url (e.g.; `domain.com/repo`), or use local build with just simple `repo` name
        -   Setting:

            ```yaml
            Image: 'slapi/schedules'
            ```

    -   **Label Setting**
        -   Optional: Labels is what SLAPI uses to build out the help list for `@bot help` & `@bot help plugin`
        -   `Labels: #nested hash`; You can enter the labels here or inside the container See [here](https://github.com/ImperialLabs/slapi/blob/master/examples/Dockerfile) for Dockerfile example or below for config example
        -   Setting:

            ```yaml
            Labels:
              arg01: "description"
              arg02: "description"
            ```

    -   **Entrypoint Settings**
        -   If you wish to override the container entrypoint
        -   Setting:

            ```yaml
            Entrypoint: /path/to/script.sh
            ```

    -   **Environment Settings**
        -   Sets exported environment variables inside plugin container
        -   `Env: # nested array`; List of environment variables, see below for example
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
                -   You can use any port (except SLAPI or Brain (Redis) ports), The `0.0.0.0` is required though or it will not be accessible by the bot
                -   Settings:

                    ```yaml
                    PortBindings:
                      8080/tcp:
                        -
                          HostIp: '0.0.0.0'
                          HostPort: '8080'
                    ```

{% include links.html %}
