---
title: SLAPI Chat API
keywords: api
last_updated: 'March 30, 2017'
tags: [api]
sidebar: framework_sidebar
permalink: api_chat.html
folder: api
---


# SLAPI Chat Endpoints

SLAPI Currently has 3 Chat specific endpoints, see below for specifics and how to test/use them

## SLAPI Speak
-   Endpoint: `$bot_url/v1/speak`
-   Type: Post
-   Params (All Required):
    -   channel: $channel - The Slack Channel ID (Public Channel Name works, private requires ID)
    -   text: $text - The text that will be posted in the channel, supports formatting

**Examples**

```bash
curl -X POST -d "channel=#integration_tests&text=Hello World!" http://localhost:4567/v1/speak
```

## SLAPI Emote
-   Endpoint: `$bot_url/v1/emote`
-   Type: Post
-   Params (All Required):
    -   channel: $channel - The Slack Channel ID (ID only supported by Emote)
    -   text: $text - The text that will be emoted in the channel

**Examples**

```bash
curl -X POST -d "channel=C445NT42J&text=Hello World!" http://localhost:4567/v1/emote
```

## SLAPI Attachment
For more specifics see [Slack Doc: Message Attachments](https://api.slack.com/docs/message-attachments)

-   Endpoint: `$bot_url/v1/attachment`
-   Type: Post
-   Params:
    -   channel: $channel - The Slack Channel ID (Public Channel Name works, private requires ID)
    -   attachments:
        -   (Required) text: The text that will be posted in the channel
        -   (Required) fallback: Text that shows in popup, not allow to be formatted
        -   (Required) title: Title of Attachment, Shows in room and notification popup
        -   (Optional) title_link: Makes title a clickable url
        -   (Optional) pretext: Optional text that appears above the attachment block
        -   (Optional) color: Sets color of attachment (default green)

**Examples**

```bash
curl -X POST -d "channel=#integration_tests&attachments[text]=hello world&attachments[fallback]=Hello World&attachments[title]=HELLO WORLD" http://localhost:4567/v1/attachment
```


{% include links.html %}
