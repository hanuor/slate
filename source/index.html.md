---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='http://bytemine.io/pricing?utm_source=docs' target="_blank">Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Bytemine.io's API Hub. You can use our API to access API endpoints and our own signals, which can get information on Fundamentals of a Ticker, Historical Data, Pre-Processed Signals and more from our database.

Currently, we have language bindings in only Shell. However, you can easily translate this to whichever platform/language you are using as these are just simple API calls. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

We offer compelling data services for a highly competitive price, if you decide to switch to one of our premium plans. On top of that you get access to the Trader's platform as well. 

If you have any questions or want to raise a concern/query, please drop in a mail at **hello@bytemine.io**. We'll try our best to answer your queries within 24 working hours.

# Authentication

> No tricky authorization mechanisms. Authorization of the API key is essential for requesting data.

```shell
# With shell, you can just pass the correct API key with each request
curl https://app.bytemine.io/api/checkForCandlestick/{api_key}/...

```

```javascript
$.ajax({
        url: "https://app.bytemine.io/api/checkForCandlestick/{api_key}/...",
        type: 'GET',
        success: function(data) {
            console.log(data);
        }
    });
```

> Make sure to replace `{api_key}` with your API key.

To use the API you have to have an API key. You can get an API key from our [developer portal](https://app.bytemine.io/developers).

**The API key should be included in all API requests to the server**


<aside class="notice">
You must replace <code>YOUR_API_KEY</code> or <code>{api_key}</code> with your personal API key.
</aside>

# Signals

## Candlestick Patterns

```shell
curl https://app.bytemine.io/api/checkForCandlestick/{api_key}/TSLA/5m
  
```

```javascript
$.ajax({
        url: "https://app.bytemine.io/api/checkForCandlestick/{api_key}/TSLA/5m",
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

`GET https://app.bytemine.io/api/checkForCandlestick/{api_key}/{ticker}/{timeframe}`

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

`GET https://app.bytemine.io/api/checkForCandlestick/5fe69c95ed70a9869d9f9af7d8400a6673bb9ces/AAPL/5m`

## Trends

```shell
curl https://app.bytemine.io/api/getTickerTrend/{api_key}/AMD/30m
```

```javascript
$.ajax({
        url: "https://app.bytemine.io/api/getTickerTrend/{api_key}/AMD/30m",
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
   "trend": "Bearish"
}
```

Trends can be classified into three categories - **Bullish**, **Bearish**, **Neutral**. This can be achieved using Long Polling. However, make sure to not call our Endpoints without adding atleast a **1 Min Delay**.


### HTTP Request

`GET https://app.bytemine.io/api/getTickerTrend/{api_key}/{ticker}/{timeframe}`


### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
api_key | true | API Key is required for authentication.
ticker | true | A ticker/symbol is needed for the appropriate candlestick pattern to be returned.
timeframe | true | Only one Timeframe out of these - 1m/2m/5m/15m/30m/60m/90m/1d/5d/1wk/1mo 


# Stock Fundamentals

## Company Details

```shell
curl https://valhalla.bytemine.workers.dev/companyDetails/{api_key}/{ticker}
  
```

```javascript
$.ajax({
        url: "https://valhalla.bytemine.workers.dev/companyDetails/{api_key}/ITC.NS",
        type: 'GET',
        success: function(data) {
            console.log(data);
        }
    });
```

> The above command returns JSON structured like this:

```json
{
   "address": [
      "Virginia House",
      "37 Jawaharlal Nehru Road"
   ],
   "businessSummary": "ITC Limited engages in the fast moving consumer goods, hotels, paperboards, paper and packaging, agri, and information technology (IT) businesses in India and internationally. The company primarily offers cigarettes and cigars; staples, spices, biscuits, confectionery and gums, snacks, noodles and pasta, beverages, dairy, ready to eat meals, chocolate, coffee, and frozen foods; personal care products; education and stationery products; safety matches; and incense sticks under various brands. It also retails formals and casual wear products, and other lifestyle products under the WLS brand. In addition, the company offers paper boards and specialty paper products; and packaging products, such as carton board, flexible, tobacco, and green packaging products, as well as operates approximately 100 hotels under the ITC Hotel, WelcomHotel, Fortune, and WelcomHeritage brands. Further, it exports feed ingredients, food grains, marine products, processed fruits, coffee products, leaf tobacco products, and spices; and offers IT services and solutions. Additionally, the company offers technology services and solutions for the banking, financial services, consumer packaged goods, manufacturing, travel, hospitality, and healthcare industries. The company also provides property infrastructure and real estate maintenance, business consulting, real estate development, and agro-forestry and other related services; manages and operates golf courses; fabricates and assembles machinery for tube filling, cartoning, wrapping, conveyor solutions, and engineering services; and produces and commercializes seed potato technology products. ITC Limited was incorporated in 1910 and is headquartered in Kolkata, India.",
   "sector": "Consumer Defensive",
   "website": "http://www.itcportal.com",
   "phone": "91 33 2288 9371",
   "country": "India",
   "zip": "700071",
   "city": "Kolkata",
   "industry": "Tobacco",
   "employeesCount": 28115,
   "officers": [
      {
         "name": "Mr. Sanjiv  Puri",
         "age": 57,
         "title": "Chairman & MD"
      },
      {
         "name": "Mr. Rajendra Kumar Singhi",
         "age": 55,
         "title": "Exec. VP, Company Sec. & Compliance Officer"
      },
      {
         "name": "Mr. Rajiv  Tandon",
         "age": 66,
         "title": "Exec. Director"
      },
      {
         "name": "Mr. Sumant  Bhargavan",
         "age": 56,
         "title": "Exec. Director & Pres of FMCG Bus.es"
      },
      {
         "name": "Mr. Nakul  Anand",
         "age": 64,
         "title": "Exec. Director"
      },
      {
         "name": "Mr. Supratim  Dutta",
         "age": 53,
         "title": "CFO & Exec. VP of Corp. Fin."
      },
      {
         "name": "Mr. Saradindu  Dutta",
         "age": 60,
         "title": "Head of Corp. Accounts"
      },
      {
         "name": "Mr. Samrat  Banerjee",
         "title": "VP & Divisional CIO"
      },
      {
         "name": "Mr. Angamuthu Shanmuga Sundaram",
         "age": 53,
         "title": "Gen. Counsel"
      },
      {
         "name": "Mr. Arif  Nazeeb",
         "age": 58,
         "title": "Head of Corp. Communications & Exec. VP"
      }
   ]
}
```

You can get company details of any stock from our API endpoints. This can be achieved using Long Polling. However, make sure to not call our Endpoints without adding atleast a **1 Min Delay**.

### HTTP Request

`GET https://valhalla.bytemine.workers.dev/companyDetails/{api_key}/{ticker}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
api_key | true | API Key is required for authentication.
ticker | true | A ticker/symbol is needed for the appropriate candlestick pattern to be returned.

<aside class="warning">
<br>
1. Remember to add atleast <strong>1 Min Delay</strong> if you're making repeated requests.<br>
2. Timeframes should be in string format. Checkout the example below.
</aside>

### Example HTTP Request

`GET https://valhalla.bytemine.workers.dev/companyDetails/afdhesdf/TSLA`


## Open High Low Close

```shell
curl https://valhalla.bytemine.workers.dev/olhc/{api_key}/{ticker}/{timeframe}/{range}
  
```

```javascript
$.ajax({
        url: "https://valhalla.bytemine.workers.dev/olhc/{api_key}/AMZN/15m/1d",
        type: 'GET',
        success: function(data) {
            console.log(data);
        }
    });
```

> The above command returns JSON structured like this:

```json
{
   "currency": "USD",
   "exchangeTimeZone": "America/New_York",
   "regularMarketPrice": 3277.71,
   "timezone": "EST",
   "symbol": "AMZN",
   "olhc": {
      "timestamp": [
         1613140200,
         1613141100,
         1613142000,
         1613142900,
         1613143800,
         1613144700,
         1613145600,
         1613146500,
         1613147400,
         1613148300,
         1613149200,
         1613150100,
         1613151000,
         1613151900,
         1613152800,
         1613153700,
         1613154600,
         1613155500,
         1613156400,
         1613157300,
         1613158200,
         1613159100,
         1613160000,
         1613160900,
         1613161800,
         1613162700
      ],
      "open": [
         3250,
         3243.64,
         3242.45,
         3247.52,
         3244.49,
         3247.46,
         3252.72,
         3255.87,
         3260.1,
         3254.01,
         3254.34,
         3252.2437,
         3252.38,
         3247.9,
         3255.0508,
         3254.44,
         3250.82,
         3257.12,
         3253.63,
         3255.33,
         3254.785,
         3255.555,
         3257.15,
         3257.31,
         3257.06,
         3269.63
      ],
      "high": [
         3251.41,
         3251.51,
         3252.24,
         3250.52,
         3249.99,
         3258.19,
         3258.7861,
         3261,
         3261,
         3256.94,
         3256.56,
         3253.58,
         3252.38,
         3256.68,
         3257.9878,
         3256.35,
         3256.69,
         3258.2,
         3257.85,
         3260.99,
         3255.47,
         3257.89,
         3261.8567,
         3258.92,
         3270.27,
         3280.25
      ],
      "low": [
         3233.31,
         3239,
         3242.45,
         3241.6501,
         3238,
         3247,
         3251.46,
         3254.07,
         3253.54,
         3252.56,
         3251.5,
         3251.36,
         3245.66,
         3247.9,
         3253.43,
         3247.84,
         3250.71,
         3251.61,
         3252.7297,
         3253.98,
         3251.12,
         3255.44,
         3256.0962,
         3255.14,
         3257.06,
         3269.06
      ],
      "close": [
         3243.96,
         3242.9,
         3247.36,
         3244.63,
         3248.345,
         3253.18,
         3254.57,
         3259.57,
         3253.85,
         3254.92,
         3253.19,
         3252.98,
         3248.15,
         3254.46,
         3254.025,
         3250.98,
         3256.58,
         3253.84,
         3255.26,
         3254.49,
         3255.29,
         3256.585,
         3257.42,
         3256.7515,
         3269.9966,
         3278.38
      ]
   }
}
```

You can get OLHC data of any stock from our API endpoints. This can be achieved using Long Polling. However, make sure to not call our Endpoints without adding atleast a **1 Min Delay**.

### HTTP Request

`GET https://valhalla.bytemine.workers.dev/olhc/{api_key}/{ticker}/{timeframe}/{range}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
api_key | true | API Key is required for authentication.
ticker | true | A ticker/symbol is needed for the appropriate candlestick pattern to be returned.
timeframe | true | Only one Timeframe out of these - 1m/2m/5m/15m/30m/60m/90m/1d/5d/1wk/1mo
range | true | Only one Range out of these - 1d/5d/1mo/3mo/6mo/1y/2y/5y/10y/ytd/max 

<aside class="warning">
<br>
Remember to add atleast <strong>1 Min Delay</strong> if you're making repeated requests.<br>
</aside>

### Example HTTP Request

`GET https://valhalla.bytemine.workers.dev/olhc/afdhesdf/TSLA/5m/5d`


## Similar Stocks

```shell
curl https://valhalla.bytemine.workers.dev/similar/{api_key}/{ticker}
  
```

```javascript
$.ajax({
        url: "https://valhalla.bytemine.workers.dev/similar/{api_key}/AMZN",
        type: 'GET',
        success: function(data) {
            console.log(data);
        }
    });
```

> The above command returns JSON structured like this:

```json
{
   "currentSymbol": "AMZN",
   "similarStocks": [
      "FB",
      "AAPL",
      "GOOG",
      "TSLA",
      "NFLX"
   ]
}
```

You can get similar stocks from our API endpoints. This can be achieved using Long Polling. However, make sure to not call our Endpoints without adding atleast a **1 Min Delay**.

### HTTP Request

`GET https://valhalla.bytemine.workers.dev/similar/{api_key}/{ticker}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
api_key | true | API Key is required for authentication.
ticker | true | A ticker/symbol is needed for the appropriate candlestick pattern to be returned.

<aside class="warning">
<br>
Remember to add atleast <strong>1 Min Delay</strong> if you're making repeated requests.<br>
</aside>

### Example HTTP Request

`GET https://valhalla.bytemine.workers.dev/similar/afdhesdf/TSLA`


## Company Summary

```shell
curl https://valhalla.bytemine.workers.dev/summary/{api_key}/{ticker}
  
```

```javascript
$.ajax({
        url: "https://valhalla.bytemine.workers.dev/summary/{api_key}/LSE.L",
        type: 'GET',
        success: function(data) {
            console.log(data);
        }
    });
```

> The above command returns JSON structured like this:

```json
{
   "symbol": "LSE.L",
   "shortName": "LONDON STOCK EXCHANGE GROUP PLC",
   "longName": "London Stock Exchange Group plc",
   "currency": "GBp",
   "lastClose": 8670,
   "volume": 604046,
   "marketCap": 39983177728,
   "fiftyTwoWeekLow": 75.147,
   "fiftyTwoWeekHigh": 9830,
   "forwardPE": 0.43916854,
   "trailingPE": 76.69039,
   "open": 8652,
   "dayLow": 8498.24,
   "dayHigh": 8666
}
```

You can get company summary of any stock from our API endpoints. This can be achieved using Long Polling. However, make sure to not call our Endpoints without adding atleast a **1 Min Delay**.

### HTTP Request

`GET https://valhalla.bytemine.workers.dev/summary/{api_key}/{ticker}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
api_key | true | API Key is required for authentication.
ticker | true | A ticker/symbol is needed for the appropriate candlestick pattern to be returned.

<aside class="warning">
<br>
Remember to add atleast <strong>1 Min Delay</strong> if you're making repeated requests.<br>
</aside>

### Example HTTP Request

`GET https://valhalla.bytemine.workers.dev/summary/afdhesdf/LSE.L`
