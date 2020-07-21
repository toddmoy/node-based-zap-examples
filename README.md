# README

I randomly exported some Zaps and peeked at what the json contained. 


## Comparison

Here are some keys that _seem_ similar between [some node-based exports](https://github.com/toddmoy/node-based-zap-examples/tree/master/set-1) and [ZDL 0.2](https://github.com/zapier/zdl/blob/master/version_0.2.md). At this time, don't assume similar sounding things are _definitely_ the same.

| 0.2               | Nodes             | Notes                                                   |
|:------------------|:------------------|:--------------------------------------------------------|
| -                 | meta              | validations, selectedGives, parammap                    |
| -                 | parent_id         |                                                         |
| -                 | paused            |                                                         |
| -                 | root_id           | Usage of `id` in 0.2 might render this unnecessary?     |
| -                 | title             |                                                         |
| -                 | tripleStores      |                                                         |
| action            | action            | Meaning might slightly differ. See `series_skip_errors` |
| app               | selected_api      |                                                         |
| authentication_id | authentication_id | Syntax differs                                          |
| id                | id                | Syntax differs                                          |
| params            | params            |                                                         |
| steps             | nodes             | Steps are an array, nodes are a hash                    |
| type              | type_of           |                                                         |
| comment           | -                 |                                                         |
| zdl_version       | -                 |                                                         |


## `meta`

Contains content like: 

```
"meta": {
  "selectedGives": { "74319203__ts": "Ts" },
  "parammap": { "thread_ts": "", "channel": "design" },
  "validation": {
    "action": { "is_opened": true },
    "params": {
      "is_valid": true,
      "invalid_mappings": {},
      "is_edited": true,
      "is_opened": true
    },
    "webhook": { "is_opened": false }
  },
  "stepTitle": "One Day Reminder (Thread)"
},
```

## `triple_stores`

Contains content like: 

```
"triple_stores": {
  "copied_from": null,
  "created_by": null,
  "polling_interval_override": 0,
  "block_and_release_limit_override": 0,
  "spread_tasks": 1
},
```

## `parent_id`, `root_id`
  
It looks like these are used to define the execution path. Both may be `null` or an integer of another step. 

I think 0.2 intuits the dependency graph, which might be the reason we don't see these explicit keys. 


## Curlies

There seems to be syntactical differences in how a curlie / reference is constructed. Both embed an `id` of another step, but 0.2 seems to use alphanumeric ids whereas node-based curlies use integers. There may be differences in the use of underscores and dashes, though it does seem `__` is used by both to separate ids from field names.

[0.2 curlie](https://github.com/zapier/zdl/blob/master/version_0.2.md#using-curlies-to-reference-step-outputs-in-params):

`{{weather_trigger__summary}}`

Node-based curlie: 

`{{8__start__dateTime_pretty}}`

> Will existing Zaps need to be modded to use the new syntax? 
> Is the Editor responsible for ensuring the uniqueness of `step_id`s? 
