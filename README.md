Deriv
=====

Symbollic differentiation
-------------------------
The original version of this software was written in R by Andrew Clausen (clausen at econ.upenn.edu) in 2007.

Mark Reid (mark.reid at anu.edu.au) sent a patch, applied 21/2/2009.

In 2014, Andrew has passed the maintenance to Serguei Sokol (sokol at insa-toulouse.fr). Since then, the software was deeply rewritten and
completed.

Main new features include:
 - new derivative engine allowing simple syntaxe for differentiation rules;
 - automatic derivation of code with multiple assignement operators;
 - many new functions are added to rule table;
 - possible simplifications are extended to rational expressions and factorizations. Expression caching is enabled by default;
 - Deriv() is made the only entry point for all types of entries:
   * expression
   * language
   * function
   * right hand side of a formula
   * character string
   * plain unevaluated code
 - few unit tests were added to the package

Installation
------------

    > devtools::install_github("sgsokol/Deriv")

Usage
-----
In R session do:

    > library(Deriv)
    > f <- function(x, n=2) x^n+sin(n*x)     # user defined function to diffierentiate
    > (df <- Deriv(f))                       # -> c(x = n * x^(n - 1) + n * cos(n * x), n = log(x) * x^n + x * cos(n * x))
    > df(2, 3)                               # ->         x         n
                                             # -> 14.880511  7.465518
    
    > Deriv(expression(f(y, 3)), "y")        # -> expression(3 * y^2 + 3 * cos(3 * y))
    > Deriv(~ f(y, 3), "y")                  # -> 3 * y^2 + 3 * cos(3 * y)
    > y <- 2; eval(Deriv(~ f(y, 3), "y"))    # -> 14.88051

For more information and examples:

    > ?Deriv
