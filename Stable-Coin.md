# Another idea for a stable coin
Cryptocurrencies like Bitcoin and Ethereum will not be widly adopted 
until they fulfill these criteria for the average customer and employee: 
- He must get paid and be able to pay with this cryptocurrency 
- His accounts value shouldn't decrease or increase unexpectedly 

Both of these current popular cryptocurrencies don't achieve this, 
because no retailer accepts money that might lose or win value 
by 20 % in a single day. And no employee wants a wage that 
changes constantly during the month. 
**Short: for wide-spread 
adoption cryptocurrencies need to be stable!**

## How are fiat currencies stable? 
The most important factor for the stability of a currency like the USD is the 
size of it's market, the larger and more diverse the market, the less likely rapid fluctuation 
in value is.

But cryptocurrencies have a small and often specialized market, if you compare it to the market of the USD, 
Euro or any other currency that is adopted by a whole country.

So if I want a stable coin I need a large market, but to get a large market, I need to be stable? 
That doesn't work ( only if a country would adopt that currency )! 
We need a way of keeping a currency stable in the time between wide-spread adoption and the beginning.
What methods for keeping coins stable are there? 

## (other) ways to stabilize 
There are currently three methods for creating stable coins, 
all of which have the disadvantage of depending on other factors 
than the adoption of the coin to survive, some have to be redeemable 
by another fiat or cryptocurrency and still others depend on people 
loaning a mint money to keep the price stable, 
all these schemes can fail, either because 
the redeemable currency crashes or the coin runs out 
of capital or because nobody loans the mint anymore money. 
In any case; the currencies price can fluctuate freely. 
I want a currency to be stable, because it is used often 
and not because of any other factor, after all we know 
that this is the way to mainstream adoption and thus to even more stable prices. 
( For more information about these other methods of keeping a coin stable, [read this article](https://hackernoon.com/stablecoins-designing-a-price-stable-cryptocurrency-6bf24e2689e5)) 

## What is my idea? 
I want to make my own proposal, this is only an idea, 
I do not have a proof of concept and there may be flaws in my reasoning, 
please forgive me and write a response explaining my flaws. 

My stable coin will have two components.

The first component stores the balance of each account 
and implements a transfer function for 
one address to transfer coins to another,
this will get important later. 

The second component is a mint that operates as a money print,
all coins in the currency originated in the mint and the mint always prints new coins and sells them
at a constant price, the value that is desired for the coin, 
thus keeping the price at an upper limit. 

## For example 
If you pegged your token to the USD, 
meaning one of your tokens = 1 USD, 
the mint would always sell new tokens 
of yours for 1 USD each. 

Nobody could thus sell coins at 2 USD, 
because the potential buyer would just 
go to the mint and buy the cheaper coin. 
The seller would eventually have to go 
down to 1 USD or **less** to sell his coin 
at all.

Here we run into the second problem,
what if the example coin is sold for less than 1 USD?
The mint wouldn't anymore sell any coins and the price 
of the coin wouldn't anymore be stable. 
How do you increase the price again? 
You decrease the number of coins available!

In a limited capacity the mint could counteract a falling price 
with the money it earned selling new coins, 
but what if the mint's reserves are dry?  

Here I want to go back to the transfer function from earlier, 
with it's help I want to increase and decreae the total pool of coins, if necessary.
```solidity
// Exchange rate to another currency, that is desired to keep the token stable
uint desired_value = 1; 
function transfer(address payable recv,uint amount) public {
  // Get exchange rate between this token and another currency
  uint exchange_rate = get_exchange_rate();
  require(balance[msg.sender] - amount >= 0);
  balance[msg.sender] -= amount;
  balance[recv] += amount*(exchange_rate/desired_value);
} 
```
This could be an implementation of the transfer function. 
As you can see it is a usual transfer method for any token, 
with a few exceptions:

The variable `desired_value` is the the exchange rate
with another currency, if you'd peg your token to
the USD and say that 1 Token = 1 USD, you set
the value of `desired_value` to `1` or `100`,
depending on how high your decimal percision
should be.

Then in the `transfer`-function the function
first gets the current exchange rate, in our
example that would be the exchange rate USD to Token.
This is later used once it is checked wheter the
transaction is valid and `amount` is subtracted
from the caller of `transfer`.

Here, in the last line of the `transfer` function,
the magic ( I hope ) happens.
Because the receiver doesn't receive a the same amount of
tokens the sender sent him, but rather he gets the amount
multiplied by the exchange rate with the compared currency.
What I want to achive with this is best explained with an
example.

## One transaction 
Lets say that  A wants to send B 500 of your tokens,
that you pegged to the USD, meaning 1 Token = 1 USD.
Now at the time of the transaction thee exchange rate
between USD and your token = 0.5 USD.
How much would be receive from the 500 Tokens that A send?
500 * 0.5 = 250 Tokens.
Why did I do that?
To decrease the supply and increase the demand and thus the price!
But why did I need to steal from B, who should have received 500 Tokens,
but only received 250?
Well, but would he eventually lose value?
He wouldn't, because once the value increased and
stablilized at 1 USD again, he would have the same
value as A had before the transaction.
( A has 500 Tokens = 250 USD, B will have 250 Tokens = 250 USD)
And because the network should be in regular use,
the price should go back to 1 USD soon,
simply because the coin became so scares
that nobody could have an incentive to
sell the coin at a lower price and nobody
has an incentive to buy the coin at a higher
price anyway.
Every users of the network has to trust that
the value will eventually restore to 1 USD
and they will thus accept this "stealing"
in the short term.

# The Cons

## Over ambitiouse creators
Of course this approach has some seriouse risks
too, what doesn't?
One of the major risks is that the creators of
the coin over estimated the value of the coin
and that the coin is just not worth what they
desired it to be. 
Than, if nobody wants to buy the currency,
everybody who owns the currency will be 
imprisoned with his money in there, because
they can't get it back.

I mostly used the word desired,
not pegged here, because that is essentially
what this whole thing is, a scheme to circumvent 
the open market and its estimation of the price.
And in every cryptocurrency that this is implemented
I would put a check in that disables this whole
scheme, once a certain number of transactions are
made with the coin every day for a certain time.
I would recommand to do this with all stable coins,
to leave it for the open market at some point and
only interfere with the price if it falls to far.

## Depending on an outside source
As you may have noticed this scheme
depends on the accuracy of the exchange 
rate it gets from the outside world, because
if that exchange rate is faulty, many people
will lose their money, so to keep this from
happening you have to come up with a secure
way to get the exchange rate into the blockchain.


# Conclusion
I think this scheme could be a method to stabilize
a currency in the time before the market is large
enough to stabilize it on its own.
But it also depends on the trust of those people,
that invest first, they won't get any later 
advantage from buying in first, like they had
with BTC or ETH, but they might be able to shape
a totaly new, stable and secure market that only
depends on the use of itself to stay stable.
And of course, before anybody will put his life
savings or anything important on this blockchain,
it must proof to him that it is trust worthy.
I know  that this explanation can't do so.

If you have an opinion on this matter, please
let me know.
 
Joris Gutjahr
