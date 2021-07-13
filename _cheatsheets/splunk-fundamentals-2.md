---
title: "Splunk Fundamentals 2"
excerpt: "For SPLK 1002 Splunk Core Certified Power User"
last_modified_at: 2021-07-13
---

## Key points
- Filter efficiency: time range -> `index` -> `source` -> `host` -> `sourcetype`
- Case sensitive: boolean operators, field names, field values from lookup, regular expressions, `eval`, `where`, tags
- Buckets: raw data + metadata (`source`, `sourcetype`, `host`) + index files
- Transforming commands: `top`, `rare`, `chart`, `timechart`, `stats`, `geostats`
- Search field tag: `tag::<field>=<tagname>`
- Workflow action: GET, POST, search
- `search` only compare one field, `where` can compare different fields
- Data models: events + search + transaction datasets
- `datamodel <datamodel> <dataset> <search mode>`
- `datamodel` returns all fields, `from` returns specified fields only
- Event types will be ordered by priority
- Apply order: field extraction -> field alias -> lookup
- `stats` is more efficient than `transaction`
- Calculated fields must be based on extracted fields

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

## `chart` and `timechart` commands
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

## `transaction` command
- Limits to 1000 events by default
- Adds fields `duration` and `eventcount`
- Used when event grouping is based on start/end values
- All events must be related by one or more fields
- `maxspan`: max total time between earliest and latest events
- `maxpause`: max time between events

## Macro
- `` `<macroname>` `` to call macro
- Macro name: `<name>(<no of argument>)`
- Arguments: `$<argument>$`
- Validation: `isnum($<argument>$)` validates argument to be a number

## Study resources
- Splunk Fundamentals 2: <https://www.splunk.com/en_us/training/courses/splunk-fundamentals-2.html>
- Exam dump: <https://www.examtopics.com/exams/splunk/splk-1002/>

## Exam
- Study time: 5 hours
- Exam time: 16 minutes
- Result: PASS
