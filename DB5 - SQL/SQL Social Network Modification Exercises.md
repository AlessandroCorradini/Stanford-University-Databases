Students at your hometown high school have decided to organize their social network using databases. So far, they have collected information about sixteen students in four grades, 9-12. Here's the schema:

Highschooler ( ID, name, grade )
English: There is a high school student with unique ID and a given first name in a certain grade.

Friend ( ID1, ID2 )
English: The student with ID1 is friends with the student with ID2. Friendship is mutual, so if (123, 456) is in the Friend table, so is (456, 123).

Likes ( ID1, ID2 )
English: The student with ID1 likes the student with ID2. Liking someone is not necessarily mutual, so if (123, 456) is in the Likes table, there is no guarantee that (456, 123) is also present.

Your modifications will run over a small data set conforming to the schema. View the database. (You can also download the schema and data.)

For your convenience, here is a graph showing the various connections between the people in our database. 9th graders are blue, 10th graders are green, 11th graders are yellow, and 12th graders are purple. Undirected black edges indicate friendships, and directed red edges indicate that one person likes another person.

Social graph


Instructions: You are to write each of the following data modification commands using SQL. Our back-end runs each modification using SQLite on the original state of the sample database. It then performs a query over the modified database to check whether your command made the correct modification, and restores the database to its original state. 

# Q1

It's time for the seniors to graduate. Remove all 12th graders from Highschooler.

```
DELETE FROM Highschooler
WHERE grade = 12
```

# Q2

If two students A and B are friends, and A likes B but not vice-versa, remove the Likes tuple.

```
DELETE FROM Likes
WHERE ID1 IN (
    SELECT L.ID1
    FROM Friend F JOIN Likes L USING(ID1)
    WHERE F.ID2 = L.ID2
) AND ID2 NOT IN(
    SELECT L.ID1
    FROM Friend F JOIN Likes L USING(ID1)
    WHERE F.ID2 = L.ID2
)
```

# Q3

For all cases where A is friends with B, and B is friends with C, add a new friendship for the pair A and C. Do not add duplicate friendships, friendships that already exist, or friendships with oneself. (This one is a bit challenging; congratulations if you get it right.)

```
INSERT INTO Friend
SELECT DISTINCT F1.ID1, F2.ID2
FROM Friend F1, Friend F2
WHERE F1.ID2 = F2.ID1
      AND F1.ID1 <> F2.ID2
      AND F1.ID1 NOT IN (
          SELECT F3.ID1
          FROM Friend F3
          WHERE F3.ID2 = F2.ID2
          );
```
