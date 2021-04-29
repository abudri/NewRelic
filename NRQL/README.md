# NRQL Query Language - NRQL

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


