# Telegram Stock Analysis Bot (Dual-Mode Trader & Investor)

This project implements a Telegram bot designed to provide dual-mode analysis for stock tickers, catering to both swing traders and long-term investors. It fetches historical stock data, calculates key technical indicators (like Z-Score, Mean, and Standard Deviation), and performs a simulated backtest to assess strategy viability.

## Features:

*   **Deep Data Fetching**: Utilizes `yfinance` to download up to 5 years of historical stock data, chunked year-by-year to bypass API rate limits.
*   **Dual Analysis Modes**: Offers insights tailored for:
    *   **Swing Traders**: Provides 'ENTER', 'RISKY', 'SHORT/SELL', or 'WAIT' signals based on Z-Score and backtested win rates, along with calculated stop-loss and target levels.
    *   **Long-Term Investors**: Identifies 'STRONG BUY', 'BUY', 'PAUSE BUYING', or 'HOLD/DRIP' signals, highlighting fair value, discount percentages, and accumulation zones.
*   **Backtesting Engine**: Simulates past trades to calculate real-world win rates and profit factors, informing the reliability of swing trading signals.
*   **Smart Ticker Handling**: Automatically appends `.JK` for Indonesian stocks if the initial search is empty.
*   **Currency Detection**: Identifies whether a stock is denominated in USD ($) or IDR (Rp) and formats prices accordingly.
*   **Meme Integration**: Sends relevant stock-themed memes (BUY, SELL, WAIT) along with the analysis report for engagement.
*   **Telegram Bot Interface**: Built with `python-telegram-bot` for easy interaction via `/analyze <TICKER>` command.

## How it Works:

1.  **User Input**: A user sends the `/analyze <TICKER>` command to the bot.
2.  **Data Retrieval**: The bot fetches 5 years of historical OHLCV (Open, High, Low, Close, Volume) data for the specified ticker.
3.  **Indicator Calculation**: It computes 20-period moving average (Mean), standard deviation (StdDev), and Z-Score for the closing prices.
4.  **Backtesting**: A simplified backtest is run on historical data to determine the win rate and profit factor for a mean-reversion swing strategy.
5.  **Signal Generation**: Based on the latest Z-Score, backtest results, and calculated levels, it generates advice for both traders and investors.
6.  **Report & Meme**: The bot compiles a comprehensive markdown report and pairs it with a relevant meme, sending both back to the user.

## Technologies Used:

*   Python
*   `yfinance` for stock data
*   `pandas` for data manipulation
*   `pandas_ta` for technical analysis (though custom calculations are used here)
*   `python-telegram-bot` for bot interaction
*   `nest_asyncio` for running asyncio in environments like Colab

## Setup:

1.  **Install dependencies**: Run the following in your Colab notebook or Python environment:
    ```bash
    !pip install python-telegram-bot yfinance pandas_ta nest_asyncio mplfinance
    ```
2.  **Obtain a Telegram Bot Token**: Create a new bot via BotFather on Telegram and get your API token.
3.  **Securely Store Token**: In Google Colab, add your bot token to the secrets manager (accessible via the "🔑" icon in the left panel) and name it `botToken`.
4.  **Run the Bot**: Execute the provided Python code in your Colab notebook. The bot will start polling for commands.

## Usage:

Once the bot is running, open your Telegram app and send a message to your bot:

*   `/start`: To initiate the bot and get a welcome message.
*   `/analyze AAPL`: To get a detailed stock analysis for a given ticker (replace `AAPL` with any valid stock ticker).
