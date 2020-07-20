# README

## Comparison

| 0.2 K             | Export  K         | Notes                                                   |
|:------------------|:------------------|:--------------------------------------------------------|
| app               | selected_api      |                                                         |
| -                 | paused            |                                                         |
| action            | action            |                                                         |
| -                 | meta              | validations, selectedGives, parammap                    |
| -                 | tripleStores      |                                                         |
| authentication_id | authentication_id | Syntax differs                                          |
| -                 | title             |                                                         |
| params            | params            |                                                         |
| id                | id                | Syntax differs                                          |
| -                 | root_id           | Usage of `id` in 0.2 might render this unnecessary?     |
| -                 | parent_id         |                                                         |
| steps             | nodes             | Steps are an array, nodes are a hash                    |
| type              | type_of           |                                                         |
| action            | action            | Meaning might slightly differ. See `series_skip_errors` |

