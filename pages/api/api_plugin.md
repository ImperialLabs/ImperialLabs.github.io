---
title: SLAPI Plugin API
keywords: api
last_updated: 'March 30, 2017'
tags: [api]
sidebar: framework_sidebar
permalink: api_plugin.html
folder: api
---

# SLAPI Plugin Endpoints

SLAPI only has 1 Plugin specific endpoint. These type of endpoints will enable to access or manage the plugins via API

## SLAPI Reload

-   Endpoint: `$bot_url/ping`
-   Type: Post
-   Params: none
-   Returns: `it worked`

**Examples**

```bash
curl -X POST http://localhost:4567/reload
```
