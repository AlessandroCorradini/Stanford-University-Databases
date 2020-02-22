# OLAP Quiz

Each multiple-choice quiz problem is based on a "root question," from which the system generates different correct and incorrect choices each time you take the quiz. Thus, you can test yourself on the same material multiple times. We strongly urge you to continue testing on each topic until you complete the quiz with a perfect score at least once. Simply click the "Reset" button at the bottom of the page for a new variant of the quiz.

After submitting your selections, the system will score your quiz, and for incorrect answers will provide an "explanation" (sometimes for correct ones too). These explanations should help you get the right answer the next time around. To prevent rapid-fire guessing, the system enforces a minimum of 10 minutes between each submission of solutions.

## Q1

Consider a fact table Sales(saleID, itemID, color, size, qty, unitPrice), and the following three queries:

```
Q1: Select itemID, color, size, Sum(qty*unitPrice)
    From Sales
    Group By itemID, color, size
Q2: Select itemID, size, Sum(qty*unitPrice)
    From Sales
    Group By itemID, size
Q3: Select itemID, size, Sum(qty*unitPrice)
    From Sales
    Where size < 10
    Group By itemID, size 
```

Depending on the order in which we execute two of these queries, the pair of actions may be viewed as an example of roll-up, drill-down or slicing. Which of the following statements is correct?

- Going from Q3 to Q2 is an example of roll-up.
- Going from Q1 to Q2 is an example of slicing.
- **Going from Q1 to Q2 is an example of roll-up.**
- Going from Q3 to Q2 is an example of slicing.

# Q2

Consider a fact table Facts(D1,D2,D3,x), and the following three queries:

```
Q1: Select D1,D2,D3,Sum(x)
    From Facts
    Group By D1,D2,D3
Q2: Select D1,D2,D3,Sum(x)
    From Facts
    Group By D1,D2,D3 WITH CUBE
Q3: Select D1,D2,D3,Sum(x)
    From Facts
    Group By D1,D2,D3 WITH ROLLUP
```

Suppose attributes D1, D2, and D3 have n1, n2, and n3 different values respectively, and assume that each possible combination of values appears at least once in table Facts. The number of tuples in the result of each of the three queries above can be specified as an arithmetic formula involving n1, n2, and n3. Pick the one tuple (a,b,c,d,e,f) in the list below such that when n1=a, n2=b, and n3=c, then the result sizes of queries Q1, Q2, and Q3 are d, e, and f respectively. (Hint: It may be helpful to first write formulas describing how d, e, and f depend on a, b, and c. Then find the answer that satisfies your formulas.)

- (5, 10, 10, 500, 1000, 550)
- **(4, 7, 3, 84, 160, 117)**
- (2, 2, 2, 8, 27, 14)
- (2, 2, 2, 8, 64, 15)