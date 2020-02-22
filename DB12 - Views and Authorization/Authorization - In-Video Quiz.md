# Authorization - In-Video Quiz

## Q1

Consider table Employee(name,dept,salary), and the SQL statement: update Employee set salary = salary+100 where dept='CS' Which of the following privileges on table Employee is NOT needed to execute this statement?

- update(salary)
- **read(name)**
- read(dept)
- read(salary)

## Q2

Consider table Employee(name,dept,salary). Is it possible to grant a user modification privileges only on those employees whose salary is above average?

- Yes
- **No**

## Q3

Consider table R with owner A. Suppose we have the sequence: (1) A grants select(R) to B with grant option; (2) A grants select(R) to C with grant option; (3) B grants select(R) to D; (4) C grants select(R) to D; (5) A revokes select(R) from B with restrict. Does step (5) generate an error?

- Yes
- **No**