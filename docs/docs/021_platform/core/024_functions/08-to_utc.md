---
sidebar_label: to_utc
---

# to_utc

### Input
datetime.datetime | str

### Output
datetime.datetime - utc converted

### Example
```yaml
actions:
- name: trigger-slack
  condition:
  - type: threshold
  # datetime_compare(t1, t2) compares t1-t2 and returns the diff in hours
  #   utcnow() returns the local machine datetime in UTC
  #   to_utc() converts a datetime to UTC
  value: keep.datetime_compare(keep.utcnow(), keep.to_utc("{{ steps.this.results[0][0] }}"))
  compare_to: 1 # hours
  compare_type: gt # greater than
```
