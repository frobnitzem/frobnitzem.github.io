---
layout: post
title:  "Consumption Function Analysis"
author: David M. Rogers
tags:
- consumption function
- microeconomics
- operations research
---

Before trying to optimize a portfolio, it seems like
we should take a moment to figure out how to deal
with risk tolerance.  Closer to retirement, it is well-known
that you should switch out of high-risk stocks and into low-risk bonds
to ensure there will be enough to spend without
having to go back to work.
Of course, in the long term spending and savings are
linked so it's also possible to avoid losses by spending less.
How do we actually settle on a spending and asset allocation
strategy?

<p>
Optimal control theory provides one way to solve this problem.
In a given year, \(t\), say you have known income, \( I_t \),
a starting amount of assets, \(W_t\), and
some fixed minimum costs of living, \(C^0_t\).
You now have to decide how much total spending, \(C_t\),
you can afford.  Whatever is unspent will be invested
and become \(W_{t+1}\) next year.
For simplicity, assume it grows with fixed rate \(R_t\).
</p>

<p>
 $$ W_{t+1} = e^{R_t} \, (W_{t} + I_t - C_t) $$
</p>

The catch is that each year you have to trade off future
spending for present spending.  If we measure discretionary
spending by the utility function, \\\(u(C) = \\log(C)\\\),
then we are trying to optimize total utility
over years 0 through T,

<p>
 $$ V(\{C_t\}, \mu) = \sum_{t=0}^T u(C_t - C^0_t) + \mu W_T.$$
</p>

This objective function contains a Lagrange multiplier,
\\\(\mu\\\) to enforce a fixed final wealth, \\\(W_T = 0\\\).
In a continuous case, we can integrate
<p>
 $$ dW/dt = R W(t) + I(t) - C(t) ,$$

to give

 $$ W(t) = e^{Rt} \left( W(0) + \int_0^t d\tau e^{-R\tau}(I(\tau) - C(\tau)) \right) .$$
</p>

The optimal spending profile is then,

<p>
 $$ C_t = C^0_t + \mu^{-1} e^{R(t-T)} .$$
</p>

It says that discretionary spending should increase
exponentially at the market rate!
The constant, \\\(\mu\\\), can be worked out from \\\( W(T) \\\).

It turns out this type of analysis is standard in economics,
where it is known as the 'perfect foresight' model.
It has several known issues.
First, if \\\(W(t)\\\) dips below zero, it means that
we have to borrow at rate \\\(R\\\), which is not usually
possible.  Second, it does not take into account market
risk, so we should do something statistical to fix that.

Third, and possibly most importantly for ordinary
folks, future income is not known exactly.
Losses in future income are also hard to insure.
The monetarist [Milton Friedman][cons1] argued that uncertainty
in future incomes should change spending vs. saving preferences
significantly in [A Theory of the Consumption Function][cons].
There's a nice paper from [Christopher Carroll][carroll]
that shows how this would work in practice.
I'll write more about it in the next post.

 [cons1]: https://www.investopedia.com/terms/m/milton-friedman.asp
 [cons]: https://press.princeton.edu/titles/978.html
 [carroll]: http://www.nber.org/papers/w8387 "Christopher D. Carroll, 'A Theory of the Consumption Function, With and Without Liquidity Constraints,' NBER Working paper 8387, 2001."

