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
        -   Load plugin
    -   Fail Tests
        -   Load plugin with missing requirements
        -   Load plugin with missing script
-   Container Based
    -   Success Tests
        -   Load plugin w/ Image from Dockerhub
        -   Load plugin w/ Image from Dockerfile
    -   Fail Tests
        -   Load plugin w/ Image from bad/missing Dockerfile
-   API Based
    -   Success Tests
        -   Load plugin w/ External Setup
        -   Load plugin w/ Managed Setup
    -   Fail Tests
        -   Test non-responsive External & Managed Plugin

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
-   Open Chat
    -   Plugins
        -   Success Tests (Each plugin type)
            -   Call plugin by name, no args
            -   Call plugin with single arguments
            -   Call plugin with multiple arguments
        -   Fail Tests (Each plugin type)
            -   Call non-existing plugin
            -   Call plugin with incorrect arguments
            -   Call plugin as a Bot user
    -   Help
        -   Success Tests
            -   Call help with Tier 1 listing
            -   Call help with Tier 2 listing
            -   Call Help with DM response
            -   Call help for specific plugin
        -   Fail Tests
            -   Call help for non-existing plugin
    -   Built-In Functions
        -   Success Tests
            -   Call ping command
            -   Call reload command
        -   Fail Tests
            -   N/A
-   Direct Message 
    -   All Open Chat Tests
    -   All Open Chat tests without @bot

{% include links.html %}
