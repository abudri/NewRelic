# NRQL Query Language - NRQL

## **What data can you query with NRQL?**

NRQL allows you to query these New Relic data types:

- [Event data](https://docs.newrelic.com/docs/using-new-relic/data/understand-data/new-relic-data-types/#event-data) from all New Relic products, including:
    - [APM events](https://docs.newrelic.com/docs/insights/insights-data-sources/default-data/apm-default-events-insights/), like `Transaction`
    - [Browser monitoring events](https://docs.newrelic.com/docs/insights/insights-data-sources/default-data/browser-default-events-insights/), like `PageView`
    - [Mobile monitoring events](https://docs.newrelic.com/docs/insights/insights-data-sources/default-data/mobile-default-events-insights/), like `Mobile`
    - [Infrastructure events](https://docs.newrelic.com/docs/infrastructure/manage-your-data/data-instrumentation/default-infrastructure-events/), like `ProcessSample`
    - [Synthetics events](https://docs.newrelic.com/docs/insights/insights-data-sources/default-data/synthetics-default-events-insights/), like `SyntheticCheck`
    - Custom events, like those reported by the [Event API](https://docs.newrelic.com/docs/insights/insights-data-sources/custom-data/introduction-event-api/)
- [Metric timeslice data](https://docs.newrelic.com/docs/using-new-relic/data/understand-data/new-relic-data-types/#timeslice-data) (metrics reported by New Relic APM, Browser, and Mobile)
- The `[Metric` data type](https://docs.newrelic.com/docs/using-new-relic/data/understand-data/new-relic-data-types/#metric-time-series) (metrics reported by the Metric API and data sources that use that API)
- The `[Span` data type](https://docs.newrelic.com/docs/using-new-relic/data/understand-data/new-relic-data-types/#trace-data) (distributed tracing data)
- The `[Log` data type](https://docs.newrelic.com/docs/using-new-relic/data/understand-data/new-relic-data-types/#log-data) (data from New Relic Logs)
____

## **Events reported by APM**

[New Relic APM](https://docs.newrelic.com/docs/apm/new-relic-apm/getting-started/) reports [event data](https://docs.newrelic.com/docs/using-new-relic/data/understand-data/new-relic-data-types/#event-data) that appears in some UI displays and is also available for [querying and charting](https://docs.newrelic.com/docs/using-new-relic/data/understand-data/query-new-relic-data/). Select an event name in the following table to see its attributes.

* **[Transaction](https://docs.newrelic.com/attribute-dictionary/?attribute_name=&events_tids%5B%5D=8357&event=Transaction)** - 
A transaction is a logical unit of work in a software application. The `Transaction` event includes information about the app, database calls, the duration of the transaction, and any errors that may occur.

* **[TransactionError](https://docs.newrelic.com/attribute-dictionary/?attribute_name=&events_tids%5B%5D=8357&event=TransactionError)** - 
Transaction errors occur when a request throws an exception in the code path that was taken to fill that request. The number of transaction errors does not equal the number of transactions, because you can specify whether you want to [collect, ignore, or mark errors as expected](https://docs.newrelic.com/docs/agents/manage-apm-agents/agent-data/manage-errors-apm-collect-ignore-or-mark-expected/).

* **[Span](https://docs.newrelic.com/attribute-dictionary/?attribute_name=&events_tids%5B%5D=8357&event=Span)** - 
Span events are created when New Relic agents, or other tracing instrumentation tools, instrument operations that are part of a distributed trace. See the definition of span.
____

## [NRQL Lesson App](https://one.newrelic.com/launcher/34b6d49a-d824-4f99-b337-1d9a5467094d.nrql-tutorial-launcher?pane=eyJuZXJkbGV0SWQiOiIzNGI2ZDQ5YS1kODI0LTRmOTktYjMzNy0xZDlhNTQ2NzA5NGQubnJxbC10dXRvcmlhbC1uZXJkbGV0In0=&platform[accountId]=2971796&platform[timeRange][duration]=1800000&platform[$isFallbackTimeRange]=true)

**NRQL** stands for New Relic Query Language. It gives you realtime access to petabytes of Metric, Event, Log, and Trace data in NRDB.

**NRDB** is the database that powers New Relic's Telemetry Data Platform. It is the world's most powerful multi-tenant telemetry database.

**About the data in these lessons**
New Relic One's Telemetry Data Platform allows you to query many sets of data quickly and easily. For the sake of convenience, examples in this tutorial use APM transaction data, because most New Relic customers will have this type of data.If you have access to more than one account, please switch to an account using APM.

You can try every query in this tutorial for yourself, on your own data, using the Chart Builder. This allows you to test what you learn against real live data reporting to your account. Just click the 'Try this query' link beneath any example query to have a go!

____

Every NRQL query must have `SELECT` and `FROM` clauses. You must `SELECT` some data and tell us where it is `FROM`.

`SELECT * FROM Transaction`

![image](https://user-images.githubusercontent.com/17362519/115918640-c2a19480-a445-11eb-8960-f83daf67237b.png)

This returns a lot of results. Each has a timestamp and a collection of attributes. For now, we only want a single result, so we will limit results to a single record using `LIMIT 1`.

![image](https://user-images.githubusercontent.com/17362519/115918619-bb7a8680-a445-11eb-9fda-4c5420a9c86e.png)

When a `LIMIT` is not supplied the default will be used, which is 100 table rows for `SELECT *` queries or 10 aggregated values for `FACET` queries and `SELECT (attributes)` queries. You can specify any limit up to the maximum. Use `LIMIT MAX` to return the maximum number of results possible.

We're now controlling the volume of results we get. But what if we don't want *all* the attributes? What if we would prefer to see only specific data points? Fortunately, like SQL, this can be done in only a few characters. We replace `*` with the name of the attribute(s) we want. In this case, we will ask for the name of a transaction and the duration of time it took.

![image](https://user-images.githubusercontent.com/17362519/115918584-af8ec480-a445-11eb-9252-54f558bd03ed.png)

```SQL
SELECT name, duration FROM Transaction
```

_____

# Query Samples

These are derived during/from the NRQL Lessons app within my New Relic One account, which is a series of lessons on NRQL.

### Lesson 1

Getting the top 5 longest Transactions, along with the HTTP Response Code:

`SELECT max(duration) FROM Transaction FACET name, httpResponseCode LIMIT 5`

<img src="https://user-images.githubusercontent.com/17362519/116704556-8a480c00-a999-11eb-9dec-a8785f8c4384.png" width="850;" />

**`FACET` [Lesson 1, Section 7]**

Often, you'll want to determine the "Top N" values grouped by a specific attribute. In NRQL, you do this using `FACET`. For example, here are the slowest Transaction calls observed on average, grouped by name. We could describe this as "faceted by name". By default, a faceted query will return the _top 10 results_; but you can customize how many results are returned with a `LIMIT`.

`SELECT average(duration) FROM Transaction FACET name, httpResponseCode LIMIT 5`

<img src="https://user-images.githubusercontent.com/17362519/116709736-f8430200-a99e-11eb-91f6-16655d7bfa44.png" width="850;" />

 In this example, we will retrieve the top 5 results displayed on a line chart with `TIMESERIES`: 
 
`SELECT average(duration) FROM Transaction FACET name, httpResponseCode SINCE 3 hours ago LIMIT 5 TIMESERIES`

<img src="https://user-images.githubusercontent.com/17362519/116710113-64be0100-a99f-11eb-8505-df0b148e9cfb.png" width="850;" />

But maybe you don't want a line chart. Perhaps you'd prefer a list of the 20 slowest Transactions. By removing the `TIMESERIES`, we can instead render a bar or pie chart:

<img src="https://user-images.githubusercontent.com/17362519/116710361-ac448d00-a99f-11eb-8048-348b8e003d9b.png" width="850;" />

This query compares the quantity of Web transactions, broken down by individual applications that report to New Relic:

`SELECT count(*) FROM Transaction WHERE transactionType='Web' FACET appName LIMIT 5 SINCE 6 hours ago TIMESERIES`

<img src="https://user-images.githubusercontent.com/17362519/116710548-e01fb280-a99f-11eb-9404-8841d4fed794.png" width="850;" />









