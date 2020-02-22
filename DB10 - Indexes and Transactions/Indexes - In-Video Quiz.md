# Indexes - In-Video Quiz

## Q1

Consider the following query:

```
Select * From Apply, College
Where Apply.cName = College.cName
And Apply.major = 'CS' and College.enrollment < 5000
```

Which of the following indexes could NOT be useful in speeding up query execution?

- Tree-based index on Apply.cName
- Hash-based index on Apply.major
- **Hash-based index on College.enrollment**
- Hash-based index on College.cName

## Q2

Consider the following query:

```
Select * From Student, Apply, College
Where Student.sID = Apply.sID and Apply.cName = College.cName
And Student.GPA > 1.5 And College.cName < 'Cornell'
```

Suppose we are allowed to create two indexes, and assume all indexes are tree-based. Which two indexes do you think would be most useful for speeding up query execution?

- **Student.sID, College.cName**
- Student.sID, Student.GPA
- Apply.cName, College.cName
- Apply.sID, Student.GPA