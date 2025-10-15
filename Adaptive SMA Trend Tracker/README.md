# Adaptive SMA Trend Tracker

A TradingView Pine Script indicator that displays adaptive Simple Moving Averages (SMAs) with trend-based shading and optional start line markers.

## Features

### Adaptive Daily SMAs
- **5-Day SMA** (Yellow) - Only shown on intraday timeframes
- **20-Day SMA** (Orange)
- **50-Day SMA** (Pink)
- **200-Day SMA** (Red)

The indicator automatically adapts to intraday timeframes by calculating the correct number of bars per day, ensuring accurate SMA periods regardless of chart resolution (1min, 5min, 15min, etc.).

### Weekly SMAs
When viewing weekly charts, the indicator automatically switches to display:
- **20-Week SMA** (Orange)
- **32-Week SMA** (Pink)
- **42-Week SMA** (Red)

### Trend-Based Shading (5-Day SMA)
On intraday charts, the area between price and the 5-day SMA is shaded to indicate trend strength:
- **Green** - Price above 5-day SMA and SMA trending up (bullish)
- **Red** - Price below 5-day SMA and SMA trending down (bearish)
- **Yellow** - Transition periods (mixed signals)

### Start Line Markers
Visual vertical lines that mark where each SMA calculation begins:
- **5-Day SMA Start Line** - Enabled by default
- **50-Day SMA Start Line** - Disabled by default
- **200-Day SMA Start Line** - Disabled by default

Each start line can be customized with Solid, Dashed, or Dotted styles and uses the matching SMA color.

## Installation

1. Open TradingView
2. Open the Pine Editor (bottom panel)
3. Click "New" to create a new indicator
4. Copy and paste the entire script
5. Click "Save" and give it a name
6. Click "Add to Chart"

## Settings

### Start Lines Group
- **Show 5-Day SMA Start Line** - Toggle visibility (default: ON)
- **5-Day SMA Start Line Style** - Solid/Dashed/Dotted (default: Dashed)
- **Show 50-Day SMA Start Line** - Toggle visibility (default: OFF)
- **50-Day SMA Start Line Style** - Solid/Dashed/Dotted (default: Dashed)
- **Show 200-Day SMA Start Line** - Toggle visibility (default: OFF)
- **200-Day SMA Start Line Style** - Solid/Dashed/Dotted (default: Dashed)

## How It Works

### Adaptive Bar Calculation
The indicator monitors the first 3 complete days on intraday charts to determine the exact number of bars per day. This ensures accurate SMA calculations across different intraday timeframes.

### Timeframe Detection
- **Intraday**: Shows daily SMAs with adaptive period calculation
- **Daily**: Shows daily SMAs with standard periods
- **Weekly**: Automatically switches to weekly SMAs

### Performance Optimization
- SMAs only displayed when sufficient historical data is available
- Efficient caching of line objects and calculations

## Technical Details

- **Pine Script Version**: v6
- **Overlay**: Yes (draws on the price chart)
- **Max Bars Back**: 5000

## License

MIT License - See file header for full license text

## Contributing

Contributions, issues, and feature requests are welcome!

## Author

Copyright (c) 2024
