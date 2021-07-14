---
title: "Splunk Power User"
excerpt: "For SPLK 1002 Splunk Core Certified Power User"
last_modified_at: 2021-07-13
---

## Key points
- Boolean order: `NOT` -> `OR` -> `AND`
- Filter efficiency: time range -> `index` -> `source` -> `host` -> `sourcetype`
- Interesting fields: in at least 20% of resulting events
- Buckets: raw data + metadata (`source`, `sourcetype`, `host`) + index files
- Workflow action: GET, POST, search
- Event types will be ordered by priority
- Apply order: field extraction -> field alias -> lookup
- Tags are field/value pairs that make data more understandable
- Default deployed with search and home app
- Jobs are available for 10 mins by default, should schedule report for longer lifetime
- Zooming in and out the timeline re-executes the search, click and drag does not
- Splunk Cloud is Splunk Enterprise as a scalable service
- Premium enhanced solutions: user behaviour analytics, IT service intelligence, enterprise security

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

# Commands
### `top` and `rare`
- Returns 10 results by default
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

### `stats`
- `count`: number of events
    - `as`: rename column
    - `(field)`: field with value
    - `by`: number of each combination
- `distinct_count(field)`, `dc(field)`: number of unique values of field
- `sum(field)`: sum of numeric values
- `avg(field)`: average of numeric values
- `list(field)`: all values of field
- `values(field)`: unique values of field

### `transaction`
- Events related by one or more fields
- Limits to 1000 events by default
- Adds fields `duration` and `eventcount`
- Used when event grouping is based on start/end values
- All events must be related by one or more fields
- `maxspan`: max total time between earliest and latest events
- `maxpause`: max time between events in a transaction

### `chart` and `timechart`
- Bubble chart: visualise 3 dimensional series, size of the bubble is the third dimension
- Trellis layout: multiple charts based on one result set
- `chart <y-axis> over <x-axis> by series` = `chart <y-axis> by <x-axis>, <series>`
- `timechart count by` series
	- x-axis: `_time`
	- `span=15m`: group by 15 minutes 
- Show top 10 results and group remaining into OTHER
	- `useother=f`: hide OTHER series
	- `usenull=f`: hide NULL series
- `limit=0`: unlimited series

### Others
- `dedup` remove duplicates
- `search`: behaves exactly like search strings before the first pipe
- `fillnull` defaults to `0`
- `@` round down to nearest time unit
- `!=` field must have value, `NOT` includes those without value (null or field does not exist at all)
- Case sensitive: boolean operators, field names, field values from lookup, regular expressions, `eval`, `where`, tags
- Transforming commands: `top`, `rare`, `chart`, `timechart`, `stats`, `geostats`
- `eval`: calculated fields must be based on extracted fields
- `eval`'s `tostring()`: hex, commas, duration
- Search field tag: `tag::<field>=<tagname>`
- `search` only compare one field, `where` can compare different fields
- `stats` fast and more efficient than `transaction`, especially in larger environments
- `datamodel` returns all fields, `from` returns specified fields only

## Macro
- Configured in Advanced Search
- `` `<macroname>` `` to call macro
- Macro name: `<name>(<no of argument>)`
- Arguments: `$<argument>$`
- Argument name: `<argument>`
- Validation: `isnum($<argument>$)` validates argument to be a number

## Field Extractor (FX)
- Delimiters: tabs, pipes, commas, spaces
- Auto identification: Event Actions > Extract Fields
- Require option: include events with the required string only
- Extracted fields persist as knowledge objects
- Field extraction cannot be edited in UI after manually editing a regex

## Pivot and data model
- Data models provide the datasets for pivots
- Pivot: creates data visualisation from data model
- Data model: events + search + transaction datasets
- `datamodel <datamodel> <dataset> <search mode>`
- Root event dataset: constraints + fields

## CIM (Common Information Model)
- Methodology to normalise data
- Includes pre-configured data models and automatic data model acceleration
- Acceleration is turned off by default
- Uses field extractions, field aliases, event types, tags, lookups
- Examples: alerts, authentication, databases, email

## Search mode
- Fast: performance over completeness
	- Non-transforming:  events (required fields only, no interesting fields) and patterns
	- Transforming: statistics or visualisations
- Smart: default
	- Non-transforming: events (all fields) and pattern
	- Transforming: statistics or visualisations
- Verbose: completeness over performance
	- Non-transforming: events (all fields) and pattern
	- Transforming: events and patterns and statistics or visualisations

## Job inspector
- Header: time to run and no. of events scanned
- Execution costs: cost to retrieve results
	- `command.search.index`: time to search the index for the location to read in rawdata files
	- `command.search.filter`: time to filter out events that do not match
	- `command.search.rawdata`: time to read events from the rawdata files
- Search job properties: performance = `scanCount` / `time`

## Study resources
- Splunk Fundamentals 1: <https://www.splunk.com/en_us/training/courses/splunk-fundamentals-1.html>
- Splunk Fundamentals 2: <https://www.splunk.com/en_us/training/courses/splunk-fundamentals-2.html>
- Exam dump: <https://www.examtopics.com/exams/splunk/splk-1002/>

## Exam
- Study time: 8 hours
- Exam time: 16 minutes
- Result: PASS
