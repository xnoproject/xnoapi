# XNO API Library

XNO API is a Python package for retrieving financial data from multiple sources with a simple and intuitive interface.

### Contents
- [Installation](#installation)
- [Documentation](#documentation)
- [Usage](#usage)
- [Available Modules](#available-modules)
- [Examples](#examples)
- [Credits](#credits)
- [License](#license)

## Installation
You can install the XNO API package using pip:

```sh
pip install xnoapi
```

Alternatively, you can clone this repository and install the package manually:

```sh
$ git clone git@github.com:yourusername/xnoapi.git
$ pip install ./xnoapi
```

After installation, you can import and start using XNO API:

```python
from xnoapi import client
from xnoapi.vn.data import stocks, derivatives
from xnoapi.vn.metrics import Metrics, Backtest_Derivates

client(apikey="your_api_key")
```

## Documentation
Full documentation is available online:

[![Documentation Status](https://readthedocs.org/projects/xnoapi/badge/?version=latest)](https://xnoapi.readthedocs.io/en/latest/?badge=latest)

A PDF version of the documentation is available [here](https://buildmedia.readthedocs.org/media/pdf/xnoapi/latest/xnoapi.pdf).

## Usage
XNO API provides a structured interface for retrieving financial data:

```python
from xnoapi import client
from xnoapi.vn.data import stocks, derivatives

client(apikey="your_api_key")

# Retrieve list of liquid assets
stocks.list_liquid_asset()

# Get historical stock data
stocks.get_hist("VIC", "1D")
```

## Available Modules
XNO API includes the following modules:

### **Financial Data**
- `xnoapi.vn.data.stocks`
    - `list_liquid_asset()`: Retrieve a list of liquid stocks.
    - `get_hist(asset_name, frequency)`: Get historical data for a given asset.
- `xnoapi.vn.data.derivatives`
    - `get_hist()`: Get historical derivative data.

### **Metrics and Analytics**
- `xnoapi.vn.metrics`
    - `Metrics`: Various financial metrics calculation.
    - `Backtest_Derivates`: Backtesting tools for derivatives.

## Examples
### **Retrieving Stock Data**
```python
from xnoapi import client
from xnoapi.vn.data import stocks

client(apikey="your_api_key")

# Get list of liquid assets
liquid_assets = stocks.list_liquid_asset()

# Get historical data for VIC stock
vic_history = stocks.get_hist("VIC", "1D")
```

### **Using Metrics**
```python
from xnoapi.vn.metrics import Metrics

# Initialize metrics instance
metrics = Metrics()

# Example usage
result = metrics.some_metric_function("VIC")
```

## Credits
This library is developed and maintained by the XNO API team. Special thanks to contributors and financial data providers for their support.

## License
This library is licensed under the [MIT License](https://choosealicense.com/licenses/mit/). See [LICENSE](https://github.com/yourusername/xnoapi/blob/master/LICENSE) for more details.

