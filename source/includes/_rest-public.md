# REST Public Endpoints

## Symbols

> Example request

```curl
curl -X GET "https://durex/v1/symbols"
```

> Example Response

```json
[
  [
    Name,  // SYMBOL,
    Stock,
    Money,
    StockPrec,  // PRICE_PRECISION,
    MoneyPrec,
    FeePrec,
    MinAmount  // MINIMUM_ORDER_SIZE,
    // MAXIMUM_ORDER_SIZE
  ],
  ["tBTCUSD","BTC","USD",8,8,8,"0.01"],
  ...
]
```

Get a list of valid symbol IDs and the pair details.

### HTTP REQUEST

`GET /v1/symbols`

## Platform Status

> Example request

```curl
curl -X GET "https://durex/v1/platform/status"
```

> Example Response

```json
[
  Operative // OPERATIVE
]

[1]
```

Get the current status of the platform.

Maintenance periods last for just few minutes and might be necessary from time to time during upgrades of core components of our infrastructure.
Even if rare it is important to have a way to notify users.

For a real-time notification we suggest to use websockets and listen to events 20060/20061

### HTTP REQUEST

`GET /v1/platform/status`

## Tickers

> Example request

```curl
curl https://durex/v1/tickers
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

`GET /v1/tickers`

## Ticker

> Example request

```curl
curl https://durex/v1/ticker/tBTCUSD
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

`GET /v1/ticker/<Symbol>`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | The symbol you want information about. You can find the list of valid symbols by calling the /symbols endpoint.

## Trades

> Example request

```curl
curl -X POST "https://durex/v1/trades/tBTCUSD/hist?start=1534228780&end=1534238780&limit=2&offset=1"
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

`GET /v1/trades/<Symbol>/hist`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | The symbol you want information about.
 start | int64 | Optional | Start timestamp
 end | int64 | Optional | End timestamp
 limit | uint64 | Optional | Number of records (0: all)
 offset | uint64 | Optional | Offset position

## Books

> Example request

```curl
curl -X GET "https://durex/v1/book/tBTCUSD/0?limit=3"
```

> Example Response

```json
// on trading pairs (ex. tBTCUSD)
[
  [  // asks
    [
      Price,  // PRICE,
      // COUNT,
      Amount  // AMOUNT
    ],
    ["25.00000000","3.00000000"],
    ["50.00000000","2.00000000"],
    ["100.00000000","1.00000000"],
    ...
  ],
  [  // bids
    ["15.00000000","3.00000000"],
    ["10.00000000","1.00000000"],
    ...
  ]
]
```

The Order Books channel allow you to keep track of the state of the Bitfinex order book.
It is provided on a price aggregated basis, with customizable precision.

### HTTP REQUEST

`GET /v1/book/<Symbol>/<Precision>`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | The symbol you want information about. You can find the list of valid symbols by calling the /symbols endpoint.
 Precision | string | Required | Level of price aggregation (0, 0.1, 0.01, 0.001, 0.0001, 0.00001, ...)
 limit | uint64 | Optional | Number of price points (0: all)

## Candles

> Example request

```curl
curl https://durex/v1/candles/trade:1m:tBTCUSD/last

curl https://durex/v1/candles/trade:1m:tBTCUSD/hist
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

`GET /v1/candles/trade:<TimeFrame>:<Symbol>/<Section>`

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
curl -X GET "https://durex/v1/time"
```

> Example Response

```json
[
  CurrentTime
]

[1435082571]
```

Get the API server time

### HTTP REQUEST

`GET /v1/time`
