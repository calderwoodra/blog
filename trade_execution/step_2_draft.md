# DRAFT TITLE: Automating complex portfolio management

How to write a draft:
- In the drafting step, get it down on paper – not elegantly, not perfectly, 
  just get it down on paper so you no longer have to hold it all in your brain!
- Don't worry about grammer, spelling, etc
- get to the point. get to the point. get to the point.
- state main point before giving the reasoning that leads to it
- put the main point of each paragraph in the first sentence
- KISS, clear and simple language

Supporting material:
- Why am I writing this?
  - I'm writing this because building a functioning rebalancer was effing hard
- Who is the audience
  - Alpaca users, Hacker News, Finance Heads
- What does the reader know/expect/want
  - They are technical, know finance things, want to learn more/ read about others approaches

## Define the problem
At Quantbase, we offer high-volatility, high-return funds retail investors can invest in. I recently wrote 
a bunch of code to manage user investments into these self-rebalancing funds. What I thought
at first would be a fairly straightforward problem, turned out to be riddled with edge-cases and complex
logic, so I figured I would write up what problems I came across, how I solved them and what I learned.

The scope of this post is to specifically cover trade execution as it relates to both automated and user 
initiated events. This post won't cover how funds are developed, what signals we use or how we consume them.
But we have other posts on that if you're interested [here](https://quantbase.substack.com).

## High-Level Explanation
Like I mentioned before, users can invest in our auto-rebalancing funds, but what that means
specifically is that clients pick a fund, denote a **dollar amount** to go into that fund, 
then we deploy their money into a basket of assets. This is slightly different than what someone 
like Vanguard does, which is offer ETFs which clients buy _shares_ of, which then creates a single
large managed pool of cash. It's very hard/costly to set up an ETF, but much easier to manage client
investments.

There are essentially 3 types of actions that can happen:
- Client initiated $ deposits
- Client initiated $ withdrawals (partial or full)
- Automated rebalances - net $0 investment change

Client deposits are fairly straight-forward to understand:
- Check the current target composition of the fund
- For each asset in the fund composition, divvy their deposit up according to its proportion of the whole fund
- place buy orders for each asset

Sell orders are also easy to understand:
- Calculate the users current fund composition based on the assets they're holding
- Check the target composition of the fund
- Calculate the difference between the current and target composition with an assumed % reduction
- place sell orders for each asset

Rebalances are a little more complex:
- Calculate the users current fund composition based on the assets they're holding
- Check the target composition of the fund
- Calculate the difference between the current and target composition. Differences can be bidirectional
here, so positions can increase, decrease or stay the same.
- Place sell orders to all assets decreasing in value
- Wait for those positions to fill and compute the sum cash of the sales
- Compute the value of the users fund investment based on  
- 


### How can I organize it?
- Define the problem
  - What is the problem
    - we offer funds, users can invest $ amounts into those funds
    - They can deposit money into a fund, withdraw from a fund, and the fund will self-manage/rebalance itself
    - The scope of this article is about how to execute the buy/sell orders, not about consuming or using the signals  
  - Why it's important
    - It's important because a fund that doesn't rebalance properly/in a timely manner, will lose money 
- Explain the solution
  - High level
    - purpose: give a gist, let folks dig deeper if they're interested
    - content:
      - types of trades
      - call out the edge cases 
  - Details
    - purpose: for the nitty gritty folks
    - content:
      - how to execute them
      - how to handle the edge cases within each
- Closing remarks
  - summary
  - anything not covered
    - stock splits
    - delisted stocks

### What are the format and style requirements
long form, SubStack or Github page

## Drafting
getting it on paper once

