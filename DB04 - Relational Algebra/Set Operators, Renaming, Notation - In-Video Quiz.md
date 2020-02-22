# Set Operators, Renaming, Notation In-Video Quiz

## Q1 

Three of the following four expressions finds the names of all students who did not apply to major in CS or EE. Which one finds something different? (Hint: You should not assume student names are unique.)

- \pi_{sName}(Student \Join (\pi_{sID}Student - (\pi_{sID}(\sigma_{major=`CS`}Apply) \cup \pi_{sID}(\sigma_{major=`EE`}Apply))))
- \pi_{sName}(Student \Join (\pi_{sID}Student - \pi_{sID}(\sigma_{major=`CS` \vee major=`EE`}Apply)))
- \pi_{sName}(\pi_{sID, sName}Student - \pi_{sID, sName}(Student \Join \pi_{sID}(\sigma_{major=`CS` \vee major=`EE`}Apply)))
- \pi_{sName}Student - \pi_{sName}(Student \Join \pi_{sID}(\sigma_{major=`CS` \vee major=`EE}Apply)) [X]

## Q2

Which of the following English sentences describes the result of this expression:

\pi_{cName}College - \pi_{cName}(Apply \Join (\pi_{sID}(\sigma_{GPA \gt 3.5}Student) \cap \pi_{sID}(\sigma_{major=`CS`}Apply)))

- All colleges with no GPA>3.5 applicants who applied for a CS major at that college
- **All colleges with no GPA>3.5 applicants who applied for a CS major at any college**
- All colleges where all applicants either have GPA>3.5 or applied for a CS major at that college
- All colleges where no applicants have GPA>3.5 or no applicants applied for a CS major at that college

## Q3

Suppose relation Student has 20 tuples. What is the minimum and maximum number of tuples in the result of this expression:

\rho_{s1(i1, n1, g, h)}Student \Join \rho_{s2(i2, n2, g, h)}Student

- minimum = 0, maximum = 400
- minimum = 20, maximum = 20
- **minimum = 20, maximum = 400**
- A4: minimum = 40, maximum = 40

## Q4 

Suppose relations College, Student, and Apply have 5, 20, and 50 tuples in them respectively. Remember that cName is a key for College. Do not assume sName is a key for Student. Do assume that college names in Apply also appear in College. What is the minimum and maximum number of tuples in the result of this expression:

\pi_{cName}College \cup \rho_{cName}(\pi_{sName}Student) \cup \pi_{cName}Apply

- **minimum = 5, maximum = 25**
- minimum = 5, maximum = 75
- minimum = 25, maximum = 45
- minimum = 75, maximum = 75