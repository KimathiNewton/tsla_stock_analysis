This project focuses on the analysis and prediction of Tesla stock market data. By utilizing historical stock data, it aims to uncover insights into Tesla's price movements, risks, and future behavior. The analysis combines Exploratory Data Analysis (EDA), data visualization, and predictive modeling techniques.

Key Questions Addressed:
* How has Tesla's stock price changed over time?
* What are the average daily returns, and how volatile are they?

## DataSet
The dataset is feteched from yfinance library. The columns include:
* Date (Index):The trading date (set as the index in the DataFrame).Each row corresponds to a single day's data.
* Open:The stock price at the start of the trading day.
* High:The highest stock price reached during the trading day.
* Low:The lowest stock price reached during the trading day.
* Close:The stock price at the end of the trading day.
* Adj Close (Adjusted Close):The closing price adjusted for corporate actions like stock splits, dividends, or rights offerings.It reflects the true value considering adjustments.
* Volume:The number of shares traded during the day. It is Used to gauge market activity and sentiment.

## Analysis

We first look at the total volume of stock being traded each day over the years

![dashboard](Images/volume.png)

Now let look at the closing prices over the years:
![Closing prices](Images/closing.png)

We now look at the Growth distribution:
![Growth](Images/growth.png)


## Risk Analysis
There are many ways we can quantify risk, one of the most basic ways using the information we've gathered on daily percentage returns is by comparing the expected return with the standard deviation of the daily returns.
## Value at Risk
Let's go ahead and define a value at risk parameter for our stocks. We can treat value at risk as the amount of money we could expect to lose (aka putting at risk) for a given confidence interval. Theres several methods we can use for estimating a value at risk. Let's go ahead and see some of them in action.

### Value at risk using the "bootstrap" method
For this method we will calculate the empirical quantiles from a histogram of daily returns.

The graph below shows the distribution of daily returns:
![Returns](Images/daily_returns.png)


## Value at Risk using the Monte Carlo method
Using the Monte Carlo to run many trials with random market conditions, then we'll calculate portfolio losses for each trial. After this, we'll use the aggregation of all these simulations to establish how risky the stock is.

Let's start with a brief explanation of what we're going to do:

Firstly, for specifying a model, We will use the geometric Brownian motion (GBM), which is technically known as a Markov process. This means that the stock price follows a random walk and is consistent with (at the very least) the weak form of the efficient market hypothesis (EMH) - past price information is already incorporated and the next price movement is "conditionally independent" of past price movements.

This means that the past information on the price of a stock is independent of where the stock price will be in the future, basically meaning, you can't perfectly predict the future solely based on the previous price of a stock.

The equation for geometric Browninan motion is given by the following equation: GBM Equation

Where, S is the stock price, μ
 is the expected return (which we calculated earlier), σ
 is the standard deviation of the returns, t is time, and ϵ
 is the random variable.

We can mulitply both sides by the stock price (S) to rearrange the formula and solve for the stock price. Now GBM Equation

Now we see that the change in the stock price is the current stock price multiplied by two terms. The first term is known as "drift", which is the average daily return multiplied by the change of time. The second term is known as "shock", for each time period the stock will "drift" and then experience a "shock" which will randomly push the stock price up or down. By simulating this series of steps of drift and shock thousands of times, we can begin to do a simulation of where we might expect the stock price to be. This is simply a way of scaling the standard deviation.

drift-shock

For more info on the Monte Carlo method for stocks, check out the following link: How to use Monte Carlo simulation with GBM

Secondly, to demonstrate a basic Monte Carlo method, we will start with just a few simulations. First we'll define the variables we'll be using.

![Monte Carlo Simulation](Images/monte.png)
