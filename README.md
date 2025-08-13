# XNO API Library
XNO API là thư viện Python dùng để truy xuất dữ liệu tài chính và phân tích định lượng, được tối ưu cho thị trường tài chính Việt Nam. Thư viện cung cấp API dạng mô-đun, rõ ràng để lấy dữ liệu cổ phiếu, phái sinh, đồng thời tích hợp công cụ backtest PnL và các chỉ số hiệu suất.

📌 Tính năng nổi bật
🔎 Lấy dữ liệu thời gian thực & dữ liệu lịch sử của cổ phiếu, phái sinh Việt Nam

📈 Tích hợp sẵn các chỉ số hiệu suất: Sharpe, Sortino, Max Drawdown, Win Rate, v.v.

📊 Công cụ backtest PnL cho phái sinh với cấu trúc phí giao dịch đặc thù Việt Nam

🧪 Hỗ trợ pandas, NumPy cho việc xây dựng chiến lược và phân tích tùy chỉnh

🖼️ Dễ mở rộng để xuất biểu đồ và báo cáo hiệu suất chiến lược

📦 Cài đặt
Cài đặt qua pip:

sh
Copy
Edit
pip install xnoapi
Hoặc clone repo:

sh
Copy
Edit
git clone https://github.com/xnoproject/xnoapi.git
pip install ./xnoapi
Khởi tạo sau khi cài đặt:

python
Copy
Edit
from xnoapi import client
from xnoapi.vn.data import stocks, derivatives
from xnoapi.vn.metrics import Metrics, Backtest_Derivates

client(apikey="your_api_key")
📚 Tài liệu
Tài liệu online: https://xnoapi.readthedocs.io



📄 Tài liệu PDF

🚀 Ví dụ nhanh
Lấy và phân tích dữ liệu cổ phiếu & phái sinh Việt Nam:

python
Copy
Edit
from xnoapi import client
from xnoapi.vn.data import stocks, derivatives

client(apikey="your_api_key")

# Danh sách cổ phiếu thanh khoản cao
stocks.list_liquid_asset()

# Dữ liệu lịch sử cổ phiếu VIC
vic = stocks.get_hist("VIC")

# Dữ liệu lịch sử hợp đồng VN30F1M (1 phút)
vn30f1m = derivatives.get_hist("VN30F1M", "1m")
🧠 Các module chính
📊 Dữ liệu tài chính
xnoapi.vn.data.stocks

list_liquid_asset(): Lấy danh sách cổ phiếu thanh khoản cao

get_hist(asset): Lấy dữ liệu lịch sử OHLCV

xnoapi.vn.data.derivatives

get_hist(asset, frequency): Lấy dữ liệu phái sinh (VD: VN30F1M)

📈 Chỉ số & Phân tích
xnoapi.vn.metrics.Metrics:

Các chỉ số: Sharpe Ratio, Sortino Ratio, Max Drawdown, Avg Gain/Loss, Win Rate...

xnoapi.vn.metrics.Backtest_Derivates:

Backtest chiến lược phái sinh, hỗ trợ tính phí giao dịch

xnoapi.metrics.single_asset.TradingBacktest:

Backtest nhẹ cho phái sinh, hỗ trợ PnL trước và sau phí

Chỉ số: Sharpe, Sortino, Calmar, Max Drawdown, Win Rate, Profit Factor, Risk of Ruin, v.v.

🧪 Ví dụ backtest
python
Copy
Edit
from xnoapi.vn.metrics import Metrics, Backtest_Derivates
from xnoapi.vn.data import derivatives
import numpy as np

# Chiến lược đơn giản dựa trên median 20 kỳ
def gen_position(df):
    return df.assign(
        position=np.sign(df["Close"] - df["Close"].rolling(20).median())
    )

# Lấy dữ liệu 1 phút VN30F1M
df = derivatives.get_hist("VN30F1M", "1m")
df_pos = gen_position(df)

# Backtest
backtest = Backtest_Derivates(df_pos, pnl_type="raw")
metrics = Metrics(backtest)

# === Backtest_Derivates ===
cumulative_pnl = backtest.PNL()
daily_cumulative_pnl = backtest.daily_PNL()
min_capital = backtest.estimate_minimum_capital()
pnl_percentage = backtest.PNL_percentage()

# === Metrics ===
metrics.avg_loss()
metrics.avg_return()
metrics.avg_win()
metrics.max_drawdown()
metrics.win_rate()
metrics.volatility()
metrics.sharpe()
metrics.sortino()
metrics.calmar()
metrics.profit_factor()
metrics.risk_of_ruin()
metrics.value_at_risk()
🤝 Đóng góp
Dự án được duy trì bởi Nhóm XNO.
Xin cảm ơn các cộng tác viên và nhà cung cấp dữ liệu đã hỗ trợ cộng đồng định lượng tại Việt Nam.

📄 Giấy phép
Phát hành theo MIT License.
Xem chi tiết tại LICENSE.


# XNO API Library

**XNO API** is a Python package for retrieving financial data and performing quantitative analysis, specifically optimized for the **Vietnamese financial market**. It provides a clean, modular interface to access data on stocks, derivatives, and backtesting tools for PnL and performance metrics.

---

## 📌 Key Features

- 🔎 Simple interface to retrieve **real-time and historical data** for Vietnamese stocks and derivatives
- 📈 Built-in support for **performance metrics**: Sharpe, Sortino, Max Drawdown, and more
- 📊 Optimized **PnL backtesting tools** for derivatives with **Vietnam-specific fee structures**
- 🧪 Compatible with pandas, NumPy for custom strategies and analysis
- 🖼️ Easily extensible for **visual output of strategies and metrics**

---

## 📦 Installation

Install via pip:

```sh
pip install xnoapi
```

Or clone this repo:

```sh
git clone https://github.com/xnoproject/xnoapi.git
pip install ./xnoapi
```

After installation:

```python
from xnoapi import client
from xnoapi.vn.data import stocks, derivatives
from xnoapi.vn.metrics import Metrics, Backtest_Derivates

client(apikey="your_api_key")
```

---

## 📚 Documentation

- Online Docs: [https://xnoapi.readthedocs.io](https://xnoapi.readthedocs.io/en/latest/)
- ![Documentation Status](https://readthedocs.org/projects/xnoapi/badge/?version=latest)
- [📄 PDF version](https://buildmedia.readthedocs.org/media/pdf/xnoapi/latest/xnoapi.pdf)

---

## 🚀 Usage Example

Retrieve and analyze Vietnamese stock & derivative data:

```python
from xnoapi import client
from xnoapi.vn.data import stocks, derivatives

client(apikey="your_api_key")

# List of liquid stocks
stocks.list_liquid_asset()

# Historical data for VIC (Vingroup)
vic = stocks.get_hist("VIC")

# Historical data for VN30F1M derivative
vn30f1m = derivatives.get_hist("VN30F1M", "1m")
```

---

## 🧠 Available Modules

### 📊 Financial Data

- `xnoapi.vn.data.stocks`

  - `list_liquid_asset()`: List of high-liquidity Vietnamese stocks.
  - `get_hist(asset)`: Historical OHLCV data.

- `xnoapi.vn.data.derivatives`
  - `get_hist(asset, frequency)`: Derivative market data (e.g., VN30F1M).

### 📈 Metrics & Analytics

- `xnoapi.vn.metrics.Metrics`:
  - Includes: Sharpe Ratio, Sortino Ratio, Max Drawdown, Avg Gain/Loss, Hit Ratio...
- `xnoapi.vn.metrics.Backtest_Derivates`:
  - Backtesting logic for trading strategies with support for fee modeling.
- `xnoapi.metrics.single_asset.TradingBacktest`:
  - Lightweight backtesting class for trading strategies on derivatives (supports raw and after-fee PnL calculation).
  - Metrics included: Sharpe, Sortino, Calmar, Max Drawdown, Win Rate, Profit Factor, Risk of Ruin, etc.

---

## 🧪 Examples

### Strategy Evaluation with Metrics

```python
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

```

---

## 🤝 Credits

Maintained by the **XNO Team**.  
Special thanks to contributors and financial data providers supporting the Vietnamese retail quant community.

---

## 📄 License

This project is licensed under the [MIT License](https://choosealicense.com/licenses/mit/).  
See [LICENSE](https://github.com/xnoproject/xnoapi/blob/main/LICENSE) for full details.
