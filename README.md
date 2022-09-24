
# Step 1 - Introduction

# Our Crypto Case Study

For this entire SQL Simplified course we will focus on our Cryptocurrency Trading SQL Case Study!

## Setting the Context

In our fictitious (but realistic) case study - my team of trusted data mentors from the Data With Danny team have been dabbling in the crypto markets since 2017.

Our main purpose for this case study is to analyse the performance of the DWD mentors over time and to "slice and dice" the data in various ways to investigate other questions we might want answers to!

## Our Datasets

All of our data for this case study exists within the `trading` schema as we mentioned in the previous tutorial.

There are 3 data tables available to us in this schema which we can use to run our SQL queries with:

1. `members`
2. `prices`
3. `transactions`

You can inspect each dataset by copying the following code snippet below and running it directly in the SQLPad GUI - please make sure to overwrite any previous queries which are already in the SQL interface!

```sql
SELECT * FROM trading.members;
```

| member_id | first_name |    region     |
| --------- | ---------- | ------------- |
| c4ca42    | Danny      | Australia     |
| c81e72    | Vipul      | United States |
| eccbc8    | Charlie    | United States |
| a87ff6    | Nandita    | United States |
| e4da3b    | Rowan      | United States |
| 167909    | Ayush      | United States |
| 8f14e4    | Alex       | United States |
| c9f0f8    | Abe        | United States |
| 45c48c    | Ben        | Australia     |
| d3d944    | Enoch      | Africa        |
| 6512bd    | Vikram     | India         |
| c20ad4    | Leah       | Asia          |
| c51ce4    | Pavan      | Australia     |
| aab323    | Sonia      | Australia     |
<br>

```sql
SELECT TOP 5 * FROM trading.prices;
```

| ticker | market_date |  price  |  open   |  high   |   low   | volume  | change |
| ------ | ----------- | ------- | ------- | ------- | ------- | ------- | ------ |
| ETH    | 2021-08-29  | 3177.84 | 3243.96 | 3282.21 | 3162.79 | 582.04K | -2.04% |
| ETH    | 2021-08-28  | 3243.90 | 3273.78 | 3284.58 | 3212.24 | 466.21K | -0.91% |
| ETH    | 2021-08-27  | 3273.58 | 3093.78 | 3279.93 | 3063.37 | 839.54K | 5.82%  |
| ETH    | 2021-08-26  | 3093.54 | 3228.03 | 3249.62 | 3057.48 | 118.44K | -4.17% |
| ETH    | 2021-08-25  | 3228.15 | 3172.12 | 3247.43 | 3080.70 | 923.13K | 1.73%  |
<br>

```sql
SELECT TOP 5 * FROM trading.transactions;
```

| txn_id | member_id | ticker |  txn_date  | txn_type | quantity | percentage_fee |      txn_time       |
| ------ | --------- | ------ | ---------- | -------- | -------- | -------------- | ------------------- |
|      1 | c81e72    | BTC    | 2017-01-01 | BUY      |       50 |           0.30 | 2017-01-01 00:00:00 |
|      2 | eccbc8    | BTC    | 2017-01-01 | BUY      |       50 |           0.30 | 2017-01-01 00:00:00 |
|      3 | a87ff6    | BTC    | 2017-01-01 | BUY      |       50 |           0.00 | 2017-01-01 00:00:00 |
|      4 | e4da3b    | BTC    | 2017-01-01 | BUY      |       50 |           0.30 | 2017-01-01 00:00:00 |
|      5 | 167909    | BTC    | 2017-01-01 | BUY      |       50 |           0.30 | 2017-01-01 00:00:00 |


Note: the `TOP 5` in the above queries will return us only the first 5 rows from each dataset.

It is a good practice to always `LIMIT` your queries just in case the tables are huge - you don't want to be trying to return all 5 million rows from a huge table when you are just inspecting the data for the first time!

## A Note on Schemas

Notice above how the "`trading.`" is included before each of our available tables.

If we were to remove this - our database will be unable to find our tables.

This query below will return you an error when ran:

```sql
SELECT * FROM members;
```

> relation "members" does not exist

In realistic scenarios - physical tables will almost always live within a schema and we'll need to reference the schema name to run our queries properly!

# Step 2 - Exploring The Members Data

Let's now inspect our `trading.members` table in a bit more depth.

## Table Records

We can see that there are 3 columns and 14 rows in this dataset:

`SELECT * FROM trading.members;`

| member_id | first_name |    region      |
| --------- | ---------- | -------------- |
| c4ca42    | Danny      | Australia      |
| c81e72    | Vipul      | United States  |
| eccbc8    | Charlie    | United States  |
| a87ff6    | Nandita    | United States  |
| e4da3b    | Rowan      | United States  |
| 167909    | Ayush      | United States  |
| 8f14e4    | Alex       | United States  |
| c9f0f8    | Abe        | United States  |
| 45c48c    | Ben        | Australia      |
| d3d944    | Enoch      | Africa         |
| 6512bd    | Vikram     | India          |
| c20ad4    | Leah       | Asia           |
| c51ce4    | Pavan      | Australia      |
| aab323    | Sonia      | Australia      |
<br>

### Question 1

> Show only the top 5 rows from the `trading.members` table

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT TOP 5 * FROM trading.members;
```

</details>
<br>

| member_id | first_name |    region     |
| --------- | ---------- | ------------- |
| c4ca42    | Danny      | Australia     |
| c81e72    | Vipul      | United States |
| eccbc8    | Charlie    | United States |
| a87ff6    | Nandita    | United States |
| e4da3b    | Rowan      | United States |
<br>

### Question 2

> Sort all the rows in the table by `first_name` in alphabetical order and show the top 3 rows

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT TO5 3 * FROM trading.members
ORDER BY first_name;
```

</details>
<br>

| member_id | first_name |    region     |
| --------- | ---------- | ------------- |
| c9f0f8    | Abe        | United States |
| 8f14e4    | Alex       | United States |
| 167909    | Ayush      | United States |
<br>

### Question 3

> Which records from `trading.members` are from the United States region?

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT * FROM trading.members
WHERE region = 'United States';
```

</details>
<br>

| member_id | first_name |    region     |
| --------- | ---------- | ------------- |
| c81e72    | Vipul      | United States |
| eccbc8    | Charlie    | United States |
| a87ff6    | Nandita    | United States |
| e4da3b    | Rowan      | United States |
| 167909    | Ayush      | United States |
| 8f14e4    | Alex       | United States |
| c9f0f8    | Abe        | United States |
<br>

### Question 4

> Select only the `member_id` and `first_name` columns for members who are not from Australia

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT
  member_id,
  first_name
FROM trading.members
WHERE region != 'Australia';
```

</details>
<br>

| member_id | first_name |
| --------- | ---------- |
| c81e72    | Vipul      |
| eccbc8    | Charlie    |
| a87ff6    | Nandita    |
| e4da3b    | Rowan      |
| 167909    | Ayush      |
| 8f14e4    | Alex       |
| c9f0f8    | Abe        |
| d3d944    | Enoch      |
| 6512bd    | Vikram     |
| c20ad4    | Leah       |
<br>

### Question 5

> Return the unique `region` values from the `trading.members` table and sort the output by reverse alphabetical order

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT DISTINCT region
FROM trading.members
ORDER BY region DESC;
```

</details>
<br>

|    region     | 
| ------------- |
| United States |
| India         |
| Australia     |
| Asia          |
| Africa        |
<br>

### Question 6

> How many mentors are there from Australia or the United States?

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT
  COUNT(*) AS mentor_count
FROM trading.members
WHERE region IN ('Australia', 'United States');
```

</details>
<br>

|  mentor_count |
| ------------- |
|            11 |
<br>

### Question 7

> How many mentors are not from Australia or the United States?

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT
  COUNT(*) AS mentor_count
FROM trading.members
WHERE region NOT IN ('Australia', 'United States');
```

</details>
<br>

| mentor_count |
| ------------ |
|            3 |
<br>

### Question 8

> How many mentors are there per region? Sort the output by regions with the most mentors to the least

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT
  region,
  COUNT(*) AS mentor_count
FROM trading.members
GROUP BY region
ORDER BY mentor_count DESC;
```

</details>
<br>

|    region     | mentor_count |
| ------------- | ------------ |
| United States |            7 |
| Australia     |            4 |
| India         |            1 |
| Africa        |            1 |
| Asia          |            1 |
<br>

### Question 9

> How many US mentors and non US mentors are there?

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT
  CASE
    WHEN region <> 'United States' THEN 'Non US'
    ELSE region
  END AS mentor_region,
  COUNT(*) AS mentor_count
FROM trading.members
GROUP BY mentor_region
ORDER BY mentor_count DESC;
```

</details>
<br>

| mentor_region | mentor_count |
| ------------- | ------------ |
| United States |            7 |
| Non US        |            7 |
<br>

### Question 10

> How many mentors have a first name starting with a letter before `'E'`?

<details>
  <summary>Click here to reveal the solution!</summary>

```sql
SELECT
  COUNT(*) AS mentor_count
FROM trading.members
WHERE LEFT(first_name, 1) < 'E';
```

</details>
<br>

| mentor_count |
| ------------ |
|            6 |
<br>

## Appendix

> `SELECT *`

In practice - always try to return specific columns which you are after and use `SELECT *` sparingly!

> `TOP`

Note that `TOP` is sometimes implemented as `LIMIT` in some database flavours.

One must also be careful when using `TOP` with newer database tools such as BigQuery - although you will only return the number of rows you ask for, BQ is billed by the total number of rows scanned and a `TOP` will not avoid this!

Best practice is to always apply `WHERE` filters on specific partitions where possible to narrow down the amount of data that must be scanned - reducing your query costs and speeding up your query execution!

> `<>` or `!=` for "not equals"

# Step 3 - Daily Prices

Our next dataset to explore will be the `trading.prices` table which contains the daily price and volume data for the 2 cryptocurrency tickers: `ETH` and `BTC` (Ethereum and Bitcoin!)

## View The Data

Before we try to solve our next set of questions below - you can try viewing a few rows from the `trading.prices` dataset:

Example Bitcoin price data:

```sql
SELECT TOP 5 * FROM trading.prices WHERE ticker = 'BTC' ;
```

| ticker | market_date |  price  |  open   |  high   |   low   | volume | change |
| ------ | ----------- | ------- | ------- | ------- | ------- | ------ | ------ |
| BTC    | 2021-08-29  | 48255.0 | 48899.7 | 49621.7 | 48101.9 | 40.96K | -1.31% |
| BTC    | 2021-08-28  | 48897.1 | 49062.8 | 49289.4 | 48428.5 | 36.73K | -0.34% |
| BTC    | 2021-08-27  | 49064.3 | 46830.2 | 49142.0 | 46371.5 | 62.47K | 4.77%  |
| BTC    | 2021-08-26  | 46831.6 | 48994.4 | 49347.8 | 46360.4 | 73.79K | -4.41% |
| BTC    | 2021-08-25  | 48994.5 | 47707.4 | 49230.2 | 47163.3 | 63.54K | 2.68%  |
<br>

Example Ethereum price data:

```sql
SELECT TOP 5 * FROM trading.prices WHERE ticker = 'ETH';
```

| ticker | market_date |  price  |  open   |  high   |   low   | volume  | change |
| ------ | ----------- | ------- | ------- | ------- | ------- | ------- | ------ |
| ETH    | 2021-08-29  | 3177.84 | 3243.96 | 3282.21 | 3162.79 | 582.04K | -2.04% |
| ETH    | 2021-08-28  | 3243.90 | 3273.78 | 3284.58 | 3212.24 | 466.21K | -0.91% |
| ETH    | 2021-08-27  | 3273.58 | 3093.78 | 3279.93 | 3063.37 | 839.54K | 5.82%  |
| ETH    | 2021-08-26  | 3093.54 | 3228.03 | 3249.62 | 3057.48 | 118.44K | -4.17% |
| ETH    | 2021-08-25  | 3228.15 | 3172.12 | 3247.43 | 3080.70 | 923.13K | 1.73%  |
<br>

## Data Dictionary

| Column Name | Description                     |
| ----------- | ------------------------------- |
| ticker      | one of either BTC or ETH        |
| market_date | the date for each record        |
| price       | closing price at end of day     |
| open        | the opening price               |
| high        | the highest price for that day  |
| low         | the lowest price for that day   |
| volume      | the total volume traded         |
| change      | % change price in price         |
<br>
 
## Data Exploration Questions

Let's answer a few simple questions to help us better understand the `trading.prices` table.

> Remember to clear all previous SQL queries from SQLPad before running each new SQL query!

### Question 1

> How many total records do we have in the `trading.prices` table?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  COUNT(*) AS total_records
FROM trading.prices;
```

</details>
<br>

| total_records |
| ------------- |
|          3404 |
<br>

### Question 2

> How many records are there per `ticker` value?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  ticker,
  COUNT(*) AS record_count
FROM trading.prices
GROUP BY ticker;
```

</details>
<br>

| ticker | record_count |
| ------ | ------------ |
| BTC    |         1702 |
| ETH    |         1702 |
<br>

### Question 3

> What is the minimum and maximum `market_date` values?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  MIN(market_date) AS min_date,
  MAX(market_date) AS max_date
FROM trading.prices;
```

</details>
<br>

|  min_date  |  max_date  |
| ---------- | ---------- |
| 2017-01-01 | 2021-08-29 |
<br>

### Question 4

> Are there differences in the minimum and maximum `market_date` values for each ticker?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  ticker,
  MIN(market_date) AS min_date,
  MAX(market_date) AS max_date
FROM trading.prices
GROUP BY ticker;
```

</details>
<br>

| ticker |  min_date  |  max_date  |
| ------ | ---------- | ---------- |
| BTC    | 2017-01-01 | 2021-08-29 |
| ETH    | 2017-01-01 | 2021-08-29 |
<br>

### Question 5

> What is the average of the `price` column for Bitcoin records during the year 2020?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  AVG(price)
FROM trading.prices
WHERE ticker = 'BTC'
  AND market_date BETWEEN '2020-01-01' AND '2020-12-31';
```

</details>
<br>

|        avg         |
| ------------------ |
| 11111.631147540984 |
<br>

### Question 6

> What is the monthly average of the `price` column for Ethereum in 2020? Sort the output in chronological order and also round the average price value to 2 decimal places

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  DATE_TRUNC('MON', market_date) AS month_start,
  -- need to cast approx. floats to exact numeric types for round!
  ROUND(AVG(price)::NUMERIC, 2) AS average_eth_price
FROM trading.prices
WHERE EXTRACT(YEAR FROM market_date) = 2020
  AND ticker = 'ETH'
GROUP BY month_start
ORDER BY month_start;
```

</details>
<br>

|      month_start       | average_eth_price |
| ---------------------- | ----------------- |
| 2020-01-01 00:00:00+00 |	156.65           |
| 2020-02-01 00:00:00+00 |	238.76           |
| 2020-03-01 00:00:00+00 |	160.18           |
| 2020-04-01 00:00:00+00 |	171.29           |
| 2020-05-01 00:00:00+00 |	207.45           |
| 2020-06-01 00:00:00+00 |	235.92           |
| 2020-07-01 00:00:00+00 |	259.57           |
| 2020-08-01 00:00:00+00 |	401.73           |
| 2020-09-01 00:00:00+00 |	367.77           |
| 2020-10-01 00:00:00+00 |	375.79           |
| 2020-11-01 00:00:00+00 |	486.73           |
| 2020-12-01 00:00:00+00 |	622.35           |
<br>



### Question 7

> Are there any duplicate `market_date` values for any `ticker` value in our table?

As you inspect the output from the following SQL query - what is your final answer?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  ticker,
  COUNT(market_date) AS total_count,
  COUNT(DISTINCT market_date) AS unique_count
FROM trading.prices
GROUP BY ticker;
```

</details>
<br>

| ticker | total_count | unique_count |
| ------ | ----------- | ------------ |
| BTC    |        1702 |         1702 |
| ETH    |        1702 |         1702 |
<br>

### Question 8

> How many days from the `trading.prices` table exist where the `high` price of Bitcoin is over $30,000?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  COUNT(*) AS row_count
FROM trading.prices
WHERE ticker = 'BTC'
  AND high > 30000;
```

</details>
<br>

| row_count |
| --------- |
|       240 |
<br>

### Question 9

> How many "breakout" days were there in 2020 where the `price` column is greater than the `open` column for each `ticker`?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  ticker,
  SUM(CASE WHEN price > open THEN 1 ELSE 0 END) AS breakout_days
FROM trading.prices
WHERE DATE_TRUNC('YEAR', market_date) = '2020-01-01'
GROUP BY ticker;
```

</details>
<br>

| ticker | breakout_days |
| ------ | ------------- |
| BTC    |           207 |
| ETH    |           200 |
<br>

### Question 10

> How many "non_breakout" days were there in 2020 where the `price` column is less than the `open` column for each `ticker`?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  ticker,
  SUM(CASE WHEN price < open THEN 1 ELSE 0 END) AS non_breakout_days
FROM trading.prices
-- this another way to specify the year
WHERE market_date >= '2020-01-01' AND market_date <= '2020-12-31'
GROUP BY ticker;
```

</details>
<br>

| ticker | non_breakout_days |
| ------ | ----------------- |
| BTC    |               159 |
| ETH    |               166 |
<br>

### Question 11

> What percentage of days in 2020 were breakout days vs non-breakout days? Round the percentages to 2 decimal places

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  ticker,
  ROUND(
    SUM(CASE WHEN price > open THEN 1 ELSE 0 END)
      / COUNT(*)::NUMERIC,
    2
  ) AS breakout_percentage,
  ROUND(
    SUM(CASE WHEN price < open THEN 1 ELSE 0 END)
      / COUNT(*)::NUMERIC,
    2
  ) AS non_breakout_percentage
FROM trading.prices
WHERE market_date >= '2020-01-01' AND market_date <= '2020-12-31'
GROUP BY ticker;
```

</details>
<br>

| ticker | breakout_percentage | non_breakout_percentage |
| ------ | ------------------- | ----------------------- |
| BTC    |                0.57 |                    0.43 |
| ETH    |                0.55 |                    0.45 |
<br>

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step2.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step4.md)

# Appendix

> Date Manipulations

We use a variety of date manipulations in questions [5](#question-5), [6](#question-6), [9](#question-9) and [11](#question-11) to filter the `trading.prices` for 2020 values only.

These are all valid methods to qualify `DATE` or `TIMESTAMP` values within a range using a `WHERE` filter:

* `market_date BETWEEN '2020-01-01' AND '2020-12-31'`
* `EXTRACT(YEAR FROM market_date) = 2020`
* `DATE_TRUNC('YEAR', market_date) = '2020-01-01'`
* `market_date >= '2020-01-01' AND market_date <= '2020-12-31'`

The only additional thing to note is that `DATE_TRUNC` returns a `TIMESTAMP` data type which can be cast back to a regular `DATE` using the `::DATE` notation when used in a `SELECT` query.

> `BETWEEN` Boundaries

An additional note for [question 5](#question-5) - the boundaries for the `BETWEEN` clause must be `earlier-date-first` AND `later-date-second`

See what happens when you reverse the order of the `DATE` boundaries using the query below - does it match your expectation?

<details>
  <summary>Click here to see the "wrong" code!</summary>
<br>

```sql
SELECT
  AVG(price)
FROM trading.prices
WHERE ticker = 'BTC'
  AND market_date BETWEEN '2020-12-31' AND '2020-01-01';
```

</details>
<br>

> Rounding Floats/Doubles

In PostgreSQL - we cannot apply the `ROUND` function directly to approximate `FLOAT` or `DOUBLE PRECISION` data types.

Instead we will need to cast any outputs from functions such as `AVG` to an exact `NUMERIC` data type before we can use it with other approximation functions such as `ROUND`

In [question 6](#question-6) - if we were to remove our `::NUMERIC` from our query - we would run into this error:

```
ERROR:  function round(double precision, integer) does not exist
LINE 3:   ROUND(AVG(price), 2) AS average_eth_price
          ^
HINT:  No function matches the given name and argument types. You might need to add explicit type casts.
```

You can try this yourself by running the below code snippet with the `::NUMERIC` removed:

<details>
  <summary>Click here to see the "wrong" code!</summary>
<br>

```sql
SELECT
  DATE_TRUNC('MON', market_date) AS month_start,
  ROUND(AVG(price), 2) AS average_eth_price
FROM trading.prices
WHERE EXTRACT(YEAR FROM market_date) = 2020
GROUP BY month_start
ORDER BY month_start;
```

</details>
<br>

> Integer Floor Division

In [question 5](#question-5) - when dividing values in SQL it is very important to consider the data types of the numerator (the number on top) and the denominator (the number on the bottom)

When there is an `INTEGER` / `INTEGER` as there is in this case - SQL will default to `FLOOR` division in this case!

You can try running the same query as the solution to question 5 above - but this time remove the 2 instances of `::NUMERIC` and the decimal place rounding to see what happens!

This is a super common error found in SQL queries and we usually recommend casting either the numerator or the denominator as a `NUMERIC` type using the shorthand `::NUMERIC` syntax to ensure that you will avoid the dreaded integer floor division!

<details>
  <summary>Click here to see the "wrong" code!</summary>
<br>

```sql
SELECT
  ticker,
  SUM(CASE WHEN price > open THEN 1 ELSE 0 END) / COUNT(*) AS breakout_percentage,
  SUM(CASE WHEN price < open THEN 1 ELSE 0 END) / COUNT(*) AS non_breakout_percentage
FROM trading.prices
WHERE market_date >= '2019-01-01' AND market_date <= '2019-12-31'
GROUP BY ticker;
```

</details>
<br>

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 4 - Transactions Table

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step3.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step5.md)

In our third `trading.transactions` database table we have each `BUY` or `SELL` transaction for a specific `ticker` performed by each `member`

## View The Data

You can inspect the most recent 10 transactions by `member_id = 'c4ca42'` (do you remember who that is?)

```sql
SELECT * FROM trading.transactions
WHERE member_id = 'c4ca42'
ORDER BY txn_time DESC
LIMIT 10;
```

## Data Dictionary

| Column Name    | Description                       |
| -------------- | --------------------------------- |
| txn_id         | unique ID for each transaction    |
| member_id      | member identifier for each trade  |
| ticker         | the ticker for each trade         |
| txn_date       | the date for each transaction     |
| txn_type       | either BUY or SELL                |
| quantity       | the total quantity for each trade |
| percentage_fee | % of total amount charged as fees |
| txn_time       | the timestamp for each trade      |
<br>

## Transactions Questions

Let's finish our initial data exploration with a few more questions for the `trading.transactions` table!

### Question 1

> How many records are there in the `trading.transactions` table?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT COUNT(*) FROM trading.transactions;
```

</details>
<br>

### Question 2

> How many unique transactions are there?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT COUNT(DISTINCT txn_id) FROM trading.transactions;
```

</details>
<br>

| count |
| ----- |
| 22918 |
<br>

### Question 3

> How many buy and sell transactions are there for Bitcoin?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  txn_type,
  COUNT(*) AS transaction_count
FROM trading.transactions
WHERE ticker = 'BTC'
GROUP BY txn_type;
```

</details>
<br>

| txn_type | transaction_count |
| -------- | ----------------- |
| SELL     |              2044 |
| BUY      |             10440 |
<br>

### Question 4

> For each year, calculate the following buy and sell metrics for Bitcoin:

* total transaction count
* total quantity
* average quantity per transaction

Also round the quantity columns to 2 decimal places.

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  EXTRACT(YEAR FROM txn_date) AS txn_year,
  txn_type,
  COUNT(*) AS transaction_count,
  ROUND(SUM(quantity)::NUMERIC, 2) AS total_quantity,
  ROUND(AVG(quantity)::NUMERIC, 2) AS average_quantity
FROM trading.transactions
WHERE ticker = 'BTC'
GROUP BY txn_year, txn_type
ORDER BY txn_year, txn_type;
```

</details>
<br>

| txn_year | txn_type | transaction_count | total_quantity | average_quantity |
| -------- | -------- | ----------------- | -------------- | ---------------- |
|     2017 | BUY      |              2261 |       12069.58 |             5.34 |
|     2017 | SELL     |               419 |        2160.22 |             5.16 |
|     2018 | BUY      |              2204 |       11156.06 |             5.06 |
|     2018 | SELL     |               433 |        2145.05 |             4.95 |
|     2019 | BUY      |              2192 |       11114.43 |             5.07 |
|     2019 | SELL     |               443 |        2316.24 |             5.23 |
|     2020 | BUY      |              2350 |       11748.76 |             5.00 |
|     2020 | SELL     |               456 |        2301.98 |             5.05 |
|     2021 | BUY      |              1433 |        7161.32 |             5.00 |
|     2021 | SELL     |               293 |        1478.00 |             5.04 |
<br>

### Question 5

> What was the monthly total quantity purchased and sold for Ethereum in 2020?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  DATE_TRUNC('MON', txn_date)::DATE AS calendar_month,
  SUM(CASE WHEN txn_type = 'BUY' THEN quantity ELSE 0 END) AS buy_quantity,
  SUM(CASE WHEN txn_type = 'SELL' THEN quantity ELSE 0 END) AS sell_quantity
FROM trading.transactions
WHERE txn_date BETWEEN '2020-01-01' AND '2020-12-31'
  AND ticker = 'ETH'
GROUP BY calendar_month
ORDER BY calendar_month;
```

</details>
<br>

| calendar_month |   buy_quantity    |   sell_quantity    |    
| -------------- | ----------------- | ------------------ |
| 2020-01-01     | 801.0541163041565 |  158.1272716986775 |
| 2020-02-01     | 687.8912804600265 | 160.06533517839912 |
| 2020-03-01     | 804.2368342042604 |  182.1895644691428 |
| 2020-04-01     |   761.87446914631 | 203.16695745059786 |
| 2020-05-01     | 787.4238801914097 | 149.08328330131854 |
| 2020-06-01     | 787.4659503521506 |  208.3362898912813 |
| 2020-07-01     | 890.7807530272569 | 117.01628097387932 |
| 2020-08-01     | 800.6004484214079 |  178.5423079909115 |
| 2020-09-01     |  767.654783160818 | 118.86826373014458 |
| 2020-10-01     | 744.7913667867248 |   174.269279883162 |
| 2020-11-01     | 698.0915637008526 | 163.74629299419385 |
| 2020-12-01     | 752.4121935735661 | 212.77643601396653 |
<br>

### Question 6

> Summarise all buy and sell transactions for each `member_id` by generating 1 row for each member with the following additional columns:

* Bitcoin buy quantity
* Bitcoin sell quantity
* Ethereum buy quantity
* Ethereum sell quantity

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  member_id,
  SUM(
    CASE
      WHEN ticker = 'BTC' AND txn_type = 'BUY' THEN quantity
      ELSE 0
    END
  ) AS btc_buy_qty,
  SUM(
    CASE
      WHEN ticker = 'BTC' AND txn_type = 'SELL' THEN quantity
      ELSE 0
    END
  ) AS btc_sell_qty,
  SUM(
    CASE
      WHEN ticker = 'ETH' AND txn_type = 'BUY' THEN quantity
      ELSE 0
    END
  ) AS eth_buy_qty,
  SUM(
    CASE
      WHEN ticker = 'BTC' AND txn_type = 'SELL' THEN quantity
      ELSE 0
    END
  ) AS eth_sell_qty
FROM trading.transactions
GROUP BY member_id;
```

</details>
<br>

| member_id |       btc_buy_qty       |     btc_sell_qty      |      eth_buy_qty       |     eth_sell_qty      |
| --------- | ----------------------- | --------------------- | ---------------------- | --------------------- |
| d3d944    |   4270.8573823425313401 | 735.87222217343213249 | 1744.65425673609669642 | 735.87222217343213249 |
| c20ad4    |  4975.75064119164404784 |  929.6597445190769838 |  2187.1154401373141792 |  929.6597445190769838 |
| c9f0f8    |   4572.8800842388871361 |  852.3638794847991004 |  2343.4690790139731866 |  852.3638794847991004 |
| eccbc8    |  2844.65155099725936589 |   305.345489355233177 |   2573.754757641582429 |   305.345489355233177 |
| 167909    |  4448.23880624893711454 |  503.0407229884321422 |  1119.7353314008790779 |  503.0407229884321422 |
| c81e72    |   2600.9308762349498788 | 974.09502352354264169 | 4852.52157101720575379 | 974.09502352354264169 |
| e4da3b    |   3567.3882471515063849 | 998.37853535959315513 |  2053.9833252960165058 | 998.37853535959315513 |
| c51ce4    |   2580.4064599247725600 | 1028.7200828179673870 |  2394.7300314796354124 | 1028.7200828179673870 |
| a87ff6    | 5023.705687783492459935 |  863.4858182768507102 |  3822.0371970017654265 |  863.4858182768507102 |
| 8f14e4    |   2647.0768334782105019 |   445.743862547520261 | 3233.47685039578173973 |   445.743862547520261 |
| 45c48c    |   3814.2424689381731354 |   198.131022250011036 | 4442.13685422790551869 |   198.131022250011036 |
| c4ca42    |   4380.4429315724604872 | 1075.5626055691556454 |  4516.5972484100717280 | 1075.5626055691556454 |
| 6512bd    |   4031.6925788360780822 | 574.78279876648434158 |  2941.2223099752008596 | 574.78279876648434158 |
| aab323    |   3491.8873912094965336 |  916.3032786678013621 | 4373.76210149024236043 |  916.3032786678013621 |
<br>

### Question 7

> What was the final quantity holding of Bitcoin for each member? Sort the output from the highest BTC holding to lowest

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  member_id,
  SUM(
    CASE
      WHEN txn_type = 'BUY' THEN quantity
      WHEN txn_type = 'SELL' THEN -quantity
      ELSE 0
    END
  ) AS final_btc_holding
FROM trading.transactions
WHERE ticker = 'BTC'
GROUP BY member_id
ORDER BY final_btc_holding DESC;
```

</details>
<br>

| member_id |    final_btc_holding    |
| --------- | ----------------------- |
| a87ff6    | 4160.219869506641749735 |
| c20ad4    |  4046.09089667256706404 |
| 167909    |  3945.19808326050497234 |
| c9f0f8    |   3720.5162047540880357 |
| 45c48c    |   3616.1114466881620994 |
| d3d944    |  3534.98516016909920761 |
| 6512bd    |  3456.90978006959374062 |
| c4ca42    |   3304.8803260033048418 |
| aab323    |   2575.5841125416951715 |
| e4da3b    |  2569.00971179191322977 |
| eccbc8    |  2539.30606164202618889 |
| 8f14e4    |   2201.3329709306902409 |
| c81e72    |  1626.83585271140723711 |
| c51ce4    |   1551.6863771068051730 |
<br>

### Question 8

> Which members have sold less than 500 Bitcoin? Sort the output from the most BTC sold to least 

We can actually do this in 3 different ways!

<details>
  <summary>Click here to reveal the `HAVING` solution!</summary>
<br>

```sql
SELECT
  member_id,
  SUM(quantity) AS btc_sold_quantity
FROM trading.transactions
WHERE ticker = 'BTC'
  AND txn_type = 'SELL'
GROUP BY member_id
HAVING SUM(quantity) < 500
ORDER BY btc_sold_quantity DESC;
```

</details>
<br>

<details>
  <summary>Click here to reveal the `CTE` solution!</summary>
<br>

```sql
WITH cte AS (
SELECT
  member_id,
  SUM(quantity) AS btc_sold_quantity
FROM trading.transactions
WHERE ticker = 'BTC'
  AND txn_type = 'SELL'
GROUP BY member_id
)
SELECT * FROM cte
WHERE btc_sold_quantity < 500
ORDER BY btc_sold_quantity DESC;
```

</details>
<br>

<details>
  <summary>Click here to reveal the `subquery` solution!</summary>
<br>

```sql
SELECT * FROM (
  SELECT
    member_id,
    SUM(quantity) AS btc_sold_quantity
  FROM trading.transactions
  WHERE ticker = 'BTC'
    AND txn_type = 'SELL'
  GROUP BY member_id
) AS subquery
WHERE btc_sold_quantity < 500
ORDER BY btc_sold_quantity DESC;
```

</details>
<br>

| member_id |  btc_sold_quantity  |
| --------- | ------------------- |
| 8f14e4    | 445.743862547520261 |
| eccbc8    | 305.345489355233177 |
| 45c48c    | 198.131022250011036 |
<br>

### Question 9

 > What is the total Bitcoin quantity for each `member_id` owns after adding all of the BUY and SELL transactions from the `transactions` table? Sort the output by descending total quantity

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  member_id,
  SUM(
    CASE
      WHEN txn_type = 'BUY'  THEN quantity
      WHEN txn_type = 'SELL' THEN -quantity
    END
  ) AS total_quantity
FROM trading.transactions
WHERE ticker = 'BTC'
GROUP BY member_id
ORDER BY total_quantity DESC;
```

</details>
<br>

| member_id |     total_quantity      |
| --------- | ----------------------- |
| a87ff6    | 4160.219869506641749735 |
| c20ad4    |  4046.09089667256706404 |
| 167909    |  3945.19808326050497234 |
| c9f0f8    |   3720.5162047540880357 |
| 45c48c    |   3616.1114466881620994 |
| d3d944    |  3534.98516016909920761 |
| 6512bd    |  3456.90978006959374062 |
| c4ca42    |   3304.8803260033048418 |
| aab323    |   2575.5841125416951715 |
| e4da3b    |  2569.00971179191322977 |
| eccbc8    |  2539.30606164202618889 |
| 8f14e4    |   2201.3329709306902409 |
| c81e72    |  1626.83585271140723711 |
| c51ce4    |   1551.6863771068051730 |
<br>

### Question 10

> Which `member_id` has the highest buy to sell ratio by quantity?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
SELECT
  member_id,
  SUM(CASE WHEN txn_type = 'BUY' THEN quantity ELSE 0 END) /
    SUM(CASE WHEN txn_type = 'SELL' THEN quantity ELSE 0 END) AS buy_to_sell_ratio
FROM trading.transactions
GROUP BY member_id
ORDER BY buy_to_sell_ratio DESC;
```

</details>
<br>

| member_id |  buy_to_sell_ratio   |
| --------- | -------------------- |
| 45c48c    | 19.91269871111331881 |
| a87ff6    | 7.486010484765204502 |
| c9f0f8    |   6.2499141870956191 |
| 8f14e4    |  5.30005322455443465 |
| eccbc8    |  4.92850232946761881 |
| c20ad4    |  4.65209743522270350 |
| 167909    |  4.60147388258864127 |
| aab323    |  4.55272149176427243 |
| 6512bd    |  4.52509140656952666 |
| c81e72    |  4.37533523692905634 |
| c4ca42    |   4.2628218979753569 |
| e4da3b    |  3.55762611425005570 |
| d3d944    |  3.35445896964968774 |
| c51ce4    |   2.3630130420937542 |
<br>

### Question 11

> For each `member_id` - which month had the highest total Ethereum quantity sold`?

<details>
  <summary>Click here to reveal the solution!</summary>
<br>

```sql
WITH cte_ranked AS (
SELECT
  member_id,
  DATE_TRUNC('MON', txn_date)::DATE AS calendar_month,
  SUM(quantity) AS sold_eth_quantity,
  RANK() OVER (PARTITION BY member_id ORDER BY SUM(quantity) DESC) AS month_rank
FROM trading.transactions
WHERE ticker = 'ETH' AND txn_type = 'SELL'
GROUP BY member_id, calendar_month
)
SELECT
  member_id,
  calendar_month,
  sold_eth_quantity
FROM cte_ranked
WHERE month_rank = 1
ORDER BY sold_eth_quantity DESC;
```

</details>
<br>

| member_id | calendar_month |  sold_eth_quantity  |
| --------- | -------------- | ------------------- |
| c51ce4    | 2017-05-01     |  66.092440429535028 |
| d3d944    | 2020-04-01     |  60.417369973983352 |
| 6512bd    | 2018-05-01     |   47.93285714951591 |
| 167909    | 2020-12-01     |   45.92423664055218 |
| c81e72    | 2018-08-01     |   41.26728177476413 |
| aab323    | 2018-09-01     | 41.1750763370983665 |
| c4ca42    | 2021-04-01     |  40.113474724022574 |
| c20ad4    | 2017-12-01     |   37.71908498970638 |
| eccbc8    | 2021-03-01     |  36.485934922948275 |
| 8f14e4    | 2017-07-01     |   36.17383743681231 |
| e4da3b    | 2019-01-01     |   30.48442641077632 |
| a87ff6    | 2020-07-01     |   27.28919836842423 |
| 45c48c    | 2020-01-01     |   20.21523406425370 |
| c9f0f8    | 2020-11-01     |  15.931855129247867 |

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step3.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step5.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 5 - Let the Data Analysis Begin!

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step4.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step6.md)

Now that we've explored all 3 of our tables - let's try to first visualize how each of the tables are joined onto eachother using an Entity Relationship Diagram or ERD for short!

## What is an ERD?

ERDs are very useful to visualize the relationships between columns in tables - especially when it comes to combining them together using tables joins (something we'll cover in this current tutorial)

Below you will see the ERD for our current case study - the most important thing is to notice how all of the columns relate to one another.

![Crypto Case Study ERD](assets/crypto-erd.png)

# Realistic Analytics

Even though we have been exploring our datasets and exploring a few of the basic SQL concepts required for data analysis - we have yet to combine our SQL queries into a single focused analytical process to solve a larger problem. This is our opportunity to try this now!

Let's say that we wish to analyse our overall portfolio performance and also each member's performance based off all the data we have in our 3 tables.

## Analyse the Ranges

Firstly - let's see what is the range of data we have to play with!

### Question 1

> What is the earliest and latest date of transactions for all members?

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  MIN(txn_date) AS earliest_date,
  MAX(txn_date) AS latest_date
FROM trading.transactions;
```

</details><br>

| earliest_date | latest_date |
| ------------- | ----------- |
| 2017-01-01    | 2021-08-27  |

### Question 2

> What is the range of `market_date` values available in the prices data? 

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  MIN(market_date) AS earliest_date,
  MAX(market_date) AS latest_date
FROM trading.prices;
```

</details><br>

| earliest_date | latest_date |
| ------------- | ----------- |
| 2017-01-01    | 2021-08-29  |
<br>

## Joining our Datasets

Now that we now our date ranges are from January 2017 through to almost the end of August 2021 for both our prices and transactions datasets - we can now get started on joining these two tables together!

Let's make use of our ERD shown above to combine the `trading.transactions` table and the `trading.members` table to answer a few simple questions about our mentors!

### Question 3

> Which top 3 mentors have the most Bitcoin quantity as of the 29th of August? 

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  members.first_name,
  SUM(
    CASE
      WHEN transactions.txn_type = 'BUY'  THEN transactions.quantity
      WHEN transactions.txn_type = 'SELL' THEN -transactions.quantity
    END
  ) AS total_quantity
FROM trading.transactions
INNER JOIN trading.members
  ON transactions.member_id = members.member_id
WHERE ticker = 'BTC'
GROUP BY members.first_name
ORDER BY total_quantity DESC
LIMIT 3;
```

</details><br>

| first_name |     total_quantity      |
| ---------- | ----------------------- |
| Nandita    | 4160.219869506641749735 |
| Leah       |  4046.09089667256706404 |
| Ayush      |  3945.19808326050497234 |
<br>

## Calculating Portfolio Value

Now let's combine all 3 tables together using only strictly `INNER JOIN` so we can utilise all of our datasets together.

### Question 4

> What is total value of all Ethereum portfolios for each region at the end date of our analysis? Order the output by descending portfolio value 

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_latest_price AS (
  SELECT
    ticker,
    price
  FROM trading.prices
  WHERE ticker = 'ETH'
  AND market_date = '2021-08-29'
)
SELECT
  members.region,
  SUM(
    CASE
      WHEN transactions.txn_type = 'BUY'  THEN transactions.quantity
      WHEN transactions.txn_type = 'SELL' THEN -transactions.quantity
    END
  ) * cte_latest_price.price AS ethereum_value,
  AVG(
    CASE
      WHEN transactions.txn_type = 'BUY'  THEN transactions.quantity
      WHEN transactions.txn_type = 'SELL' THEN -transactions.quantity
    END
  ) * cte_latest_price.price AS avg_ethereum_value
FROM trading.transactions
INNER JOIN cte_latest_price
  ON transactions.ticker = cte_latest_price.ticker
INNER JOIN trading.members
  ON transactions.member_id = members.member_id
WHERE transactions.ticker = 'ETH'
GROUP BY members.region, cte_latest_price.price
ORDER BY avg_ethereum_value DESC;
```

</details><br>

|    region     |        ethereum_value        |    avg_ethereum_value     |
| ------------- | ---------------------------- | ------------------------- |
| Australia     | 40076021.0922707343527642712 | 10752.8900167080049298064 |
| United States | 50688412.2772532532882719016 | 10549.0972481276281626456 |
| Asia          |  5011670.9776990206825808176 |  8933.4598532959370421432 |
| India         |   6276426.482786365114210656 |   8036.397545181005116104 |
| Africa        |  2183933.3382704268238606128 |  3899.8809611971907658600 |
<br>

### Question 5

> What is the average value of each Ethereum portfolio in each region? Sort this output in descending order

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_latest_price AS (
  SELECT
    ticker,
    price
  FROM trading.prices
  WHERE ticker = 'ETH'
  AND market_date = '2021-08-29'
)
SELECT
  members.region,
  AVG(
    CASE
      WHEN transactions.txn_type = 'BUY'  THEN transactions.quantity
      WHEN transactions.txn_type = 'SELL' THEN -transactions.quantity
    END
  ) * cte_latest_price.price AS avg_ethereum_value
FROM trading.transactions
INNER JOIN cte_latest_price
  ON transactions.ticker = cte_latest_price.ticker
INNER JOIN trading.members
  ON transactions.member_id = members.member_id
WHERE transactions.ticker = 'ETH'
GROUP BY members.region, cte_latest_price.price
ORDER BY avg_ethereum_value DESC;
```

</details><br>

|    region     |    avg_ethereum_value     |
| ------------- | ------------------------- |
| Australia     | 10752.8900167080049298064 |
| United States | 10549.0972481276281626456 |
| Asia          |  8933.4598532959370421432 |
| India         |   8036.397545181005116104 |
| Africa        |  3899.8809611971907658600 |
<br>

Mmm hang on a second...does the output for the above query look correct to you?

Let's try again - this time we will calculate the total sum of portfolio value and then manually divide it by the total number of mentors in each region! 

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_latest_price AS (
  SELECT
    ticker,
    price
  FROM trading.prices
  WHERE ticker = 'ETH'
  AND market_date = '2021-08-29'
),
cte_calculations AS (
SELECT
  members.region,
  SUM(
    CASE
      WHEN transactions.txn_type = 'BUY'  THEN transactions.quantity
      WHEN transactions.txn_type = 'SELL' THEN -transactions.quantity
    END
  ) * cte_latest_price.price AS ethereum_value,
  COUNT(DISTINCT members.member_id) AS mentor_count
FROM trading.transactions
INNER JOIN cte_latest_price
  ON transactions.ticker = cte_latest_price.ticker
INNER JOIN trading.members
  ON transactions.member_id = members.member_id
WHERE transactions.ticker = 'ETH'
GROUP BY members.region, cte_latest_price.price
)
-- final output
SELECT
  *,
  ethereum_value / mentor_count AS avg_ethereum_value
FROM cte_calculations
ORDER BY avg_ethereum_value DESC;
```

</details><br>

|    region     |        ethereum_value        | mentor_count |      avg_ethereum_value      |
| ------------- | ---------------------------- | ------------ | ---------------------------- |
| Australia     | 40076021.0922707343527642712 |            4 | 10019005.2730676835881910678 |
| United States | 50688412.2772532532882719016 |            7 |  7241201.7538933218983245574 |
| India         |   6276426.482786365114210656 |            1 |   6276426.482786365114210656 |
| Asia          |  5011670.9776990206825808176 |            1 |  5011670.9776990206825808176 |
| Africa        |  2183933.3382704268238606128 |            1 |  2183933.3382704268238606128 |
<br>

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step4.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step6.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 6 - Planning Ahead for Data Analysis

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step5.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step7.md)

# Planning Ahead

Sometimes when creating SQL queries - we can jump to the initial problem at hand, but what happens when we stop and plan through our approach to a multi-part problem?

## Further Portfolio Questions

Let's take this next series of questions and methodically break down our approach before we reveal the answers.

**Questions 1-4**

> What is the total portfolio value for each mentor at the end of 2020?

> What is the total portfolio value for each region at the end of 2019?

> What percentage of regional portfolio values does each mentor contribute at the end of 2018?

> Does this region contribution percentage change when we look across both Bitcoin and Ethereum portfolios independently at the end of 2017?

We can see that most questions are based off total portfolio value apart from the final question - which requires both tickers to be separated.

Additionally, the `region` value for each mentor is going to be important also for both questions 3 and 4.

We also need to factor in the timing aspect for these questions - it's not going to be as straightforward as our previous questions which required only the final portfolio value.

For these questions - let's first create a base table which we can refer to later to solve our problems!

## Create a Base Table

We can make use of a `TEMP` table which is stored in a temporary schema which will disappear once the SQL session is closed down - this is very useful in practice because you don't always have write access to production databases all the time!

First let's create a portfolio quantity base table which summarizes our data with the required data first.

### Step 1

> Create a base table that has each mentor's name, `region` and end of year total quantity for each ticker

**You must run the query below in order to run all following queries in this tutorial!**

<details><summary>Click here to reveal the solution!</summary><br>


```sql
DROP TABLE IF EXISTS temp_portfolio_base;
CREATE TEMP TABLE temp_portfolio_base AS
WITH cte_joined_data AS (
  SELECT
    members.first_name,
    members.region,
    transactions.txn_date,
    transactions.ticker,
    CASE
      WHEN transactions.txn_type = 'SELL' THEN -transactions.quantity
      ELSE transactions.quantity
    END AS adjusted_quantity
  FROM trading.transactions
  INNER JOIN trading.members
    ON transactions.member_id = members.member_id
  WHERE transactions.txn_date <= '2020-12-31'
)
SELECT
  first_name,
  region,
  (DATE_TRUNC('YEAR', txn_date) + INTERVAL '12 MONTHS' - INTERVAL '1 DAY')::DATE AS year_end,
  ticker,
  SUM(adjusted_quantity) AS yearly_quantity
FROM cte_joined_data
GROUP BY first_name, region, year_end, ticker;
```

</details><br>

### Step 2

Let's take a look at our base table now to see what data we have to play with - to keep things simple, let's take a look at Abe's data from our new temp table `temp_portfolio_base`

> Inspect the `year_end`, `ticker` and `yearly_quantity` values from our new temp table `temp_portfolio_base` for Mentor Abe only. Sort the output with ordered BTC values followed by ETH values

<details><summary>Click here to reveal the solution!</summary><br>


```sql
SELECT
  year_end,
  ticker,
  yearly_quantity
FROM temp_portfolio_base
WHERE first_name = 'Abe'
ORDER BY ticker, year_end;
```

</details><br>

|  year_end  | ticker |   yearly_quantity    |
| ---------- | ------ | -------------------- |
| 2017-12-31 | BTC    | 861.0106371411443039 |
| 2018-12-31 | BTC    | 755.1495855476883388 |
| 2019-12-31 | BTC    |  765.655338171040942 |
| 2020-12-31 | BTC    | 859.3718776810842491 |
| 2017-12-31 | ETH    | 543.2120486925716504 |
| 2018-12-31 | ETH    |  350.000100283493089 |
| 2019-12-31 | ETH    |  464.317705594980087 |
| 2020-12-31 | ETH    | 508.4673343549910666 |
<br>

We can see from the output above that the yearly quantity is exactly the total portfolio quantity values that we need - we will need to create a cumulative sum of the `yearly_quantity` column that is separate for each mentor and ticker, using the `year_end` as the ordering column.

We can do exactly this using a SQL window function!

### Step 3

To create the cumulative sum - we'll need to apply a window function!

Although we will only touch on this briefly in this course - the complete Data With Danny [Serious SQL course](https://www.datawithdanny.com/courses/serious-sql) covers this topic and many other SQL concepts in a lot of depth!

> Create a cumulative sum for Abe which has an independent value for each ticker

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  year_end,
  ticker,
  yearly_quantity,
  /* this is a multi-line comment!
     for this case we don't actually need first_name
     but we include it anyway to prepare for the next query! */
  SUM(yearly_quantity) OVER (
    PARTITION BY first_name, ticker
    ORDER BY year_end
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
  ) AS cumulative_quantity
FROM temp_portfolio_base
WHERE first_name = 'Abe'
ORDER BY ticker, year_end;
```

</details><br>


|  year_end  | ticker |   yearly_quantity    |  cumulative_quantity  |
| ---------- | ------ | -------------------- | --------------------- |
| 2017-12-31 | BTC    | 861.0106371411443039 |  861.0106371411443039 |
| 2018-12-31 | BTC    | 755.1495855476883388 | 1616.1602226888326427 |
| 2019-12-31 | BTC    |  765.655338171040942 | 2381.8155608598735847 |
| 2020-12-31 | BTC    | 859.3718776810842491 | 3241.1874385409578338 |
| 2017-12-31 | ETH    | 543.2120486925716504 |  543.2120486925716504 |
| 2018-12-31 | ETH    |  350.000100283493089 |  893.2121489760647394 |
| 2019-12-31 | ETH    |  464.317705594980087 | 1357.5298545710448264 |
| 2020-12-31 | ETH    | 508.4673343549910666 | 1865.9971889260358930 |
<br>

### Step 4

Now let's apply our same window function to the entire temporary dataset and start answering our questions.

We can actually `ALTER` and `UPDATE` our temp table to add in an extra column with our new calculation

> Generate an additional `cumulative_quantity` column for the `temp_portfolio_base` temp table

<details><summary>Click here to reveal the solution!</summary><br>

```sql
-- add a column called cumulative_quantity
ALTER TABLE temp_portfolio_base
ADD cumulative_quantity NUMERIC;

-- update new column with data
UPDATE temp_portfolio_base
SET (cumulative_quantity) = (
  SELECT
      SUM(yearly_quantity) OVER (
    PARTITION BY first_name, ticker
    ORDER BY year_end
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
  )
);
```

</details><br>

Now let's check that our updates to the temp table worked by inspecting Abe's records again!

<details><summary>Click here to reveal the solution!</summary><br>

```sql
-- query the updated table to check rows for Abe
SELECT
  year_end,
  ticker,
  yearly_quantity,
  cumulative_quantity
FROM temp_portfolio_base
WHERE first_name = 'Abe'
ORDER BY ticker, year_end;
```

</details><br>

| year_end   | ticker |   yearly_quantity    | cumulative_quantity  |
| ---------- | ------ | -------------------- | -------------------- |
| 2017-01-01 | BTC    | 861.0106371411443039 | 861.0106371411443039 |
| 2018-01-01 | BTC    | 755.1495855476883388 | 755.1495855476883388 |
| 2019-01-01 | BTC    |  765.655338171040942 |  765.655338171040942 |
| 2020-01-01 | BTC    | 859.3718776810842491 | 859.3718776810842491 |
| 2021-01-01 | BTC    | 479.3287662131302019 | 479.3287662131302019 |
| 2017-01-01 | ETH    | 543.2120486925716504 | 543.2120486925716504 |
| 2018-01-01 | ETH    |  350.000100283493089 |  350.000100283493089 |
| 2019-01-01 | ETH    |  464.317705594980087 |  464.317705594980087 |
| 2020-01-01 | ETH    | 508.4673343549910666 | 508.4673343549910666 |
| 2021-01-01 | ETH    |  223.204709336221616 |  223.204709336221616 |
<br>

Wait a moment....it didn't work - the cumulative and the yearly quantity is exactly the same!

This is because our `UPDATE` step only takes into account a single row at a time, which is exactly what we must not do with our window functions!

We will need to create an additional temp table with our cumulative sum instead!

**You must run this step for all following queries to work!**

<details><summary>Click here to reveal the solution!</summary><br>

```sql
DROP TABLE IF EXISTS temp_cumulative_portfolio_base;
CREATE TEMP TABLE temp_cumulative_portfolio_base AS
SELECT
  first_name,
  region,
  year_end,
  ticker,
  yearly_quantity,
  SUM(yearly_quantity) OVER (
    PARTITION BY first_name, ticker
    ORDER BY year_end
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
  ) AS cumulative_quantity
FROM temp_portfolio_base;
```

</details><br>

You can make sure this step is ran by checking the outputs from this query:

```sql
SELECT * FROM temp_cumulative_portfolio_base LIMIT 20;
```

| first_name |    region     |  year_end  | ticker |    yearly_quantity    |  cumulative_quantity   |
| ---------- | ------------- | ---------- | ------ | --------------------- | ---------------------- |
| Abe        | United States | 2017-12-31 | BTC    |  861.0106371411443039 |   861.0106371411443039 |
| Abe        | United States | 2018-12-31 | BTC    |  755.1495855476883388 |  1616.1602226888326427 |
| Abe        | United States | 2019-12-31 | BTC    |   765.655338171040942 |  2381.8155608598735847 |
| Abe        | United States | 2020-12-31 | BTC    |  859.3718776810842491 |  3241.1874385409578338 |
| Abe        | United States | 2017-12-31 | ETH    |  543.2120486925716504 |   543.2120486925716504 |
| Abe        | United States | 2018-12-31 | ETH    |   350.000100283493089 |   893.2121489760647394 |
| Abe        | United States | 2019-12-31 | ETH    |   464.317705594980087 |  1357.5298545710448264 |
| Abe        | United States | 2020-12-31 | ETH    |  508.4673343549910666 |  1865.9971889260358930 |
| Alex       | United States | 2017-12-31 | BTC    |  453.4749593742834454 |   453.4749593742834454 |
| Alex       | United States | 2018-12-31 | BTC    |  447.1910423241274346 |   900.6660016984108800 |
| Alex       | United States | 2019-12-31 | BTC    |   490.959718475924108 |  1391.6257201743349880 |
| Alex       | United States | 2020-12-31 | BTC    |   444.259179847377622 |  1835.8849000217126100 |
| Alex       | United States | 2017-12-31 | ETH    |   678.274023865761511 |    678.274023865761511 |
| Alex       | United States | 2018-12-31 | ETH    | 546.83620089990823574 | 1225.11022476566974674 |
| Alex       | United States | 2019-12-31 | ETH    |  476.8692888907140746 | 1701.97951365638382134 |
| Alex       | United States | 2020-12-31 | ETH    |  621.5582550264365449 | 2323.53776868282036624 |
| Ayush      | United States | 2017-12-31 | BTC    |  794.5344541497821383 |   794.5344541497821383 |
| Ayush      | United States | 2018-12-31 | BTC    |  955.3494738695000753 |  1749.8839280192822136 |
| Ayush      | United States | 2019-12-31 | BTC    |  743.2345666894748266 |  2493.1184947087570402 |
| Ayush      | United States | 2020-12-31 | BTC    | 954.85594846498402504 | 3447.97444317374106524 |


Now that we've obtained our base table properly - let's start answering some of these questions!

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step5.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step7.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 7 - Answering Data Questions

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step6.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step8.md)

# Answering the Questions

Before running any of the solution queries below for this tutorial's questions - you can run the entire SQL prep queries directly below!

<details><summary>Click here to reveal the entire data prep SQL script!</summary><br>

```sql
DROP TABLE IF EXISTS temp_portfolio_base;
CREATE TEMP TABLE temp_portfolio_base AS
WITH cte_joined_data AS (
  SELECT
    members.first_name,
    members.region,
    transactions.txn_date,
    transactions.ticker,
    CASE
      WHEN transactions.txn_type = 'SELL' THEN -transactions.quantity
      ELSE transactions.quantity
    END AS adjusted_quantity
  FROM trading.transactions
  INNER JOIN trading.members
    ON transactions.member_id = members.member_id
  WHERE transactions.txn_date <= '2020-12-31'
)
SELECT
  first_name,
  region,
  (DATE_TRUNC('YEAR', txn_date) + INTERVAL '12 MONTHS' - INTERVAL '1 DAY')::DATE AS year_end,
  ticker,
  SUM(adjusted_quantity) AS yearly_quantity
FROM cte_joined_data
GROUP BY first_name, region, year_end, ticker;

DROP TABLE IF EXISTS temp_cumulative_portfolio_base;
CREATE TEMP TABLE temp_cumulative_portfolio_base AS
SELECT
  first_name,
  region,
  year_end,
  ticker,
  yearly_quantity,
  SUM(yearly_quantity) OVER (
    PARTITION BY first_name, ticker
    ORDER BY year_end
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
  ) AS cumulative_quantity
FROM temp_portfolio_base;
```

</details><br>

Here is the ERD diagram below just in case you forgot about how all the tables are joined together!

![Crypto Case Study ERD](assets/crypto-erd.png)

## Question 1

> What is the total portfolio value for each mentor at the end of 2020?

We can now inner join our `trading.prices` table (I hope you haven't forgot about this one yet!) to our new temp table `temp_cumulative_portfolio_base`

Let's also order our results by highest portfolio value to lowest rounded to 2 decimal places.

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  base.first_name,
  ROUND(
    SUM(base.cumulative_quantity * prices.price),
    2
  ) AS portfolio_value
FROM temp_cumulative_portfolio_base AS base
INNER JOIN trading.prices
  ON base.ticker = prices.ticker
  AND base.year_end = prices.market_date
WHERE base.year_end = '2020-12-31'
GROUP BY base.first_name
ORDER BY portfolio_value DESC;
```

</details><br>

| first_name | portfolio_value |
| ---------- | --------------- |
| Nandita    |    105391731.03 |
| Leah       |    100724284.81 |
| Ayush      |    100071736.51 |
| Abe        |     95203693.60 |
| Ben        |     92722998.25 |
| Enoch      |     88346609.78 |
| Vikram     |     88000702.69 |
| Danny      |     84696448.83 |
| Sonia      |     67932183.73 |
| Rowan      |     67241367.69 |
| Charlie    |     66761769.49 |
| Alex       |     54857750.71 |
| Vipul      |     43123911.62 |
| Pavan      |     41764439.70 |
<br>

## Question 2

> What is the total portfolio value for each region at the end of 2019?

Let's also perform the same ordering and rounding for this query too.

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  base.region,
  ROUND(
    SUM(base.cumulative_quantity * prices.price),
    2
  ) AS portfolio_value
FROM temp_cumulative_portfolio_base AS base
INNER JOIN trading.prices
  ON base.ticker = prices.ticker
  AND base.year_end = prices.market_date
WHERE base.year_end = '2019-12-31'
GROUP BY base.region
ORDER BY portfolio_value DESC;
```

</details><br>

|    region     | portfolio_value |
| ------------- | --------------- |
| United States |     98795362.60 |
| Australia     |     52861452.00 |
| Asia          |     18305366.24 |
| India         |     16168831.76 |
| Africa        |     16078915.65 |
<br>

## Question 3

> What percentage of regional portfolio values does each mentor contribute at the end of 2018?

Let's make our percentages between 0 and 100, rounded to decimal places - order the output with the regions with highest portfolio value first and then by descending mentor contributions within each group.

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_mentor_portfolio AS (
  SELECT
    base.region,
    base.first_name,
    ROUND(
      SUM(base.cumulative_quantity * prices.price),
      2
    ) AS portfolio_value
  FROM temp_cumulative_portfolio_base AS base
  INNER JOIN trading.prices
    ON base.ticker = prices.ticker
    AND base.year_end = prices.market_date
  WHERE base.year_end = '2018-12-31'
  GROUP BY base.first_name, base.region
),
cte_region_portfolio AS (
SELECT
  region,
  first_name,
  portfolio_value,
  SUM(portfolio_value) OVER (PARTITION BY region) AS region_total
FROM cte_mentor_portfolio
)
-- final output
SELECT
  region,
  first_name,
  ROUND(100 * portfolio_value / region_total, 2) AS contribution_percentage
FROM cte_region_portfolio
ORDER BY region_total DESC, contribution_percentage DESC;
```

</details><br>

|    region     | first_name | contribution_percentage |
| ------------- | ---------- | ----------------------- |
| United States | Nandita    |                   20.00 |
| United States | Ayush      |                   18.61 |
| United States | Abe        |                   17.45 |
| United States | Rowan      |                   14.34 |
| United States | Charlie    |                   12.52 |
| United States | Alex       |                   10.00 |
| United States | Vipul      |                    7.08 |
| Australia     | Danny      |                   31.55 |
| Australia     | Ben        |                   30.41 |
| Australia     | Sonia      |                   24.53 |
| Australia     | Pavan      |                   13.51 |
| Asia          | Leah       |                  100.00 |
| Africa        | Enoch      |                  100.00 |
| India         | Vikram     |                  100.00 |
<br>

## Question 4

> Does this region contribution percentage change when we look across both Bitcoin and Ethereum portfolios independently at the end of 2017?

We can use a similar approach to question 3 - but we will need to avoid the first level of aggregation.

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_mentor_portfolio AS (
  SELECT
    base.region,
    base.first_name,
    base.ticker,
    base.cumulative_quantity * prices.price AS portfolio_value
  FROM temp_cumulative_portfolio_base AS base
  INNER JOIN trading.prices
    ON base.ticker = prices.ticker
    AND base.year_end = prices.market_date
  WHERE base.year_end = '2017-12-31'
),
cte_region_portfolio AS (
SELECT
  region,
  first_name,
  ticker,
  portfolio_value,
  SUM(portfolio_value) OVER (
    PARTITION BY region, ticker
  ) AS region_total
FROM cte_mentor_portfolio
)
-- final output
SELECT
  region,
  first_name,
  ticker,
  ROUND(100 * portfolio_value / region_total, 2) AS contribution_percentage
FROM cte_region_portfolio
ORDER BY ticker, region, contribution_percentage DESC;
```

</details><br>

|    region     | first_name | ticker | contribution_percentage |
| ------------- | ---------- | ------ | ----------------------- |
| Africa        | Enoch      | BTC    |                  100.00 |
| Asia          | Leah       | BTC    |                  100.00 |
| Australia     | Ben        | BTC    |                   32.96 |
| Australia     | Danny      | BTC    |                   29.99 |
| Australia     | Sonia      | BTC    |                   21.86 |
| Australia     | Pavan      | BTC    |                   15.19 |
| India         | Vikram     | BTC    |                  100.00 |
| United States | Nandita    | BTC    |                   20.99 |
| United States | Abe        | BTC    |                   17.69 |
| United States | Ayush      | BTC    |                   16.32 |
| United States | Rowan      | BTC    |                   14.65 |
| United States | Charlie    | BTC    |                   12.13 |
| United States | Alex       | BTC    |                    9.32 |
| United States | Vipul      | BTC    |                    8.91 |
| Africa        | Enoch      | ETH    |                  100.00 |
| Asia          | Leah       | ETH    |                  100.00 |
| Australia     | Ben        | ETH    |                   34.34 |
| Australia     | Danny      | ETH    |                   30.06 |
| Australia     | Sonia      | ETH    |                   29.93 |
| Australia     | Pavan      | ETH    |                    5.66 |
| India         | Vikram     | ETH    |                  100.00 |
| United States | Nandita    | ETH    |                   21.21 |
| United States | Vipul      | ETH    |                   20.91 |
| United States | Alex       | ETH    |                   18.18 |
| United States | Abe        | ETH    |                   14.56 |
| United States | Charlie    | ETH    |                   12.36 |
| United States | Rowan      | ETH    |                   10.11 |
| United States | Ayush      | ETH    |                    2.66 |
<br>

## Bonus Question 5

> Calculate the ranks for each mentor in the US and Australia for each year and ticker

The final output we wish to generate looks like this:

|    region     | first_name | BTC 2017 | BTC 2018 | BTC 2019 | BTC 2020 | ETH 2017 | ETH 2018 | ETH 2019 | ETH 2020 |
| ------------- | ---------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| Australia     | Ben        |        1 |        2 |        1 |        1 |        1 |        1 |        1 |        1 |
| Australia     | Danny      |        2 |        1 |        2 |        2 |        2 |        2 |        2 |        2 |
| Australia     | Sonia      |        3 |        3 |        3 |        3 |        3 |        3 |        3 |        3 |
| Australia     | Pavan      |        4 |        4 |        4 |        4 |        4 |        4 |        4 |        4 |
| United States | Nandita    |        1 |        1 |        1 |        1 |        1 |        2 |        2 |        2 |
| United States | Abe        |        2 |        3 |        3 |        3 |        4 |        4 |        4 |        4 |
| United States | Ayush      |        3 |        2 |        2 |        2 |        7 |        7 |        7 |        7 |
| United States | Rowan      |        4 |        4 |        4 |        4 |        6 |        6 |        6 |        6 |
| United States | Charlie    |        5 |        5 |        5 |        5 |        5 |        5 |        5 |        5 |
| United States | Alex       |        6 |        6 |        6 |        6 |        3 |        3 |        3 |        3 |
| United States | Vipul      |        7 |        7 |        7 |        7 |        2 |        1 |        1 |        1 |
<br>

Our first step is to try and create a long table first with all of our ranks for each ticker and year end.

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  year_end,
  region,
  first_name,
  ticker,
  RANK() OVER (
    PARTITION BY region, year_end
    ORDER BY cumulative_quantity DESC
  ) AS ranking
FROM temp_cumulative_portfolio_base
WHERE region IN ('United States', 'Australia')
ORDER BY year_end, region, ranking;
```

</details><br>

Let's now pivote this long table to a slightly easier to read wide table

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_ranks AS (
SELECT
  year_end,
  region,
  first_name,
  ticker,
  RANK() OVER (
    PARTITION BY region, year_end, ticker
    ORDER BY cumulative_quantity DESC
  ) AS ranking
FROM temp_cumulative_portfolio_base
WHERE region IN ('United States', 'Australia')
)
SELECT
  region,
  first_name,
  MAX(CASE WHEN ticker = 'BTC' AND year_end = '2017-12-31' THEN ranking ELSE NULL END) AS "BTC 2017",
  MAX(CASE WHEN ticker = 'BTC' AND year_end = '2018-12-31' THEN ranking ELSE NULL END) AS "BTC 2018",
  MAX(CASE WHEN ticker = 'BTC' AND year_end = '2019-12-31' THEN ranking ELSE NULL END) AS "BTC 2019",
  MAX(CASE WHEN ticker = 'BTC' AND year_end = '2020-12-31' THEN ranking ELSE NULL END) AS "BTC 2020",
  MAX(CASE WHEN ticker = 'ETH' AND year_end = '2017-12-31' THEN ranking ELSE NULL END) AS "ETH 2017",
  MAX(CASE WHEN ticker = 'ETH' AND year_end = '2018-12-31' THEN ranking ELSE NULL END) AS "ETH 2018",
  MAX(CASE WHEN ticker = 'ETH' AND year_end = '2019-12-31' THEN ranking ELSE NULL END) AS "ETH 2019",
  MAX(CASE WHEN ticker = 'ETH' AND year_end = '2020-12-31' THEN ranking ELSE NULL END) AS "ETH 2020"
FROM cte_ranks
GROUP BY region, first_name
ORDER BY region, "BTC 2017";
```

</details><br>

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step6.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step8.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 8 - The Final Case Study

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step7.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step9.md)

Now that we've tackled a more complicated series of questions - let's take it to the next level!

In these final questions - we will try to assess the profitability of our mentors and their crypto portfolios.

It's not enough for our team of mentors to just hold a lot of crypto - we wish to see the various prices for every transaction that occured, calculate the total fee amounts and also calculate some final profit metrics.

## Simple Scenario Breakdown

Often when faced with a difficult problem like we have right now - the first step is to try and break down our complex situation into a very simple scenarios to try and understand what we have to do!

1. Buy and hold (HODL Strategy)
2. Buy and keep buying (Bull Strategy)
3. Buy and sell (Trader Strategy)

In the next 3 steps - we will cover each strategy by simplifying our existing `trading.transactions` table to answer more questions!

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step7.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step9.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 9 - Buy and Hold Analysis

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step8.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step10.md)

![hodl](assets/hodl.jpeg)

Meet Leah - she is our mentor who will take the buy and hold strategy otherwise known as the "HODL strategy" or hold on for dear life!

She is risk averse and just wants to leave her initial investment alone because she believes her original holdings will grow over time with low risk.

## Leah's Transaction History

1. She purchases 50 BTC and 50 ETH on Jan 1st 2017
2. She holds onto all of her portfolio and does not sell anything (HODL)
3. She also does not purchase any additional quantity of either crypto
4. By August 29th 2021 (the last date of our price data) - we can assess her individual performance

> Remember that we are simplifying our problem at the moment so Leah's records will actually be different in the final `trading.transactions` dataset!

## The Data

For this simplified scenario - we first need to create a new temp table called `leah_hodl_strategy` using the code below:

```sql
CREATE TEMP TABLE leah_hodl_strategy AS
SELECT * FROM trading.transactions
WHERE member_id = 'c20ad4'
AND txn_date = '2017-01-01'
AND quantity = 50;
```

You can inspect the data by running the following query after creating the temp table above:

```sql
SELECT * FROM leah_hodl_strategy;
```

| txn_id | member_id | ticker |  txn_date  | txn_type | quantity | percentage_fee |      txn_time       |
| ------ | --------- | ------ | ---------- | -------- | -------- | -------------- | ------------------- |
|     12 | c20ad4    | BTC    | 2017-01-01 | BUY      |       50 |           0.30 | 2017-01-01 00:00:00 |
|     26 | c20ad4    | ETH    | 2017-01-01 | BUY      |       50 |           0.30 | 2017-01-01 00:00:00 |
<br>

## Required Metrics

For this basic scenario - we wish to calculate the following metrics:

1. The initial value of her original 50 BTC and 50 ETH purchases
2. The dollar amount of fees she paid for those 2 transactions
3. The final value of her portfolio on August 29th 2021
4. The profitability by dividing her final value by initial value

## Solutions

### Question 1 & 2

We can calculate the first 2 questions using a single query

> 1. The initial value of her original 50 BTC and 50 ETH purchases
> 2. The dollar amount of fees she paid for those 2 transactions

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  SUM(transactions.quantity * prices.price) AS initial_value,
  SUM(transactions.quantity * prices.price * transactions.percentage_fee / 100) AS fees
FROM leah_hodl_strategy AS transactions
INNER JOIN trading.prices
  ON transactions.ticker = prices.ticker
  AND transactions.txn_date = prices.market_date;
```

</details><br>

| initial_value |         fees         |
| ------------- | -------------------- |
|      50180.00 | 150.5400000000000000 |
<br>

### Question 3

> The final value of her portfolio on August 29th 2021

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  SUM(transactions.quantity * prices.price) AS final_value
FROM leah_hodl_strategy AS transactions
INNER JOIN trading.prices
  ON transactions.ticker = prices.ticker
WHERE prices.market_date = '2021-08-29';
```

</details><br>

| final_value |
| ----------- |
|  2571642.00 |

### Question 4

> Calculate the profitability by dividing Leah's final value by initial value

We can actually do one better and combine all 4 metrics into a single query!

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_portfolio_values AS (
  SELECT
    -- initial metrics
    SUM(transactions.quantity * initial.price) AS initial_value,
    SUM(transactions.quantity * initial.price * transactions.percentage_fee / 100) AS fees,
    -- final value
    SUM(transactions.quantity * final.price) AS final_value
  FROM leah_hodl_strategy AS transactions
  INNER JOIN trading.prices AS initial
    ON transactions.ticker = initial.ticker
    AND transactions.txn_date = initial.market_date
  INNER JOIN trading.prices AS final
    ON transactions.ticker = final.ticker
  WHERE final.market_date = '2021-08-29'
)
SELECT
  initial_value,
  fees,
  final_value,
  final_value / initial_value AS profitability
FROM cte_portfolio_values;
```

</details><br>

| initial_value |         fees         | final_value |    profitability    |
| ------------- | -------------------- | ----------- | ------------------- |
|      50180.00 | 150.5400000000000000 |  2571642.00 | 51.2483459545635711 |
<br>

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step8.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step10.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 10 - The Bull Strategy

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step9.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step11.md)

![bull](assets/bull.jpeg)

Vikram is also similar to Leah but purchases Bitcoin frequently because he believes the price will go up in the future!

## Vikram's Transaction History

* Vikram also purchases 50 units of both ETH and BTC just like Leah on Jan 1st 2017
* He continues to purchase more throughout the entire 4 year period
* He does not sell any of his crypto - he's in it for the long run

## Vikram's Data

Because this is also a simplified version of our dataset - we will create another temp table called `vikram_bull_strategy` with our data for these questions.

```sql
CREATE TEMP TABLE vikram_bull_strategy AS
SELECT * FROM trading.transactions
WHERE member_id = '6512bd'
AND txn_type = 'BUY';
```

Again, we can inspect the data by running the following query after creating the temp table above:

```sql
SELECT * FROM vikram_bull_strategy LIMIT 10;
```

| txn_id | member_id | ticker |  txn_date  | txn_type |     quantity     | percentage_fee |          txn_time          |
| ------ | --------- | ------ | ---------- | -------- | ---------------- | -------------- | -------------------------- |
|     11 | 6512bd    | BTC    | 2017-01-01 | BUY      |               50 |           0.30 | 2017-01-01 00:00:00        |
|     25 | 6512bd    | ETH    | 2017-01-01 | BUY      |               50 |           0.30 | 2017-01-01 00:00:00        |
|     30 | 6512bd    | ETH    | 2017-01-01 | BUY      | 8.84298701787532 |           0.30 | 2017-01-01 06:22:20.202995 |
|     31 | 6512bd    | BTC    | 2017-01-01 | BUY      | 2.27106258645779 |           0.21 | 2017-01-01 06:40:48.691577 |
|     35 | 6512bd    | BTC    | 2017-01-01 | BUY      | 6.73841780964583 |           0.30 | 2017-01-01 11:00:14.002519 |
|     36 | 6512bd    | BTC    | 2017-01-01 | BUY      | 9.37875791241961 |           0.30 | 2017-01-01 12:03:33.017453 |
|     55 | 6512bd    | BTC    | 2017-01-02 | BUY      | 5.54383811940401 |           0.30 | 2017-01-02 11:12:42.895079 |
|     63 | 6512bd    | ETH    | 2017-01-02 | BUY      | 5.04372609654009 |           0.07 | 2017-01-02 20:48:13.480413 |
|     65 | 6512bd    | BTC    | 2017-01-02 | BUY      | 3.01276029896716 |           0.30 | 2017-01-02 21:00:49.341793 |
|     99 | 6512bd    | ETH    | 2017-01-04 | BUY      | 1.83100404691078 |           0.30 | 2017-01-04 22:04:12.689306 |
<br>

## Required Metrics

To assess Vikram's performance we also need to regularly match the prices for his trades throughout the 4 years and not just at the start of the entire dataset, like in the case of Leah's HODL strategy.

We will need to calculate the following metrics:

* Total investment amount in dollars for all of his purchases
* The dollar amount of fees paid
* The dollar cost average per unit of BTC and ETH purchased by Vikram
* The final investment value of his portfolio on August 29th 2021
* Profitability can be measured by final portfolio value divided by the investment amount
* Profitability split by BTC and ETH

## Solutions

### Question 1 & 2

> Calculate the total investment amount in dollars for all of Vikram's purchases and his dollar amount of fees paid

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  SUM(transactions.quantity * prices.price) AS initial_investment,
  SUM(transactions.quantity * prices.price * transactions.percentage_fee / 100) AS fees
FROM vikram_bull_strategy AS transactions
INNER JOIN trading.prices
  ON transactions.ticker = prices.ticker
  AND transactions.txn_date = prices.market_date;
```

</details><br>

|     initial_investment      |            fees             |
| --------------------------- | --------------------------- |
| 50730451.023400136384298882 | 128821.14163246531801672694 |
<br>

### Question 3

> What is the average cost per unit of BTC and ETH purchased by Vikram

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_portfolio AS (
  SELECT
    transactions.ticker,
    SUM(transactions.quantity) AS total_quantity,
    SUM(transactions.quantity * prices.price) AS initial_investment
  FROM vikram_bull_strategy AS transactions
  INNER JOIN trading.prices
    ON transactions.ticker = prices.ticker
    AND transactions.txn_date = prices.market_date
  GROUP BY transactions.ticker
)
SELECT
  ticker,
  initial_investment / total_quantity AS dollar_cost_average
FROM cte_portfolio;
```

</details><br>

| ticker |   dollar_cost_average   |
| ------ | ----------------------- |
| BTC    | 12190.13846337579877423 |
| ETH    |  538.402092304626902638 |
<br>

### Question 4

> Calculate profitability by using final portfolio value divided by the investment amount

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_portfolio_values AS (
  SELECT
    SUM(transactions.quantity * prices.price) AS initial_investment,
    SUM(transactions.quantity * final.price) AS final_value
  FROM vikram_bull_strategy AS transactions
  INNER JOIN trading.prices
    ON transactions.ticker = prices.ticker
    AND transactions.txn_date = prices.market_date
  INNER JOIN trading.prices AS final
    ON transactions.ticker = final.ticker
  WHERE final.market_date = '2021-08-29'
)
SELECT
  final_value / initial_investment AS profitability
FROM cte_portfolio_values;
```

</details><br>

|    profitability     |
| -------------------- |
| 4.019204544489789883 |

### Question 5

> Calculate Vikram's profitability split by BTC and ETH

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_ticker_portfolio_values AS (
  SELECT
    transactions.ticker,
    SUM(transactions.quantity * prices.price) AS initial_investment,
    SUM(transactions.quantity * final.price) AS final_value
  FROM vikram_bull_strategy AS transactions
  INNER JOIN trading.prices
    ON transactions.ticker = prices.ticker
    AND transactions.txn_date = prices.market_date
  INNER JOIN trading.prices AS final
    ON transactions.ticker = final.ticker
  WHERE final.market_date = '2021-08-29'
  GROUP BY transactions.ticker
)
SELECT
  ticker,
  final_value / initial_investment AS profitability
FROM cte_ticker_portfolio_values;
```

</details><br>

| ticker |    profitability     |
| ------ | -------------------- |
| BTC    |  3.95852763649714995 |
| ETH    | 5.902354477110731653 |
<br>

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step9.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step11.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 11 - The Trader Strategy

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step10.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step12.md)

# Scenario 3: The Trader

![trader](assets/trader.jpeg)

Nandita is the Queen of crypto trading - she wants to follow the popular trader's adage of **BUY LOW, SELL HIGH**

## Nandita's Transaction History

* She also starts out with a 50 BTC and ETH purchase just like Leah and Vikram
* She continues to buy more crypto over the 4 years
* She starts selling some of her crypto portfolio to realise gains

## Nandita's Data

This final scenario 3 is actually exactly the same as our real `trading.transactions` dataset!

To complete our individual scenarios before we calculate all our metrics for all mentors - let's also prepare another temp table called `nandita_trading_strategy`

```sql
CREATE TEMP TABLE nandita_trading_strategy AS
SELECT * FROM trading.transactions
WHERE member_id = 'a87ff6';
```

You can inspect the data by running the following query after creating the temp table above:

```sql
SELECT * FROM nandita_trading_strategy LIMIT 10;
```

| txn_id | member_id | ticker |  txn_date  | txn_type |     quantity     | percentage_fee |          txn_time          |
| ------ | --------- | ------ | ---------- | -------- | ---------------- | -------------- | -------------------------- |
|      3 | a87ff6    | BTC    | 2017-01-01 | BUY      |               50 |           0.00 | 2017-01-01 00:00:00        |
|     19 | a87ff6    | ETH    | 2017-01-01 | BUY      |               50 |           0.20 | 2017-01-01 00:00:00        |
|     41 | a87ff6    | ETH    | 2017-01-01 | BUY      | 1.98666102006509 |           0.30 | 2017-01-01 17:39:10.894181 |
|     49 | a87ff6    | ETH    | 2017-01-02 | BUY      | 8.78673520720906 |           0.30 | 2017-01-02 04:48:50.044665 |
|     53 | a87ff6    | BTC    | 2017-01-02 | BUY      | 5.95980481918755 |           0.30 | 2017-01-02 09:55:27.347188 |
|     60 | a87ff6    | BTC    | 2017-01-02 | BUY      | 9.01117722642621 |           0.30 | 2017-01-02 17:16:29.062839 |
|     64 | a87ff6    | ETH    | 2017-01-02 | BUY      | 1.37715908309016 |           0.01 | 2017-01-02 20:49:33.771818 |
|     77 | a87ff6    | BTC    | 2017-01-03 | BUY      | 3.80769453794553 |           0.30 | 2017-01-03 12:30:20.779105 |
|     89 | a87ff6    | BTC    | 2017-01-04 | BUY      | 5.68677206948404 |           0.00 | 2017-01-04 08:13:07.752195 |
|     93 | a87ff6    | BTC    | 2017-01-04 | BUY      | 8.13772499730359 |           0.30 | 2017-01-04 12:25:48.367139 |
<br>

## Final Evaluation Metrics

By the end of our assessment period on the 29th of August 2021 - we can calculate Nandita's metrics as follows for each individual BTC and ETH portfolio:

* Count of buy and sell transactions
* Total investment amount of purchases
* The dollar amount of fees for purchase transactions
* Dollar cost average of purchases
* Total gross revenue of sell transactions
* Average sell price for each unit sold
* Final portfolio value and quantity
* Profitability measured as (final portfolio value + gross sales revenue - purchase fees - sales fees) / initial investment amount

**Bonus Question**

We also want to calculate the difference if Nandita didn't sell any of her crypto and compare it to the final value at the end of August - how much does this impact her overall profitability?

## Solutions

### Question 1

> Calculate Nandita's purchase metrics for each of her BTC and ETH portfolios:
>
> * Count of purchase transactions
> * Initial investment
> * Purchase fees
> * Dollar cost average of purchases

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_purchases AS (
  SELECT
    transactions.ticker,
    COUNT(*) AS purchase_count,
    SUM(transactions.quantity) AS purchase_quantity,
    SUM(transactions.quantity * prices.price) AS initial_investment,
    SUM(transactions.quantity * prices.price * transactions.percentage_fee / 100) AS purchase_fees
  FROM nandita_trading_strategy AS transactions
  INNER JOIN trading.prices
    ON transactions.ticker = prices.ticker
    AND transactions.txn_date = prices.market_date
  WHERE transactions.txn_type = 'BUY'
  GROUP BY transactions.ticker
)
SELECT
  ticker,
  purchase_count,
  purchase_quantity,
  initial_investment,
  purchase_fees,
  initial_investment / purchase_quantity AS dollar_cost_average
FROM cte_purchases;
```

</details><br>

| ticker | purchase_count |    purchase_quantity    |      initial_investment      |        purchase_fees         |    dollar_cost_average    |
| ------ | -------------- | ----------------------- | ---------------------------- | ---------------------------- | ------------------------- |
| BTC    |            954 | 5023.705687783492459935 | 63735345.6973630892576024850 | 162919.943377863222128081502 | 12686.9187126851255182628 |
| ETH    |            756 |   3822.0371970017654265 |   2287096.578215583047801140 |    5783.32678170688531189239 |    598.397257883758534604 |
<br>

### Question 2

> Calculate Nandita's sales metrics for each of her BTC and ETH portfolios:
>
> * Count of sales transactions
> * Gross revenue amount
> * Sales fees
> * Average selling price

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_sales AS (
  SELECT
    transactions.ticker,
    COUNT(*) AS sales_count,
    SUM(transactions.quantity) AS sales_quantity,
    SUM(transactions.quantity * prices.price) AS gross_revenue,
    SUM(transactions.quantity * prices.price * transactions.percentage_fee / 100) AS sales_fees
  FROM nandita_trading_strategy AS transactions
  INNER JOIN trading.prices
    ON transactions.ticker = prices.ticker
    AND transactions.txn_date = prices.market_date
  WHERE transactions.txn_type = 'SELL'
  GROUP BY transactions.ticker
)
SELECT
  ticker,
  sales_count,
  sales_quantity,
  gross_revenue,
  sales_fees,
  gross_revenue / sales_quantity AS average_selling_price
FROM cte_sales;
```

</details><br>

| ticker | sales_count |    sales_quantity    |       gross_revenue        |         sales_fees         |  average_selling_price  |
| ------ | ----------- | -------------------- | -------------------------- | -------------------------- | ----------------------- |
| BTC    |         167 | 863.4858182768507102 | 10975745.05336688201117242 | 29522.09286188312984442411 | 12710.97315213559195557 |
| ETH    |          70 | 318.1506358514526923 |  172591.915512909206341725 |   447.93810830446683009024 |  542.484898862480594053 |
<br>

### Question 3

> What is Nandita's final BTC and ETH portfolio value and quantity?

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_adjusted_transactions AS (
  SELECT
    member_id,
    txn_date,
    txn_type,
    ticker,
    percentage_fee,
    CASE
      WHEN txn_type = 'BUY' THEN quantity
      WHEN txn_type = 'SELL' THEN -quantity
    END as quantity
  FROM nandita_trading_strategy
)
SELECT
  transactions.ticker,
  SUM(transactions.quantity) AS final_quantity,
  SUM(transactions.quantity * prices.price) AS final_portfolio_value
FROM cte_adjusted_transactions AS transactions
INNER JOIN trading.prices
  ON transactions.ticker = prices.ticker
WHERE prices.market_date = '2021-08-29'
GROUP BY transactions.ticker;
```

</details><br>

| ticker |     final_quantity      |     final_portfolio_value     |
| ------ | ----------------------- | ----------------------------- |
| BTC    | 4160.219869506641749735 | 200751409.8030429976334624250 |
| ETH    |   3503.8865611503127342 |   11134790.869485909819250128 |
<br>

### Question 4 & 5 (bonus!)

> What is Nandita's overall profitability and theoretical profitability if she didn't sell any of her portfolio?

We will try to minimise how many times we access the temp table `nandita_trading_strategy` to optimise our query performance!

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_portfolio AS (
  SELECT
    transactions.ticker,
    transactions.txn_type,
    COUNT(*) AS transaction_count,
    SUM(transactions.quantity) AS total_quantity,
    SUM(transactions.quantity * prices.price) AS gross_values,
    SUM(transactions.quantity * prices.price * transactions.percentage_fee / 100) AS fees 
  FROM nandita_trading_strategy AS transactions
  INNER JOIN trading.prices
    ON transactions.ticker = prices.ticker
    AND transactions.txn_date = prices.market_date
  GROUP BY 1,2
),
cte_summary AS (
  SELECT
    ticker,
    SUM(
      CASE
        WHEN txn_type = 'BUY' THEN total_quantity
        WHEN txn_type = 'SELL' THEN -total_quantity
      END
    ) AS final_quantity,
    SUM(CASE WHEN txn_type = 'BUY' THEN gross_values ELSE 0 END) AS initial_investment,
    SUM(CASE WHEN txn_type = 'SELL' THEN gross_values ELSE 0 END) AS sales_revenue,
    SUM(CASE WHEN txn_type = 'BUY' THEN fees ELSE 0 END) AS purchase_fees,
    SUM(CASE WHEN txn_type = 'SELL' THEN fees ELSE 0 END) AS sales_fees,
    SUM(CASE WHEN txn_type = 'BUY' THEN total_quantity ELSE 0 END) AS purchase_quantity,
    SUM(CASE WHEN txn_type = 'SELL' THEN total_quantity ELSE 0 END) AS sales_quantity,
    SUM(CASE WHEN txn_type = 'BUY' THEN transaction_count ELSE 0 END) AS purchase_transactions,
    SUM(CASE WHEN txn_type = 'SELL' THEN transaction_count ELSE 0 END) AS sales_transactions
  FROM cte_portfolio
  GROUP BY ticker
),
cte_metrics AS (
  SELECT
    summary.ticker,
    summary.final_quantity * final.price AS actual_final_value,
    summary.purchase_quantity * final.price AS theoretical_final_value,
    summary.sales_revenue,
    summary.purchase_fees,
    summary.sales_fees,
    summary.initial_investment,
    summary.purchase_quantity,
    summary.sales_quantity,
    summary.purchase_transactions,
    summary.sales_transactions,
    summary.initial_investment / purchase_quantity AS dollar_cost_average,
    summary.sales_revenue / sales_quantity AS average_selling_price
  FROM cte_summary AS summary
  INNER JOIN trading.prices AS final
    ON summary.ticker = final.ticker
  WHERE final.market_date = '2021-08-29'
)
SELECT
  ticker,
  actual_final_value AS final_portfolio_value,
  ( actual_final_value + sales_revenue - purchase_fees - sales_fees ) / initial_investment AS actual_profitability,
  ( theoretical_final_value - purchase_fees ) / initial_investment AS theoretical_profitability,
  dollar_cost_average,
  average_selling_price,
  sales_revenue,
  purchase_fees,
  sales_fees,
  initial_investment,
  purchase_quantity,
  sales_quantity,
  purchase_transactions,
  sales_transactions
FROM cte_metrics;
```

</details><br>

| ticker |     final_portfolio_value     |  actual_profitability   | theoretical_profitability |    dollar_cost_average    |  average_selling_price  |       sales_revenue        |        purchase_fees         |         sales_fees         |      initial_investment      |    purchase_quantity    |    sales_quantity    | purchase_transactions | sales_transactions |
| ------ | ----------------------------- | ----------------------- | ------------------------- | ------------------------- | ----------------------- | -------------------------- | ---------------------------- | -------------------------- | ---------------------------- | ----------------------- | -------------------- | --------------------- | ------------------ |
| BTC    | 200751409.8030429976334624250 | 3.318954506414827841503 |   3.800967820444996477195 | 12686.9187126851255182628 | 12710.97315213559195557 | 10975745.05336688201117242 | 162919.943377863222128081502 | 29522.09286188312984442411 | 63735345.6973630892576024850 | 5023.705687783492459935 | 863.4858182768507102 |                   954 |                167 |
| ETH    |   11134790.869485909819250128 |  4.94126554503705553061 |    5.30805715638391209991 |    598.397257883758534604 |  542.484898862480594053 |  172591.915512909206341725 |    5783.32678170688531189239 |   447.93810830446683009024 |   2287096.578215583047801140 |   3822.0371970017654265 | 318.1506358514526923 |                   756 |                 70 |
<br>

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step10.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step12.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# Step 12 - Final Case Study Questions

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step11.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step13.md)

To finish up our entire cryptocurrency case study - let's now calculate exactly the same query that we just created for Nandita's data with our entire dataset with all mentors included!

## Create The Base Table

> Create a summary table `mentor_performance` which includes the following metrics for each member and ticker:

* Count of purchase transactions
* Initial investment
* Purchase fees
* Dollar cost average of purchases
* Count of sales transactions
* Gross revenue amount
* Sales fees
* Average selling price
* Actual Profitability (final portfolio value + gross sales revenue - purchase fees - sales fees) / initial investment amount
* Theoretical Profitability (final portfolio value with no sales - purchase fees) / initial investment amount

<details><summary>Click here to reveal the solution!</summary><br>

```sql
CREATE TEMP TABLE mentor_performance AS
WITH cte_portfolio AS (
  SELECT
    members.first_name,
    members.region,
    transactions.ticker,
    transactions.txn_type,
    COUNT(*) AS transaction_count,
    SUM(transactions.quantity) AS total_quantity,
    SUM(transactions.quantity * prices.price) AS gross_values,
    SUM(transactions.quantity * prices.price * transactions.percentage_fee / 100) AS fees 
  FROM trading.transactions
  INNER JOIN trading.members
    ON transactions.member_id = members.member_id
  INNER JOIN trading.prices
    ON transactions.ticker = prices.ticker
    AND transactions.txn_date = prices.market_date
  GROUP BY
    members.first_name,
    members.region,
    transactions.ticker,
    transactions.txn_type
),
cte_summary AS (
  SELECT
    first_name,
    region,
    ticker,
    SUM(
      CASE
        WHEN txn_type = 'BUY' THEN total_quantity
        WHEN txn_type = 'SELL' THEN -total_quantity
      END
    ) AS final_quantity,
    SUM(CASE WHEN txn_type = 'BUY' THEN gross_values ELSE 0 END) AS initial_investment,
    SUM(CASE WHEN txn_type = 'SELL' THEN gross_values ELSE 0 END) AS sales_revenue,
    SUM(CASE WHEN txn_type = 'BUY' THEN fees ELSE 0 END) AS purchase_fees,
    SUM(CASE WHEN txn_type = 'SELL' THEN fees ELSE 0 END) AS sales_fees,
    SUM(CASE WHEN txn_type = 'BUY' THEN total_quantity ELSE 0 END) AS purchase_quantity,
    SUM(CASE WHEN txn_type = 'SELL' THEN total_quantity ELSE 0 END) AS sales_quantity,
    SUM(CASE WHEN txn_type = 'BUY' THEN transaction_count ELSE 0 END) AS purchase_transactions,
    SUM(CASE WHEN txn_type = 'SELL' THEN transaction_count ELSE 0 END) AS sales_transactions
  FROM cte_portfolio
  GROUP BY
    first_name,
    region,
    ticker
),
cte_metrics AS (
  SELECT
    summary.first_name,
    summary.region,
    summary.ticker,
    summary.final_quantity * final.price AS actual_final_value,
    summary.purchase_quantity * final.price AS theoretical_final_value,
    summary.sales_revenue,
    summary.purchase_fees,
    summary.sales_fees,
    summary.initial_investment,
    summary.purchase_quantity,
    summary.sales_quantity,
    summary.purchase_transactions,
    summary.sales_transactions,
    summary.initial_investment / purchase_quantity AS dollar_cost_average,
    summary.sales_revenue / sales_quantity AS average_selling_price
  FROM cte_summary AS summary
  INNER JOIN trading.prices AS final
    ON summary.ticker = final.ticker
  WHERE final.market_date = '2021-08-29'
)
SELECT
  first_name,
  region,
  ticker,
  actual_final_value AS final_portfolio_value,
  ( actual_final_value + sales_revenue - purchase_fees - sales_fees ) / initial_investment AS actual_profitability,
  ( theoretical_final_value - purchase_fees ) / initial_investment AS theoretical_profitability,
  dollar_cost_average,
  average_selling_price,
  sales_revenue,
  purchase_fees,
  sales_fees,
  initial_investment,
  purchase_quantity,
  sales_quantity,
  purchase_transactions,
  sales_transactions
FROM cte_metrics;
```

</details><br>

Make sure to checkout the results from the temp table by running a `SELECT` query before tackling the following questions!

```sql
SELECT * FROM mentor_performance;
```

**Warning - this is a very very wide table!!!**

| first_name |    region     | ticker |     final_portfolio_value     |  actual_profitability   | theoretical_profitability |    dollar_cost_average    |  average_selling_price   |        sales_revenue        |        purchase_fees         |         sales_fees         |      initial_investment      |    purchase_quantity    |    sales_quantity     | purchase_transactions | sales_transactions |
| ---------- | ------------- | ------ | ----------------------------- | ----------------------- | ------------------------- | ------------------------- | ------------------------ | --------------------------- | ---------------------------- | -------------------------- | ---------------------------- | ----------------------- | --------------------- | --------------------- | ------------------ |
| Vipul      | United States | ETH    |  13102554.8171483815588462536 | 4.672465959057919903182 |   5.314621992146962886758 |   597.6673234944262953386 |    626.24202540473186303 |    456793.90734028892884625 |   7104.569887725402883402542 |  1188.37948073671816727685 |  2900193.5795488220132164898 |  4852.52157101720575379 |   729.420717245970714 |                   991 |                149 |
| Vikram     | India         | ETH    |    6276426.482786365114210656 |  4.31181306610612708721 |    5.89972140484864266246 |    538.402092304626902638 |   576.741885087371095795 |   557225.943027915290149790 |    4169.62855809858209505223 |  1467.03920970122463238123 |   1583560.245623696053185812 |   2941.2223099752008596 |  966.1617396549943312 |                   577 |                204 |
| Sonia      | Australia     | ETH    |  11320688.2256349723009004896 | 4.478791700263700984631 |   5.292086399343751113029 |   600.1977155852074903438 |  547.8389664223296338686 |  444504.2206952554872967260 |   6743.608268140600050792052 | 1074.114521166652869369938 |  2625122.0218275999023003858 |  4373.76210149024236043 | 811.37751773682107399 |                   864 |                161 |
| Rowan      | United States | ETH    |   4678642.5109952568421167048 | 5.074269504377240055910 |    6.70449304368406104767 |    473.813548833111016754 |  451.5349656200992805727 |  262663.3359667433250122461 |    2383.35566531251972219524 |  617.385725289504123294627 |    973205.128602539867412883 |   2053.9833252960165058 | 581.71206211245256233 |                   398 |                127 |
| Pavan      | Australia     | ETH    |    4188486.703924433521762992 |  3.85446785580589944402 |    6.16497270013013441338 |    515.248248322169372184 |   531.294867143263816005 |   572045.492969362533176448 |    3229.56956929045240213967 |  1350.07976580743016281956 |   1233880.453924375664710254 |   2394.7300314796354124 | 1076.7005825695475786 |                   462 |                215 |
| Nandita    | United States | ETH    |   11134790.869485909819250128 |  4.94126554503705553061 |    5.30805715638391209991 |    598.397257883758534604 |   542.484898862480594053 |   172591.915512909206341725 |    5783.32678170688531189239 |   447.93810830446683009024 |   2287096.578215583047801140 |   3822.0371970017654265 |  318.1506358514526923 |                   756 |                 70 |
| Leah       | Asia          | ETH    |   5011670.9776990206825808176 | 4.270686580003484588095 |    5.48302943975337301171 |    579.309226305712103035 |  661.5229873200303442848 |  403560.1542523780850137170 |    3216.06018209301609128188 |  986.188509194701148571051 |   1267016.153467224471656408 |   2187.1154401373141792 | 610.04706108140806606 |                   435 |                126 |
| Enoch      | Africa        | ETH    |   2183933.3382704268238606128 | 2.927688747446586597299 |   5.826836991147052000975 |   545.1397546539025353837 |    571.75035531306719678 |    604577.95275612948938510 |   2441.664983053686080567615 |  1602.26015552138487694330 |   951080.3934730024378543018 |  1744.65425673609669642 |  1057.415963344853958 |                   351 |                209 |
| Danny      | Australia     | ETH    |   11138441.431815681783446160 |  5.08249463426467766581 |    6.23008931789695811035 |    509.872366169852376539 |   566.702626000625094273 |   573254.802885147022737177 |    5824.68526547388391619532 |  1455.00530622275440216891 |   2302888.126083087786695727 |   4516.5972484100717280 | 1011.5619313973581290 |                   904 |                200 |
| Charlie    | United States | ETH    |    5655595.638497926206310488 |  4.38490746540649869678 |    5.82323930041798717653 |     545.48335086195787859 |   636.245983138421001829 |   505215.393166603619467180 |    3500.08393571387478289503 |  1162.34054359444856996608 |    1403940.36949523667356874 |    2573.754757641582429 |  794.0567116424364033 |                   501 |                158 |
| Ben        | Australia     | ETH    |  13428404.7308956467466546296 | 5.566492182258915860530 |   5.798153939300467470194 |   547.8409611043090877031 |    575.24111102831531919 |    124538.44970426124410866 |   6102.488840463623164634342 |   311.46640129618281001108 |  2433584.5235770879150933104 |  4442.13685422790551869 |   216.497825549417380 |                   877 |                 44 |
| Ayush      | United States | ETH    |    1311604.529255899622334984 |  2.68703356830932432729 |    5.81625080031458481996 |    546.136841365536146123 |   472.423274839163292495 |   334003.599653997130003622 |    1535.33554277335488666741 |   874.60265072177019376644 |    611528.717056667941945237 |   1119.7353314008790779 |  707.0007288859948728 |                   222 |                145 |
| Alex       | United States | ETH    |   8166074.5514961468370127832 | 5.160548701564200259435 |   6.195710408303723678880 |   512.7005436032844769009 |    594.10347686987495653 |    394356.04132861779977087 |   4190.280933001530243794585 |  1055.12264813874726085400 |  1657805.3389265534531313035 |  3233.47685039578173973 |   663.783426089917745 |                   651 |                136 |
| Abe        | United States | ETH    |    6639149.360373732402400560 |  6.30636732390684560266 |    6.96696762485071066549 |    455.956218714819773258 |   402.869591682089677282 |   102436.515287599786845294 |    2830.40882752809559852513 |   280.26871378724081389402 |   1068519.299942312419013546 |   2343.4690790139731866 |  254.2671807517156776 |                   452 |                 49 |
| Vipul      | United States | BTC    |   78502964.072588956226743050 |  2.68714530854748256805 |    3.68294320587067762687 |   13093.31447811552297915 | 13475.453907836528677637 | 13126372.591344438019363620 |   86003.42201666670006452538 | 33121.33857697519500985826 |   34054805.89838476266109091 |   2600.9308762349498788 | 974.09502352354264169 |                   491 |                202 |
| Vikram     | India         | BTC    |  166813181.437258245953618100 |  3.52715101148526165567 |    3.95599133132907749521 |   12190.13846337579877423 | 11616.444334417796046131 |  6676932.386251731199555320 |  124651.51307436673592167471 | 16956.79224576098138040873 |   49146890.77777644033111307 |   4031.6925788360780822 | 574.78279876648434158 |                   792 |                115 |
| Sonia      | Australia     | BTC    |   124284811.35069950050073250 |  3.22239151512076129431 |    3.98017619235346804918 |   12116.19259536080282520 |  13301.41484742083517680 |  12188130.03561228407096717 |  106218.63998275465210197183 | 32557.52213358600760727724 |   42308380.15320625283012337 |   3491.8873912094965336 |  916.3032786678013621 |                   692 |                192 |
| Rowan      | United States | BTC    |  123967563.642518772902551350 |  3.21604584843623520833 |    3.99480787192328942564 |   12071.72576961881153034 | 14698.463685865612609155 | 14674630.646730677455969795 |  109785.90179561532962420871 | 34896.99704422013042418676 |   43064532.63337412145429443 |   3567.3882471515063849 | 998.37853535959315513 |                   731 |                192 |
| Pavan      | Australia     | BTC    |    74876626.12728888362311500 |  2.96170097119995459091 |    4.19446871610550698321 |   11497.41992360170303301 |  12736.34639275082929004 |  13102135.31594895329161890 |   75946.04432629785510284083 | 35021.69278578816478913785 |   29668016.64332961950593339 |   2580.4064599247725600 | 1028.7200828179673870 |                   526 |                197 |
| Nandita    | United States | BTC    | 200751409.8030429976334624250 | 3.318954506414827841503 |   3.800967820444996477195 | 12686.9187126851255182628 |  12710.97315213559195557 |  10975745.05336688201117242 | 162919.943377863222128081502 | 29522.09286188312984442411 | 63735345.6973630892576024850 | 5023.705687783492459935 |  863.4858182768507102 |                   954 |                167 |
| Leah       | Asia          | BTC    |  195244116.218934723675250200 |  3.20713866637997563156 |    3.69585020094976729586 |  13047.716421455726604292 |  14163.27115481523942743 |  13167023.04333994792518748 |  162182.80997147155924445895 | 34511.92424266569639230177 |  64922183.350145074994503074 |  4975.75064119164404784 |  929.6597445190769838 |                   985 |                178 |
| Enoch      | Africa        | BTC    |  170580708.903959882263220550 |  3.32210366299759732651 |    3.81349609220645770901 |   12645.17491200523085792 | 12221.728791595667220353 |  8993630.724672519050054694 |  139549.78578174917338018370 | 22127.73733517252665241326 |   54005738.62395010934056671 |   4270.8573823425313401 | 735.87222217343213249 |                   820 |                146 |
| Danny      | Australia     | BTC    |   159477000.13128947514105900 |  3.15215421180060014193 |    3.86323307663085347221 |   12482.56627031336321059 |  12136.89819062786950087 |  13053993.84143928202879456 |  139898.65835627135429570787 | 33921.86482473383782701913 |   54679169.18667898299926584 |   4380.4429315724604872 | 1075.5626055691556454 |                   841 |                216 |
| Charlie    | United States | BTC    |  122534214.004535973744886950 |  3.72521619894663216642 |    4.00865603400732590012 |  12029.849955058029497028 |   16533.3629303089026886 |    5048387.7946428438527447 |   89519.44751889309135946118 |   13459.650465263838174873 |  34220731.332920134486598673 |  2844.65155099725936589 |   305.345489355233177 |                   557 |                 51 |
| Ben        | Australia     | BTC    |   174495457.85993726210654700 |  3.58080995618084189922 |    3.72643936325482578725 |   12940.57274048096941435 |   12007.5028729516103273 |    2379058.8188878469437270 |  124879.65939037520247690716 |  6292.82529374197896891580 |   49358482.11912615398782341 |   3814.2424689381731354 |   198.131022250011036 |                   738 |                 38 |
| Ayush      | United States | BTC    |  190375533.507735667440266700 |  3.60665921157546573899 |    3.94587234371446856760 |  12221.424291634983319324 |  11627.47349802419417012 |   5849092.67497492474683032 |  137094.21663401017780783864 | 15782.14185896643545309336 |  54363813.801684160086909672 |  4448.23880624893711454 |  503.0407229884321422 |                   879 |                 95 |
| Alex       | United States | BTC    |   106225322.51226045757462950 |  3.17134902464366229781 |    3.64732289428635720234 |   13221.31584224600059279 |   10912.7808704054692250 |    4864305.0963092239886611 |   86273.62341244515836663134 |   12991.807119280435744693 |   34997838.87410784294077066 |   2647.0768334782105019 |   445.743862547520261 |                   534 |                 84 |
| Abe        | United States | BTC    |   179533509.46040851816270350 |  3.45022907603633744257 |    4.02573821957975606285 |   11978.89286334087078326 |  11297.72474955164239817 |   9629772.49687926822047538 |  142276.80367018421615985439 | 24216.72648756990733881614 |   54778040.60600280511777383 |   4572.8800842388871361 |  852.3638794847991004 |                   900 |                171 |
<br>

## Question 1

> Which mentors have the greatest actual profitability for each ticker?

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_ranks AS (
SELECT
  first_name,
  ticker,
  actual_profitability,
  RANK() OVER (PARTITION BY ticker ORDER BY actual_profitability DESC) AS profitability_rank
FROM mentor_performance
)
SELECT * FROM cte_ranks
WHERE profitability_rank = 1;
```

</details><br>

| first_name | ticker |  actual_profitability  | profitability_rank |
| ---------- | ------ | ---------------------- | ------------------ |
| Charlie    | BTC    | 3.72521619894663216642 |                  1 |
| Abe        | ETH    | 6.30636732390684560266 |                  1 |
<br>

## Question 2

> Which mentors have the greatest difference in actual vs theoretical profitability for each ticker?

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_ranks AS (
SELECT
  first_name,
  ticker,
  ABS(actual_profitability - theoretical_profitability) AS difference,
  RANK() OVER (
    PARTITION BY ticker
    ORDER BY ABS(actual_profitability - theoretical_profitability) DESC
  ) AS difference_rank
FROM mentor_performance
)
SELECT * FROM cte_ranks
WHERE difference_rank = 1;
```

</details><br>

| first_name | ticker |       difference       | difference_rank |
| ---------- | ------ | ---------------------- | --------------- |
| Pavan      | BTC    | 1.23276774490555239230 |               1 |
| Ayush      | ETH    | 3.12921723200526049267 |               1 |
<br>

## Question 3

> What is the total amount of sales revenue made by all mentors for each region? (combined BTC and ETH)

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  region,
  SUM(sales_revenue) AS total_sales
FROM mentor_performance
GROUP BY region
ORDER BY total_sales DESC;
```

</details><br>

|    region     |         total_sales          |
| ------------- | ---------------------------- |
| United States | 66396367.0625050180915045221 |
| Australia     | 42437660.9781423926224266410 |
| Asia          | 13570583.1975923260102011970 |
| Africa        |   9598208.677428648539439794 |
| India         |   7234158.329279646489705110 |
<br>

## Question 4

> What is the average actual profitability for each region for each ticker?

<details><summary>Click here to reveal the solution!</summary><br>

```sql
SELECT
  region,
  ticker,
  AVG(actual_profitability) AS avg_profitability
FROM mentor_performance
GROUP BY region, ticker
ORDER BY ticker, avg_profitability DESC;
```

</details><br>

|    region     | ticker |    avg_profitability    |
| ------------- | ------ | ----------------------- |
| India         | BTC    |  3.52715101148526165567 |
| Africa        | BTC    |  3.32210366299759732651 |
| United States | BTC    | 3.310799882085806180525 |
| Australia     | BTC    |  3.22926416357553948159 |
| Asia          | BTC    |  3.20713866637997563156 |
| United States | ETH    | 4.746694009665583482267 |
| Australia     | ETH    | 4.745561593148298488748 |
| India         | ETH    |  4.31181306610612708721 |
| Asia          | ETH    | 4.270686580003484588095 |
| Africa        | ETH    | 2.927688747446586597299 |
<br>

## Question 5

> Which mentors have the largest initial investment in each ticker?

<details><summary>Click here to reveal the solution!</summary><br>

```sql
WITH cte_rank AS (
SELECT
  first_name,
  ticker,
  initial_investment,
  RANK() OVER (PARTITION BY ticker ORDER BY initial_investment DESC) AS investment_rank
FROM mentor_performance
)
SELECT * FROM cte_rank
WHERE investment_rank = 1;
```

</details><br>

| first_name | ticker |     initial_investment      | investment_rank |
| ---------- | ------ | --------------------------- | --------------- |
| Leah       | BTC    | 64922183.350145074994503074 |               1 |
| Vipul      | ETH    | 2900193.5795488220132164898 |               1 |
<br>

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step11.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step13.md)

<p align="center">
    <img src="./../images/sql-masterclas-banner.png" alt="sql-masterclass-banner">
</p>

[![forthebadge](./../images/badges/version-1.0.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/powered-by-coffee.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)]()
[![forthebadge](https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg)]()

# SQL Masterclass Summary

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step12.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/the-end.md)

Congratulations you have reached the end of this SQL Masterclass!

Here are some of the topics which you covered in this short but sweet SQL Masterclass course:

> Step 2: Inspecting the `trading.members` table

* Selecting rows and columns from database tables with `SELECT`
* Use `LIMIT` to only return a set number of rows from a query
* Counting the number of records using `COUNT(*)`
* Counting the number of unique column and table records using `COUNT(DISTINCT)
* Filtering data using a `WHERE` filter
* Selecting `DATE` ranges using `BETWEEN`, `>`, `>=`, `<`, `<=`
* Using the `IN` and `NOT IN` filter conditions to remove and keep records
* Use `CASE WHEN` to apply simple if-else logic to an existing column

> Step 3: Analyzing daily BTC and ETH prices in the `trading.prices` table

* Finding the `MIN` and `MAX` dates
* Use `GROUP BY` to aggregate data at different levels for analysis
* Extracting information from dates using `DATE_TRUNC` and `EXTRACT`
* Using `DATE_TRUNC` to obtain the begining date of month for a `DATE`
* Using `AVG` to find the average price
* Casting float data types to an exact `NUMERIC` to use with the `ROUND` function
* Using `AND` conditions to apply multiple logical rules for `WHERE` filters
* Using `SUM CASE WHEN` to aggregate logical values similar to a COUNTIF in Excel
* Casting `INTEGER` data types to a `NUMERIC` to avoid integer floor division errors

> Step 4: View all transaction histories in the `trading.transactions` table

* More advanced usage of `SUM CASE WHEN` to replicate SUMIF functionality in Excel
* How to filter records from a `GROUP BY` result using the `HAVING` clause
* Using CTEs and subqueries to perform the same filtering of results
* Use a `RANK` window function to perform custom ordering for a results set

> Step 5: Starting data analysis

* Interpreting entity relationship diagrams (ERDs) to visualize table joins
* Analyzing ranges of data to make sure the analysis periods are aligned
* Perform an `INNER JOIN` to combine datasets to select columns from both tables
* Combining CTEs and joins for step-wise queries
* Combining multiple aggregation functions to generate larger table outputs

> Steps 6-7: Planning ahead and using base tables for data analysis

* Drop and create a temporary table to re-use in future SQL queries
* Add time `INTERVAL` to a date
* Use `ALTER` and `UPDATE` statements to manipulate an existing temporary table
* Use a custom `WINDOW FRAME` clause to specify a sliding window for cumulative metrics
* Use a `SUM` window function to calculate a denominator value for percentage calculations
* Use `MAX CASE WHEN` to pivot data from long to wide

> Steps 8-12: Final Case Study Scenarios

* Creating simplified data scenarios to better understand each question
* Implementing a `SUM PRODUCT` aggregation to calculate initial investments
* Performing multiple joins to the same tables with different joining conditions
* Multiplying many columns to generate fees based off percentages
* Calculating hypothetical scenarios and implementing complex logic using SQL
* Creating a complete CTE workflow to generate a reporting dataset
* Aggregating data at multiple levels to generate multiple insights

[![forthebadge](./../images/badges/go-to-previous-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/step12.md)
[![forthebadge](./../images/badges/go-to-next-tutorial.svg)](https://github.com/datawithdanny/sql-masterclass/tree/main/course-content/the-end.md)
