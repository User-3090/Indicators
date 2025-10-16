# Adaptive SMA Trend Tracker

A Pine Script indicator that provides **higher precision SMAs** than TradingView's standard implementation by calculating on actual intraday timeframes and adapting to real market trading hours.

## Key Features

### 🎯 **Higher Precision**
- Calculates SMAs using actual intraday bars, not simplified daily approximations
- Example: 5-day SMA on 5-min chart = 390 bars (6.5h market), not just 5 daily closes
- Provides true intraday moving average behavior

### 🔄 **Adaptive Calculation**
- Automatically detects actual market hours (stocks: 6.5h, crypto: 24h, futures: 23h, etc.)
- Adapts to Regular Trading Hours (RTH) vs Extended Trading Hours (ETH) switches
- Continuously updates via rolling 10-day window

### 🌍 **Universal Compatibility**
- Works on any market: Stocks, Crypto, Forex, Futures, Commodities
- Supports intraday timeframes: 30-second to multi-hour charts
- Handles holidays, data gaps, and irregular sessions automatically

## Features

- **Daily SMAs**: 5, 20, 50, 200-day with dynamic shading (bullish/bearish/transition)
- **Weekly SMAs**: 20, 32, 42-week for weekly charts
- **Start Lines**: Optional vertical markers showing SMA calculation start points
- **Adaptive Shading**: Background color indicates trend state relative to 5-day SMA

## Requirements

- Minimum 100 bars of historical data
- Data spanning at least 3 trading days for accurate calculation

## Behavior

- First 3 days: Uses theoretical calculation (may be inaccurate)
- After 3 days: Switches to scanned actual bar counts (accurate)
- Continuously adapts: Rolling window tracks most recent trading patterns
- Adaptive repainting: Historical values update when session settings change

## Technical Details

- **Algorithm**: Rolling window (10 days) with mode-based bar count detection
- **Performance**: O(1) per bar, minimal memory footprint
- **Validation**: Filters holidays, data gaps (5-1,200 bars/day range)
- **Precision**: True intraday calculation vs approximate daily-based SMAs

---

**License**: MIT  
**Version**: Pine Script v6