# YouTube Script: Options Scanner

## Title Ideas

### keep this one
- Option Scanner by Claude
- Claude finds the best Options
- "Use Claude to find the Best Options (Python)"
- "Claude Code Finds Mis-Priced Options (Python)"

- "I Built a Free Web App That Finds Mispriced Options"
- "See Which Options Are Overpriced — In One Chart"
- "Click Scan → See the Best Options to Sell (Free Tool)"
- "The Options Screener Your Broker Doesn't Have"
- "Find Overpriced Options in 30 Seconds (Free, Any Ticker)"
- "I Built an Options Scanner with Claude Code — Here's How to
  Use It"

---

## HOOK (0:00–1:15)

[10 SHOW Yahoo Finance Option Chain]*

If you sell options — covered calls, cash secured puts,
you've probably stared at an option chain and wondered
which contract is actually the best one to sell.

Same goes for option buyers.

[11 Option Scanner load screen]

So I decided to build a tool to help, a free option scanner
made with Claude Code.  I built it in a few nights.  It finds the best
options from Yahoo Finance Option Chains and

(scroll to see pre populated chart and tables)
shows them to you in a chart and 2 tables.

(BACK TO top — refresh page, type **ticker**)

[12 Refresh so no results]

Let me demonstrate:

Let's say you have 100 shares of [Disney] and you're
interested in making some extra income on these shares by selling a
covered call. [hover over the controls you may need to set]
You'd like to keep the option open for at least a year so you
can be taxed at the long term rate on the premium you collect.
It also works for shorter dated options.

Let's do the scan and see what it finds...
(Type a ticker. Click Scan)

[13 Results]

The Spot is the underlying stock's current price, shown here and on the chart
it's the vertical line.

It found 3 expirations, and you can select each one here in this dropdown.
which will update the chart and two tables below.
The one it selects at first is the expiration with the best option
shown in the bottom table, this one.

You can see the next earnings is [date].
Earnings have a big effect on option volatilty when they're near.

[20 VOLATILITY SURFACE CHART — dots and dashed curve]*

(scroll down to chart)

Now lets look at the chart.

Each dot on this chart is a call for [Dis] at this Expiration, that
meets our scan criteria. 

The bigger green dots are the more attractive options, meaning their
volatility is higher than what the other options suggest it should be.
This expiration only has one attractive option, but look at this one,
it has 4, but none as good as the other expiration.

The dashed line is what the option scanner says each
strike's implied volatility *should* be —
to be fancy, it's a fitted volatility surface.

[21 POINT TO GREEN DOTS ABOVE THE LINE]

Again, the green dots are sitting above the line. That means the market
is pricing those options richer than their neighbors. More
premium for the same amount of risk. Those are the calls to consider selling.

(POINT TO RED DOTS BELOW)

The smaller Red dots are the opposite — cheaper than they should be.
If you're buying calls, you'd be interested in those.
But probably not the ones you'd want to sell.

(HOVER OVER A DOT — tooltip shows strike, IV+pp, delta)

Hover over any dot, and you get the strike, the expiration, how many
percentage points it sits above the surface, the delta, and the
open interest. That's about everything you need to decide whether to sell it,
Other than your situation and circumstances.

[22 Like and subscribe Slide]
We'll spend a little more time on the chart, and then go over the 2 tables.
Then we'll talk about what you need to set this up and start using it.
It's quick and easy.
And lastly I'll describe how I made it with Claude.

Please consider liking and subscribing if you're enjoying this content.
---

## WHAT THE TOOL IS DOING (1:15–2:30)

*[30 CHART AGAIN — annotate as you talk]*
Alright, back to the chart...
It provides a great way to see the attractiveness of all options
for a given expiration.

A stock's option chain should form a smooth surface. Plotting the
implied volatility against strike, and it traces a shape — the
volatility smile. Smooth transitions between expirations.
Market makers like to keep it that way.

The dashed line in the chart is that smooth shape, fit to the
chain. When an option's actual IV sits noticeably above the
line, something made it more expensive than its neighbors — a
stale quote, a thin market, event risk that isn't evenly
distributed, or just an inefficiency. That's the option you
want to consider first, to sell.

[31 COLOR LEGEND]*

The color of the dot tells you the gap, in percentage points, between the
actual IV and the fitted surface. We call it IV-plus-pp. Small
gaps — under three percentage points — mean the option is
uniformly priced and the ranking is mostly noise. If you can find some with
Five or more points above the line, it could be a genuine signal.

[32 SCROLL DOWN TO THE TABLES]*

Below the chart are two tables.

The first is the chain view. It shows every option in the
expiration selected in the chart dropdown above, sorted by
strike — it's like reading an option chain from your broker with extra
information. The rows are shaded: green means IV+pp is meaningfully above
the average for that expiration, gray means it's price is close to its expected
price, and red means the price of the option is less than usual.

[33 POINT TO ROW SHADING IN CHAIN VIEW]*

You see all the strikes for the expiration at a glance,
and the shading does the filtering for you —
you can see in seconds which strikes have rich
premium and which ones are unremarkable.

[34 POINT TO YELLOW BID/ASK CELLS]*

Two other signals in the table. Yellow Bid and Ask cells mean
the spread is wider than typical for this chain — the gap
between what buyers will pay and sellers will accept. A wide
spread means your real execution price may land 
worse than the mid-price suggests. Yellow OI or Vol means open
interest or today's volume is low — which makes it harder to
fill at a good price.

Hover over the column headers with yellow shaded cells, and it explains
what the yellow color means.  You can also hover over the IV+pp column header
for a more detailed explanation of it.

[35 POINT TO SECOND TABLE — "TOP CANDIDATES — ALL CHAINS"]*

Let's move down to the top candidates table — the highest-ranked
options by IV+pp pulled from every expiration are shown here.
The top table showed me everything for single expiration, sorted by strike.
But this table shows me the best ten, regardless of expiration or strike.

[36 POINT TO DELTA COLUMN]*

Delta is your approximate probability of being assigned at
expiration. A delta of 0.30 means roughly a thirty percent
chance the stock closes above your strike at expiration, for a covered call. 
Lower delta means you keep the stock more often — 
you give up some premium, but there's less chance the stock will
rise above your strike, and you won't lose out on as much
underlying stock appreciation if it gets called away.

[37 POINT TO ANN% COLUMN]*

Ann% is the annualized yield on the premium you'd collect —
for calls, relative to the stock's current price.  It's a good
measure of how much income you'd make by selling the call,
and should move the opposite direction of delta.

For puts, Annualized percent is relative to the strike, which is the capital
you'd be putting at risk. This metric lets you compare options across
different expirations on the same income footing.

---

## A QUICK ASIDE: PERCENTAGE POINTS VS. PERCENT (2:30–3:15)

[40 IV+pp SLIDE WITH THE EXAMPLE NUMBERS]*

Let's talk about IV+PP, the key metric to understand.

This is wonky but an important concept to understand when using
this tool. The IV+pp column you keep seeing — pp stands for
**percentage points**, and that is deliberately different from
percent. They are not the same thing.

Here's why it matters. Implied volatility itself is already a
percentage — forty-five percent, fifty percent, and so on. So
when you talk about the gap between two of those numbers, you
have to be careful. Going from forty-five percent to
forty-eight percent is plus three
**percentage points**. Calling that plus three
**percent** would be wrong — the relative percent change there
is more like plus six-point-seven percent.

Two practical takeaways from that.

**One.** When you read a plus-five-pp signal in the table or
see a green dot floating five units above the fitted curve,
that's an absolute IV gap. Same unit on every strike and every
expiration, which is what makes the ranking comparable across
the whole chain.

**Two.** Do not confuse IV+pp with a return. A plus-five-pp
option is not paying you five percent. The Ann% column on the
table is your actual annualized yield on the premium collected or paid
— that's where you check the real return on capital.

So: pp is the language of volatility differences. Once you've
got that distinction, then you'll have a better understanding of the tool.

---

## Other controls on form

[50 filters]

Let's see what other filters we have to play with...

If you have an option expiring in a few days or months and want to roll it,
check the "Rolling an existing position?" radio.

(CHECK THE ROLL BOX — FIELDS APPEAR)

Fields appear for your current strike and expiration. Fill them
in, scan, and a Net Credit column appears in the table — the
net credit you'd receive after paying to close the old position.
Positive means you'd collect cash on the roll. Negative is a
debit.

[51 Direction]
(Switch back to Find new options)

Flip the Direction radio from Sell to Buy. Same
surface fit, but now the ranking inverts — you're looking for
the most underpriced options, the dots farthest *below* the
curve. In buy mode the color scale flips — green now means
cheap relative to the surface, so the green dots below the
curve are the candidates.

[52 Option Type, DTE]

You can view calls, puts, or both with the Option Type radio button.

(CHANGE MIN DTE TO 30, MAX DTE TO 90, SCAN)

Min and Max DTE lets you change the range for Days to Expiration.
Leaving Max DTE as 0 will not set a max DTE.

[53 DELTA SLIDER]

Here's the delta range slider. Default is 0.10 to 0.75 —
a wide range that covers everything from conservative out-of-the-
money strikes to some in-the-money ones. Set this to your preference.

(DRAG SLIDER TO 0.25–0.40, CLICK SCAN)

You could narrow it to 0.25 to 0.40 — enough premium to be
worthwhile, enough strike distance to not get called away every
time the stock moves.  But you'll see fewer strikes and options
on the chart and in the tables.
with all with delta confined in that tighter range.

[54 Top N, Scan and Dropdown]

The Top N value lets you control how many candidates you want to see
in the bottom Top Candidate table accross all expirations.


(Scan and Dropdown)

Again, after Scanning, you can use this dropdown to switch between the
available expirations, and view their chart and tables.
The number of Top N picks for each Expriation is in parenthesis

---

## PORTFOLIO SCAN (7:15–8:30)

[60 PORTFOLIO TAB]

Here's a nice feature that could save you some time: the Portfolio Tab
You can upload your entire brokerage transaction log, CSV format  —
it supports Schwab, Robinhood, Fidelity, or Merrill,
   but you have to tell it which format.

(Scan Schwab 556)
The tool detects every open position in the log, and scans each for good options.

This isn't actually uploading your transaction log anywhere,
It all stays local.

---

## WHAT YOU NEED — SETUP (10:30–12:00)

[70 Setup 1-2 slide]

Now Let's summarize how to run this yourself.
This is all explained in detail in the Option Scanner Readme.


**Step 1 Get Code from Github

Go to the GitHub repository linked in the description.
Either download the zip or clone it.

```
git clone https://github.com/medloh/stockpile.git
cd stockpile
```

You'll need Git installed if you want to clone — git-scm.com has installers for
Windows and Mac.  Or you can just download it.


**Step 2 — Install Python.**

You'll need Python 3.12 or newer. Go to python.org, download
the installer for your platform. On Windows, check the box that
says "Add Python to PATH" during installation — that's the one
people miss.


[71 Setup 3-4 Slide]

Install UV
*SHOW TERMINAL*

**Step 3 — Install uv.**

This project uses uv, which is a fast Python package manager.
One command installs it:

On Mac or Linux:
```
curl -LsSf https://astral.sh/uv/install.sh | sh
```

On Windows, open PowerShell and run:
```
powershell -ExecutionPolicy Bypass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

If you really don't want to install uv, you can use plain pip
instead — but uv is much faster and handles the workspace
structure this project uses.

[Get Deps]
*[SHOW TERMINAL — RUN uv sync]*

**Step 4 — Install dependencies.**

From the stockpile folder:

```
uv sync
```

This installs everything — yfinance, numpy, streamlit, tabulate,
all of it. Takes about thirty seconds the first time.


[72 Run it]
SHOW TERMINAL — RUN THE WEB UI COMMAND

**Step 5 — Start the web app.**

From the stockpile folder, one command:

```
uv run streamlit run options-scanner/run_app.py
```

That opens the app in your browser at localhost:8501. From here
on, you don't need the terminal — type a ticker, hit Scan.


The README in the options-scanner folder has the full setup instructions.
Everything in this video is documented there.

**One important thing.**  If you use the portfolio scanner, it stays on
your machine. It never leaves and Anthropic server sees it.

-----

## HOW I BUILT THIS — AND HOW LONG IT TOOK (9:00–10:30)

[80 CLAUDE CODE terminal startup]

Now let me show you what it actually took to build this,
because I think it might surprise you.


I built 95% of this tool — the scanner, the IV surface model, the roll
mode, the portfolio scan, the HTML reports, the Streamlit web
UI — in about 20 back-and-forth messages with Claude Code.


[81 Build prompts slide]

Here's a sample of what those conversations looked like:

> "Thinking of building a tool to look at an option chain and
  help me pick the best option to sell."
> "I want to target LEAPS for long-term capital gains on the
  premium. Note earnings dates."
 
Claude suggests the UI to use and builds it in a few minutes once I confirm.
 
> "How do I run it?"
 
> "Lets add a delta range filter."
> "Lets implement HTML output, buy mode, and short-dated options."
> "How about making a full portfolio scanner from broker transaction logs.
>  we can leverage the code we made for the other tools in this project.
>  Don't stop to ask me anything — just do it."

That's the gist. No architecture meetings, no tickets, no
planning documents. I described what I wanted, Claude built it,
I tested it,  reviewed, came up with new ideas, asked for changes.

A couple more days of polish and here it is.
Claude also helped tremendously with the YouTube script.

[82 SHOW GIT LOG OR FILE DIFF]*

The result: just under 2000 lines of Python across
ten source files. Option Chain fetching, IV surface fitting, earnings
detection, HTML report generation, portfolio parsing, and the Streamlit app.

95% written part-time in a couple evenings, Two nights.
Then some polish this weekend while working on this YouTube episode.

[83 Before After Claude Slide]

I'm going to make a claim here that I can't prove precisely,
but I believe is in the right ballpark: this took roughly
one 20th the effort it would have taken me BC - before Claude.
If I even considered it before, I would have quickly given up.

Think about what "before Claude" looks like for a project
like this. You'd spend an evening just researching the right
library for IV surface fitting, reading documentation, looking
at Stack Overflow answers that are three years old and half
wrong. Another evening getting the option chain data into a
usable shape. A weekend on the HTML report. Another session
on the Streamlit UI. You'd hit walls, debug things that
shouldn't be broken, context-switch back to the docs to keep them updated,
and a hundred other things

I didn't do any of that. I described what I wanted. Claude
knew what libraries to use, knew the right mathematical
approach, wrote the boilerplate, and kept all the context
in its head across sessions. My effort was deciding what I
wanted — not figuring out how to build it.  I did occasionally 
coach Claude into better refactorings, and he made a few strange
decisions about things to display.  But easily fixed with iterations.
He messed up just enough so I still can feel useful as a developer,
rather than just an idea man.

That's the shift. The bottleneck used to be implementation.
Now it's just knowing what to ask, and nudging Claude in the 
right direction.

---

[90 Data Source Slide]

**One honest caveat about the data source.** Everything here
comes from Yahoo Finance, which is free and requires no account.
That's a real advantage for getting started. But Yahoo Finance
has limitations.

The implied volatility numbers it returns are sometimes stale
— especially on thinly traded strikes where the last trade was
hours or days ago. The Greeks aren't provided at all; delta
here is calculated from Black-Scholes using Yahoo's IV, which
means if the IV is stale, the delta is too. And for LEAPS
specifically, wide bid-ask spreads and low volume mean some of
the IV readings are noise rather than signal.

None of this breaks the tool — it still surfaces real
patterns — but you should treat the output as a starting
point for further research, not a trading signal on its own.
Always verify the bid-ask spread on you broker before acting on anything
the scanner surfaces. Stale IV also tends to show up as a
single dot far from its neighbors with no obvious reason — if
something looks too good to be true on the chart, it usually is.

A natural future enhancement would be plugging in a better
data source, like the Schwab developer API — free for account
holders — that returns full option chains with real-time
quotes and proper Greeks:  That would make this significantly more accurate,
especially for the IV surface fitting.

It's on my TODO list.

## Disclaimer (read on camera or include in description)
 
[91 Show disclaimer slide]

And the fine print...

DISCLAIMER

This tool is free, open-source software provided as-is with no
warranty of any kind. There is no guarantee of accuracy,
completeness, or fitness for any purpose.

Nothing this tool produces
should be interpreted as a guarantee of any trading outcome.

This is not financial advice. Options trading involves
substantial risk of loss and is not right for every investor.
Do your own research before acting on anything this scanner
surfaces. The author is not responsible for any losses or
other damages from using this software.

## OUTRO (12:00–12:30)

*[92 Thumbnail]*

That's it, hope you find this option scanner useful.
Please leave a comment, good or bad.
Let me know how you're using it, or how I could make it better.

(configure last two episodes to show)
Take a look at my previous two episodes about other tools
in this repo, showing up now.

---

# Not part of the script, YouTube attributes:

## DESCRIPTION

Options Scanner made by Claude — Find mis-priced Options
to Sell.

This is an open-source option chain scanner I made with Claude Code.
It's a free web app that runs on your laptop, 
and that ranks every call or put by how
overpriced it is relative to a fitted volatility surface, and
shows the result on a chart so you can see the rich strikes at
a glance. Useful for selling covered calls, cash-secured puts,
and rolling existing positions, and buying options.

**What it does:**
- Browser-based UI — no terminal required to use it
- Volatility-surface chart: every option as a dot, fitted curve
  overlaid, green dots = attractive, red dots = unattractive
- Fetches the full option chain from Yahoo Finance (free,
  no API key)
- Fits a 2-D volatility surface to find options priced above
  where they should be
- Ranks by IV excess — the gap between actual and expected
  implied volatility
- Per-expiration chain view sorted by strike: row shading
  shows which strikes are rich, average, or weak at a glance
- Flags wide bid-ask spreads and low open interest with yellow
  cell highlights so you spot execution risk before acting
- Earnings dates shown in chain title with days-to-go count
- Filters by delta (default 0.10–0.75), open interest, DTE
- Roll mode: shows net credit for rolling an existing position
- Portfolio scan: drag-and-drop your brokerage CSV and scan
  every open position automatically
- CLI also available for scripting and automation

**What you need:**
- Python 3.12+
- uv (free, one-command install)
- The repo (free on GitHub, link below)
- Optional: a brokerage CSV export for the portfolio scan

**Steps covered:**
0:00 Hook — scanning NVDA in the web app
1:15 How the volatility surface chart works
2:30 Why pp, not % — a wonky but important detail
3:15 Selling covered calls — the main use case
5:15 More features: puts, rolling, buy mode, short-dated
7:15 Portfolio scan — drag in your brokerage CSV
9:00 How I built it — 22 prompts, 2 evenings, ~1900 lines
10:30 Setup — Python, uv, cloning the repo, running it

**Links:**
GitHub repo: https://github.com/medloh/stockpile
Claude Code: https://claude.ai/code
Previous episode (cost basis charts): [link]
Previous episode (Google Sheets tracker): [link]

Your brokerage data stays on your machine. This tool only
calls Yahoo Finance's public API — no accounts, no keys, no
data leaves your computer.

If you hit a snag, drop a comment — I check them.

#options #coveredcalls #python #claudecode #optionstrading
#thetagang #leaps #stockmarket #investing #cashsecuredputs

---

## PRODUCTION NOTES

### Before Recording
- **Commit the options-scanner work to git first.** The "how
  I built this" section references the git log and file count —
  you need those to be real and visible on screen. Run:
  `git add options-scanner && git commit -m "Add options-scanner tool"`
  Then use `git log --oneline` and `git diff HEAD~1 --stat` to
  show the scope of what was added in one commit.
- **Have the Streamlit app running before you hit record.** The
  hook depends on it being up the moment you switch to the
  browser. Startup takes 3–4 seconds — don't make viewers wait.
- **Pick a ticker with a visible spread on the chart.** The
  whole hook fails if every dot is sitting on the curve. Before
  recording, scan NVDA, AAPL, TSLA, and 2–3 others — pick the
  one with the most clearly green/red dots away from the line.
  A volatile day or a day before earnings helps.
- If no ticker has a strong spread that day, acknowledge it on
  camera — "today's chains are uniformly priced, which itself
  is useful information; here's what it looks like when there
  IS a signal" — then show a screenshot from a previous day.
- For the chart hook, zoom the browser to ~125% so the dots
  read clearly on a phone screen.
- Pre-generate the HTML report so you can cut straight to it
  without waiting for the download.
- Have a real brokerage CSV ready for the portfolio scan demo
  — redact or blur any sensitive position sizes if needed.
- For the "how I built this" section, decide whether to show
  the actual Claude Code conversation transcript scrolling, or
  just read the prompt summary bullets on screen. The transcript
  is more compelling but harder to read on camera.

### Sections that need strong pacing
- Hook: keep it under 75 seconds — the chart speaks for itself,
  don't over-narrate. The reveal moment is the chart appearing
  with green dots above the curve; let it land.
- Setup section: this will be the hardest for non-technical
  viewers — go slowly, show every keystroke, mention that
  the README has written instructions they can follow at
  their own pace. The payoff is the web app opening — make
  sure that moment is on screen.

### Before Publishing
- Add chapters (timestamps in description)
- Thumbnail set before publishing
- First two lines of description are visible before "show
  more" — make sure they're compelling
- Add cards at 40% and 70% of runtime pointing to the
  Google Sheets and cost basis chart episodes

### After Publishing
- Share to r/thetagang, r/options, r/learnpython,
  r/investing — lead with the scanner output, not the setup
- Pin a comment with the repo link and a prompt:
  "What other signals would make this more useful?"
- Reply to every comment in the first 48 hours
- Add this video to the exit screens of the previous two
  episodes

### Exit Screens
Add to exit screen of:
- Cost basis charts episode
- Google Sheets tracker episode

---


