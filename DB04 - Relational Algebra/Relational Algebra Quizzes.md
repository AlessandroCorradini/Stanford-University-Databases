# Relational Algebra Quiz


Each multiple-choice quiz problem is based on a "root question," from which the system generates different correct and incorrect choices each time you take the quiz. Thus, you can test yourself on the same material multiple times. We strongly urge you to continue testing on each topic until you complete the quiz with a perfect score at least once. Simply click the "Reset" button at the bottom of the page for a new variant of the quiz.

After submitting your selections, the system will score your quiz, and for incorrect answers will provide an "explanation" (sometimes for correct ones too). These explanations should help you get the right answer the next time around. To prevent rapid-fire guessing, the system enforces a minimum of 10 minutes between each submission of solutions.

## Q1 

Suppose relation R(A,C) has the following tuples:

A	C
3	3
6	4
2	3
3	5
7	1

and relation S(B,C,D) has the following tuples:

B	C	D
5	1	6
1	5	8
4	3	9

Compute the natural join of R and S. Which of the following tuples is in the result? Assume each tuple has schema (A,B,C,D).

- (2, 3, 1, 6)
- **(3, 1, 5, 8)**
- (3, 3, 5, 8)
- (7, 1, 5, 8)

## Q2

Suppose relation R(A,B) has the following tuples:

A	B
1	a
7	t
2	g
4	c
9	t

and relation S(B,C,D) has the following tuples:

B	C	D
c	5	6
a	7	8
t	8	9

Compute the theta-join of R and S with the condition R.B = S.B AND R.A < S.C Which of the following tuples is in the result? Assume each tuple has schema (A, R.B, S.B, C, D).

- (1, a, a, 8, 9)
- (4, c, c, 7, 8)
- (9, t, t, 8, 9)
- **(7, t, t, 8, 9)**

## Q3

Consider a relation R(A,B) with r tuples, all unique within R, and a relation S(B,C) with s tuples, all unique within S. Let t represent the number of tuples in R natural-join S. Which of the following triples of values (r,s,t) is possible?

- (2,3,8)
- (5,2,10)
- (3,3,27)
- (1,1,2)

## Q4 

Consider a relation R(A) with r tuples, all unique within R, and a relation S(A) with s tuples, all unique within S. Let t represent the number of tuples in R minus S. Which of the following triples of values (r,s,t) is possible?

- (5,3,4)
- (10,5,2)
- ( 5,2,0)
- (5,10,10)

## Q5

Suppose relation R(A,B) has the following tuples:

A	B
1	2
3	4
5	6

and relation S(B,C,D) has the following tuples:

B	C	D
2	4	6
4	6	8
4	7	9

Compute the natural join of R and S. Which of the following tuples is in the result? Assume each tuple has schema (A,B,C,D).

- (1,2,4,8)
- **(3,4,6,8)**
- (1,2,6,8)
- (5,6,7,9)

# Q6

Suppose relation R(A,B) has the following tuples:

A	B
1	2
3	4
5	6

and relation S(B,C,D) has the following tuples:

B	C	D
2	4	6
4	6	8
4	7	9

Compute the theta-join of R and S with the condition R.A < S.C AND R.B < S.D. Which of the following tuples is in the result? Assume each tuple has schema (A, R.B, S.B, C, D).

- (3,4,4,7,8)
- **(3,4,2,4,6)**
- (5,6,2,4,6)
- (3,4,5,7,9)

# Q7 

Suppose relation R(A,B,C) has the following tuples:

A	B	C
1	2	3
4	2	3
4	5	6
2	5	3
1	2	6

Compute the projection π C,B (R). Which of the following tuples is in the result?

- **(6,5)**
- (1,2,6)
- (2,5)
- (4,2,3)

# Q8

Suppose relation R(A,B,C) has the following tuples:

A	B	C
1	2	3
4	2	3
4	5	6
2	5	3
1	2	6

and relation S(A,B,C) has the following tuples:

A	B	C
2	5	3
2	5	4
4	5	6
1	2	3

Compute the union of R and S. Which of the following tuples DOES NOT appear in the result?

- **(1,5,4)**
- (2,5,3)
- (2,5,4)
- (1,2,3)

# Q9 

Suppose relation R(A,B,C) has the following tuples:

A	B	C
1	2	3
4	2	3
4	5	6
2	5	3
1	2	6

and relation S(A,B,C) has the following tuples:

A	B	C
2	5	3
2	5	4
4	5	6
1	2	3

Compute the intersection of the relations R and S. Which of the following tuples is in the result?

- (2,2,6)
- (1,2,4)
- **(1,2,3)**
- (2,5,4)

# Q10

Suppose relation R(A,B,C) has the following tuples:

A	B	C
1	2	3
4	2	3
4	5	6
2	5	3
1	2	6

and relation S(A,B,C) has the following tuples:

A	B	C
2	5	3
2	5	4
4	5	6
1	2	3

Compute (R - S) union (S - R), often called the "symmetric difference" of R and S. Which of the following tuples is in the result?

- **(2,5,4)**
- (1,2,3)
- (2,2,3)
- (4,5,3)