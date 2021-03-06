---
title: Plugins Advanced
keywords: 'plugins'
tags:
  - plugins
sidebar: framework_sidebar
permalink: plugins_advanced.html
folder: plugins
---

# Overview

Below are items that most likely only used in advanced or unique situations.

# Additional Plugin Config

## Container Config Level

These settings apply to both Container and API plugin (if managed) types

You can use any option available to the [Docker API Client](https://github.com/swipely/docker-api) that fits under config/host config. The following list is just the settings we found most likely used.

-   All of these settings are nested under

    ```yaml
    Plugin:
       config:
    ```

    -   **TTY Setting**
        -   Set true/false for container TTY
        -   Default: `true`
        -   Settings:

            ```yaml
            Tty: false
            ```

    -   **User Setting**
        -   Set user in container to run commands as
        -   Default: `nil`
        -   Setting:

            ```yaml
            User: user
            ```

    -   **Volumes Setting**
        -   Set volumes to attach to container
        -   Default: `nil`
        -   Setting:

            ```yaml
            Volumes:
              - '/from/host:/to/container'
            ```

    -   **Working Directory Setting**
        -   Change working directory inside container
        -   Default: Dockerfile/Image setting
        -   Setting:

            ```yaml
            WorkingDir: '/path/to/dir'
            ```

-   Example of these options in the plugin yml config

    ```yaml
    config:
      Tty: true
      User: user
      Volumes:
        - '/from/host:/to/container'
      WorkingDir: '/path/to/dir'
    ```

## Host Config Level

-   All of these settings are nested under (see below) and these directly affect the container

    ```yaml
    Plugin:
       config:
         HostConfig:
    ```

    -   **DNS Setting**
        -   Change DNS Servers for container
        -   Default: Docker Default
        -   Setting:

            ```yaml
            Dns:
              - 8.8.8.8
              - 8.8.4.4
            ```

    -   **DNS Search Setting**
        -   Sets the domain names that are searched when a bare unqualified hostname is used inside of the container
        -   Default: Docker Default
        -   Setting:

            ```yaml
            DnsSearch:
              - google.com
              - domain.com
            ```

    -   **Extra Hosts Setting**
        -   Adds hosts to /etc/hosts in container
        -   Default: Docker Default
        -   Setting:

            ```yaml
            ExtraHosts:
              - "hostname:127.0.0.1"
            ```

    -   **Links Setting**
        -   Using this option as you run a container gives the new container’s /etc/hosts an extra entry named ALIAS that points to the IP address of the container identified by CONTAINER_NAME_or_ID
        -   Default: Docker Default
        -   Setting:

            ```yaml
            Links:
              - 'container:hello'
            ```

    -   **Publish All Ports Setting**
        -   True/False Publish all exposed ports to the host interfaces
        -   Default: Docker Default
        -   Setting:

            ```yaml
            PublishAllPorts: true
            ```

    -   **Restart Policy Setting**
        -   <https://docs.docker.com/engine/reference/run/#/restart-policies---restart>
        -   Default:
            ```yaml
            RestartPolicy:
              Name: on-failure
              MaximumRetryCount: 2
            ```
        -   Setting:

            ```yaml
            RestartPolicy:
              Name: on-failure # no|always|unless-stopped are valid options. on-failure requires MaximumRetryCount
              MaximumRetryCount: 0 # Max number of time to attempt to restart container/plugin before quiting
            ```

    -   **Read Only Root FS Setting**
        -   True/False to make Root Filesystem read only
        -   Default: Docker Default
        -   Setting:

            ```yaml
            ReadonlyRootfs: false
            ```

    -   **Volumes From Setting**
        -   Volume From other Docker Containers
        -   Default: Docker Default

            ```yaml
            VolumesFrom:
              - container1
              - container2
            ```

-   Example of these options in the plugin yml config

    ```yaml
    config:
      HostConfig:
        Dns:
          - 8.8.8.8
          - 8.8.4.4
        ExtraHosts:
          - "hostname:127.0.0.1"
        Links:
          - 'container:hello'
        NetworkMode: host
        PublishAllPorts: true
        RestartPolicy:
         Name: on-failure
         MaximumRetryCount:
        ReadonlyRootfs: false
        VolumesFrom:
          - container1
          - container2
    ```

{% include links.html %}
