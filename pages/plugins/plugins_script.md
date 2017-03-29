---
title: Script Based Plugins
keywords: 'getting_started, plugins'
last_updated: 'March 27, 2017'
tags:
  - getting_started
  - plugins
sidebar: framework_sidebar
permalink: plugins_script.html
folder: plugins
---

# Overview

In a effort to make the simplest expandable bot possible we have several options when it comes to utilizing plugins

The easiest and lowest entry point into creating a "plugin" for SLAPI.

Just a simple script you wish to run as a bot command.

It will write out the run: | portion into the appropriate file, mount, and run inside a container.

## Plugin w/ Embedded Script

Will take the data from `write: |` and write it out to a file with the plugin name as filename and appropriate language extension

### Minimum Requirements

-   Example of file `on_call.yml`
-   This example uses ruby and will write out to on_call.rb

```yaml
plugin:
  type: script
  language: ruby
  description: "gets on-calls for pagerduty"
  write: >
    #!/usr/bin/env ruby
    # -*- coding: UTF-8 -*-

    require 'httparty'

    API_TOKEN = 'GFd723tgwEbnDcvixPV1'.freeze

    response = HTTParty.get(
    'https://api.pagerduty.com/oncalls',
    headers: {
      'Content-Type' => 'application/json',
      'Accept' => 'application/vnd.pagerduty+json;version=2',
      'Authorization' => "Token token=#{API_TOKEN}"
    }
    )

    puts response.body
```

### All Available Options

-   Example of file `list_schedules.yml`
-   This example uses python and will write out to schedules.py

```yaml
plugin:
  type: script
  language: python
  description: "gets pagerduty schedules for configured account"
  help: # will be used to populate help options for schedules command
    schedules: "gets pagerduty schedules for configured account" # overrides the description set due to being the primary command for plugin.
  write: |
    #!/usr/bin/env python
    import requests

    # Update to match your API key
    API_KEY = '3c3gRvzx7uGfMYEnWKvF'

    # Update to match your chosen parameters
    QUERY = ''


    def list_schedules():
        url = 'https://api.pagerduty.com/schedules'
        headers = {
            'Accept': 'application/vnd.pagerduty+json;version=2',
            'Authorization': 'Token token={token}'.format(token=API_KEY)
        }
        payload = {
            'query': QUERY
        }
        r = requests.get(url, headers=headers, params=payload)
        print 'Status Code: {code}'.format(code=r.status_code)
        print r.json()

    if __name__ == '__main__':
        list_schedules()
```

## Plugin w/ Script Path

Providing a script path will allow SLAPI to just mount and run the desired script in the language container of choice

### Minimum Requirements

- example of file `on_call.yml`

```yaml
plugin:
  type: script
  language: ruby
  description: "gets on-calls for pagerduty"
  path: /path/to/scripts/on_call.rb
```

### All Available Options

- example of file `list_schedules.yml`

```yaml
plugin:
  type: script
  language: python
  description: "gets pagerduty schedules for configured account" # is overrode by the `help:` setting if configured with `command: desc`
  help: # will be used to populate help options for schedules command
    schedules: "gets pagerduty schedules for configured account" # overrides the description set due to being the primary command for plugin.
  path: /path/to/scripts/schedules.py
```

## Usable Languages and Libraries

Docker Image listed below that we utilize to run scripts in and the included 3rd party libraries.

-   Bash/Shell:
    -   Language Setting: `bash`, `shell`, or `sh`

-   Python:
    -   Language Setting: `python` or `py`
    -   DockerHub: <https://hub.docker.com/r/slapi/python/>
    -   Github: <https://github.com/ImperialLabs/docker-python>
    -   Installed Tools & Libraries
        -   [HTTPie](https://github.com/jkbrzt/httpie)
        -   [Arrow](https://github.com/crsmithdev/arrow)
        -   [Requests](https://github.com/kennethreitz/requests)
        -   [awscli](https://github.com/aws/aws-cli)

-   Ruby:
    -   Language Setting: `ruby` or `rb`
    -   DockerHub: <https://hub.docker.com/r/slapi/ruby/>
    -   Github: <https://github.com/ImperialLabs/docker-ruby>
    -   Installed Tools & Libraries
        -   [httparty](http://johnnunemaker.com/httparty/)

-   NodeJS:
    -   Language Setting: `node`, `nodejs`, `javascript`, or `js`
    -   DockerHub: <https://hub.docker.com/r/slapi/nodejs/>
    -   Github: <https://github.com/ImperialLabs/docker-nodejs>
    -   Installed Tools & Libraries
        -   [Request](https://www.npmjs.com/package/request)
        -   [Moment](https://www.npmjs.com/package/moment)
        -   [Node Rest Client](https://www.npmjs.com/package/node-rest-client)

-   PHP: (PENDING)
    -   Installed Tools & Libraries

-   PowerShell: (PENDING)
    -   Installed Tools & Libraries

## Example Code used

-   [Pagerduty Ruby V2 Examples](https://github.com/PagerDuty/API_Ruby_Examples/tree/master/REST_API_v2)
-   [Pagerduty Python V2 Examples](https://github.com/PagerDuty/API_Python_Examples/tree/master/REST_API_v2)

## Config Breakdown
Extensive breakdown of the Script Type config options

-   Plugin Level: `plugin:`
    -   Type Setting; This lets SLAPI know the type of plugin being loaded
        -   `type: 'script'`
    -   Language Setting; This is the setting used to determine the language of the image used. (see [above](#usable-languages-and-libraries) for supported languages)
        -   `language: ruby`
    -   Description Setting: Used to display next to help list of plugin, used as general overview of what plugin does (pending [issue](https://github.com/ImperialLabs/slapi/issues/51))
        -   `description: "gets on-calls for pagerduty"`

{% include links.html %}
