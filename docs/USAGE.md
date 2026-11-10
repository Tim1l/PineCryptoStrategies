# Indicator Usage & Chart Checks

## Files

- [Confirmed HTF Candles](../indicators/confirmed_htf_candles.pine)
- [Confirmed HTF Bollinger Bands](../indicators/confirmed_htf_bollinger.pine)

Both examples target standard, time-based TradingView charts and Pine Script v6.

## Add an Example

1. Open a chart, for example BTCUSDT on 15 minutes.
2. Open Pine Editor and paste one indicator's source.
3. Use Save and Add to chart.
4. Leave Higher timeframe at 60 for the first check.
5. Repeat with the other indicator in a separate script.

The selected higher timeframe must be strictly greater than the chart timeframe. The script raises an explanatory error for an equal or lower selection.

## Confirmed HTF Candles

The indicator requests the previous completed higher-timeframe open, high, low, and close. Those values repeat across the current lower-timeframe bars.

- Higher timeframe chooses the source interval.
- Bullish candle and Bearish candle control body colours and transparency.
- Show wicks controls wick visibility.
- A new completed candle becomes visible when the next higher-timeframe period starts.

This is a context overlay; it does not reconstruct a full-width higher-timeframe candle or predict the unfinished candle's closing values.

## Confirmed HTF Bollinger Bands

Bands are calculated on higher-timeframe closes, not on repeated lower-timeframe values. The previous completed bar's basis, upper band, and lower band are displayed on the chart.

- Higher timeframe chooses the source interval.
- BB length controls the number of higher-timeframe bars.
- Standard deviation multiplier controls band width.
- Display inputs control line colours, fill and thickness.
- Values remain unavailable until sufficient higher-timeframe history exists.

The step-like update is intentional. Only completed higher-timeframe values are used.

## Chart Verification Checklist

These checks require Pine Editor and an actual TradingView chart:

- [ ] Both scripts compile and add to the chart without errors.
- [ ] Default settings are readable on a 15-minute chart with a 60-minute source.
- [ ] The requested values match the previous completed source-timeframe candle/bands.
- [ ] Values remain consistent while the current source-timeframe candle is developing.
- [ ] Values update at the next source-timeframe period.
- [ ] Reloading the chart preserves the confirmed historical values.
- [ ] Equal and lower source timeframes produce the expected error.
- [ ] Colour, wick, line-width and band inputs behave as described.
- [ ] An actual chart screenshot is captured after verification, without a Strategy Tester performance panel.

Static review and independent timing calculations do not replace these chart checks.

## Implementation References

The examples follow TradingView's documented confirmed-data approach:

- [Other timeframes and data — avoiding repainting](https://www.tradingview.com/pine-script-docs/concepts/other-timeframes-and-data/#avoiding-repainting)
- [Bar plotting](https://www.tradingview.com/pine-script-docs/visuals/bar-plotting/)
- [Timeframes](https://www.tradingview.com/pine-script-docs/concepts/timeframes/)

The higher-timeframe expression is offset inside its context and requested with lookahead_on. This deliberately uses an already completed bar; changing only one part of that pattern can change the meaning.
