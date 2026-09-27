# pine-indicators

TradingView Pine Script v6 indicators.

## Indicators

### Turn Confirmation Levels (`indicators/turn_confirmation_levels.pine`)

Overlay indicator that builds confluence clusters from Fibonacci retracements of
the dominant swing leg, a set of moving averages, and recent pivot highs/lows.
The densest cluster above price becomes the **primary trigger**; the next
densest becomes the **secondary trigger**. A breakout is reported only when the
bar *closes* above the primary trigger and volume exceeds the configured
multiple of its rolling average. The most recent pivot low is drawn as the
invalidation level.

**Inputs** are grouped into Leg/Fib, Moving Averages, Cluster/Trigger, Volume
Filter, Display, and Colors.

**Alerts:** an `alertcondition` for chart-based alerts, plus a runtime `alert()`
firing once per confirmed bar close with ticker, trigger price, confluence
count, and volume ratio.

**Latching.** The clusters are rebuilt on every bar from the levels above the
close, so the *selection* floats upwards as price rises even though the levels
themselves mostly do not move: as price approaches one band, a higher one is
chosen. An unlatched trigger is therefore a moving target. The **Latch** group
freezes it. `Latch triggers` turns the freeze on and `Latch anchor bar` is an
interactive input — click a bar on the chart and the triggers are held as they
stood there until you switch the latch off. Because the anchor is an absolute
timestamp rather than an offset, the same bar is chosen again on every reload.
A latched level signals once rather than on every subsequent bar above it.

### Confluence Ladder (`indicators/confluence_ladder.pine`)

Companion to the above, answering a different question. It does no banding at
all: it lists every distinct level above the close in ascending order and
reports the cumulative count of levels a move would clear on the way to each
one. The highlighted trigger is the highest rung inside a configurable distance
budget, so it clears the most levels available within that range.

The two scripts can legitimately disagree. Turn Confirmation Levels optimises
for the densest band; this one makes the distance-versus-levels-cleared
trade-off visible and leaves the choice to you. Neither output is a
recommendation.

It carries the same **Latch** group, freezing the trigger rung at an anchor bar
you click on the chart.

## Usage

Open TradingView → Pine Editor → paste the file contents → *Add to chart*.
