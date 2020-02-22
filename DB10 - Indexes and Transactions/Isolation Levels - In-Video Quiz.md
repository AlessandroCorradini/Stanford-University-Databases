# Transactions Properties - In-Video Quiz

## Q1

Consider a table R(A) containing {(1),(2)}. Suppose transaction T1 is "update R set A = 2*A" and transaction T2 is "select avg(A) from R". If transaction T2 executes using "read uncommitted", what are the possible values it returns?

- **1.5, 2, 2.5, 3**
- 1.5, 2, 3
- 1.5, 2.5, 3
- 1.5, 3

## Q2

Consider tables R(A) and S(B), both containing {(1),(2)}. Suppose transaction T1 is "update R set A = 2*A; update S set B = 2*B" and transaction T2 is "select avg(A) from R; select avg(B) from S". If transaction T2 executes using "read committed", is it possible for T2 to return two different values?

- **Yes**
- No

## Q3

Consider tables R(A) and S(B), both containing {(1),(2)}. Suppose transaction T1 is "update R set A = 2*A; update S set B = 2*B" and transaction T2 is "select avg(A) from R; select avg(B) from S". If transaction T2 executes using "read committed", is it possible for T2 to return a smaller avg(B) than avg(A)?

- Yes
- **No**

## Q4

Consider table R(A) containing {(1),(2)}. Suppose transaction T1 is "update T set A=2*A; insert into R values (6)" and transaction T2 is "select avg(A) from R; select avg(A) from R". If transaction T2 executes using "repeatable read", what are the possible values returned by its SECOND statement?

- **1.5, 4**
- 1.5, 2, 4
- 1.4, 3, 4
- 1.5, 2, 3, 4