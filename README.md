# README

## Comparison

Here are some keys that _seem_ similar between [some zap exports](https://github.com/toddmoy/node-based-zap-examples/tree/master/set-1) and [ZDL 0.2](https://github.com/zapier/zdl/blob/master/version_0.2.md). At this time, don't assume similar sounding things are definitely the same.

| 0.2               | Export            | Notes                                                   |
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

**Other**

- Curly syntax looks like it might differ a bit. Will we "upgrade" old zaps to the new syntax?
