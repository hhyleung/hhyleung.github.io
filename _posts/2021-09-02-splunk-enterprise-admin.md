---
title: "Splunk Enterprise Admin"
excerpt: "For SPLK 1003 Splunk Enterprise Certified Admin"
last_modified_at: 2021-09-02
toc: true
toc_label: "Content"
toc_sticky: true
categories:
  - Cheatsheets
tags:
  - Splunk
---

## Key points
- Post install: `splunk enable boot-start -user <username>`
- Diag: server spec + `$SPLUNK_HOME/etc`
- Add-on: contains reusable component supporting other apps and has no web UI
- Only one retention policy per index
- Integrity of index / bucket: `splunk check-integrity`

## Directory
- `$SPLUNK_HOME`: `/opt/splunk`
- `$SPLUNK_HOME/bin`: executables (for `splunk` commands)
- `$SPLUNK_HOME/etc`: licenses, config, apps
- `$SPLUNK_HOME/var/lib/splunk`: indexes (`$SPLUNK_DB`)

## Default ports
- `splunkd`: 8089
- Splunk web: 8000
- Web app-server proxy: 8065
- KV store: 8191

## Licenses
- Under `$SPLUNK_HOME/etc/licenses`
- Enterprise license: full functionality with no-enforcement license
- Trial license: valid for 60 days, same as enterprise license with 500 MB/day limit
- Free license: 500 MB/day without alerts, scheduled searches, authentication, clustering, distributed search, summarisation, and forwarding to non-Splunk servers
- Forwarder license: sets the server up as a heavy forwarder
- Violation: after 5 warnings in a rolling 30-day period
- Does not count as license quota:
    - Replicated data (Index Clusters)
    - Summary indexes
    - Splunk internal logs (_internal, _audit)
    - Structural components of an index (metadata, tsidx)

## Apps
- Can be visible or hidden
- `splunk remove app` to delete app and dependencies
- Permissions:
    - Read: use app, add KO, modify KOs they own
    - Write: share KOs they own, delete KOs used in the app

## Configuration files
- Case sensitive with `[stanza]` and `attribute = value` format
- `outputs.conf`: where to forward date
- `props.conf`: parsing, field extractions, lookups
- `inputs.conf`: what data is collected
- Conflict priority: global context (index time) > app/user context (search time)
- Global context: user independent tasks
    - Precedence: `etc/system/local` > `etc/apps/<app>/local` > `etc/apps/<app>/default` > `etc/system/default`
- App/user context: user related activity
    - Precedence: `etc/users/<user>/<app>/local` > `etc/apps/<app>/local` > `etc/apps/<app>/default` > `etc/system/local` > `etc/system/default`
- Best practice: store config at `etc/apps/<app>/local` instead of `etc/system/local`
- Validate on-disk config: `splunk btool <conf> list`
    - `--debug` to show config location
    - `--user=<user> --app=<app>` to see user/app context layering 
- Validate in-memory config: `splunk show config <conf>`
- Force reload config at `http://<server>:<port>/debug/refresh`
- Reload all config by restarting `splunk restart`

### `indexes.conf`
- Number of hot buckets: `maxHotBuckets`
    - Default: `3`
    - Best practice: `10`
- Age of hot buckets: `maxHotSpanSecs`
- Bucket size: `maxDataSize`
    - `auto` = 750 MB
    - `auto_high_volume` = 10 GB
- Number of warm buckets: `maxWarmDBCount`
- Directory size: `homePath.maxDataSizeMB`, `coldPath.maxDataSizeMB`
- Max index size: `maxTotalDataSizeMB`
- Retention limit: `frozenTimePeriodInSecs`
- Default non-existent index: `lastChangeIndex` (default to empty, drop events)
- Volumes for fast (hot and warm) and slow (cold)

```
[volume:<volume>]
path = <path>
maxVolumeDataSizeMB = <MB>

[<index>]
homePath = volume:<volume>/<path>
homePath.maxDataSizeMB = <MB>
```

### `authorize.conf`
- Should not modify `$SPLUNK_HOME/etc/system/default/authorize.conf`
- Modify locals `$SPLUNK_HOME/etc/system/local` or `$SPLUNK_HOME/etc/apps/<app>/local`
- Stanza: `[role_<role>]`
- Grant owned roles only: `edit_roles_grantable`

## Indexes
- `_internal`: Splunk's own logs and metrics
- `_audit`: Splunk audit trails and optional audit
- `_introspection`: track system performance
- `_thefishbucket`: checkpoint information for file monitoring inputs
- `summary`: default index for summary
- `main`: default index for inputs

## Buckets
- Hot: read/write
    - Stored in Home Path
    - Roll over when max bucket size or time span reached or indexer restarted
- Warm: read only with time range in name
    - Stored in Home Path
    - Roll over when max Home Path size (default unconstrained) or max warm bucket count (default 300)
- Cold: read only and same name as warm bucket
    - Stored in Cold Path
    - Deleted when all events exceed retention limit (default 6 years) or max index size (default 500 GB)
- Frozen: optional, not searchable but can be brought back to thawed
    - Restore: copy bucket from frozen path to thawed path and `splunk rebuild <thawedPath>`

## Index management
- Fishbucket: track monitored input files
- Mark event as deleted and stop showing up from searches: `| delete` with `can_delete` role
- Delete all event from index: `splunk clean [eventdata|userdata|all] -index <index>`
- Reset fishbucket: `splunk cmd btprobe -d $SPLUNK_DB/fishbucket/splunk_private_db --file <file> --reset`
- Reset all sources:
    - `splunk clean eventdata -index _thefishbucket`
    - `rm -r $SPLUNK_DB/fishbucket`

## Users
- User password at `$SPLUNK_HOME/etc/passwd`
    - Blank file disables native authentication
- Non-native authentication: LDAP, SAML, RADIUS (script)
    - Can only change time zone and default app
- Unlock user: `splunk edit user <user> -locked-out false -auth <admin:password>`
- Setup admin password: `splunk start --accept-license --answer-yes --no-prompt --seed-passwd <password>`
- Random admin password: `splunk start --accept-license --answer-yes --no-prompt --gen-and-print-passwd`

## Study resources
- Splunk Enterprise System Administration: <https://www.splunk.com/en_us/training/courses/splunk-enterprise-system-administration.html>
- Splunk Enterprise Data Administration: <https://www.splunk.com/en_us/training/courses/splunk-enterprise-data-administration.html>
- Exam dump: <https://www.examtopics.com/exams/splunk/splk-1003>

## Exam
- Study time: 5 half days of virtual training
- Exam time: 21 minutes
- Result: PASS
