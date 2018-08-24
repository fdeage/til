# P and NP problems

## Description

- P is the class of problems that have efficient polynomial-time solutions
- NP is the class of problems that have efficient polynomial time *verifications* of correct solutions

I'll give you an example: multiplying two numbers together is in P. If you increase the number of digits in my input, I have to do more but not that much more work (strictly speaking, about n\^1.425 work), where n is the number of digits in the larger input. n\^1.425 is a polynomial, and thus this entire problem is "in polynomial time", the proof is by construction.

Here's an example of a problem that is in NP: factoring a number. We don't have a constructive algorithm that will give us a number's factors in polynomial time (it is an open question if there is one), but if a genie were to present you with the factors, you can very easily verify if the purported factors are indeed correct, by multiplication. Thus, factoring is in NP.

## NP-completeness

Now there are some problems in NP that are "as hard" as all other problems in NP, because a solution can be used to bootstrap solutions to all other NP problems. The classic example is the traveling salesman problem. If you had a genie that could always solve traveling salesman problems, you can easily translate any other NP problem (such as factoring) into an instance of the traveling salesman problem, give it to your genie, take the resulting solution, and use that to get the factors. We thus call traveling salesman "NP complete". There are a surprisingly large number of practical problems that are NP complete, and identifying a wide set of them basically kicked off this field.

## P=NP?

The question now comes around: Are NP-complete problems solvable in polynomial time? This may seem like a surprising question, because the instinctive answer is "Of course not! Why on Earth would you think it would be so?" But a proof has been surprisingly elusive, and meanwhile, we've built more and more systems that implicitly rely on P!=NP (like crypto), and its various downstream consequences, so it would be nice to know for sure.

cf. [1971 Karp's 21 NP-complete problems](https://en.wikipedia.org/wiki/Karp%27s_21_NP-complete_problems)
