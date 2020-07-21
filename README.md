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

I'm not sure what this is used for. It doesn't seem to be sample data and I don't think it's modifiable in the UI. It contains content like: 

```
"triple_stores": {
  "copied_from": null,
  "created_by": null,
  "polling_interval_override": 0,
  "block_and_release_limit_override": 0,
  "spread_tasks": 1
},
```

## `id`, `parent_id`, `root_id`
  
It looks like these are used to define the execution path. Values are either `null` or an integer referencing a `step_id`. 

I think 0.2 intuits the dependency graph, which might be the reason we don't see these explicit keys. 

> [0.1 RFC](https://docs.google.com/document/d/1x7qSOrOUSsGOGIs5c0NoZpBVrgNySla3su-DK1wVbsI/edit#): _ The id property is optional, and it can be user-defined. (Or defined by a tool like the editor.) There's no requirement to retrieve an id from the server for each task like there is with nodes in the current model ... You can also see that there is no explicit graph here. There is no children_ids or parent_id or similar pointer from one task to another. Instead, the data flow is implicit based on the nesting and the ordering characteristics determined by parent tasks._

**Questions**

- Assume we have a Zap with multiple actions, none of which reference each other via curlies. In this situation, there's no dependency-based ordering we can intuit. Do we assume that the order from the `steps` array is how it should be presented in the editor? Does the engine execute in that order too? I'm thinking about delay step, for example.


## Curlies

There seems to be syntactical differences in how a [curlie / reference](https://github.com/zapier/zdl/blob/master/version_0.2.md#using-curlies-to-reference-step-outputs-in-params) is constructed. Both embed an `id` of another step, but 0.2 seems to use alphanumeric ids whereas node-based curlies use integers. There may be differences in the use of underscores and dashes, though it does seem `__` is used by both to separate ids from field names.

| 0.2                            | Node                            |
|:-------------------------------|:--------------------------------|
| `{{weather_trigger__summary}}` | `{{8__start__dateTime_pretty}}` |

**Questions**

- Will existing Zaps need to be modded to use the new syntax? 
- Is the Editor responsible for ensuring the uniqueness of `step_id`s? 

## `paused`

Node-based steps contain a `paused` boolean. What's this used for? 

## `type` vs `type_of`

Node based steps contain a `type_of` key that contains a value like: `read`, `write`, `filter`. In O.2, it seems the equivalent step key is `type`. Is this accurate? 

## `app` vs `selected_api`

Both of these seem to define the vendor app to be used. Is this accurate? 

## `authentication_id`

The syntax for these values might be different. One looks like a hexidecimal string and the other an integer.

| 0.2        | Node                                                               |
|:-----------|:-------------------------------------------------------------------|
| `16231265` | `8259fdb1e0119a59d6fe35bea72f640e8a2afa2ae8a6e7ac6130386b44a9d604` |

## Array vs Hash

0.2 defines `steps` as an array whereas node-based Zaps defined `nodes` in a dictionary/hash. Does this introduce any challenges for Editor? 

## `params`

These look similar across both 0.2 and node-based zaps. Note: the examples are not 1:1 comparisons.

0.2: 

```
"params": {
  "as_bot": "yes",
  "add_edit_link": "yes",
  "unfurl": "yes",
  "link_names": "yes",
  "reply_broadcast": "no",
  "channel": "CHTQUD329",
  "text": "Today's forecast: {{weather_trigger__summary}}"
}
```

Nodes:

```
"params": {
  "unfurl": "false",
  "thread_ts": "{{11__ts}}",
  "as_bot": "yes",
  "icon": ":full_moon:",
  "add_edit_link": "true",
  "channel": "C024Y16JP",
  "reply_broadcast": "no",
  "username": "BigGroup™ Bot",
  "link_names": "yes",
  "text": "In 1 day, we'll all meet together as a BigGroup™ \n\nThis is a time to get feedback, brainstorm, get help with tedious work, discuss tools/techniques, do a retro, etc.\n\nThere is a different leader each week who will bring something to the group. @ev will be posting who the leader is here shortly. If he's OOO - please refer to the schedule here https://coda.io/d/Design-Team_dATDb-6dfPV/Review-Collabs_suB3j#_lu3qc"
},
```

## Nesting & Paths

0.2 introduces a nesting model, which changes the structure of data in Paths. Historically (factcheck me), Nodes represented all steps at the same level of indenture. `parent_id` / `root_id` was used to specify which branches and steps were evaluated. 

## Paths `type`

In 0.2, BranchingAPI is type `filter` and contains embedded filter criteria within `params`. In Nodes, BranchingAPI is type `write` and a Filter app is assumed to be the first step "within" a branch.

**Questions:**

* Any structural changes to this block?



