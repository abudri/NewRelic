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

### Level 1: Learning the Ropes

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

### Level 2: Controlling Your Data

There may also be scenarios in which you need percentages instead of counts, sums, or averages. Using the `percentage()` function allows you to calculate the percentage of a value in the data set that matches a specified condition. This function takes two arguments: the first is an aggregator function for your desired attribute, such as `count()`. The second is a `WHERE` condition to specify the subset of data you'd like to query.

In this sample query, we are finding the percentage of transactions over the last day that had a duration (or response time) greater than 100 milliseconds.

`SELECT percentage(count(*), WHERE duration > 0.1) FROM Transaction SINCE 1 day ago` - From [Level 2, Section 2]

<img src="https://user-images.githubusercontent.com/17362519/116712228-a2bc2480-a9a1-11eb-8a59-187e626c2cdf.png" width="850;" />

It's very common to view application performance and/or customer experience data using percentiles rather than averages. With the `percentile()` function we can understand the experience of the *nth* percentile.

For example, let's say we want to know what the worst experience (highest duration) of 98% of our customers is today. We can ask NRDB for `percentile(duration, 98)` from the last 24 hours:

`SELECT percentile(duration, 98) FROM Transaction SINCE 1 day ago` - From [Level 2, Section 2]

<img src="https://user-images.githubusercontent.com/17362519/116712820-3b52a480-a9a2-11eb-8772-5644f2d495f9.png" width="850;" />

### Level 3: Advancing Your Dashboard

`filter()` is a powerful tool that allows you to aggregate multiple data points in a single query, offering more control over which events are included in function results. In this example, we use `filter()` to return the separate values for total transactions, total web transactions, and total non-web transactions:

`SELECT count(*) as 'All Transactions', filter(count(*), where transactionType ='Web') as 'Web Transactions', filter(count(*), where transactionType !='Web') as 'Non-Web Transactions' from Transaction since 24 hours ago` 

<img src="https://user-images.githubusercontent.com/17362519/116723946-0b110300-a9ae-11eb-9db5-9f493fd2152b.png" width="850;" />

Since it returns a number, you can also perform math on its results. For example, we can divide total web transactions by all transactions to determine what percent of transaction were web transactions:

`SELECT (filter(count(*), where transactionType ='Web') / count(*)) * 100 as 'Percent web' from Transaction since 24 hours ago`

<img src="https://user-images.githubusercontent.com/17362519/116724071-309e0c80-a9ae-11eb-98fa-8e5600b9b87a.png" width="850;" />

As you learned in previous lessons, `FACET` is a great way to both segment your data, and understand it from differently grouped perspectives (such as seeing average response time based on different response codes). When you use `FACET`, NRDB organizes data into groups based on the values of provided attributes. But what if you wanted to group multiple values together, such as HTTP response codes 200, 201, etc.?

`FACET CASES()` solves for this issue by allowing you to choose how facet buckets are broken out. The operator takes any number of parameters in the format "`WHERE attr OP value`". In the example below we've categorized all transactions with response code starting with "2" into a "2xx Responses" bucket. We could also do this for 3xx, 4xx, and 5xx response codes to group our data in ways that increase readability and help us understand what's happening in our application(s

`SELECT count(*) from Transaction FACET CASES(where response.status LIKE '2%' OR httpResponseCode LIKE '2%', where response.status LIKE '3%' OR httpResponseCode LIKE '3%', where response.status LIKE '4%' OR httpResponseCode LIKE '4%', where response.status LIKE '5%' OR httpResponseCode LIKE '5%')` - [Level 3, Section 4]

<img src="https://user-images.githubusercontent.com/17362519/116725877-8bd0fe80-a9b0-11eb-9855-b75e5c158f9c.png" width="850;" />

As you can see, these groupings are useful but difficult to read. Let's clean them up using something we learned in level 2 of this course:

`SELECT count(*) from Transaction FACET CASES(where response.status LIKE '2%' OR httpResponseCode LIKE '2%' as '2xx Responses', where response.status LIKE '3%' OR httpResponseCode LIKE '3%' as '3xx Responses', where response.status LIKE '4%' OR httpResponseCode LIKE '4%' as '4xx Responses', where response.status LIKE '5%' OR httpResponseCode LIKE '5%' as '5xx Responses')`

<img src="https://user-images.githubusercontent.com/17362519/116725984-ac995400-a9b0-11eb-8890-e31c653e2dd4.png" width="850;" />

#### Section 5

So far, we've made queries that pull data from a single source. But what if you want to plot 2 data points that are stored as two different event types? Querying NRDB data is not limited to a single event type! To query from multiple event types you can include each event type seperated by a comma.

`SELECT count(*) as 'Combined Events' FROM Transaction, PageView SINCE 1 day ago` 

<img src="https://user-images.githubusercontent.com/17362519/116727365-74931080-a9b2-11eb-99fa-2f629e0034a4.png" width="850;" />

To make this even more useful, the `eventType()` function tells us which event type a record is from. We can use this to control our data output. In this example, we see the total number of *Transaction* and *PageView* events combined, as well as the totals for only *Transaction* and *PageView*.

`SELECT count(*) as 'Combined Events', filter(count(*), WHERE eventType() = 'PageView') as 'Page Views', filter(count(*), WHERE eventType()='Transaction') as 'Transactions' FROM Transaction, PageView SINCE 1 day ago`

<img src="https://user-images.githubusercontent.com/17362519/116727562-b9b74280-a9b2-11eb-9c10-d9be81c73633.png" width="850;" />

Let's look at this in more detail: `count(*)` is the total number of both Transaction and PageView events. However, we can use the aggregator function `filter()` we recently learned about to do something unique. We tell it `WHERE eventType()='PageView'`. This invokes the filter function to observe the event type as part of the total result set, then filter to display only those specific events. We can even add `TIMESERIES` to visualize 2 directly comparable data points on a line graph.

`SELECT count(*) as 'Combined Events', filter(count(*), WHERE eventType() = 'PageView') as 'Page Views', filter(count(*), WHERE eventType()='Transaction') as 'Transactions' FROM Transaction, PageView SINCE 1 day ago TIMESERIES max`

<img src="https://user-images.githubusercontent.com/17362519/116727785-03079200-a9b3-11eb-84cd-cd8e47ceef24.png" width="850;" />

### Level 4: NRQL Power User

#### Section 6

**Nested aggregation**
NRQL does not support the type of joins used in traditional SQL databases. However, you can write nested aggregation queries that resemble sub queries. This allows you to answer questions such as:

How many requests per minute did my application handle, and what was the maximum rate of requests per minute in the last hour?
What is the average CPU usage of all my servers, and which specific servers are over 90%?
What percentage of all user sessions bounced immediately (i.e. only one PageView in the session)?
Let's explore each of these use cases in more detail.

Example 1 - Max RPM for Last Hour
First we count the number of transactions per minute over the last hour. There is nothing new here. This returns 60 data points on a graph:

`SELECT count(*) AS rpm FROM Transaction TIMESERIES 1 MINUTE`

<img src="https://user-images.githubusercontent.com/17362519/116728689-37c81900-a9b4-11eb-94b2-0a1bb831b366.png" width="850;" />

