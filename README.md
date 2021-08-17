# Shark-Config

### Configuration Files

```
# Strategy code lives here.
strategies/

# Backtest code lives here.
backtests/

# Trading configuration.
trading-config.yml
```

### Configuration is checked out from the Shark server

```
 git clone http://<shark_server>/Shark-Config
```

### After amendments, configuration is pushed back to the Shark server

push.sh validates the config, and then pushes it to the Shark server.

```
 cd Shark-Config && ./push.sh
```

### Main configuration file - trading-config.yml

The structure of the file is important (being yaml).


```yaml
---
- instrument: <instrument>
  group: <grouping of like instruments>
  plugin:
  - name: <name_of_plugin>
    desc: <description to appear on UI>
    group: <ui grouping of plugin>
    instrument: <instrument>
    <arg> : <arg
    <arg> : <arg>
    <arg> : <arg>
    <arg> : <arg
    ...
```

### Example - configuration for ticker AMC using several plugins (rsi, sma, strategy, backtest)

See the [plugins](https://github.com/danielneil/Shark/blob/main/doc/README.PLUGINS.md) for a list of capabilities.

```yaml
---
- instrument: AMC
  group: Materials
  plugin:
  - name: yahoo_finance_data
    desc: "Yahoo Finance - Download of AMC Historical Data File"
    group: "Yahoo Finance - Historical Data"
    instrument: AMC.AX
    start_date: 1597479263
    end_date: 1629015263
    interval: 1d
    adjusted_close: true
    frequency: daily
  - name: rsi
    desc: RSI Check - 14 Days
    group: "RSI [ 14 Day ]"
    instrument: AMC
    period: 14
    min: 10
    max: 90
  - name: sma
    desc: "Simple Moving Average - 50 Days"
    group: "SMA: [ 50 Day ]"
    instrument: AMC
    period: 50
  - name: sma
    desc: "Simple Moving Average - 5 Days"
    group: "SMA: [ 5 Day ]"
    instrument: AMC
    period: 5
  - name: strategy
    desc: "STRATEGY - Moving Averages"
    group: "STRATEGY: [ Moving Averages ]"
    instrument: AMC
    file: moving_averages.py
  - name: backtest
    desc: "BACKTEST: [ Moving Averages ]"
    group: "Backtesting"
    instrument: AMC
    file: backtest_moving_averages.py
    shares: 1000
    capital: 100000
```
