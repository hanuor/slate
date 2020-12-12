---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Bytemine.io's API Hub. You can use our API to access API endpoints and our own signals, which can get information on Fundamentals of a Ticker, Historical Data, Pre-Processed Signals and more from our database.

Currently, we have language bindings in only Shell. However, you can easily translate this to whichever platform/language you are using as these are just simple API calls. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

We offer compelling data services for a highly competitive price, if you decide to switch to one of our premium plans. On top of that you get access to the Trader's platform as well. 

If you have any questions or want to raise a concern/query, please drop in a mail at hello@bytemine.io. We'll try our best to answer your queries within 24 working hours.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"

```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

To use the API you have to have an API key. You can get an API key from our [developer portal](https://bytemine.io/developers).

The API key should be included in all API requests to the server in a header that looks like the following:

`Authorization: YOUR_API_KEY`

<aside class="notice">
You must replace <code>YOUR_API_KEY</code> with your personal API key.
</aside>

# Signals

## Candlestick Patterns

```shell
curl https://bytemine.io/api/checkForCandlesticks/{api_key}/TSLA/5m
  
```

```javascript
$.ajax({
        url: "https://bytemine.io/api/checkForCandlesticks/{api_key}/TSLA/5m",
        type: 'GET',
        success: function(data) {
            console.log(data);
        }
    });
```

> The above command returns JSON structured like this:

```json
{
   "success": true,
   "data": [
      {
         "time": "2020-12-08 09:30",
         "pattern": "Bearish Engulfing",
         "close": 604.48,
         "high": 654.32,
         "open": 653.69,
         "low": 588
      }
   ]
}
```

You can get Candlestick Patterns from our API endpoints. This can be achieved using Long Polling. However, make sure to not call our Endpoints without adding atleast a **1 Min Delay**.

### HTTP Request

`GET https://bytemine.io/api/checkForCandlesticks/{api_key}/{ticker}/{timeframe}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
api_key | true | API Key is required for authentication.
ticker | true | A ticker/symbol is needed for the appropriate candlestick pattern to be returned.
timeframe | true | Only one Timeframe out of these - 1m/2m/5m/15m/30m/60m/90m/1d/5d/1wk/1mo 

<aside class="warning">
<br>
1. Remember to add atleast <strong>1 Min Delay</strong> if you're making repeated requests.<br>
2. Timeframes should be in string format. Checkout the example below.
</aside>

### Example HTTP Request

`GET https://bytemine.io/api/checkForCandlesticks/5fe69c95ed70a9869d9f9af7d8400a6673bb9ces/AAPL/5m`

## Trends

```shell
curl https://bytemine.io/api/getTickerTrend/{api_key}/TSLA/5m
```

```javascript
$.ajax({
        url: "https://bytemine.io/api/getTickerTrend/{api_key}/TSLA/5m",
        type: 'GET',
        success: function(data) {
            console.log(data);
        }
    });
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

Trends can be classified into two categories - **Bullish** and **Bearish**. This can be achieved using Long Polling. However, make sure to not call our Endpoints without adding atleast a **1 Min Delay**.


### HTTP Request

`GET https://bytemine.io/api/getTickerTrend/{api_key}/{ticker}`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve


