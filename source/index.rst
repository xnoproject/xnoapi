.. xnoapi documentation master file, created by
   sphinx-quickstart on Mon Mar 31 16:42:27 2025.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

xnoapi documentation
====================

XNO API is a Python package for retrieving financial data from multiple sources with a simple and intuitive interface. To sign up for API Key access, register free account at xbot.xno.vn

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

After installation, you can import and start using XNO API:

.. code:: python

   from xnoapi import client
   from xnoapi.vn.data import stocks, derivatives
   from xnoapi.vn.metrics import Metrics, Backtest_Derivates

   client(apikey="your_api_key")

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

   api/stocks
   api/derivatives
   api/metrics
   api/backtest_derivatives

----

Usage
-----

XNO API provides a structured interface for retrieving financial data and modules for efficient PNL calculation and performance tracking in the Vietnamese Financial Market:

.. code:: python

   from xnoapi import client
   from xnoapi.vn.data import stocks, derivatives

   client(apikey="your_api_key")

   # List of liquid stocks
   stocks.list_liquid_asset()

   # Historical data for VIC (Vingroup)
   vic = stocks.get_hist("VIC")

   # Historical data for VN30F1M derivative
   vn30f1m = derivatives.get_hist("VN30F1M", "1m")

----

Available Modules
-----------------

**Financial Data**

- `xnoapi.vn.data.stocks`
  - `list_liquid_asset()`: List of high-liquidity Vietnamese stocks.
  - `get_hist(asset)`: Historical OHLCV data.
- `xnoapi.vn.data.derivatives`
  - `get_hist(asset, frequency)`: Derivative market data (e.g., VN30F1M).

**Metrics and Analytics**

- `xnoapi.vn.metrics.Metrics`:
  - Includes: Sharpe Ratio, Sortino Ratio, Max Drawdown, Avg Gain/Loss, Hit Ratio...
- `xnoapi.vn.metrics.Backtest_Derivates`:
  - Backtesting logic for trading strategies with support for fee modeling.
- `xnoapi.metrics.single_asset.TradingBacktest`:
  - Lightweight backtesting class for trading strategies on derivatives (supports raw and after-fee PnL calculation).
  - Metrics included: Sharpe, Sortino, Calmar, Max Drawdown, Win Rate, Profit Factor, Risk of Ruin, etc.

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

**Retrieving Stock Data**

.. code:: python

   from xnoapi import client
   from xnoapi.vn.data import stocks

   client(apikey="your_api_key")

   # Get list of liquid assets
   liquid_assets = stocks.list_liquid_asset()

   # Get historical data for VIC stock
   vic_history = stocks.get_hist("VIC")

----

**Retrieving Derivatives Data**

.. code:: python

   from xnoapi import client
   from xnoapi.vn.data import derivatives

   client(apikey="your_api_key")

   # Get historical data for VN30F1M derivative
   vn30f1m_history = derivatives.get_hist("VN30F1M", "1m")

----

**Using Metrics**

.. code:: python
   from xnoapi.vn.metrics import Metrics, Backtest_Derivates
   from xnoapi.vn.data import derivatives
   import numpy as np

   # Generate signal: simple strategy based on 20-period median
   def gen_position(df):
      return df.assign(
         position=np.sign(df["Close"] - df["Close"].rolling(20).median())
      )

   # Fetch 1-minute historical data
   df = derivatives.get_hist("VN30F1M", "1m")
   df_pos = gen_position(df)

   # Backtest the strategy
   backtest = Backtest_Derivates(df_pos, pnl_type="raw")

   # Initialize metrics
   metrics = Metrics(backtest)

   # === Backtest_Derivates Methods ===

   # Cumulative PNL
   cumulative_pnl = backtest.PNL()

   # Daily cumulative PNL
   daily_cumulative_pnl = backtest.daily_PNL()

   # Estimate Minimum Capital Required
   min_capital = backtest.estimate_minimum_capital()

   # PNL Percentage
   pnl_percentage = backtest.PNL_percentage()

   # === Metrics Methods ===

   # Average Loss
   metrics.avg_loss()

   # Average Return
   metrics.avg_return()

   # Average Win
   metrics.avg_win()

   # Max Drawdown
   metrics.max_drawdown()

   # Win Rate
   metrics.win_rate()

   # Volatility
   metrics.volatility()

   # Sharpe Ratio
   metrics.sharpe()

   # Sortino Ratio
   metrics.sortino()

   # Calmar Ratio
   metrics.calmar()

   # Profit Factor
   metrics.profit_factor()

   # Risk of Ruin
   metrics.risk_of_ruin()

   # Value at Risk
   metrics.value_at_risk()

----

Credits
-------

This library is developed and maintained by the XNO API team. Special thanks to contributors and financial data providers for their support.

----

License
-------

This library is licensed under the MIT License. See the LICENSE file for more details.



