# Shark-Default-Config

### Configuration file for trading setup 

```
trading-config.yml
```

### The structure of the file is important (being yaml).

```yaml
# <INSTRUMENT_NAME>:
#  INSTRUMENT_GROUP: "<name>"
#  <INDICATOR_GROUP>: "<name>"
#   DESCRIPTION: "<string that appears on the UI>"
#   PLUGIN: <plugin_name>
#   <plugin_arg>: <arg>
#   <plugin_arg>: <arg>
#   <plugin_arg>: <arg>
```

### Example - strategy configuration for ticker AMC using several plugins (check_rsi, check_sma, check_strategy, check_backtest)

See the [plugins](https://github.com/danielneil/Shark/blob/main/doc/README.PLUGINS.md) for a list of capabilities.

```yaml
instrument: AMC
 instrument_group: Materials
     
  plugin:
   name: check_rsi
   desc: "RSI [ 14 Day ]"
   ticker: AMC
   period: 14
   min: 10
   max: 90
     
  plugin:
   name: check_sma
   desc: "Simple Moving Average - 50 Days:
   group: "SMA: [ 50 Day ]" 
   ticker: AMC
   period: 50

  plugin:
   name: check_sma
   desc: Simple Moving Average - 5 Days:
  DESCRIPTION: "SMA: [ 5 Day ]"
  ticker: AMC
  period: 5

plugin:
 Opportunity Detection: 
  DESCRIPTION: "STRATEGY: [ Moving Averages ]"
  PLUGIN: check_strategy
  ticker: AMC
  name: moving_averages.py
   
   plugin:
 Backtesting:
  DESCRIPTION: "BACKTEST: [ Moving Averages ]"
  PLUGIN: check_backtest
  ticker: AMC
  name: backtest_moving_averages.py
  shares: 1000
  capital: 100000
```
