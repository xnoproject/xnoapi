

Introduction
============

XNO API is a Python package for retrieving financial data from multiple sources with a simple and intuitive interface.

Author: XNO API Team

License: MIT License

----

Installation
------------

You can install the XNO API package using pip:

.. code:: none

   pip install xnoapi

Alternatively, you can clone this repository and install the package manually:

.. code:: none

   $ git clone https://github.com/xnoproject/xnoapi.git
   $ pip install ./xnoapi

----

Contents
--------

.. toctree::
   :caption: Guide
   :maxdepth: 2

   installation
   usage
   available_modules
   examples

.. toctree::
   :caption: API
   :maxdepth: 2

   api/xnoapi
   .. api/derivatives
   .. api/metrics
   .. api/backtest_derivatives

----

Usage
-----

XNO API provides a structured interface for retrieving financial data:

.. code:: python

   from xnoapi import client
   from xnoapi.vn.data import stocks, derivatives

   client(apikey="your_api_key")

   # Retrieve list of liquid assets
   stocks.list_liquid_asset()

   # Get historical stock data
   stocks.get_hist("VIC", "1D")

   # Get historical derivatives
   derivatives.get_hist("VN30F1M", "1m")

----

Available Modules
-----------------

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

----

API Documentation
-----------------

.. toctree::
   :caption: Stocks API
   :maxdepth: 2

   api/stocks.list_liquid_asset
   api/stocks.get_hist

.. toctree::
   :caption: Derivatives API
   :maxdepth: 2

   api/derivatives.get_hist

.. toctree::
   :caption: Metrics API
   :maxdepth: 2

   api/metrics.Metrics
   api/metrics.Backtest_Derivates

----

Examples
--------

### **Retrieving Stock Data**

.. code:: python

   from xnoapi import client
   from xnoapi.vn.data import stocks

   client(apikey="your_api_key")

   # Get list of liquid assets
   liquid_assets = stocks.list_liquid_asset()

   # Get historical data for VIC stock
   vic_history = stocks.get_hist("VIC", "1D")

### **Using Metrics**

.. code:: python

   from xnoapi.vn.metrics import Metrics, Backtest_Derivates
   from xnoapi.vn.data import derivatives

   # Initialize metrics instance
   historical = derivatives.get_hist("VN30F1M", "1m")
   backtest = Backtest_Derivates(historical, "raw")
   metrics = Metrics(backtest)

   # Example usage
   result = metrics.avg_loss()

----

Credits
-------

This library is developed and maintained by the XNO API team. Special thanks to contributors and financial data providers for their support.

----

License
-------

This library is licensed under the MIT License. See the LICENSE file for more details.



