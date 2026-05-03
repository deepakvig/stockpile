# YouTube Script: "Visualize Your Position's Cost Basis with Claude Code"

## Title
Charts Your Broker Doesn't Show You (Using Claude Code)

## Thumbnail Ideas

Done - Choosing #1

**Concept 1 — The Chart IS the Thumbnail** *(recommended)*
Background: screenshot of the Midnight-scheme chart (dark navy,
blue/orange lines). Bold white text overlaid:
- Large: Chart YOUR REAL COST BASIS
- Small (bottom): Build it with Claude Code

Give Gemini: the chart screenshot + "make a YouTube thumbnail with
bold white text 'YOUR REAL COST BASIS' in the upper third and small
text 'Built with Claude Code' at the bottom, keep the chart visible"

**Concept 2 — Split / Contrast**
Left half: greyed-out brokerage account view. Right half: colorful
chart. Bold text across the center:
- vs. THIS

Give Gemini: both images side by side + "YouTube thumbnail split
screen, left side desaturated/grey, right side vibrant, bold text
'vs. THIS' across the middle"

**Concept 3 — The Hook**
Dark background, your face (surprised/impressed) on one side, chart
on the other. Text:
- YOUR BROKER HIDES THIS

Give Gemini: your photo + chart screenshot + "YouTube thumbnail, face
on left looking surprised, chart on right, bold red/white text 'YOUR
BROKER HIDES THIS' at the top"

---

## HOOK (0:00–1:30)

*[10 Animation: chart fly-in — close price line draws left to right,
then adjusted cost basis line draws underneath it, transaction
markers pop in, right-edge labels appear showing P&L]*

DONE -----

This episode is all about charting your positions with Claude Code.
It's related to my last episode about making Google Sheets for your
positions with Claude Code, linked in the description.

We're going to once again use transaction logs from your brokerage,
but this time we're going to visualize your position performance
with charts.

Borrowing the theme from last episode, the charts in this episode
will show you something your brokerage account doesn't — your positions
*real* performance.

[11 Switch to a real chart]

DONE -----

Here's a more complex chart.
We'll dive deeper into this chart later in this episode.

It visualizes every call and put you've ever bought or sold,
every dividend you've collected, and every time you've bought and
sold shares.  This information will be in the transaction logs
you'll download from your brokerage.

I built this entire thing without writing a single line of code,
I just described what I wanted, and Claude wrote all the
code to produce these charts, and document them. It even suggested
the free charting tool to use.

[Back to Animation]

DONE -----

This is Claude Design, a new product that comes with Claude Code.
I simply asked it to animate one of the static charts I generated
from my transaction log.

That's what you're seeing here and all I did was ask. That was my first
experiment with Claude Design, and I'm looking forward to using it more
in the future.

---

## SETUP THE PROBLEM (1:30–2:10)

[Show actual chart]

DONE -----

Back to the more detailed static Cost Basis Chart

Most people look at their brokerage account and see a table or chart
showing a simple average cost per share. We'll do better.
These charts will enhance your typical broker's position view with every
transaction related to each of your positions. The Python script
parses your transaction history, runs First In, First Out accounting
on every trade, and subtracts all the income you've collected. Each
of the lines you see here is a view of a different metric measuring how
profitable your position is.

It also includes the real historical price from Yahoo
Finance, this blue line.  So you can see the full picture at a glance.

---

## LIVE DEMO — ADDING PNG EXPORT (2:10–4:10)
*[Screen: terminal with Claude Code open, chart HTML visible]*

DONE -----

Before we really dig in to the features of the chart just shown,
let's see how to add a feature to the chart with Claude Code.

The chart outputs as HTML, which is great — but what if I want to
share one as an image in a doc or a Slack message?  I could just do a
screen capture, but it might be easier to generate a PNG of the 
chart.

Let me ask Claude...
But first, I need to remind claude how we run things around here,
and I'll ask him to put it in his Claude.md file so he remembers 
going forward.

[go over text in screen...]

DONE -----

*[Type into Claude Code: "add a --png flag that saves a static PNG
of the chart alongside the HTML"]*

*[Claude writes the code — briefly show the diff scrolling]*

DONE -----

"Done. Let's run it."

*[Terminal:]*
`uv run python cost-basis-charts/run_charts.py --symbol PFE --png`

*[File explorer: PFE_cost_basis.png appears in the charts/ folder]*
*[Open the PNG]*

DONE -----

"That's the whole workflow. Describe what you want, Claude writes it,
you test it. No docs, no Stack Overflow, no writing code."

---

## THE CHART IN DETAIL (4:10–7:40)
*[Show a chart with open options — dashed live cost line visible]*

"Let's take a closer look at everything on this chart.

The blue line is the closing price from Yahoo Finance — that's what
the stock actually traded at each day.

The purple line is your stock FIFO cost basis. That's the raw
average cost of your shares based on the order you bought them —
first in, first out. Every time you buy shares, it includes them in
the average. Every time you sell, the oldest lots come off first
and it adjusts.
 
---- ^^ Done

The orange line is your adjusted cost basis. Every time you collect
a premium on a covered call or put, or receive a dividend, that income
gets subtracted from your cost. Over time, if you're actively selling
options and/or collecting dividends, you'll see this
line drift lower and lower — meaning your cost basis is less, and
it's easier for the position to be profitable. The one exception is
if you sell a debit roll, not a credit, then the line will drift
higher.  For selling options, that means you paid more premium to close out
your old position than you collected to open your new position.


**** looks like rolls aren't showing the STO transaction?
bug to fix, look at transaction log.

The dots on the lines mark individual transactions — buys, sells,
options trades, dividends. Hover over any dot, and you'll see
exactly what the transaction was. Hover anywhere on the price line,
and you get the closing price plus your P&L per share against your
adjusted cost at that date.

The labels on the right edge show your current numbers at a glance —
close price, adjusted cost, and FIFO cost, with P&L in green or red.

If you have open covered calls or puts right now, the chart gets
one more line — the dashed one. The script estimates the current
market value of each open option using Black-Scholes (linked in
description) and adds that liability back into your cost basis. So
you can see your *true* break-even today. This accounts for what it
would cost to close your open positions. That line updates every
time you run the script.

The dashed horizontal line shows your strike price over the lifetime
of your open option — from when you opened it to expiration. You
can see at a glance whether the stock is above or below your
strikes.

Below the main lines you'll also see Intrinsic Value and Time Value.
These break down the current worth of your open options. Intrinsic
value is how far in the money the option is — the portion that has
real dollar value right now.

Time value is everything else — the probability premium that decays
to zero as you approach expiration. Depending on circumstances, Time
value can be a great indicator of whether to close your position.
For example, if a covered call is deep ITM and will almost surely
get called away, and its remaining Time Value is very small compared
to the position's close out value, then you may consider taking
action.

You'd probably be better off closing the position and investing in
better yielding cash or finding another investment opportunity.

---

## HOW I BUILT THIS WITH CLAUDE CODE (7:40–8:20)

"The entire script for building these cost basis charts was written by
Claude Code. I described what I wanted 
 — parse broker CSVs
 - compute FIFO cost basis,
 - make a line showing this, make another line showing that
 - Annotate this line like this
 - add the historical Yahoo Finance prices,
 - and a line for the current option

And on and on, and Claude wrote it. Then I iterated visually:
tweaked the chart layout, added things like the Black-Scholes estimate of
the open option line, added the annotation collision-avoidance so labels
don't overlap.

The whole workflow is:
- describe the feature I want to Claude,
- let Claude work its magic and implement it.
- look at the output,
- say what's wrong, 
- repeat.

So much easier than the olden days when I actually had to write the code
from scratch.  And Claude is a better coder, documenter, and refactorer
than I ever was.

---

## WHAT YOU'LL NEED (8:20–8:45)

If you'd like to do this yourself with your transaction logs,
You'll need to do some setup.  The easy-mode way to do this is to get
a subscription to Claude Code (linked in the description and project README),
and start Claude in the stockpile/cost-basis-charts directory after cloning
or downloading the repository.  Then ask it to help you get it running with
your transactions file.

You'll need:

1. A transaction history export from your brokerage. My repo
   currently supports Schwab and Robinhood, more brokerages soon.
2. Python installed on your machine, see the README for details
   and let Claude help if you have a Claude subscription.
3. This repo — link in the description, it's free on GitHub.

---

## EXPORTING YOUR TRANSACTIONS (8:45–9:15)
*[Screen recording of Schwab web UI]*

I won't bore you with how to download your brokerage full transaction
history, just put it somewhere — the /input directory in the root of
this repo works. Make sure you go back as far as you can to increase
your chances of getting all your position history. Create a copy of 
config.toml.example and name it config.toml in the cost-basis-charts folder.
Then point the configuration in that file to your downloaded transactions file
from your brokerage.

---

## RUNNING IT (9:15–10:15)
*[Terminal: `uv run python cost-basis-charts/run_charts.py`]*

Once you've done all the setup, you'll run it with one command from
the repo root. It'll parse your transactions, pull
historical prices from Yahoo Finance, and write an interactive HTML
file for each ticker into the `cost-basis-charts/charts` folder.

*[Go to charts folder and open one with Chrome]*

Open one of the charts you just made, and have a look — be sure to
hover the mouse over the lines.

If you want to tweak it, improve or add new features, feel
free! Subscribe to Claude Code, fork my repo, and let us know what
you did.

---

## OUTRO (10:15–10:35)
Link to the repo is in the description — it's all open source. If
you're running covered calls, wheeling, or just want a more complete
picture of your positions' performance, this will help.

Let me know in the comments what other views or features would
be useful, I'd love to hear your ideas about other interesting things
we could do with our transaction logs.

Please consider liking and subscribing, and have a look at my last
episode, which was about making Google Sheets from your transaction
logs.

---

## RESOURCES (description links)

- Repo: https://github.com/medloh/stockpile
- Black-Scholes explained:
  https://www.investopedia.com/terms/b/blackscholes.asp
- Previous episode (Google Sheets positions tracker):
  https://youtu.be/9uf3cyOWPBQ?si=kRyNK88tkc9qD5o0

Support the work:
- GitHub Sponsors: https://github.com/sponsors/medloh
- Patreon: https://www.patreon.com/OptionsforLongTermInvestors

---

## PRODUCTION NOTES

### Before Recording
- Write the description first — YouTube indexes it for search
- Pick a target keyword phrase ("cost basis covered calls", "Claude
  Code python stock charts") and say it naturally in the first 30s
- Record a strong first 30 seconds — audience retention at 30s is a
  key ranking signal

### Before Publishing
- Add chapters (timestamps in description) — viewers scrub instead
  of leaving, which increases watch time
- Add 3–5 tags matching your target keywords
- Write strong first 2 lines of description — that's what shows
  before "show more" in search results
- Set custom thumbnail BEFORE publishing, not after
- Add cards at ~20%, 40%, 60% of runtime pointing to the Google
  Sheets episode

### Immediately After Publishing (first 48 hours matter most)
- Share to relevant communities:
  - r/options, r/thetagang, r/learnprogramming
  - Claude/AI Discord servers
  Early velocity signals quality to the algorithm
- Pin a comment with the repo link and a seed question:
  "What other charts would be useful?"
- Reply to every early comment — engagement in the first 48 hours
  boosts distribution

### Exit Screens
Go back and add this video to the exit screen of:
- The Google Sheets episode https://youtu.be/9uf3cyOWPBQ?si=3MoC5Mfjvf39ujn0
- Any other popular episodes on your channel
Viewers already interested in your tools are most likely to watch
both.

### Ongoing (2 weeks after)
- Check YouTube Studio analytics
  - If click-through rate is under ~4%, test a new thumbnail
  - If one chapter gets most views, consider a standalone short on
    just that topic
