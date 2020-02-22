# Constraints of Several Types - In-Video Quiz

## Q1

Consider the following general assertion on tables Faculty(name,homeDept) and Teaches(prof,course,dept): create assertion A (not exists (select * from Faculty where name not in (select prof from Teaches where dept = homeDept))) Which of the following modifications can NOT cause the constraint to become violated?

- update to Faculty.homeDept
- deletion from Teaches
- update to Teaches.prof
- **insertion into Teaches**

## Q2

Consider the following general assertion on table Item(category,price): create assertion A (25 < any (select sum(price) from Item group by category)) Which of the following modifications can NOT cause the constraint to become violated? Choose the best (most reasonable) answer of the four choices.

- **insertion into Item**
- deletion from Item
- update to Item.category
- update to Item.price