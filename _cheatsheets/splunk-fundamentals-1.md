---
title: "Splunk Fundamentals 1"
excerpt: "For Splunk Core Certified User"
last_modified_at: 2021-01-23
tags:
  - Splunk
---

## Key points
- boolean order: `NOT` -> `OR` -> `AND`
- default deployed with search and home app
- `top` and `rare` return 10 results
- field names are case sensitive, field values are not
- `@` round down to nearest time unit
- jobs are available for 10 mins by default, should schedule report for longer lifetime
- interesting fields: in at least 20% of resulting events
- `!=` field must have value, `NOT` includes those without value (null or field does not exist at all)
- `dedup` remove duplicates
- zooming in and out the timeline re-executes the search, click and drag does not
- Splunk Cloud is Splunk Enterprise as a scalable service
- premium enhanced solutions: user behaviour analytics, IT service intelligence, enterprise security

## Splunk components
- Indexer: process and index data, includes license meter
- Search head: search indexed data
- Forwarder: send data
    - Heavy forwarder: can parse data and send event-based data to indexers
- Deployment server: distribute to search head cluster
- Cluster master
    - Search head cluster: at least 3 search heads
    - Index cluster: traditional vs non-replicating
- License master

## Syntax colouring
- <span style="color:#F78B21">Orange</span>: booleans `OR` and command modifiers `by`
- <span style="color:#1F5CFF">Blue</span>: commands `stats`
- <span style="color:#5CA301">Green</span>: command arguments `span`
- <span style="color:#D100D3">Purple</span>: functions `sum`

## `top` and `rare` commands
- `limit`: number of results
    - default: `10`
    - `=0`: returns unlimited results
- `countfield`: number of events
    - default: "count"
    - `="string"`: rename column
- `showperc`: percentage of events
    - default: `t`
    - `=f` to disable
- `by`: split result
    - user `by` game: top users for each game
    - game `by` user: top games for each user

## `stats` command
- `count`: number of events
    - `as`: rename column
    - `(field)`: field with value
    - `by`: number of each combination
- `distinct_count(field)`, `dc(field)`: number of unique values of field
- `sum(field)`: sum of numeric values
- `avg(field)`: average of numeric values
- `list(field)`: all values of field
- `values(field)`: unique values of field

## Study resources
- <https://education.splunk.com/course/splunk-7x-fundamentals-part-1-elearning>
- <https://www.examtopics.com/exams/splunk/splk-1001/>
