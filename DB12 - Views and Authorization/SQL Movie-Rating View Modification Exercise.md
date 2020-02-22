# SQL Movie-Rating View Modification Exercises

You've started a new movie-rating website, and you've been collecting data on reviewers' ratings of various movies. Here's the schema:

Movie ( mID, title, year, director )
English: There is a movie with ID number mID, a title, a release year, and a director.

Reviewer ( rID, name )
English: The reviewer with ID number rID has a certain name.

Rating ( rID, mID, stars, ratingDate )
English: The reviewer rID gave the movie mID a number of stars rating (1-5) on a certain ratingDate.

In addition to the base tables, you've created three views:

View LateRating contains movie ratings after January 20, 2011. The view contains the movie ID, movie title, number of stars, and rating date.

```
create view LateRating as
  select distinct R.mID, title, stars, ratingDate
  from Rating R, Movie M
  where R.mID = M.mID
  and ratingDate > '2011-01-20'
```

View HighlyRated contains movies with at least one rating above 3 stars. The view contains the movie ID and movie title.

```
create view HighlyRated as
  select mID, title
  from Movie
  where mID in (select mID from Rating where stars > 3)
```

View NoRating contains movies with no ratings in the database. The view contains the movie ID and movie title.

```
create view NoRating as
  select mID, title
  from Movie
  where mID not in (select mID from Rating)
```

Your exercises will run over a small data set conforming to the schema, with the views predefined. View the database. (You can also download the schema and data.)

Instructions: Each of the problems asks you to enable a certain type of modification to one of the views by writing an "instead-of" trigger. Our back-end creates your trigger using SQLite on the original state of the sample database. It then issues a modification statement on the view, which should activate your trigger to modify the base tables accordingly. Our back-end checks the trigger's base-table modifications, then restores the database to its original state. When you're satisfied with your solution for a given problem, click the "Submit" button to check your answer.

Important Notes:

- Our backend system is SQLite, so you must conform to the instead-of view modification trigger constructs supported by SQLite. A guide to SQLite triggers is here, although you may find it easier to start from the examples in the "View modifications using triggers" video demonstrations.
- You are to translate the English into a trigger that performs the desired actions for all possible databases and view modifications. All we actually check is that the verification query gets the right answer on the small sample database. Thus, even if your solution is marked as correct, it is possible that your solution does not correctly reflect the problem at hand. Circumventing the system in this fashion will get you a high score on the exercises, but it won't help you learn about view-modifications. On the other hand, an incorrect attempt at a general solution is unlikely to behave correctly, so you shouldn't be led astray by our checking system.

## Q1 

Write an instead-of trigger that enables updates to the title attribute of view LateRating.

Policy: Updates to attribute title in LateRating should update Movie.title for the corresponding movie. (You may assume attribute mID is a key for table Movie.) Make sure the mID attribute of view LateRating has not also been updated -- if it has been updated, don't make any changes. Don't worry about updates to stars or ratingDate.

```
CREATE TRIGGER titleupdate
INSTEAD OF UPDATE OF title ON LateRating
FOR EACH ROW 
WHEN New.mID = Old.mID AND New.title <> Old.title
BEGIN
  UPDATE Movie
  SET title = New.title
  WHERE mID = New.mID;
END;
```

## Q2 

Write an instead-of trigger that enables updates to the stars attribute of view LateRating.

Policy: Updates to attribute stars in LateRating should update Rating.stars for the corresponding movie rating. (You may assume attributes [mID,ratingDate] together are a key for table Rating.) Make sure the mID and ratingDate attributes of view LateRating have not also been updated -- if either one has been updated, don't make any changes. Don't worry about updates to title.

```
CREATE TRIGGER starsupdate
INSTEAD OF UPDATE OF stars ON LateRating
FOR EACH ROW 
WHEN New.mID = Old.mID AND New.ratingDate = Old.ratingDate AND New.stars <> Old.stars
BEGIN
  UPDATE Rating
  SET stars = New.stars
  WHERE mID = New.mID AND ratingDate = New.ratingDate;
END;
```

## Q3 

Write an instead-of trigger that enables updates to the mID attribute of view LateRating.

Policy: Updates to attribute mID in LateRating should update Movie.mID and Rating.mID for the corresponding movie. Update all Rating tuples with the old mID, not just the ones contributing to the view. Don't worry about updates to title, stars, or ratingDate.

```
CREATE TRIGGER mIDupdate
INSTEAD OF UPDATE OF mID ON LateRating
FOR EACH ROW 
WHEN New.mID <> Old.mID
BEGIN
  UPDATE Movie SET mID = New.mID WHERE mID = Old.mID;
  UPDATE Rating SET mID = New.mID WHERE mID = Old.mID; 
END;
```

## Q4

Finally, write a single instead-of trigger that combines all three of the previous triggers to enable simultaneous updates to attributes mID, title, and/or stars in view LateRating. Combine the view-update policies of the three previous problems, with the exception that mID may now be updated. Make sure the ratingDate attribute of view LateRating has not also been updated -- if it has been updated, don't make any changes.

```
CREATE TRIGGER allupdate
INSTEAD OF UPDATE ON LateRating
FOR EACH ROW 
WHEN New.ratingDate = Old.ratingDate
BEGIN
  UPDATE Movie SET title = New.title, mID = New.mID WHERE mID = Old.mID;
  UPDATE Rating SET stars = New.stars WHERE mID = Old.mID AND ratingDate = old.ratingDate; 
  UPDATE Rating SET mID = New.mID WHERE mID = Old.mID; 
END;
```

## Q5 

Write an instead-of trigger that enables deletions from view HighlyRated.

Policy: Deletions from view HighlyRated should delete all ratings for the corresponding movie that have stars > 3.

```
CREATE TRIGGER deletehigh
INSTEAD OF DELETE ON HighlyRated
FOR EACH ROW 
BEGIN
  DELETE FROM Rating
  WHERE mID = Old.mID AND stars > 3;
END;
```

## Q6

Write an instead-of trigger that enables deletions from view HighlyRated.

Policy: Deletions from view HighlyRated should update all ratings for the corresponding movie that have stars > 3 so they have stars = 3.

```
CREATE TRIGGER udpatehigh
INSTEAD OF DELETE ON HighlyRated
FOR EACH ROW 
BEGIN
  UPDATE Rating
  SET stars = 3
  WHERE mID = Old.mID AND stars > 3;
END;
```

## Q7

Write an instead-of trigger that enables insertions into view HighlyRated.

Policy: An insertion should be accepted only when the (mID,title) pair already exists in the Movie table. (Otherwise, do nothing.) Insertions into view HighlyRated should add a new rating for the inserted movie with rID = 201, stars = 5, and NULL ratingDate.

```
CREATE TRIGGER inserthigh
INSTEAD OF INSERT ON HighlyRated
FOR EACH ROW 
WHEN EXISTS (SELECT * FROM Movie WHERE mID = New.mID AND title = New.title)
BEGIN
  INSERT INTO Rating VALUES (201, New.mID, 5, NULL);
END;
```

## Q8

Write an instead-of trigger that enables insertions into view NoRating.

Policy: An insertion should be accepted only when the (mID,title) pair already exists in the Movie table. (Otherwise, do nothing.) Insertions into view NoRating should delete all ratings for the corresponding movie.

```
CREATE TRIGGER insertno
INSTEAD OF INSERT ON NoRating
FOR EACH ROW 
WHEN EXISTS (SELECT * FROM Movie WHERE mID = New.mID AND title = New.title)
BEGIN
  DELETE FROM Rating WHERE mID = New.mID;
END;
```

## Q9 

Write an instead-of trigger that enables deletions from view NoRating.

Policy: Deletions from view NoRating should delete the corresponding movie from the Movie table.

```
CREATE TRIGGER deleteno_movie
INSTEAD OF DELETE ON NoRating
FOR EACH ROW 
WHEN EXISTS (SELECT * FROM Movie WHERE mID = Old.mID AND title = Old.title)
BEGIN
  DELETE FROM Movie WHERE title = Old.title AND title = Old.title;
END;
```

## Q10

Write an instead-of trigger that enables deletions from view NoRating.

Policy: Deletions from view NoRating should add a new rating for the deleted movie with rID = 201, stars = 1, and NULL ratingDate.

```
CREATE TRIGGER deleteno_rating
INSTEAD OF DELETE ON NoRating
FOR EACH ROW 
WHEN EXISTS (SELECT * FROM Movie WHERE mID = Old.mID AND title = Old.title)
BEGIN
  INSERT INTO Rating VALUES (201, Old.mID, 1, NULL);
END;
```