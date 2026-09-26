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

## Usage

Open TradingView → Pine Editor → paste the file contents → *Add to chart*.
