# Adaptive SMA Trend Tracker

Pine Script indicator providing **precision SMAs** that adapt to actual market trading hours, plus integrated ATR risk calculator with position sizing.

## Why This Indicator?

### 🎯 **True Intraday Precision**
Standard TradingView SMAs on intraday charts use daily closes (5 data points for 5-day SMA). This indicator uses **all intraday bars** - 390 bars for a 5-day SMA on a 5-minute chart.

### 🔄 **Adaptive to Market Hours**
Automatically detects actual trading hours and adapts when you switch between Regular Trading Hours (RTH) and Extended Trading Hours (ETH). No manual configuration needed.

### 💰 **Integrated Risk Calculator**
Built-in ATR display with position sizing - shows your dollar risk for stocks or per-contract risk for futures. Auto-detects instrument type.

## Features

### Adaptive SMAs
- **Daily**: 5, 20, 50, 200-day SMAs calculated on actual intraday bars
- **Weekly**: 20, 32, 42-week SMAs for weekly charts
- **Trend Shading**: Background color indicates bullish/bearish/transition states
- **Start Lines**: Optional markers showing where SMA calculation begins

### ATR Risk Display
- **Configurable Period**: Adjust ATR period (1-500 bars, default: 20)
- **Position Sizing**:
  - **Stocks/Forex**: Enter dollar position size → see risk in currency
  - **Futures**: Enter contracts/lots → auto-calculates using contract specifications
- **Customizable**: Choose position (4 corners), colors, and text size
- **Example Output**: `ATR(20): 2.45% | 245.00 USD`

## How It Works

The indicator scans the last 10 trading days, counts bars per day, and uses the most common bar count (statistical mode) to calculate precise SMA periods. This ensures SMAs reflect actual trading hours regardless of timeframe.

**Example**: On a 5-minute chart with a 6.5-hour stock market:
- Detects ~78 bars per day
- 5-day SMA = 390 bars (5 × 78)
- 20-day SMA = 1,560 bars (20 × 78)

Continuously adapts via rolling 10-day window to track session changes.

## Supported Markets & Timeframes

### Markets
- ✅ Stocks (any exchange)
- ✅ Crypto (24h)
- ✅ Forex (variable hours)
- ✅ Futures (any contract)
- ✅ Commodities

### Timeframes
- ✅ **Intraday**: 30-second to multi-hour candles (optimal)
- ✅ **Daily**: Works, uses standard 1 bar = 1 day logic
- ✅ **Weekly**: Works, separate weekly SMA calculations

## Requirements & Behavior

### Initial Setup
- Minimum 20 bars of data to start
- Requires 3 trading days for accurate calculation
- First 3 days use theoretical approximation (assumes 6.5h stock market), then switches to precise scanned values

### Adaptive Behavior
- Values update as new days are scanned (rolling 10-day window)
- Automatically adapts to RTH/ETH switches
- Filters holidays and data gaps automatically

### Known Limitations
- **Fresh IPOs**: First 3 trading days use 6.5h stock market assumption, auto-corrects after scanning
- **Crypto/24h Markets**: Initial approximation less accurate (assumes stock hours), refines after 3 days
- **Very Low Timeframes** (< 30s): May need more historical data for initialization

## Configuration

### Start Lines
- Toggle display for 5, 50, and 200-day SMAs
- Choose line style: Solid, Dashed, or Dotted

### ATR Display
- **Show ATR**: Toggle on/off
- **ATR Period**: Adjust calculation period
- **Position Size ($)**: For stocks/forex/crypto
- **Contracts/Lots**: For futures (auto-detected)
- **Position**: Top Left, Top Right, Bottom Left, Bottom Right
- **Colors**: Background and text colors
- **Text Size**: Auto, Tiny, Small, Normal, Large, Huge

## Technical Notes

### Algorithm
- Scans using `timeframe.change("D")` to detect day boundaries
- Uses statistical mode of bar counts (most common session length)
- Filters outliers: 1-1,200 bars/day range (catches holidays and corrupt data)
- Efficient: O(1) per bar, minimal memory footprint

### Why ATR Not ADR?
ATR (Average True Range) accounts for price gaps between sessions, making it superior for risk management. ADR (Average Daily Range) only measures high-low spread and misses overnight/weekend gaps.

### Pine Script Limitations
The adaptive calculation must run in the current chart's timeframe context. Pine Script's higher-timeframe data requests cannot maintain the stateful logic required for bar counting across multiple days.

---

**License**: MIT
**Version**: Pine Script v6
