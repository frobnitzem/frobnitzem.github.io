---
layout: post
title:  "Stumbling Through Path Integrals"
author: David M. Rogers
tags:
- stochastic processes
- large deviations
- macroeconomics
---

It is Winter break.  Having recently finished
reading [Boyd and Vandenberghe's Book][cvxopt]
on Convex Optimization I decided to take time out
to read [Hagen Kleinert][kleinert]'s
paper on the [Lévy distribution in finance][levy].
There's a more complete description in [Ch20].
The paper shows that both the short- and long-time behavior of
returns on the S&P500 index look like a Lévy distribution,

<p>
  $$P(\Delta x|t) = \int_{-\infty}^\infty \frac{dp}{2\pi}
    e^{ip\Delta x - t H(p)},
    \quad H(p) = -|c p|^\lambda $$

  Here, \(\Delta x = x_t - x_0\) is the change in
  \(x\) over time \(t\).
</p>

This is the symmetric version of the general 'Stable' Lévy
distribution implemented in [scipy][stable].
Kleinert uses the alternate notation, \\\(\\sigma^\\lambda/2 = c^\\lambda\\\).

It's called stable because the characteristic function
is obviously \\\( H(p) \\\), and adding random variables
multiplies their characteristic functions together
(the CF of the sum is the product of the CFs).

<p>
  So, using \( dx(t) = \log(S(t+dt)/S(t)) \sim \) Lévy\((\lambda,c)\),
\(\int_0^T dx \sim\) Lévy\((\lambda,T^{1/\lambda}c)\) is
then the distribution of \(\log(S(t+T)/S(t))\)
</p>

### It's conceptually useful, and the graphs look nice, so what can we do with it?

Well, gains in the market from fancy prediction algorithms
widely use Gaussian correlations (that is, Einstein's Brownian
motion on harmonic oscillators).  Those correlations
would allow you to 'know' the direction a stock is moving
and then buy or sell to make a profit.

<p>
The Lévy distribution itself doesn't help with that directly.
Instead, it is supposed to model the tails of the distribution better.
Fits to real data show \(\lambda \sim 3/2\), and
the tails fall off as \(\Delta x^{-5/2}\).  That means
the variance is infinite and Black Swan events are present
in the model.
</p>

Using Bayesian methods to get correlations under the presence
of Lévy distributions might help, but again the correlations are
infinite, so we need to check other distributions (truncated
Lévy, gamma, etc.).

Because it models fat tails, the Lévy distribution
would be ideally suited for market risk analysis -- for
example to optimize a portfolio's returns under
a constraint that the probability of negative returns is
less than one tenth of a percent or something.
This brings us to Boyd and Vendenberghe's book.  Their
'Example 4.8' (p. 158) is a variant of the Markowitz
portfolio optimization problem.

It might also help predict changes in a portfolio
over time to help decide on a long-term allocation
strategy.  This latter problem is commonly thought
of as retirement planning, and brings us to the next post
-- which will be on optimal control theory.

 [kleinert]: http://users.physik.fu-berlin.de/~kleinert/kleinert/
 [levy]: http://users.physik.fu-berlin.de/~kleinert/kleinert/?p=articles&page=4#333 "Option Pricing from Path Integral for Non-Gaussian Fluctuations. Natural Martingale and Application to Truncated Lévy Distributions"
 [stable]: https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.levy_stable.html "Lévy Stable Distribution"
 [Ch20]: http://users.physik.fu-berlin.de/~kleinert/b5/psfiles/pthic20.pdf "Kleinert, Path Integrals, Chapter 20."
 [cvxopt]: https://web.stanford.edu/~boyd/cvxbook/

