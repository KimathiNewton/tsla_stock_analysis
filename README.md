This project delves into the analysis and prediction of Tesla's stock market performance. By leveraging historical stock data, the goal is to gain insights into Tesla's price movements, volatility, and potential future behavior. The analysis integrates Exploratory Data Analysis (EDA), data visualization, and predictive modeling techniques.



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
The volume fluctuates significantly over time, with periods of high volume followed by periods of low volume. This suggests that there are periods of high investor interest and trading activity, interspersed with periods of lower interest.
Overall, there appears to be an increasing trend in volume over the years. This could indicate growing investor interest and market participation in Tesla stock.

Now let look at the closing prices over the years:
![Closing prices](Images/closing.png)
The chart shows the adjusted closing price of Tesla stock over time, starting from around 2010 to the present.
As from the year 2020, closing price trend is strongly upward, indicating a significant increase in Tesla's stock price.



We now look at the Growth distribution:
![Growth](Images/growth.png)
The slightly positive mean suggests that Tesla's stock price has been trending upward over time. This could be due to the company's strong growth prospects, innovative products, and positive market sentiment.
There is a wide range of daily growth rates indicates that Tesla's stock price is subject to significant fluctuations. This could be due to news events, product launches, earnings reports, and market-wide sentiment.
The graph shows right-skewness which suggests that there is a higher likelihood of larger upward movements in Tesla's stock price compared to larger downward movements. This could be attractive to investors who are seeking high-growth potential.

## Risk Analysis
There are many ways we can quantify risk, one of the most basic ways using the information we've gathered on daily percentage returns is by comparing the expected return with the standard deviation of the daily returns.

The graph below shows the distribution of daily returns:
![Returns](Images/daily_returns.png)


## Value at Risk using the Monte Carlo method
Using the Monte Carlo to run many trials with random market conditions, then we'll calculate portfolio losses for each trial. After this, we'll use the aggregation of all these simulations to establish how risky the stock is.

Let's start with a brief explanation of what we're going to do:
Stock prices follow a Markov process (random walk) consistent with the weak form of the Efficient Market Hypothesis (EMH), where future prices are independent of past movements.
This means that the stock price follows a random walk and is consistent with (at the very least) the weak form of the efficient market hypothesis (EMH) - past price information is already incorporated and the next price movement is "conditionally independent" of past price movements.

This means that the past information on the price of a stock is independent of where the stock price will be in the future, basically meaning, you can't perfectly predict the future solely based on the previous price of a stock.

The equation for geometric Browninan motion is given by the following equation: GBM Equation
dS=μSdt+σSdϵ
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

We create a histogram of the end results for a much larger run.

![Histogram for the simulation](Images/hist.png)

The histogram shows the distribution of final stock prices after 365 days across all simulation runs. The prices are mostly clustered between 1.05 and 1.25, with a peak around 1.15–1.20. This suggests that the stock has a high probability of remaining close to its starting price, with some potential upside (beyond 1.25) and a small chance of downside (below 1.05).
Now we have looked at the 1% empirical quantile of the final price distribution to estimate the Value at Risk for the Google stock, which looks to be 0.09 dollar for every investment of 1.19 dollar (the price of one inital Tesla stock).

This means for every initial stock you purchase, you are putting about $ 0.09 at risk 99% of the time from our Monte Carlo Simulation.