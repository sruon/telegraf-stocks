# Telegraf Stocks
Retrieve stock informations from Yahoo Finance in a format ready to consume for Telegraf - InfluxDB.

# Installing
```
pip install -r requirements.txt
./telegraf_stocks -h
```

# Usage
```
usage: telegraf_stocks [-h] --ticker TICKER [--measurement MEASUREMENT]

Retrieves stock information from Yahoo Finance and formats them in InfluxDB
line format.

optional arguments:
  -h, --help            show this help message and exit
  --ticker TICKER       Ticker symbol to check on Yahoo Finance.
  --measurement MEASUREMENT
                        Measurement name for InfluxDB.
```

# Retrieve AAPL stock informations
```
$> ./telegraf_stocks --ticker AAPL

stocks,stock_exchange=NMS,days_range=115.75\ -\ 117.38,last_trade_with_time=4:00pm\ -\ <b>116.64</b>,change__percent_change=+0.67\ -\ +0.58,symbol=AAPL,year_range=89.47\ -\ 118.69,currency=USD,last_trade_date=12/19/2016,last_trade_time=4:00pm,dividend_pay_date=11/10/2016,ex_dividend_date=11/3/2016,percebt_change_from_year_high=-1.73%,name=Apple\ Inc. previous_close=115.970000,percent_change_from_two_hundredday_moving_average=8.700000,price_book=4.830000,price_eps_estimate_current_year=12.950000,change_from_two_hundredday_moving_average=9.330000,average_daily_volume=33706600.000000,year_high=118.690000,dividend_yield=1.970000,open=115.800000,ebitda=70530000000.000000,year_low=89.470000,oneyr_target_price=131.840000,change_from_year_low=27.170000,pe_ratio=14.040000,change_from_year_high=-2.050000,market_capitalization=621960000000.000000,last_trade_price_only=116.640000,price_eps_estimate_next_year=11.620000,percent_change_from_fiftyday_moving_average=4.830000,book_value=24.030000,eps_estimate_next_quarter=2.140000,eps_estimate_current_year=9.010000,percent_change=0.580000,peg_ratio=1.480000,bid=116.640000,dividend_share=2.280000,volume=27779423.000000,ask=116.680000,price_sales=2.870000,change=0.670000,eps_estimate_next_year=10.040000,percent_change_from_year_low=30.370000,fiftyday_moving_average=111.270000,short_ratio=1.730000,two_hundredday_moving_average=107.310000,days_low=115.750000,changein_percent=0.580000,change_from_fiftyday_moving_average=5.370000,days_high=117.380000,earnings_share=8.310000
```

# Integrate with Telegraf
```
[[inputs.exec]]
  commands = ["./telegraf_stocks --ticker AAPL", "./telegraf_stocks --ticker AMZN"]

  ## Timeout for command to complete.
  timeout = "10s"

  # Data format to consume.
  # NOTE json only reads numerical measurements, strings and booleans are ignored.
  data_format = "influx"
```

# Yahoo API throttling
2,000 requests/hr per IP when *unauthenticated*
