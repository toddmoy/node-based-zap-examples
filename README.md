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


## Notes

### `meta`

Contains content like: 

```
"meta": {
  "selectedGives": {},
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
  "parammap": { "time_unit": "", "calendarid": "#design Calendar" },
  "stepTitle": "Trigger One Day Before Event"
}
```

### `triple_stores`

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

**Other**

- Curly syntax looks like it might differ a bit. Will we "upgrade" old zaps to the new syntax?
