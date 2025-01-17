---
sidebar_label: What is a function?
sidebar_position: 1
---

# + Functions

## What is a Function?
| :exclamation:  To use a keep function, prefix it with `keep.`, for example, use `keep.len` and not `len`  :exclamation: |
|-----------------------------------------|

In Keep's context, functions extend the power of context injection.

For example, if a step returns a list, you can use the `keep.len` function to count and use the number of results instead of the actual results.


```yaml
condition:
- type: threshold
  # Use the len of the results instead of the results
  value:  "keep.len({{ steps.db-no-space.results }})"
  compare_to: 10
```

## How to create a new function?

Keep functions are designed to be easily extendible!<br />
To create a new function, all you have to do is to add it to the [functions](https://github.com/keephq/keep/blob/main/keep/functions/__init__.py) directory `__init__.py` file.
