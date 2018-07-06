# Endpoints

<aside class="endpointnotice"><span style="font-size:20px">All API calls should be done to <b>http://owapro.hurra.com</b></span></aside>

## Fetch a list of customers

> This request:

```shell
curl --request GET \
  --url 'http://owapro.hurra.com/api/report/customer?page_limit={{page_limit}}&page_number={{page_number}}' \
  -H 'Accept: application/json' \
  -H "Authorization: Bearer {access_token}"
```

> Gives the following 200 response:

```shell
response???
```

<aside class="getmethod"><span style="font-size:20px"><b>GET</b> /api/report/customer</span></aside>

Returns all available `customer` names and IDs.

##### QUERY PARAMS
|||
|-|-|
|`page_limit`|<b>integer</b><br>The number of pages in the response.|
|`page_number`|<b>integer</b><br>The page number in the response.|

## Fetch a list of trackgroups

> This request:

```shell
curl --request GET \
  --url 'http://owapro.hurra.com/api/report/customer_trackgroup?customerid={{customerid}}&page_limit={{page_limit}}&page_number={{page_number}}' \
  -H "Authorization: Bearer {access_token}"
```

> Gives the following 200 response:

```shell
response???
```

<aside class="getmethod"><span style="font-size:20px"><b>GET</b> /api/report/customer_trackgroup</span></aside>

Returns `customer_trackgroup` names and IDs within the specified `customerid`.

##### QUERY PARAMS
|||
|-|-|
|`customerid`|<b>integer</b> <span style="color: red"><i>(required)</i></span><br>The ID of the `customer`.|
|`page_limit`|<b>integer</b><br>The number of pages in the response.|
|`page_number`|<b>integer</b><br>The page number in the response.|

## Fetch a list of reports

> This request:

```shell
curl --request GET \
  --url 'http://owapro.hurra.com/api/report/config?page_limit={{page_limit}}&page_number={{page_number}}' \
  -H "Authorization: Bearer {access_token}"
```

> Gives the following 200 response:

```shell
response???
```

<aside class="getmethod"><span style="font-size:20px"><b>GET</b> /api/report/config</span></aside>

Returns all available report `config` names and IDs.

##### QUERY PARAMS
|||
|-|-|
|`page_limit`|<b>integer</b><br>The number of pages in the response.|
|`page_number`|<b>integer</b><br>The page number in the response.|

## Fetch a report's details

> This request:

```shell
curl --request GET \
  --url 'http://owapro.hurra.com/api/report/config/{{configid}}?customerid={{customerid}}' \
  -H "Authorization: Bearer {access_token}"
```

> Gives the following 200 response:

```shell
response???
```

<aside class="getmethod"><span style="font-size:20px"><b>GET</b> /api/report/config/<i>{{configid}}</i></span></aside>

Returns report `config` details, which include required filters, default dimensions and metrics, and all other columns available for the report for the defined `customer`.

##### PATH VARIABLES
|||
|-|-|
|`configid`|<b>integer</b> <span style="color: red"><i>(required)</i></span><br>The ID of the report `config`. See the list of all OWAPro reports <a href="#reports">here</a>.|

##### QUERY PARAMS
|||
|-|-|
|`customerid`|<b>integer</b> <span style="color: red"><i>(required)</i></span><br>The ID of the `customer`.|

## Generate a report

> This is an example for requesting the Channels report (2 blocks):

```json
{
  "params": {
    "session_key": "4053-mbytgca2uGvs-14",
    "currency": "-C-",
    "user": {
      "lang": "EN",
      "userid": "4053",
      "role": "developer"
    },
    "data_sources_overwrite": {
      "filters": [
        {
          "operator": "between",
          "value": [
            "7_day_ago",
            "yesterday"
          ],
          "field": "date"
        },
        {
          "operator": "in",
          "value": [
            "27372",
            "27552",
            "27554",
            "27556",
            "27690",
            "27692",
            "27694",
            "28364",
            "28366",
            "28368",
            "28370",
            "28620",
            "33584",
            "33638",
            "33640",
            "33642",
            "33728",
            "39608",
            "40146",
            "40706",
            "42132"
          ],
          "field": "customer_trackgroupid"
        }
      ],
      "data_blocks": {
        "1": [
          {
            "sort": [
              {
                "date": "asc"
              }
            ],
            "dimensions": [
              "date"
            ],
            "metrics": [
              "click_count_pub",
              "sale_count"
            ],
            "page_number": 1
          }
        ],
        "2": [
          {
            "dimensions": [
              "customer_trackgroup",
              "customer"
            ],
            "metrics": [
              "uu_count",
              "view_count_pub",
              "click_count_pub",
              "ctr",
              "cpc",
              "lead_count",
              "sale_count",
              "sale_conv",
              "cpo",
              "sale_amount",
              "assist_sale_count",
              "assist_sale_amount",
              "cost_income",
              "roas",
              "kuv"
            ],
            "page_limit": 250,
            "page_number": 1
          }
        ]
      }
    },
    "configid": "1"
  },
  "non_blocking": 1,
  "url": "http://api.owapro.hurra.com/owa/generate_reports",
  "method": "POST"
}
```

> Example JSON output for the Channels report - (2 blocks):

```json
{
  "status": 1,
  "meta_data": {
    "app_version": "3.76.1",
    "owa3_log_reqid": "3190034"
  },
  "data": [
    {
      "status": {
        "source": "cache",
        "msg": "OK",
        "worker": "owa-fra1-cron7 PID:371 2018-04-19 16:36:32",
        "mem": 205,
        "elapsed_time": "0.149983",
        "code": 0,
        "items": 7
      },
      "data_blockid": "1",
      "metadata": {
        "metrics_order": [
          "click_count_pub",
          "sale_count"
        ],
        "show_summary": 0,
        "metric": {
          "sale_count": {
            "format": "integer",
            "min": "14",
            "avg": "26.4285714285714",
            "max": "34",
            "category": "sale",
            "sum": 185,
            "cnt": 7
          },
          "click_count_pub": {
            "format": "integer",
            "min": 0,
            "avg": 0,
            "max": 0,
            "category": "click",
            "sum": 0,
            "cnt": 0
          }
        },
        "dimensions_order": [
          "date"
        ],
        "currency": "EUR",
        "sort": [
          {
            "date": "asc"
          }
        ],
        "dimension": {
          "date": {
            "dw_name_id": "date",
            "alt_text": "",
            "is_translatable": "0"
          }
        },
        "data_sources_overwritten": {
          "include_organic": "0",
          "dimensions": [
            "date"
          ],
          "filters": [
            {
              "operator": "between",
              "value": [
                "7_day_ago",
                "yesterday"
              ],
              "field": "date"
            },
            {
              "operator": "in",
              "value": [
                "27372",
                "27552",
                "27554",
                "27556",
                "27690",
                "27692",
                "27694",
                "28364",
                "28366",
                "28368",
                "28370",
                "28620",
                "33584",
                "33638",
                "33640",
                "33642",
                "33728",
                "39608",
                "40146",
                "40706",
                "42132"
              ],
              "field": "customer_trackgroupid"
            }
          ],
          "page_limit": null,
          "data_blockid": "1",
          "metrics": [
            "click_count_pub",
            "sale_count"
          ],
          "data_source_order": "1",
          "page_number": 1,
          "sort": [
            {
              "date": "asc"
            }
          ]
        }
      },
      "data": [
        {
          "sale_count": "23",
          "date": "2018-04-13",
          "click_count_pub": 0
        },
        {
          "sale_count": "14",
          "date": "2018-04-14",
          "click_count_pub": 0
        },
        {
          "sale_count": "19",
          "date": "2018-04-15",
          "click_count_pub": 0
        },
        {
          "sale_count": "33",
          "date": "2018-04-16",
          "click_count_pub": 0
        },
        {
          "sale_count": "31",
          "date": "2018-04-17",
          "click_count_pub": 0
        },
        {
          "sale_count": "31",
          "date": "2018-04-18",
          "click_count_pub": 0
        },
        {
          "sale_count": "34",
          "date": "2018-04-19",
          "click_count_pub": 0
        }
      ]
    },
    {
      "status": {
        "code": 0,
        "items": 14,
        "pages": 1
      },
      "data_blockid": "2",
      "data": [
        {
          "sale_count": 0,
          "roas": 0,
          "view_count_pub": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": 0,
          "customer_trackgroupid": "33584",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": 0,
          "sale_conv": 0,
          "cpc": 0,
          "kuv": 0,
          "assist_sale_count": 0,
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "5",
          "view_count_pub": 0,
          "roas": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "1991.53001403809",
          "customer_trackgroupid": "27690",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": "6116.29",
          "sale_conv": 0,
          "kuv": 0,
          "cpc": 0,
          "assist_sale_count": "11",
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "9",
          "view_count_pub": 0,
          "roas": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "5466.28002929688",
          "customer_trackgroupid": "33638",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": "474.96",
          "sale_conv": 0,
          "kuv": 0,
          "cpc": 0,
          "assist_sale_count": "1",
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "7",
          "roas": 0,
          "view_count_pub": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "2833.08990478516",
          "customer_trackgroupid": "33642",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": 0,
          "sale_conv": 0,
          "cpc": 0,
          "kuv": 0,
          "assist_sale_count": 0,
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": 0,
          "roas": 0,
          "view_count_pub": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": 0,
          "customer_trackgroupid": "33640",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": 0,
          "sale_conv": 0,
          "cpc": 0,
          "kuv": 0,
          "assist_sale_count": 0,
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": 0,
          "roas": 0,
          "view_count_pub": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": 0,
          "customer_trackgroupid": "27552",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": 0,
          "sale_conv": 0,
          "cpc": 0,
          "kuv": 0,
          "assist_sale_count": 0,
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "60",
          "view_count_pub": 0,
          "roas": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "37151.0903320312",
          "customer_trackgroupid": "27554",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": "3166.51",
          "sale_conv": 0,
          "kuv": 0,
          "cpc": 0,
          "assist_sale_count": "5",
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": 0,
          "view_count_pub": 0,
          "roas": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": 0,
          "customer_trackgroupid": "40146",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": "3723.97",
          "sale_conv": 0,
          "kuv": 0,
          "cpc": 0,
          "assist_sale_count": "4",
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "12",
          "roas": 0,
          "view_count_pub": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "5066.22994995117",
          "customer_trackgroupid": "28370",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": 0,
          "sale_conv": 0,
          "cpc": 0,
          "kuv": 0,
          "assist_sale_count": 0,
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "4",
          "view_count_pub": 0,
          "roas": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "874.859992980957",
          "customer_trackgroupid": "27556",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": "3757.26",
          "sale_conv": 0,
          "kuv": 0,
          "cpc": 0,
          "assist_sale_count": "6",
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "12",
          "view_count_pub": 0,
          "roas": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "5578.69989013672",
          "customer_trackgroupid": "28366",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": "791.58",
          "sale_conv": 0,
          "kuv": 0,
          "cpc": 0,
          "assist_sale_count": "2",
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "74",
          "roas": 0,
          "view_count_pub": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "44429.1295166016",
          "customer_trackgroupid": "27372",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": 0,
          "sale_conv": 0,
          "cpc": 0,
          "kuv": 0,
          "assist_sale_count": 0,
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": "2",
          "view_count_pub": 0,
          "roas": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": "691.580001831055",
          "customer_trackgroupid": "27692",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": "416.62",
          "sale_conv": 0,
          "kuv": 0,
          "cpc": 0,
          "assist_sale_count": "1",
          "customerid": "4445",
          "ctr": 0
        },
        {
          "sale_count": 0,
          "view_count_pub": 0,
          "roas": 0,
          "cost_income": 0,
          "click_count_pub": 0,
          "uu_count": 0,
          "sale_amount": 0,
          "customer_trackgroupid": "40706",
          "cpo": 0,
          "lead_count": 0,
          "assist_sale_amount": "916.6",
          "sale_conv": 0,
          "kuv": 0,
          "cpc": 0,
          "assist_sale_count": "2",
          "customerid": "4445",
          "ctr": 0
        }
      ],
      "metadata": {
        "currency": "EUR",
        "metrics_order": [
          "uu_count",
          "view_count_pub",
          "click_count_pub",
          "ctr",
          "cpc",
          "lead_count",
          "sale_count",
          "sale_conv",
          "cpo",
          "sale_amount",
          "assist_sale_count",
          "assist_sale_amount",
          "cost_income",
          "roas",
          "kuv"
        ],
        "show_summary": "3",
        "dimension": {
          "customer_trackgroup": {
            "dw_name_id": "customer_trackgroupid",
            "alt_text": "",
            "dict": {
              "27372": "Other",
              "27552": "Hurra Google AdWords Brand",
              "27554": "Hurra Google AdWords Non Brand",
              "27556": "Hurra Google RMKT (Remarketing",
              "27690": "Google Product Listing Ads",
              "27692": "PLA mobile",
              "28366": "Hurra Google Tablet Non Brand",
              "28370": "Hurra Google Mobile Non Brand",
              "33584": "Bing Shopping",
              "33638": "Hurra Bing Ads",
              "33640": "Hurra Bing Ads Non Brand",
              "33642": "Hurra Bing Ads Brand",
              "40146": "Hurra Google DSA",
              "40706": "PLA tablet"
            },
            "is_translatable": "0"
          },
          "customer": {
            "dw_name_id": "customerid",
            "alt_text": "",
            "dict": {
              "4445": "Toolport FR"
            },
            "is_translatable": "0"
          }
        },
        "metric": {
          "sale_count": {
            "format": "integer",
            "avg": "20.5555555555556",
            "max": "74",
            "category": "sale",
            "sum": 185,
            "cnt": 9
          },
          "lead_count": {
            "format": "integer",
            "category": "lead"
          },
          "roas": {
            "sum_sa": "104082.489631653",
            "format": "currency",
            "avg": 0,
            "category": "other",
            "sum": ""
          },
          "view_count_pub": {
            "format": "integer",
            "category": "view"
          },
          "assist_sale_amount": {
            "format": "currency",
            "avg": "2420.47375",
            "min": "416.62",
            "max": "6116.29",
            "category": "sale",
            "sum": "19363.79",
            "cnt": 8
          },
          "sale_conv": {
            "sum_sc": 185,
            "format": "percent",
            "avg": 0,
            "category": "sale",
            "sum": ""
          },
          "cost_income": {
            "format": "currency",
            "category": "other"
          },
          "kuv": {
            "sum_sa": "104082.489631653",
            "format": "percent",
            "avg": 0,
            "category": "other",
            "sum": ""
          },
          "cpc": {
            "format": "currency",
            "avg": 0,
            "category": "click",
            "sum": ""
          },
          "click_count_pub": {
            "format": "integer",
            "category": "click"
          },
          "uu_count": {
            "format": "integer",
            "category": "user"
          },
          "assist_sale_count": {
            "format": "integer",
            "avg": 4,
            "min": "1",
            "max": "11",
            "category": "sale",
            "sum": 32,
            "cnt": 8
          },
          "sale_amount": {
            "format": "currency",
            "avg": "11564.7210701836",
            "max": "44429.1295166016",
            "category": "sale",
            "sum": "104082.489631653",
            "cnt": 9
          },
          "cpo": {
            "sum_sc": 185,
            "format": "currency",
            "avg": 0,
            "category": "sale",
            "sum": ""
          },
          "ctr": {
            "format": "percent",
            "avg": 0,
            "category": "click",
            "sum": ""
          }
        },
        "dimensions_order": [
          "customer_trackgroup",
          "customer"
        ],
        "data_sources_overwritten": {
          "include_organic": "0",
          "dimensions": [
            "customer_trackgroup",
            "customer"
          ],
          "filters": [
            {
              "operator": "between",
              "value": [
                "7_day_ago",
                "yesterday"
              ],
              "field": "date"
            },
            {
              "operator": "in",
              "value": [
                "27372",
                "27552",
                "27554",
                "27556",
                "27690",
                "27692",
                "27694",
                "28364",
                "28366",
                "28368",
                "28370",
                "28620",
                "33584",
                "33638",
                "33640",
                "33642",
                "33728",
                "39608",
                "40146",
                "40706",
                "42132"
              ],
              "field": "customer_trackgroupid"
            }
          ],
          "page_limit": 250,
          "data_blockid": "2",
          "metrics": [
            "uu_count",
            "view_count_pub",
            "click_count_pub",
            "ctr",
            "cpc",
            "lead_count",
            "sale_count",
            "sale_conv",
            "cpo",
            "sale_amount",
            "assist_sale_count",
            "assist_sale_amount",
            "cost_income",
            "roas",
            "kuv"
          ],
          "data_source_order": "1",
          "page_number": 1,
          "sort": null
        }
      }
    }
  ],
  "message": {
    "info": {},
    "error": {}
  }
}
```

<aside class="postmethod"><span style="font-size:20px"><b>POST</b> /api/report/dw_generate_report</i></span></aside>

Generates a report according to the config; i.e., filters, dimensions, and metrics. The config is specified in the request header.

##### HTTP HEADERS
|||
|-|-|
|`configid`|<b>integer</b> <span style="color: red"><i>(required)</i></span><br>The ID of the report `config`. See the list of all OWAPro reports <a href="#reports">here</a>.|
