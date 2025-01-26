---
title: Derivatives
layout: page
---

* This will become a table of contents (this text will be scraped).
{:toc}

# Notation

When I started my calculus refresher, I found myself needing to be reminded of the subtleties of the various notations... What's the difference between x dot and x prime? How do I show second derivatives, etc. When I looked into it I found four notations for derivatives in common use, each one introduced/popularized by a famous physicist or mathematician.


| Originator | First derivative   | Second derivative            | Indicates ... |
| :--        | :--:               | :--:                         | :-- |
| Newton     | $ \dot{s} $       | $ \ddot{s} $                | change in s wrt time |
| Leibniz    | $ \frac{dy}{dt} $ | $ \frac{d^{2}y}{d{t}^{2}} $ | change in y wrt t |
| Lagrange   | $ y' $            | $ y'' $                     | change in y wrt an unspecified variable |
| Euler      | $ f'(t) $         | $ f''(t) $                  | change in f wrt t |

Example equivalent first derivatives: $ \frac{dy}{dx}=y'=f'(x) $

*Notes:*
+ *Newton's Notation* - This notation is compact and although it doesn't show the independent variable, by convention it is always time
+ *Leibniz's Notation* - While this notation implies that dy/dx is a fraction that can be manipulated by the rules of algebra, traditional Real Analysis gives it no special algebraic meaning and d/dx is simply an operator. That said, manipulation of dy and dx using the rules of algebra is commonly done by physicists and this has been put on strong mathematical footing (axiomatic) using the theory of Infinitesimal Calculus.
+ *Lagrange's Notation* - This notication is compact but doesn't show the independent variable
+ *Euler's Notation* - This notation is similar to Lagrange's notation but also shows the independent variable
