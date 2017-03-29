---
title: Step By Step - Common
keywords: 'getting_started, quick start'
last_updated: 'March 29, 2017'
tags:
  - step-by-step
  - framework
sidebar: framework_sidebar
permalink: common_start.html
folder: quick_start
---

# SLAPI: Step By Step Guide

## Common Steps

Regardless of how you start the bot, these tasks will be identical

### Interact

So you have your bot connected? What do you do now?

Let's try a few things. (replace `@bot` with whatever you named your bot)

-   Check that your bot is working - `@bot ping`
    {% include image.html file="bot_ping.png" %}
-   See what plugins are installed = `@bot help`
    {% include image.html file="bot_help_empty.png" %}

Hmm, seems like we're a little bland eh? Let's try something more advanced.

### Get SLAPIN!

The bot is on and it's responding. Let's add a little something to it.

Leave the bot running for this whole process, no need to restart it.

-   Take the following code and put it in the file `./config/plugins/hello.yml`, this is what we refer to as a [Script](https://imperiallabs.github.io/plugins_script.html) type plugin.

    ```yaml
    plugin:
        type: script
        language: bash
        listen_type: passive
        help:
          world: "Says Hello World!"
        description: "simple hello world"
        write: |
          #!/bin/bash
          if [ "${1}" == 'world' ]; then
              echo 'Hello World!'
          else
              echo 'No World for You!'
          fi
    ```

Alright! our first plugin, or as we call them. SLAPINS!

Now go back to chat and run the following

-   `@bot reload`
    {% include image.html file="bot_reload.png" %}
-   Lets try `@bot help` again
    {% include image.html file="bot_help.png" %}
-   Oh, there's a plugin now. Lets try it! `@bot hello`
    {% include image.html file="bot_hello.png" %}
-   Eh, my bad. Maybe I should read the instructions
-   Lets dig into the help and see what it can do `@bot help hello`
    {% include image.html file="bot_help_arg.png" %}
-   Ahh, so.. it helps to read instructions. Try `@bot hello world`
    {% include image.html file="bot_hello_world.png" %}

What?! How easy was that? The built in reload option will let you add plugins on the fly or update them right from the chat room.

### What's Next?

This is where the step by step ends for now.

We are working on more documentation and plugins to cover.

We will also have a roadmap showing what upcoming and in what order for SLAPI. Until then, kick the tires and think about turning your favorite cli tool into a SLAPIN or make your own from scratch!

See the [Plugins](https://imperiallabs.github.io/plugins_landing.html) section to get started

{% include links.html %}
