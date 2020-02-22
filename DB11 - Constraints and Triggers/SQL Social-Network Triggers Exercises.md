# SQL Social-Network Triggers Exercises

Students at your hometown high school have decided to organize their social network using databases. So far, they have collected information about sixteen students in four grades, 9-12. Here's the schema:

Highschooler ( ID, name, grade )
English: There is a high school student with unique ID and a given first name in a certain grade.

Friend ( ID1, ID2 )
English: The student with ID1 is friends with the student with ID2. Friendship is mutual, so if (123, 456) is in the Friend table, so is (456, 123).

Likes ( ID1, ID2 )
English: The student with ID1 likes the student with ID2. Liking someone is not necessarily mutual, so if (123, 456) is in the Likes table, there is no guarantee that (456, 123) is also present.

Your triggers will run over a small data set conforming to the schema. View the database. (You can also download the schema and data.)

For your convenience, here is a graph showing the various connections between the people in our database. 9th graders are blue, 10th graders are green, 11th graders are yellow, and 12th graders are purple. Undirected black edges indicate friendships, and directed red edges indicate that one person likes another person.

![](/social.png)


Instructions: You are to solve each of the following problems by writing one or more triggers. Our back-end creates triggers using SQLite on the original state of the sample database. It then performs a data modification statement that activate the trigger(s), runs a query to check that the final database state is correct, and restores the database to its original state. When you're satisfied with your solution for a given problem, click the "Submit" button to check your answer.

Important Notes:

- Our backend system is SQLite, so you must conform to the trigger constructs supported by SQLite. A guide to SQLite triggers is here, although you may find it easier to start from the triggers used in the video demonstrations.
- In the workbench and the grading program, triggers are executed with recursive triggering disabled ("recursive_triggers=off").
- You are to translate the English into one or more triggers that perform the desired actions for all possible databases and modifications. All we actually check is that the verification query gets the right answer on the small sample database. Thus, even if your solution is marked as correct, it is possible that your solution does not correctly reflect the problem at hand. Circumventing the system in this fashion will get you a high score on the exercises, but it won't help you learn about triggers. On the other hand, an incorrect attempt at a general solution is unlikely to behave correctly, so you shouldn't be led astray by our checking system.

You may perform these exercises as many times as you like, so we strongly encourage you to keep working with them until you complete the exercises with full credit.

## Q1

Write a trigger that makes new students named 'Friendly' automatically like everyone else in their grade. That is, after the trigger runs, we should have ('Friendly', A) in the Likes table for every other Highschooler A in the same grade as 'Friendly'.

```
CREATE TRIGGER F 
AFTER INSERT ON Highschooler 
WHEN new.name='Friendly' 
BEGIN 
	INSERT INTO Likes SELECT new.id, h.id FROM highschooler as h WHERE new.grade = h.grade AND NOT (new.id=h.id); 
END
```

## Q2

Write one or more triggers to manage the grade attribute of new Highschoolers. If the inserted tuple has a value less than 9 or greater than 12, change the value to NULL. On the other hand, if the inserted tuple has a null value for grade, change it to 9.

```
CREATE TRIGGER gradeTrigger1 
AFTER INSERT ON highschooler 
WHEN new.grade < 9 OR new.grade > 12 
BEGIN 
	UPDATE highschooler SET grade=NULL WHERE id=new.id; 
END 

| 

CREATE TRIGGER gradeTrigger2 
AFTER INSERT ON highschooler 
WHEN new.grade IS NULL 
BEGIN 
	UPDATE highschooler SET grade=9 WHERE id=new.id; 
END
```

## Q3 

Write one or more triggers to maintain symmetry in friend relationships. Specifically, if (A,B) is deleted from Friend, then (B,A) should be deleted too. If (A,B) is inserted into Friend then (B,A) should be inserted too. Don't worry about updates to the Friend table.

```
CREATE TRIGGER friendInsert 
AFTER INSERT ON friend 
BEGIN 
	INSERT INTO friend VALUES (new.id2, new.id1); 
END 

| 

CREATE TRIGGER friendDelete 
AFTER DELETE ON friend 
BEGIN 
	DELETE FROM friend WHERE id1=old.id2 AND id2=old.id1; 
END
```

## Q4

Write a trigger that automatically deletes students when they graduate, i.e., when their grade is updated to exceed 12.

```
CREATE TRIGGER graduateTrigger 
AFTER UPDATE on highschooler 
WHEN new.grade > 12 
BEGIN 
	DELETE FROM highschooler WHERE id=new.id; 
END
```

## Q5

Write a trigger that automatically deletes students when they graduate, i.e., when their grade is updated to exceed 12 (same as Question 4). In addition, write a trigger so when a student is moved ahead one grade, then so are all of his or her friends.

```
CREATE TRIGGER graduateTrigger 
AFTER UPDATE on highschooler 
WHEN new.grade > 12 
BEGIN 
	DELETE FROM highschooler WHERE id=new.id; 
END 

| 

CREATE TRIGGER moveAhead 
AFTER UPDATE on highschooler 
WHEN new.grade = old.grade + 1 
BEGIN 
	UPDATE highschooler SET grade = grade+1 WHERE id in (SELECT id2 FROM friend WHERE id1=new.id); 
END
```

## Q6 

Write a trigger to enforce the following behavior: If A liked B but is updated to A liking C instead, and B and C were friends, make B and C no longer friends. Don't forget to delete the friendship in both directions, and make sure the trigger only runs when the "liked" (ID2) person is changed but the "liking" (ID1) person is not changed.

```
CREATE TRIGGER likeTrigger 
AFTER UPDATE ON likes 
WHEN exists(SELECT * FROM friend WHERE id1=new.id2 AND id2=old.id2) 
	AND new.id1 = old.id1 AND NOT new.id2 = old.id2 
BEGIN 
	DELETE FROM friend WHERE id1=new.id2 AND id2=old.id2; 
	DELETE FROM friend WHERE id1=old.id2 AND id2=new.id2; 
END
```