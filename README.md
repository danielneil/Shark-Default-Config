# Shark-Config

This is the demo configuration for the Shark Automated Trading Platform.

### Configuration resides in a git repo on the Shark server
```
# Check out the configuration for customisation.
git clone http://<shark_server>/Shark-Config.git
```
### Config File Structure
```
trading-config.yml - Main configuration file.
backtests/ - Back test code directory
strategies/ - Strategy codde directory.
```
### After applying configuration, commit it and then push back to the server as regular git use.
```
# Verify your changes first.
./bin/verify.sh

git add trading-config.yml backtests strategies
git commit -m 'RSI2 Configuration, backtest and strategy code'
git push
```
### Refresh the Shark server with your new configuration.
```
./bin/refresh.sh
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

### Example - configuration for ticker BTC using several plugins (yahoo_finance_data, sma, backtest)

See the [plugins](https://github.com/danielneil/Shark/blob/main/doc/README.PLUGINS.md) for a list of capabilities.

```yaml
---
- instrument: BTC
  group: B
  plugin:
  - name: yahoo_finance_data
    desc: "Yahoo Finance [ Download of BTC Historical Data File ]"
    group: "Yahoo Finance [ Historical Data ]"
    instrument: BTC
    start_date: 1597479263
    end_date: 1629015263
    interval: 1d
    adjusted_close: true
    frequency: daily
  - name: sma
    desc: "Simple Moving Average - 50 Days"
    group: "SMA: [ 50 Day ]"
    instrument: BTC
    period: 50
  - name: sma
    desc: "Simple Moving Average - 5 Days"
    group: "SMA: [ 5 Day ]"
    instrument: BTC
    period: 5
  - name: backtest
    desc: "BACKTEST: [ Moving Averages ]"
    group: "Backtesting"
    instrument: AMC
    file: backtest_moving_averages.py
    shares: 1000
    capital: 100000
```
