# Reports

## Structure

<img src="images/block.png">

Data structure:



Report can contains blocks. Single block is a separate part of report and usually it can be visualize as single table (or a tab in Excel file). Each blocks can be created from many ordes. To get final block some operation have to be run like join (left_join, outer_join, innet_join), union, merge_chain, sort, or pivot operation.

Date filtering:

Filtering operation on date dimension can use predefined values: today, yesterday, week_begin, month_begin, year_begin, quarter_begin, quarter_end, n_day_ago, last_n_month_begin, last_n_month_end where n is a number of days

>Backend simple input JSON example format (only one order and one block):

```json
  {
    "currency": String,
    "data_sources_overwrite": {
      "sort": [ { String: String, ... } ],
      "dimensions": [ String, ... ],
      "metrics": [ String, ... ],
      "filters": [
        {
          "operator": String,
          "value": [ ... ],
          "field": String
        }, ... ],
      "page_limit": Integer,
      "page_number": Integer
    },
    "configid": Integer
  }
```

> Backend output JSON format:

```json
{
    "data": [ { String: ..., ...}, {...}, ... ],
    "metadata": {
      "metric": {
        String: {
          "format": String,
          "category": String,
          "min": Float,
          "max": Float,
          "avg": Float,
          "cnt": Integer,
          "sum": Float
        }, ... },
      "metrics_order": [ String, ... ],
      "dimension": {
        String: {
          "dw_name_id": String,
          "alt_text": String,
          "dict": {
            String: String
          },
          "is_translatable": Bool
        }, ... },
      "dimensions_order": [ String, ... ],
      "currency": String,
      "show_summary": Integer,
      "data_blockid": Integer,
      "page_limit": Integer,
      "page_number": Integer,
      "data_source_order": Integer,
      "data_sources_overwritten": { ... }
    },
    "status": {
      "code": Integer,
      "items": Integer,
      "mem": Integer,
      "msg": String,
      "source": String,
      "worker": String,
      "elapsed_time": Float
    }
  }
```

currency – 3 letter shortcut of currency, default EUR; for using customer setting set to -C-

data_sources_overwrite – key with report parameters

sort – list of hashes where key is column name and value is order of sort direction: asc, desc

dimensions – list of needed dimensions  (at least one is required), list of available dimensions per report can be obtain url to doc of frontend WS with dimension list

metrics – list of needed metrics (at least one is required), list of available metrics per report can be obtain url to doc of frontend WS with dimension list

filters – list of hashes with filter structure, required list per report can be obtain url to doc of frontend WS with required filter list

operator – supported operatos: exists, does_not_exist, does_not_existid, eq, ne, lt, le, gt, ge, in, not_in, between, contains, does_not_contain, starts_with, ends_with

          value – single vale or array (depends on operator)

          field – name of filtering column (dimension or metric)

page_limit – number of pages in report

page_number – number of report page

configid – report configuration id, list of available reports can be obtain url to doc of frontent WS with lists of reports

### output

data – key with report data, returned as array of hash, where keys in hash represents columns (dimensions and metrics)

metadata – key contains additional information about data

metric – key with metrics information's

format – metric format: text, url, integer, float, percent, currency, date, time, datetime, boolean, text_array

category – metric category,

min - if numeric format minimum value of metric

max - if numeric format maximum value of metric

avg - if numeric format average value of metric

cnt - if numeric format maximum value of metric

sum - if numeric format, sum of all values

metrics_order – array of dimensions, describe order; in OWA metrics are putted after dimensions by default

dimension – key with dimensions information’s

dw_name_id – name of field with id

alt_text -

dict – hash contains dictionary with translation id values to string names

is_translatable -

dimensions_order – array of dimensions, describes order; in OWA dimesions are putted before metrics by default

currency – 3 letter shortcut of currency

show_summary – information flag about summary row format

data_blockid – number of block (url to data description)

page_limit – number of pages in report

page_number – number of report page

data_source_order – number of order (url to data description)

data_sources_overwritten – hash with not standard parameters  used in report and all filters

status – key contains information about  report processing:

code – numeric error code, default 0,

items – count number of items in data key

mem – worker memory consumption in MB (it should be filter out in final version ?)

msg – sting error message related with code

source – shows source data  (external, db, cache)

worker – generation process signature

elapsed_time – generation time in seconds

## Configs

### Channels (configid: 1)

backend_name|column group|api_name|display name|description|data type|example
|-|-|-|-|-|
acc_channel|Channel Details|acc_channel|Accounting Channel|The name of the Accounting Channel.|string|Google
acc_group|Channel Details|acc_group|Accounting Group|The name of the Accounting Group.|string|SEA
acc_invoice_channel|Channel Details|acc_invoice_channel|Invoice Channel|The name of the Invoice Channel.|string|Consulting
acc_invoice_group|Channel Details|acc_invoice_group|Invoice Group|The name of the Invoice Group.|string|Service
acc_invoice_subchannel|Channel Details|acc_invoice_subchannel|Invoice Subchannel|The name of the Invoice Subchannel.|string|MSN Non Brand
acc_subchannel|Channel Details|acc_subchannel|Accounting Subchannel|The name of the Accounting Subchannel.|string|Google Brand
acc_subgroup|Channel Details|acc_subgroup|Accounting Subgroup|The name of the Accounting Subgroup.|string|SEA Brand
customer|Basic|customer|Account|The name of the `customer`.|string|Demo Account
customer_trackgroup|Basic|trackgroup|Channel|The name of the tracking channel.|string|Google Ads Mobile
date|Time|date|Date|Date in YYYY-MM-DD format.|int|08/08/2018
day_of_quarter|Time Details|day_of_quarter|Day of Quarter|The ordinal day number of the quarter of the year in DD format.|int|43
day_of_week|Time Details|day_of_week|Day of Week|The name of the day of the week.|string|Sunday
day_of_year|Time Details|day_of_year|Day of Year|The ordinal day number of the year in DDD format.|int|311
level1_customer_trackgroup|Channel Details|level1_trackgroup|1st Level Channel|The name of the first-level `trackgroup` within the `trackgroup` tree.|string|Display
level2_customer_trackgroup|Channel Details|level2_trackgroup|2nd Level Channel|The name of the second-level `trackgroup` within the `trackgroup` tree.|string|Remarketing
level3_customer_trackgroup|Channel Details|level3_trackgroup|3rd Level Channel|The name of the third-level `trackgroup` within the `trackgroup` tree.|string|Google Ads
level4_customer_trackgroup|Channel Details|level4_trackgroup|4th Level Channel|The name of the fourth-level `trackgroup` within the `trackgroup` tree.|string|Google Ads Mobile
level5_customer_trackgroup|Channel Details|level5_trackgroup|5th Level Channel|The name of the fifth-level `trackgroup` within the `trackgroup` tree.|string|Google Ads Mobile Brand
month|Time|month|Month|The name of the month.|string|March
month_of_year|Time Details|month_of_year|Month of Year|The ordinal month number of the year in YYYY-MM format.|int|2018-09
tag|Basic|trackgroup_tag|Channel Tag|The name defining a label attributed to the `trackgroup`.|string|attribution_channel
week|Time|week|Week|The ordinal week number of the year in WW format. The first week starts on Monday nearest to January 1.|int|16
week_of_year|Time Details|week_of_year|Week of Year|The ordinal week number of the year in YYYY-WW format. The first week starts on Monday nearest to January 1.|int|2018-19
week_of_year_friday|Time Details|week_of_year_friday|Week of Year (from Friday)|The ordinal Friday-based week number of the year in YYYY-WW format. The first week of such year starts on Friday nearest to January 1.|int|2018-19
year|Time|year|Year|The year in YYYY format.|int|2018
year_by_week|Time Details|year_by_week|Year by Week|The week-numbering year number in YYYY format. Such year starts on Monday nearest to January 1.|int|2018
year_quarter|Time Details|year_quarter|Quarter of Year|The ordinal number of the quarter of the year in YYYY-Q format.|int|2018-3
group_type|Channel Details|trackgroup_group|Channel Group|The group of the `trackgroup`.|string|Display
