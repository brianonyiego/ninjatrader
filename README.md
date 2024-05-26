# ninjatrader
NinjaScript strategy code for NinjaTrader
This NinjaScript strategy implements a basic moving average crossover strategy in NinjaTrader. It buys when a faster Simple Moving Average (SMA) crosses above a slower SMA and sells when the faster SMA crosses below the slower SMA.

## Installation

To use this strategy in NinjaTrader, follow these steps:

1. Open NinjaTrader.
2. Go to the "File" menu and select "Utilities" -> "Import NinjaScript..."
3. Locate the `MyStrategy.cs` file in your local directory and select it for import.
4. Once imported, you should be able to find the strategy under the Strategy Analyzer in NinjaTrader.

## Strategy Details

The strategy logic is defined in the `MyStrategy.cs` file. Here's a breakdown of the key components:

### Strategy Initialization

```csharp
using System;
using NinjaTrader.Cbi;
using NinjaTrader.NinjaScript.StrategyAnalyzer;

namespace NinjaTrader.NinjaScript.StrategyAnalyzer
{
    public class MyStrategy : StrategyAnalyzerBase
    {
        private SMA fastSMA;
        private SMA slowSMA;

        protected override void OnStateChange()
        {
            if (State == State.SetDefaults)
            {
                // Strategy settings
                Description = @"Enter the description for your new custom Strategy Analyzer";
                Name = "MyStrategy";
                // Other default settings...
            }
            else if (State == State.Configure)
            {
                // Initialize SMAs with period settings
                fastSMA = SMA(14);
                slowSMA = SMA(28);
            }
        }
```

### Strategy Logic

```csharp
protected override void OnBarUpdate()
{
    if (BarsInProgress != 0) return;

    // Check for crossover
    if (CrossAbove(fastSMA, slowSMA, 1))
    {
        // Buy logic here
        EnterLong(1, "FastSMA CrossAbove");
    }
    else if (CrossBelow(fastSMA, slowSMA, 1))
    {
        // Sell logic here
        EnterShort(1, "FastSMA CrossBelow");
    }
}
```

## Usage

Once the strategy is imported into NinjaTrader, you can apply it to any chart or instrument. Adjust the SMA period settings as desired for different timeframes and market conditions.

