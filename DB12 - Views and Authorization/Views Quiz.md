# Views Quiz

## Q1 

Consider the following base tables. Capitalized attributes are primary keys. All non-key attributes are permitted to be NULL.

```
   MovieStar(NAME, address, gender, birthdate)
   MovieExecutive(LICENSE#, name, address, netWorth)
   Studio(NAME, address, presidentLicense#)
```

Each of the choices describes, in English, a view that could be created with a query on these tables. Which one can be written as a SQL view that is updatable according to the SQL standard?

- **A view "StudioPres" containing the license number, name, address, of all executives who are studio presidents.**
- A view "ExecutiveStar" containing the name, gender, and executive license number of all individuals who are both stars and executives.
- A view "GenderBalance" containing the number of male and number of female movie stars.
- A view "StudioPresInfo" containing the studio name, executive name, and license number for all executives who are studio presidents.

## Q2 

Consider the following schema:

```
  Book(ISBN, title, year) // ISBN and title cannot be NULL
  Author(ISBN, name) // ISBN and name cannot be NULL
```

and the following view definition over this schema:

```
  Create View V as
    Select Book.ISBN, count(*)
    From Book, Author
    Where Book.ISBN = Author.ISBN
    And Author.name Like 'A%'
    And Book.year > 2000
    Group By Book.ISBN
```

This view is not updatable according to the SQL standard, for a number of reasons. Which of the following is a valid reason for the view being non-updatable according to the standard?

- **Two tables in FROM clause**
- The condition Book.year > 2000
- NULL values are not permitted in Book.ISBN
- Book.year is omitted from the view

## Q3 

Suppose a table T(A,B,C) has the following tuples: (1,1,3), (1,2,3), (2,1,4), (2,3,5), (2,4,1), (3,2,4), and (3,3,6). Consider the following view definition:

```
   Create View V as
     Select A+B as D, C
     From T
```

Consider the following query over view V:

```
   Select D, sum(C)
   From V
   Group By D
   Having Count(*) <> 1
```

Which of the following tuples is in the query result?

- (1,8)
- **(5,9)**
- (6,4)
- (2,7)