# REST Public Endpoints

## Symbols

> Example request

```curl
curl https://durex/v1/symbols
```

> Example Response

```json
[
  [
    SYMBOL,
    PRICE_PRECISION,
    MINIMUM_ORDER_SIZE,
    MAXIMUM_ORDER_SIZE
  ],
  ...
]
```

Get a list of valid symbol IDs and the pair details.

### HTTP REQUEST

`GET /v1/symbols`

## Platform Status

> Example request

```curl
curl https://durex/v2/platform/status
```

> Example Response

```json
[OPERATIVE]
```

Get the current status of the platform.

Maintenance periods last for just few minutes and might be necessary from time to time during upgrades of core components of our infrastructure.
Even if rare it is important to have a way to notify users.

For a real-time notification we suggest to use websockets and listen to events 20060/20061

### HTTP REQUEST

`GET /v2/platform/status`

## Tickers

> Example request

```curl
curl https://durex/v2/tickers?symbols=tBTCUSD,tLTCUSD
```

> Example Response

```json
[
  // on trading pairs (ex. tBTCUSD)
  [
    SYMBOL,
    BID,
    BID_SIZE,
    ASK,
    ASK_SIZE,
    DAILY_CHANGE,
    DAILY_CHANGE_PERC,
    LAST_PRICE,
    VOLUME,
    HIGH,
    LOW
  ]
  ...
]
```

The ticker is a high level overview of the state of the market. It shows you the current best bid and ask, as well as the last trade price. It also includes information such as daily volume and how much the price has moved over the last day.

### HTTP REQUEST

`GET /v2/tickers`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 symbols | string | Required | The symbols you want information about. ex: tBTCUSD

## Ticker

> Example request

```curl
curl https://durex/v2/ticker/tBTCUSD
```

> Example Response

```json
// on trading pairs (ex. tBTCUSD)
[
  BID,
  BID_SIZE,
  ASK,
  ASK_SIZE,
  DAILY_CHANGE,
  DAILY_CHANGE_PERC,
  LAST_PRICE,
  VOLUME,
  HIGH,
  LOW
]
```

The ticker is a high level overview of the state of the market. It shows you the current best bid and ask, as well as the last trade price. It also includes information such as daily volume and how much the price has moved over the last day.

### HTTP REQUEST

`GET /v2/ticker/<Symbol>`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | The symbol you want information about. You can find the list of valid symbols by calling the /symbols endpoint.

## Trades

> Example request

```curl
curl https://durex/v2/trades/tBTCUSD/hist
```

> Example Response

```json
// on trading pairs (ex. tBTCUSD)
[
  [
    ID,
    MTS,
    AMOUNT,
    PRICE
  ]
]
```

Trades endpoint includes all the pertinent details of the trade, such as price, size and time.

### HTTP REQUEST

`GET /v2/trades/<Symbol>/hist`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | The symbol you want information about.
 limit | int32 | Optional | Number of records
 start | string | Optional | Millisecond start time
 end | string | Optional | Millisecond end time

## Books

> Example request

```curl
curl https://durex/v2/book/tBTCUSD/P0
```

> Example Response

```json
// on trading pairs (ex. tBTCUSD)
[
  [
    PRICE,
    COUNT,
    AMOUNT
  ]
]
```

The Order Books channel allow you to keep track of the state of the Bitfinex order book.
It is provided on a price aggregated basis, with customizable precision.

### HTTP REQUEST

`GET /v2/book/<Symbol>/<Precision>`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | The symbol you want information about. You can find the list of valid symbols by calling the /symbols endpoint.
 Precision | string | Required | Level of price aggregation (P0, P1, P2, P3, R0)
 len | int32 | Optional |Number of price points ("25", "100")

## Candles

> Example request

```curl
curl https://durex/v2/candles/trade:1m:tBTCUSD/last

curl https://durex/v2/candles/trade:1m:tBTCUSD/hist
```

> Example Response

```json
// response with Section = "last"
[
  MTS,
  OPEN,
  CLOSE,
  HIGH,
  LOW,
  VOLUME
]

// response with Section = "hist"
[
  [ MTS, OPEN, CLOSE, HIGH, LOW, VOLUME ],
  ...
]
```

Provides a way to access charting candle info

### HTTP REQEUST

`GET /v2/candles/trade:<TimeFrame>:<Symbol>/<Section>`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 TimeFrame | string | Required | Available values: '1m', '5m', '15m', '30m', '1h', '3h', '6h', '12h', '1D', '7D', '14D', '1M'
 Symbol | string | Required | The symbol you want information about.
 Section | string | Required | Available values: "last", "hist"
 limit | int32 | Optional | Number of candles requested
 start | string | Optional | Filter start (ms)
 end | string | Optional | Filter end (ms)

## Time

> Example request

```curl
curl https://durex/v2/time
```

> Example Response

```json
[
  1435082571
]
```

Get the API server time

### HTTP REQUEST

`GET /v2/time`
