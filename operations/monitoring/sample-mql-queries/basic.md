## Sample MQL queries

#### Fetching a metric
```text
fetch gce_instance
| metric compute.googleapis.com/instance/memory/balloon/ram_used
```

```text
fetch gce_instance::compute.googleapis.com/instance/cpu/utilization

```

#### Filtering

```text
fetch gce_instance
| metric compute.googleapis.com/instance/memory/balloon/ram_used
| filter zone =~ 'us-west1.*'
```

```text
fetch gce_instance::compute.googleapis.com/instance/cpu/utilization
| filter instance_name =~ 'gke.*'
```

#### Grouping
```text
fetch gce_instance::compute.googleapis.com/instance/cpu/utilization
| filter zone =~ 'us-central.*'
| group_by [zone], mean(val())
```

```text
fetch gce_instance
| metric compute.googleapis.com/instance/memory/balloon/ram_used
| filter zone =~ 'us-west1.*'
| group_by [resource.zone], mean(value.ram_used)
```

#### Selecting a time series
```text
fetch gce_instance::compute.googleapis.com/instance/cpu/utilization | top 2 
```

#### Cobining selections
```text
fetch gce_instance::compute.googleapis.com/instance/cpu/utilization
| {
    top 1, max(val())
  ;
    bottom 1, min(val())
  }
| union
```

#### Arithmetic computation
```text
fetch gce_instance
  | metric 'compute.googleapis.com/instance/disk/read_bytes_count'
  | mul(10)
```

#### Outer join
#### Ratios
#### Using group_by and /

## Structure
- start with a fetch
- With pipe build up the query
- Use filter to filter information
- Aggregate information using group by
- Combine multiple queries using { ; } and join operations
