---
title: "The Power of 10: Rules for Developing Safety-Critical Code"
date: 2021-08-30T13:47:06+07:00
description: The rules are intended to eliminate certain C coding practices which make code difficult to review or statically analyze. 
tags: [informational, tips]
featured_image: https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse3.mm.bing.net%2Fth%3Fid%3DOIP.crAkB9ZSlFg8hgUS2pcjLwHaDd%26pid%3DApi&f=1
categories: Programming
comment : false
---

The Power of 10 Rules were created in 2006 by [Gerard J. Holzmann](https://en.wikipedia.org/wiki/Gerard_J._Holzmann) of the [NASA/JPL](https://en.wikipedia.org/wiki/JPL) Laboratory for Reliable Software.
The rules are intended to eliminate certain C coding practices which make code difficult to review or statically analyze.
These rules are a complement to the [MISRA C](https://en.wikipedia.org/wiki/MISRA_C) guidelines and have been incorporated into the greater set of JPL [coding standards](https://en.wikipedia.org/wiki/Coding_conventions).

# Rules
the ten rules are:

1. Avoid complex flow constructs, such as [goto](https://en.wikipedia.org/wiki/Goto) and [recursion](https://en.wikipedia.org/wiki/Recursion_(computer_science)).
2. All loops must have fixed bounds. This prevents runaway code.
3. Avoid [heap memory allocation](https://en.wikipedia.org/wiki/Memory_management#DYNAMIC).
4. Restrict functions to a single printed page.
5. Use a minimum of two [runtime assertions](https://en.wikipedia.org/wiki/Assertion_(software_development)#Assertions_for_run-time_checking) per function.
6. Restrict the scope of data to the smallest possible.
7. Check the return value of all non-void functions, or cast to void to indicate the return value is useless.
8. Use the [preprocessor](https://en.wikipedia.org/wiki/Preprocessor) sparingly.
9. Limit pointer use to a single [dereference](https://en.wikipedia.org/wiki/Dereference_operator), and do not use [function pointers](https://en.wikipedia.org/wiki/Function_pointer).
10. Compile with all possible warnings active; all warnings should then be addressed before release of the software.

# References
1. [Wikipedia page](https://en.wikipedia.org/wiki/The_Power_of_10:_Rules_for_Developing_Safety-Critical_Code)
2. [The Power of 10: Rules for Developing Safety-Critical Code](http://web.eecs.umich.edu/~imarkov/10rules.pdf)
