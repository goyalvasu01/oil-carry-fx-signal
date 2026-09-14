# Oil Carry-Based FX Signal

**Module:** Financial Econometrics, Imperial College London

A systematic FX trading strategy driven by a Brent crude oil term-structure carry signal, with a point-in-time signal construction designed to eliminate look-ahead bias.

## Method

The signal is derived from the spread between Brent 3rd-nearby (CO3) and 12th-nearby (CO12) futures contracts — a measure of whether the oil futures curve is in backwardation or contango. Two signal variants are constructed:

- **SIGNAL_CARRY**: +1 if the CO3–CO12 spread is positive (backwardation), -1 if negative (contango)
- **SIGNAL_CARRY_MOM**: +1 if the spread is above its 4-week rolling average, -1 otherwise

These signals are used to trade FX futures on a weekly basis, tested over an 18-year sample from 2007 to 2025.

## Point-in-Time Construction

An earlier version of the signal used the same Friday closing price to both observe the carry signal and execute the FX trade — which is not achievable in live trading, since you cannot observe a closing price and transact at that same price simultaneously.

This version corrects that: the carry signal is observed from **Thursday's close**, and the FX trade is executed at **Friday's close**, introducing a realistic one-day information lag between signal and execution. Public holidays that fall on a Thursday (Christmas Day and New Year's Day, occurring 5 times across the sample) are handled by falling back to the last available trading day (Wednesday), reflecting how a trader would actually source a price in that scenario.

## Performance Evaluation

Strategy robustness was assessed using lead/lag Information Ratio (IR) analysis, comparing the realistic Thursday-signal implementation against a theoretical zero-lag benchmark, to quantify the true cost of the one-day execution lag.

## Tools

Python (Pandas, NumPy, Matplotlib)

## Files

- `Signal_Construction_Thursday.ipynb` — signal construction and point-in-time correction logic

*Raw futures price data (Bloomberg Brent CO3/CO12) and FX price data are omitted from this repository due to data provider licensing restrictions.*

---
Vasu Goyal | MSc Financial Technology, Imperial College London (2025–2026)
https://linkedin.com/in/goyalvasu01 | vasu.goyal25@imperial.ac.uk
