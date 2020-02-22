# SQL Social-Network Query Exercises

Students at your hometown high school have decided to organize their social network using databases. So far, they have collected information about sixteen students in four grades, 9-12. Here's the schema:

Highschooler ( ID, name, grade )
English: There is a high school student with unique ID and a given first name in a certain grade.

Friend ( ID1, ID2 )
English: The student with ID1 is friends with the student with ID2. Friendship is mutual, so if (123, 456) is in the Friend table, so is (456, 123).

Likes ( ID1, ID2 )
English: The student with ID1 likes the student with ID2. Liking someone is not necessarily mutual, so if (123, 456) is in the Likes table, there is no guarantee that (456, 123) is also present.

Your queries will run over a small data set conforming to the schema. View the database. (You can also download the schema and data.)

For your convenience, here is a graph showing the various connections between the students in our database. 9th graders are blue, 10th graders are green, 11th graders are yellow, and 12th graders are purple. Undirected black edges indicate friendships, and directed red edges indicate that one student likes another student.

![](/social.png)

Instructions: Each problem asks you to write a query in SQL. To run your query against our back-end sample database using SQLite, click the "Submit" button. You will see a display of your query result and the expected result. If the results match, your query will be marked "correct". You may run as many queries as you like for each question.

Important Notes:

- Your queries are executed using SQLite, so you must conform to the SQL constructs supported by SQLite.
- Unless a specific result ordering is asked for, you can return the result rows in any order.
- You are to translate the English into a SQL query that computes the desired result over all possible databases. All we actually check is that your query gets the right answer on the small sample database. Thus, even if your solution is marked as correct, it is possible that your query does not correctly reflect the problem at hand. (For example, if we ask for a complex condition that requires accessing all of the tables, but over our small data set in the end the condition is satisfied only by Star Wars, then the query "select title from Movie where title = 'Star Wars'" will be marked correct even though it doesn't reflect the actual question.) Circumventing the system in this fashion will get you a high score on the exercises, but it won't help you learn SQL. On the other hand, an incorrect attempt at a general solution is unlikely to produce the right answer, so you shouldn't be led astray by our checking system.

# Q1

Find the names of all students who are friends with someone named Gabriel.

```
SELECT name
FROM HighSchooler
WHERE ID IN (SELECT ID1
             FROM Highschooler JOIN Friend ON ID = ID2
             WHERE name = 'Gabriel')
```

# Q2

For every student who likes someone 2 or more grades younger than themselves, return that student's name and grade, and the name and grade of the student they like.

```
SELECT S1.name, S1.grade, S2.name, S2.grade
FROM Highschooler S1, Highschooler S2, Likes L
WHERE S1.ID = L.ID1 AND S2.ID = L.ID2 AND S1.grade - S2.grade >= 2;
```

# Q3

For every pair of students who both like each other, return the name and grade of both students. Include each pair only once, with the two names in alphabetical order.

```
SELECT S1.name, S1.grade, S2.name, S2.grade  
FROM Likes L1, Likes L2, Highschooler S1, Highschooler S2
WHERE L1.ID1 = L2.ID2
      AND L2.ID1 = L1.ID2
      AND L1.ID1 = S1.ID
      AND L1.ID2 = S2.ID
      AND S1.name < S2.name;
```


# Q4

Find all students who do not appear in the Likes table (as a student who likes or is liked) and return their names and grades. Sort by grade, then by name within each grade.

```
SELECT name, grade
FROM Highschooler
WHERE ID NOT IN (
    SELECT ID
    FROM Likes, Highschooler
    WHERE ID = ID1 OR ID = ID2
```

# Q5

For every situation where student A likes student B, but we have no information about whom B likes (that is, B does not appear as an ID1 in the Likes table), return A and B's names and grades.

```
SELECT S1.name, S1.grade, S2.name, S2.grade
FROM  HighSchooler S1, HighSchooler S2, Likes
WHERE S1.ID = ID1 AND S2.ID = ID2 AND S2.ID IN
(SELECT ID
FROM Highschooler
WHERE ID NOT IN (
    SELECT ID1
    FROM LIKES
))
```

# Q6

Find names and grades of students who only have friends in the same grade. Return the result sorted by grade, then by name within each grade.

```
SELECT S1.name, S1.grade
FROM Highschooler S1
WHERE S1.ID NOT IN (SELECT S1.ID
                    FROM Highschooler S2, Friend F
                    WHERE S1.grade <> S2.grade
                          AND F.ID1 = S1.ID
                          AND F.ID2 = S2.ID
                   )
ORDER BY S1.grade, S1.name
```

# Q7

For each student A who likes a student B where the two are not friends, find if they have a friend C in common (who can introduce them!). For all such trios, return the name and grade of A, B, and C.


```
SELECT S1.name, S1.grade, S2.name, S2.grade, S3.name, S3.grade
FROM Highschooler S1, Highschooler S2, Highschooler S3, Likes L, Friend F1, Friend F2
WHERE S1.ID = L.ID1 AND S2.ID = L.ID2
      AND S1.ID = F1.ID1 AND S3.ID = F1.ID2
      AND S2.ID = F2.ID1 AND S3.ID = F2.ID2
      AND S1.ID NOT IN(SELECT ID2
                       FROM Friend
                       WHERE ID1 = S2.ID)
```

# Q8

Find the difference between the number of students in the school and the number of different first names.

```
SELECT COUNT(*) - COUNT(DISTINCT name)
FROM Highschooler
```

# Q9

Find the name and grade of all students who are liked by more than one other student.

```
SELECT name, grade
FROM HighSchooler S1, (SELECT ID2, COUNT(ID2) AS well_liked
                        FROM LIKES
                        GROUP BY ID2
                      ) AS temp
WHERE S1.id = temp.ID2 AND temp.well_liked > 1
```