

# Another idea for a stable coin
Cryptocurrencies like Bitcoin and Ethereum will not be in wide adoption 
until they fulfill these criteria for the average customer and employee: 
- He must get paid and be able to pay with this cryptocurrency 
- His accounts value shouldn't decrease or increase unexpectedly 

Both of these current popular cryptocurrencies don't achieve this, 
because no retailer accepts money that might lose or win value 
by 20 % in a single day. Nor does the employee want a wage that 
changes constantly during the month. Short: for wide-spread 
adoption cryptocurrencies need to be stable! 

## How are fiat currencies stable? 
The most important factor for the stability of a currency like the USD is the 
size of it's market, the larger the market, the less likely rapid fluctuation 
in value is.

But cryptocurrencies have a small market, if you compare it to the market of USD, 
Euro or any other currency that is used by a whole country. 
So if we want a stable coin we need a large market, but to get a large market, we need to be stable? 
That doesn't work ( or only if a country would adopt our currency )! 
We need a way of keeping a currency stable in the time between wide-spread adoption and the initial.  
What methods for keeping coins stable are there? 
There are currently three methods for creating stable coins, 
all of which have the disadvantage of depending on other factors 
than the use of the coin to survive, some have to be redeemable 
by another fiat or cryptocurrency and still others depend on people 
lowing a mint money to keep the price stable, 
all these schemes can fail, either because 
the redeemable currency crashes or the coin runs out 
of capital or because nobody lows the mint anymore money, 
in both cases the currencies price can fluctuate freely. 
I want a currency to be stable, because it is used often 
and not because of any other factor, after all we know 
that this is the way to mainstream adoption and thus to even more stable prices. 
( For more information about these other methods of keeping a coin stable, read this article[https://hackernoon.com/stablecoins-designing-a-price-stable-cryptocurrency-6bf24e2689e5]) 
What is my idea? I want to make my own proposal, this is only an idea, 
I do not have a proof of concept and there may be flaws in my reasoning, 
please forgive me and write a response explaining my flaws. 
My stable coin will have two components, one component stores the balance of each account 
and implements a transfer function for one address to transfer coins to another,
this will get important later. The second component is a mint that operates as a money print,
all coins in the currency originated in the mint and the mint always prints new coins and sells them, 
thus keeping the price at an upper limit. The mint acts as a central bank, 
selling coins at a fixed value and from the profits made buys coins up, 
if the price is below the desired value. 
## For example 
If you pegged your token to the USD, 
meaning one of your tokens = 1 USD, 
the mint would always sell new tokens 
of yours for 1 USD each. Nobody could 
thus sell coins at, for example, 2 USD, 
because the potential buyer would just 
go to the mint and by the cheaper coin. 
The seller would eventually have to go 
down to 1 USD or less to sell his coin 
at all. Here we run into the second problem,
what if the example coin is sold for less than 1 USD?
The mint wouldn't anymore sell any coins and the price 
of the coin wouldn't anymore be stable. 
How do you increase the price again? 
You decrease the number of coins available! 
( Decrease in supply leads to increase in price).  
In a limited capacity the mint could counteract a falling price 
with the money it earned selling new coins, 
but what if the mint's reserves are dry?  

Here I want to go back to the transfer function from earlier, 
with it's help I want to increase the total pool of coins.

This could be an implementation of the transfer function. 
As you can see it is a usual transfer method for any token, 
with a few exceptions; desired_value is a variable used

An example Let's say that A wants to send B 500 STK 
(a symbol I made up that stands for Stable Token) 
and the current exchange rate of STK is 2 USD,
although the desired value is 1 USD. 
In this case B would receive 500 STK * 2 USD = 1000 STK,
this may seem like the exchange creates money out of air,
but it just also increased the amount of STKs in circulation, 
increasing supply and decreasing price until the price is only 1 USD, 
back to the desired value.
