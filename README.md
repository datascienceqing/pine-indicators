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

### Breakdown Confluence Levels (`indicators/breakdown_confluence_levels.pine`)

The downside mirror of Turn Confirmation Levels. Candidates are collected
*below* the close, clusters are ranked by how many levels they hold, and the
trigger is the cluster's **top** edge — the first price a decline meets on the
way into the shelf. A confirmed breakdown is a close below that level on
above-average volume, with the bar closing in the lower part of its own range
(a "breakdown" bar that closes on its high is not one).

Adds beyond the upside script: an ATR-based suggested stop, the next shelf down
as a target with the resulting R:R, and a retest line marking the level that was
broken.

## Usage

Open TradingView → Pine Editor → paste the file contents → *Add to chart*.
