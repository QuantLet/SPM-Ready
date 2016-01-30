
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SPMadditive** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SPMadditive

Published in : Nonparametric and Semiparametric Models

Description : Computes an additive fit.

Keywords : nonparametric, regression, plot, graphical representation

See also : SPMadditivebostonh, SPMadditivecorrelated, SPMgamkredit

Author : Marlene Müller

Submitted : Mon, August 01 2011 by Awdesch Melzer

Example : Plot of the regression and data points.

```

![Picture1](SPMadditive-1.png)


```r

# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# install and load packages
libraries = c("gam")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)

n = 75
a = 2.5
x = matrix(runif(n * 4, min = -a, max = a), n, 4)

x1 = x[, 1]
x2 = x[, 2]
x3 = x[, 3]
x4 = x[, 4]

g1 = -2 * sin(x1)
g2 = x2^2 - (2 * a)^2/12
g3 = x3
g4 = exp(-x4) - (exp(a) - exp(-a))/(2 * a)
y  = g1 + g2 + g3 + g4 + rnorm(n)

print(c(mean(g1), mean(g2), mean(g3), mean(g4)))

am = gam(y ~ s(x1) + s(x2) + s(x3) + s(x4), family = gaussian)
print(summary(am))

b = coef(am)

par(mfrow = c(2, 2))

o = order(x1)
plot(x1[o], g1[o], type = "l", main = "g1")
lines(x1[o], x1[o] * b[2] + am$smooth[o, 1], col = "blue", lwd = 2)
rug(x1)

o = order(x2)
plot(x2[o], g2[o], type = "l", main = "g2")
lines(x2[o], x2[o] * b[3] + am$smooth[o, 2], col = "blue", lwd = 2)
rug(x2)

o = order(x3)
plot(x3[o], g3[o], type = "l", main = "g3")
lines(x3[o], x3[o] * b[4] + am$smooth[o, 3], col = "blue", lwd = 2)
rug(x3)

o = order(x4)
plot(x4[o], g4[o], type = "l", main = "g4")
lines(x4[o], x4[o] * b[5] + am$smooth[o, 4], col = "blue", lwd = 2)
rug(x4)

par(mfrow = c(1, 1))

```
