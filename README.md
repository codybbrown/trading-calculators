# Personal Tools for Futures Trading

## TradingView Style R/R Calculator
This will use the multi-page form and results flow until calculations and reactivity/components are done.  Then implement as described below.

### Top Section
0. **Buy/Sell Buttons**
   - Buttons colored to reflect Long/Short
   - *Eventually* assist in form validation
     - e.g. If long, S/L cannot be above entry price etc
1. **Calculates a R/R Ratio from**
   - Full width div with 2 cols
     - Number of units/contracts
     - % or $ amount to risk
### Bottom Section
2. **T/P, R/Metric, S/L Columns**
   - Full width div with 3 cols
   - Set S/L & T/P by price, USD, or % values
   - The selected method causes other 2 methods and R to update accordingly
   - Displays Gain & Loss as
     - USD
     - Percent
3. **R:R**
   - Updates reactively to all inputs
   - Is not setable on its own (yet)
### Style
4. **Color**
   - Color set dynamically by Sell/Buy Buttons

