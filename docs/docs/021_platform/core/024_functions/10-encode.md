---
sidebar_label: encode
---

# encode(string)

### Input
string - string

### Output
string - URL encoded string

### Example
```yaml
actions:
- name: trigger-slack
  condition:
  - type: equals
  value: keep.encode('abc def')
  compare_to: 'abc%20def'
  compare_type: eq
```
