---
title: SLAPI - Test Cases
keywords: getting_started, testing
last_updated: July 12, 2017
tags: [testing]
sidebar: framework_sidebar
permalink: test_cases.html
folder: testing
---

## Testing

This section covers every situation we test or plan to test for

## Test Cases

Below are all the individual tests that exist or need to be created

### API
-   Chat
    -   Success Tests
        -   Utilize Speak Endpoint Successfully
        -   Utilize Attachment Endpoint Successfully
        -   Utilize Emote Endpoint Successfully
    -   Fail Tests
        -   Provide Incorrect Params for Speak Endpoint
        -   Provide Incorrect Params for Attachment Endpoint
        -   Provide Incorrect Params for Emote Endpoint
-   Plugins
    -   Success Tests
        -   Utilize reload Endpoint Successfully
    -   Fail Tests
        -   None currently
-   Brain
    -   Success Tests
        -   Successfully save data via save Endpoint
        -   Successfully search hashes via search_hash Endpoint
        -   Successfully search key via search_key Endpoint
        -   Successfully delete data via delete Endpoint
    -   Fail Tests
        -   Try to save incomplete data
        -   Try to search non-existent hashes
        -   Try to search non-existent key
        -   Try to delete non-existent data

### Plugins
-   Script Based
    -   Success Tests
    -   Fail Tests
-   Container Based
    -   Success Tests
    -   Fail Tests
-   API Based
    -   Success Tests
    -   Fail Tests

### Brain
**Note:** Need to determine if having both API and Unit testing is appropriate, API may test thoroughly enough
-   Success Tests
    -   Successfully save data via save method
    -   Successfully search hashes via search_hash method
    -   Successfully search key via search_key method
    -   Successfully delete data via delete method
-   Fail Tests
    -   Try to save incomplete data
    -   Try to search non-existent hashes
    -   Try to search non-existent key
    -   Try to delete non-existent data

### User Interaction
-   Plugins
    -   Success Tests
    -   Fail Tests
-   Help
    -   Success Tests
    -   Fail Tests
-   Functions
    -   Success Tests
    -   Fail Tests

```

{% include links.html %}
