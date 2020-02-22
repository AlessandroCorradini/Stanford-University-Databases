# Indexes Quiz

Each multiple-choice quiz problem is based on a "root question," from which the system generates different correct and incorrect choices each time you take the quiz. Thus, you can test yourself on the same material multiple times. We strongly urge you to continue testing on each topic until you complete the quiz with a perfect score at least once. Simply click the "Reset" button at the bottom of the page for a new variant of the quiz.

After submitting your selections, the system will score your quiz, and for incorrect answers will provide an "explanation" (sometimes for correct ones too). These explanations should help you get the right answer the next time around. To prevent rapid-fire guessing, the system enforces a minimum of 10 minutes between each submission of solutions.

## Q1

Consider the following relational schema:

```
   Course(courseName unique, department, instrID)
   Instructor(instrID unique, office)
   Student(studentID unique, major)
   Enroll(studentID, courseName, unique (studentID,courseName))
```

Suppose there are five types of queries commonly asked on this schema:

- Given a course name, find the department offering that course.
- List all studentIDs together with all of the departments they are taking courses in.
- Given a studentID, find the names of all courses the student is enrolled in.
- List the offices of instructors teaching at least one course.
- Given a major, return the studentIDs of students in that major.

Which of the following indexes could NOT be useful in speeding up execution of one or more of the above queries?

- Index on Enroll.studentID
- **Index on Instructor.office**
- Index on Course.courseName
- Index on Enroll.courseName

## Q2

Consider a table storing temperature readings taken by sensors:

```
   Temps(sensorID, time, temp)
```

Assume the pair of attributes [sensorID,time] is a key. Consider the following query:

``` 
   select * from Temps
   where sensorID = 'sensor541'
   and time = '05:11:02'
```

Consider the following scenarios:

A - No index is present on any attribute of Temps

B - An index is present on attribute sensorID only

C - An index is present on attribute time only

D - Separate indexes are present on attributes sensorID and time

E - A multi-attribute index is present on (sensorID,time)

Suppose table Temps has 50 unique sensorIDs and each sensorID has exactly 20 readings. Furthermore there are exactly 10 readings for every unique time in Temps.

For each scenario A-E, determine the maximum number of tuples that might be accessed to answer the query, assuming one "best" index is used whenever possible. (Don't count the number of index accesses.) Which of the following combinations of values is correct?

- A:1000, B:20, E:10
- A:1000, C:1000, D:10
- **B:20, C:10, D:10**
- B:1000, C:10, D:10