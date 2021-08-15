# Shark-Config

### Configuration file for trading setup 

```
trading-config.yml
```

### The structure of the file is important (being yaml).

```yaml
---
instrument: <instrument>

 instrument_group: <ui grouping of plugin>
     
  plugin:
   name: <name_of_plugin>
   desc: <description to appear on UI>
   group: <ui grouping of plugin>
   <arg> : <arg>
   <arg> : <arg>
   <arg> : <arg>
```

### Example - strategy configuration for ticker AMC using several plugins (check_rsi, check_sma, check_strategy, check_backtest)

See the [plugins](https://github.com/danielneil/Shark/blob/main/doc/README.PLUGINS.md) for a list of capabilities.

```yaml
---

instrument: AMC

 instrument_group: Materials

  plugin:
   name: yahoo_finance_data
   desc: "Yahoo Finance - Download of AMC Historical Data File"
   group: "Yahoo Finance - Historical Data"  
   instrument: AMC.AX
   start_date: 1597479263
   end_date: 1629015263
   interval: 1d
   adjusted_close: true 
   frequency: daily
   
  plugin:
   name: rsi
   desc: RSI Check - 14 Days
   group: "RSI [ 14 Day ]"
   instrument: AMC
   period: 14
   min: 10
   max: 90
     
  plugin:
   name: sma
   desc: "Simple Moving Average - 50 Days:"
   group: "SMA: [ 50 Day ]" 
   instrument: AMC
   period: 50

  plugin:
   name: sma
   desc: "Simple Moving Average - 5 Days:"
   group: "SMA: [ 5 Day ]"
   instrument: AMC
   period: 5

  plugin:
   name: strategy
   desc: "STRATEGY - Moving Averages"
   group: "STRATEGY: [ Moving Averages ]"  
   instrument: AMC
   file: moving_averages.py
   
  plugin:
   name: backtest
   desc: "BACKTEST: [ Moving Averages ]"
   group: "Backtesting" 
   instrument: AMC
   file: backtest_moving_averages.py
   shares: 1000
   capital: 100000
```
