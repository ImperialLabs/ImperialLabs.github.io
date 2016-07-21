---
title: API Framework
keywords: getting_started, api
last_updated: July 21, 2016
tags: [api]
sidebar: framework_sidebar
permalink: api_framework.html
folder: api
---

## Framework Speak

```json
{
    "framework": {
        "speak": "Command Response"
    }
}
```

## Framework Emote

```json

{
    "framework": {
        "emote": "Push Information"
    }
}
```

## Framework Formatted

Utilize Slack's Message Formatting (see doc [here](https://api.slack.com/docs/message-formatting))

### Markdown Formatted

See example output [here](https://api.slack.com/docs/messages/builder?msg=%7B%0A%20%20%22text%22%3A%20%22*bold*%20%60code%60%20_italic_%20~strike~%22%2C%0A%20%20%22username%22%3A%20%22markdownbot%22%2C%0A%20%20%22mrkdwn%22%3A%20true%0A%7D)

```json
{
    "framework": {
        "formatted": "*bold* `code` _italic_ ~strike~"
    }
}
```

### Attachment Formatted

See example output [here](https://api.slack.com/docs/messages/builder?msg=%7B%0A%20%20%20%20%22attachments%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22title%22%3A%20%22Title%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22pretext%22%3A%20%22Pretext%20_supports_%20mrkdwn%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22text%22%3A%20%22Testing%20*right%20now!*%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22mrkdwn_in%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22text%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22pretext%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%5D%0A%7D)

```json
{
    "framework": {
        "attachment": {
            "title": "Title",
            "pretext": "Pretext _supports_ mrkdwn",
            "text": "Testing *right now!*",
            "mrkdwn_in": [
                "text",
                "pretext"
            ]
        }
    }
}
```

{% include links.html %}
