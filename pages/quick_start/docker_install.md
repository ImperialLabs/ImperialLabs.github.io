---
title: Step By Step - Docker Install
keywords: 'getting_started, quick start'
last_updated: 'March 29, 2017'
tags:
  - step-by-step
  - docker
sidebar: framework_sidebar
permalink: docker_install.html
folder: quick_start
---

# Docker Install

Due to some of the features used, SLAPI requires docker 1.10 or later installed.

You will also need Docker Compose 1.8 or greater if planning on using the compose files

-   Website: <https://www.docker.com/>

## Install

-   All OS Docs: <https://docs.docker.com/engine/installation/#platform-support-matrix>

-   Docker Machine Install: <https://docs.docker.com/machine/install-machine/>
    -   Required to run Containers
-   Docker Compose Install: <https://docs.docker.com/compose/install/>
    -   Required to setup DinD Host and SLAPI with Compose Files

## Important Info

If the user that is running the SLAPI bot can't run docker (i.e.; run `docker ps` with user) then SLAPI will fail to start in local mode.

-   These instructions will show you how to create a Docker group and fix this issue <https://docs.docker.com/engine/installation/linux/linux-postinstall/>

{% include links.html %}
