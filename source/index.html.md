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


# Stock Market Data

## Country Abbreviations

In some cases you might need country abbreviations to query the data. For example - if you want to find the list of stocks that a country has then you'd have to use country abbreviations.
You can check the list of supported countries and their abbreviations from over here - <a href="https://airtable.com/shrffQ8hRyl0LKAQH/tbl9lvQLZq9nryClu" target="_blank">https://airtable.com/shrffQ8hRyl0LKAQH/tbl9lvQLZq9nryClu</a>.

## Get List of Symbols from a Country

```shell
curl https://server1.bytemine.workers.dev/stocks/{api_key}/{country_abbreviation}/{offset}
  
```

```javascript
$.ajax({
        url: "https://server1.bytemine.workers.dev/stocks/{api_key}/cz/0",
        type: 'GET',
        success: function(data) {
            console.log(data);
        }
    });
```

> The above command returns JSON structured like this:

```json
{
  "start": 0,
  "totalCount": 36,
  "tickersReturned": 36,
  "data": {
    "0": {
      "tickerSymbol": "RDSA.PR",
      "open": 437.85,
      "low": 434.6,
      "high": 437.85,
      "ltp": 434.6,
      "volume": 251,
      "dayChange": 6.600006,
      "dayChangePercent": 1.5420575,
      "fiftyTwoWeekLow": 275,
      "fiftyTwoWeekHigh": 509,
      "marketCap": 3278153187328
    },
    "1": {
      "tickerSymbol": "VOLVB.PR",
      "open": 535,
      "low": 535,
      "high": 535,
      "ltp": 535,
      "volume": 50,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 290,
      "fiftyTwoWeekHigh": 608,
      "marketCap": 1089062043648
    },
    "2": {
      "tickerSymbol": "EOAN.PR",
      "open": 255.5,
      "low": 255.5,
      "high": 255.5,
      "ltp": 255.5,
      "volume": 223,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 220,
      "fiftyTwoWeekHigh": 275.05,
      "marketCap": 671160205312
    },
    "3": {
      "tickerSymbol": "VER.PR",
      "open": 1600,
      "low": 1600,
      "high": 1600,
      "ltp": 1600,
      "volume": 15,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 923,
      "fiftyTwoWeekHigh": 1832.5,
      "marketCap": 556734414848
    },
    "4": {
      "tickerSymbol": "NOKIA.PR",
      "open": 94.99,
      "low": 92,
      "high": 94.99,
      "ltp": 92,
      "volume": 520,
      "dayChange": 1,
      "dayChangePercent": 1.0989012,
      "fiftyTwoWeekLow": 76.82,
      "fiftyTwoWeekHigh": 126.88,
      "marketCap": 511416041472
    },
    "5": {
      "tickerSymbol": "ERBAG.PR",
      "open": 766.8,
      "low": 756,
      "high": 766.8,
      "ltp": 756,
      "volume": 44238,
      "dayChange": 2,
      "dayChangePercent": 0.265252,
      "fiftyTwoWeekLow": 440,
      "fiftyTwoWeekHigh": 773.6,
      "marketCap": 306056757248
    },
    "6": {
      "tickerSymbol": "CEZ.PR",
      "open": 567,
      "low": 566,
      "high": 573,
      "ltp": 571.5,
      "volume": 163983,
      "dayChange": 6.5,
      "dayChangePercent": 1.1504425,
      "fiftyTwoWeekLow": 433.5,
      "fiftyTwoWeekHigh": 573,
      "marketCap": 306023366656
    },
    "7": {
      "tickerSymbol": "OTP.PR",
      "open": 978,
      "low": 978,
      "high": 978,
      "ltp": 978,
      "volume": 1,
      "dayChange": -25,
      "dayChangePercent": -2.4925225,
      "fiftyTwoWeekLow": 651,
      "fiftyTwoWeekHigh": 1003,
      "marketCap": 264351432704
    },
    "8": {
      "tickerSymbol": "PKO.PR",
      "open": 186.5,
      "low": 186.5,
      "high": 186.5,
      "ltp": 186.5,
      "volume": 1,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 110,
      "fiftyTwoWeekHigh": 186.5,
      "marketCap": 226819424256
    },
    "9": {
      "tickerSymbol": "PKN.PR",
      "open": 368,
      "low": 368,
      "high": 368,
      "ltp": 368,
      "volume": 10,
      "dayChange": 2,
      "dayChangePercent": 0.54644805,
      "fiftyTwoWeekLow": 225.9,
      "fiftyTwoWeekHigh": 434.6,
      "marketCap": 155653701632
    },
    "10": {
      "tickerSymbol": "RBI.PR",
      "open": 474.4,
      "low": 474.4,
      "high": 474.4,
      "ltp": 474.4,
      "volume": 230,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 332,
      "fiftyTwoWeekHigh": 494.6,
      "marketCap": 157174415360
    },
    "11": {
      "tickerSymbol": "AVST.PR",
      "open": 143.15,
      "low": 140.9,
      "high": 143.15,
      "ltp": 143,
      "volume": 198961,
      "dayChange": 0.3500061,
      "dayChangePercent": 0.24536005,
      "fiftyTwoWeekLow": 119.6,
      "fiftyTwoWeekHigh": 177,
      "marketCap": 145669816320
    },
    "12": {
      "tickerSymbol": "KOMB.PR",
      "open": 684,
      "low": 678,
      "high": 686,
      "ltp": 678,
      "volume": 94533,
      "dayChange": -2,
      "dayChangePercent": -0.29411766,
      "fiftyTwoWeekLow": 460,
      "fiftyTwoWeekHigh": 725,
      "marketCap": 128044367872
    },
    "13": {
      "tickerSymbol": "MOL.PR",
      "open": 156.2,
      "low": 156.2,
      "high": 156.2,
      "ltp": 156.2,
      "volume": 200,
      "dayChange": -1.5,
      "dayChangePercent": -0.9511732,
      "fiftyTwoWeekLow": 115,
      "fiftyTwoWeekHigh": 176,
      "marketCap": 117469896704
    },
    "14": {
      "tickerSymbol": "TELEC.PR",
      "open": 261,
      "low": 260,
      "high": 264,
      "ltp": 260,
      "volume": 40454,
      "dayChange": -1,
      "dayChangePercent": -0.38314176,
      "fiftyTwoWeekLow": 209,
      "fiftyTwoWeekHigh": 264,
      "marketCap": 78229315584
    },
    "15": {
      "tickerSymbol": "VIG.PR",
      "open": 590.5,
      "low": 586,
      "high": 595,
      "ltp": 595,
      "volume": 3429,
      "dayChange": 11,
      "dayChangePercent": 1.8835617,
      "fiftyTwoWeekLow": 469,
      "fiftyTwoWeekHigh": 619,
      "marketCap": 76236161024
    },
    "16": {
      "tickerSymbol": "TABAK.PR",
      "open": 14600,
      "low": 14500,
      "high": 14620,
      "ltp": 14600,
      "volume": 1286,
      "dayChange": 100,
      "dayChangePercent": 0.6896552,
      "fiftyTwoWeekLow": 13000,
      "fiftyTwoWeekHigh": 15780,
      "marketCap": 40082694144
    },
    "17": {
      "tickerSymbol": "MONET.PR",
      "open": 78,
      "low": 77.55,
      "high": 78.15,
      "ltp": 77.65,
      "volume": 1665687,
      "dayChange": -0.5499954,
      "dayChangePercent": -0.70331895,
      "fiftyTwoWeekLow": 48.25,
      "fiftyTwoWeekHigh": 84.3,
      "marketCap": 39679152128
    },
    "18": {
      "tickerSymbol": "JUVE.PR",
      "open": 20.92,
      "low": 20.67,
      "high": 20.92,
      "ltp": 20.67,
      "volume": 174,
      "dayChange": -0.8600006,
      "dayChangePercent": -3.994429,
      "fiftyTwoWeekLow": 19.82,
      "fiftyTwoWeekHigh": 29,
      "marketCap": 26427215872
    },
    "19": {
      "tickerSymbol": "STOCK.PR",
      "open": 85.5,
      "low": 85,
      "high": 86,
      "ltp": 85,
      "volume": 3715,
      "dayChange": -0.19999695,
      "dayChangePercent": -0.2347382,
      "fiftyTwoWeekLow": 50.4,
      "fiftyTwoWeekHigh": 87.5,
      "marketCap": 17314670592
    },
    "20": {
      "tickerSymbol": "BVB.PR",
      "open": 136,
      "low": 135,
      "high": 136,
      "ltp": 135,
      "volume": 223,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 119.4,
      "fiftyTwoWeekHigh": 172.9,
      "marketCap": 12491508736
    },
    "21": {
      "tickerSymbol": "FACC.PR",
      "open": 247,
      "low": 247,
      "high": 247,
      "ltp": 247,
      "volume": 100,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 126.1,
      "fiftyTwoWeekHigh": 276.4,
      "marketCap": 11015656448
    },
    "22": {
      "tickerSymbol": "CZG.PR",
      "open": 374,
      "low": 370,
      "high": 374,
      "ltp": 373,
      "volume": 895,
      "dayChange": 2,
      "dayChangePercent": 0.53908354,
      "fiftyTwoWeekLow": 280,
      "fiftyTwoWeekHigh": 410,
      "marketCap": 11129574400
    },
    "23": {
      "tickerSymbol": "KOFOL.PR",
      "open": 273,
      "low": 272,
      "high": 274,
      "ltp": 273,
      "volume": 8947,
      "dayChange": 1,
      "dayChangePercent": 0.36764705,
      "fiftyTwoWeekLow": 212,
      "fiftyTwoWeekHigh": 26900,
      "marketCap": 6085688832
    },
    "24": {
      "tickerSymbol": "PEN.PR",
      "open": 80,
      "low": 79,
      "high": 80,
      "ltp": 79,
      "volume": 370,
      "dayChange": -1,
      "dayChangePercent": -1.25,
      "fiftyTwoWeekLow": 30,
      "fiftyTwoWeekHigh": 115,
      "marketCap": 3911606016
    },
    "25": {
      "tickerSymbol": "PINK.PR",
      "open": 1100,
      "low": 1100,
      "high": 1100,
      "ltp": 1100,
      "volume": 3460,
      "dayChange": -100,
      "dayChangePercent": -8.333334,
      "fiftyTwoWeekLow": 500,
      "fiftyTwoWeekHigh": 1500,
      "marketCap": 2750000128
    },
    "26": {
      "tickerSymbol": "SABFG.PR",
      "open": 10600,
      "low": 10600,
      "high": 10600,
      "ltp": 10600,
      "volume": 310,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 10500,
      "fiftyTwoWeekHigh": 10600,
      "marketCap": 2731959296
    },
    "27": {
      "tickerSymbol": "TOMA.PR",
      "open": 1290,
      "low": 1290,
      "high": 1290,
      "ltp": 1290,
      "volume": 650,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 1200,
      "fiftyTwoWeekHigh": 1380,
      "marketCap": 1718628352
    },
    "28": {
      "tickerSymbol": "PRIUA.PR",
      "open": 352,
      "low": 352,
      "high": 352,
      "ltp": 352,
      "volume": 600,
      "dayChange": -4,
      "dayChangePercent": -1.1235955,
      "fiftyTwoWeekLow": 240,
      "fiftyTwoWeekHigh": 358,
      "marketCap": 1537930240
    },
    "29": {
      "tickerSymbol": "PVT.PR",
      "open": 1.99,
      "low": 1.25,
      "high": 1.99,
      "ltp": 1.25,
      "volume": 5511,
      "dayChange": -0.09000003,
      "dayChangePercent": -6.7164207,
      "fiftyTwoWeekLow": 0.5,
      "fiftyTwoWeekHigh": 1.99,
      "marketCap": 1331337472
    },
    "30": {
      "tickerSymbol": "PRAB.PR",
      "open": 392,
      "low": 392,
      "high": 392,
      "ltp": 392,
      "volume": 500,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 354,
      "fiftyTwoWeekHigh": 402,
      "marketCap": 392000000
    },
    "31": {
      "tickerSymbol": "EFORU.PR",
      "open": 103,
      "low": 103,
      "high": 103,
      "ltp": 103,
      "volume": 4,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 92,
      "fiftyTwoWeekHigh": 103,
      "marketCap": 246338912
    },
    "35": {
      "tickerSymbol": "DBK.PR",
      "open": 273.1,
      "low": 273.1,
      "high": 273.1,
      "ltp": 273.1,
      "volume": 5,
      "dayChange": 0,
      "dayChangePercent": 0,
      "fiftyTwoWeekLow": 153.4,
      "fiftyTwoWeekHigh": 293.6,
      "marketCap": 552189100032
    }
  }
}
```

The API endpoint requires 3 parameters -> API key, country abbreviation and finally an offset.
You can get the country abbreviation from the above step.
For offset the default value that you should enter is 0. Since the data is picked up from our SQL database hence we require an offset param to determine which next set of data should we output.
You can read about offset from <a href='https://www.w3schools.com/php/php_mysql_select_limit.asp' target="_blank">here</a>. 
If you still have questions about this then please contact us at contact@bytemine.io.


## Company Details

```shell
curl https://valhalla.bytemine.workers.dev/companyDetails/{api_key}/ITC.NS
  
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


## Open High Low Close Volume

```shell
curl https://valhalla.bytemine.workers.dev/olhc/{api_key}/AMZN/15m/1d
  
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
curl https://valhalla.bytemine.workers.dev/summary/{api_key}/LSE.L
  
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
