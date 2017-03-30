---
title: SLAPI Bot API
keywords: api
last_updated: 'March 30, 2017'
tags: [api]
sidebar: framework_sidebar
permalink: api_bot.html
folder: api
---

# SLAPI Bot Endpoints

SLAPI only has 1 Bot specific endpoint. These type of endpoints will enable to access or manage the bot via API

## SLAPI Ping

-   Endpoint: `$bot_url/ping`
-   Type: Get
-   Params: none
-   Returns: `pong`

**Examples**

```bash
curl -X GET http://localhost:4567/ping
```
