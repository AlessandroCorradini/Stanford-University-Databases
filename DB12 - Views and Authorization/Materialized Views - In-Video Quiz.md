# Materialized Views - In-Video Quiz

## Q1

Consider a materialized view on tables Faculty(name,homeDept) and Teaches(prof,course,dept): create materialized view V as select name from Faculty where name not in (select prof from Teaches where dept = homeDept) Which of the following modifications can NOT cause a change to V?

- insertion into Teaches
- deletion from Teaches
- insertion into Faculty
- **update to Teaches.course**

## Q2

Consider a materialized view on table Item(category,price): create view V as select category from Item group by category having min(price) < 25 Which of the following modifications can NOT cause tuples to be deleted from V?

- deletion from Item
- update to Item.category
- update to Item.price that increases value
- **update to Item.price that decreases value**

## Q3

Consider tables R(A,B) and S(B,C) and a query Q = select A,C from R,S where R.B=S.B and A < 10 and C > 20. Which of the following materialzed views can NOT be used to help evaluate Q?

- V1 = select A,C from R,S where R.B=S.B
- **V2 = select A,C from R,S where A < 10 and C > 20**
- V3 = select A,R.B,S.B,C from R,S where A < 10 and C > 20
- V4 = select * from R where A < 10