## dbt Event Logging
> :warning: **ADDING THIS PACKAGE TO YOUR DBT PROJECT CAN SIGNIFICANTLY SLOW
DOWN YOUR DBT RUNS**. This is due to the number of insert statements executed by
this package, especially as a post-hook. Please consider if this package is
appropriate for your use case before using it.


Requires dbt >= 0.12.2

This package provides out-of-the-box functionality to log events for all dbt
invocations, including run start, run end, model start, and model end. It
outputs all data and models to schema `[target.schema]_meta`. There are three
convenience models to make it easier to parse the event log data.

### Setup

1. Include this package in your `packages.yml` -- check [here](https://hub.getdbt.com/fishtown-analytics/logging/latest/)
for installation instructions.
2. Include the following in your `dbt_project.yml` directly within your
`models:` block (making sure to handle indenting appropriately):

```YAML
# dbt_project.yml
...

models:
  ...
  pre-hook: "{{ logging.log_model_start_event() }}"
  post-hook: "{{ logging.log_model_end_event() }}"
```

That's it! You'll now have a stream of events for all dbt invocations in your
warehouse.

### Adapter support
This package is currently compatible with dbt's Snowflake, Redshift, and
Postgres integrations.
