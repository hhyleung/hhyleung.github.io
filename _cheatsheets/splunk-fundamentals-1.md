---
title: "Splunk Fundamentals 1"
date: 2021-01-23
excerpt: "Splunk Fundamentals 1 Course Cheatsheet"
---
# Key points
- boolean order: `NOT` -> `OR` -> `AND`
- deployed with search and home app
- `top` and `rare` return 10 results
- field names are case sensitive, field values are not
- `@` round down to nearest time unit
- jobs are available for 10 mins by default, should schedule report for longer lifetime
- interesting fields: in at least 20% of resulting events
- `!=` must have value, `NOT` includes those without value (null or field does not exist at all)
- `dedup` remove duplicates
- Splunk Cloud is Splunk Enterprise as a scalable service
- Premium enhanced solutions: user behaviour analytics, IT service intelligence, enterprise security
- Zooming in and out re-executes the search, click and dragging does not

# Components
- Indexer: process and index data, includes license meter
- Search head: search indexed data
- Forwarder: send data
    - Heavy forwarder: can parse data and send event-based data to indexers
- Deployment server: distribute to search head cluster
- Cluster master
    - Search head cluster: at least 3 search heads
    - Index cluster: traditional vs non-replicating
- License master

# Color coding
- <span style="color:orange">Orange</span>: boolean `OR` and command modifier `by`
- <span style="color:blue">Blue</span>: command `stats`
- <span style="color:green">Green</span>: command argument `span`
- <span style="color:purple">Purple</span>: function `sum`

# `top` and `rare`
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


# `stats`
- `count`: number of events
    - `as`: rename column
    - `(field)`: field with value
    - `by`: number of each combination
- `distinct_count(field)`, `dc(field)`: number of unique values of field
- `sum(field)`: sum of numeric values
- `avg(field)`: average of numeric values
- `list(field)`: all values of field
- `values(field)`: unique values of field
