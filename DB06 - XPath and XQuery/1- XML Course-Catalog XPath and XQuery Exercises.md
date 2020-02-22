# XML Course-Catalog XPath and XQuery Exercises

## Q1

Return all Title elements (of both departments and courses). 

Note: Your solution will need to reference doc("courses.xml") to access the data. 

**Answer**

```
doc("courses.xml")//Title
```

## Q2

Return last names of all department chairs. 

Note: Your solution will need to reference doc("courses.xml") to access the data. 

**Answer**

```
doc("courses.xml")//Chair//Last_Name
```

## Q3

Return titles of courses with enrollment greater than 500. 

Note: Your solution will need to reference doc("courses.xml") to access the data. 

**Answer**

```
doc("courses.xml")//Course[data(@Enrollment)>500]/Title
```

## Q4

Return titles of departments that have some course that takes "CS106B" as a prerequisite. 

Note: Your solution will need to reference doc("courses.xml") to access the data. 

**Answer**

```
doc("courses.xml")/Course_Catalog/Department[Course/Prerequisites/Prereq="CS106B"]/Title
```

## Q5

Return last names of all professors or lecturers who use a middle initial. Don't worry about eliminating duplicates. 

Note: Your solution will need to reference doc("courses.xml") to access the data. 

**Answer**

```
doc("courses.xml")//(Professor | Lecturer)[Middle_Initial]/Last_Name
```

## Q6

Return the count of courses that have a cross-listed course (i.e., that have "Cross-listed" in their description). 

Note: Your solution will need to reference doc("courses.xml") to access the data. 

**Answer**

```
doc("courses.xml")/Course_Catalog/count(Department/Course[contains(Description,"Cross-listed")])
```

## Q7

Return the average enrollment of all courses in the CS department. 

Note: Your solution will need to reference doc("courses.xml") to access the data. 

**Answer**

```
doc("courses.xml")//Department[@Code="CS"]/avg(Course/@Enrollment)
```

## Q8

Return last names of instructors teaching at least one course that has "system" in its description and enrollment greater than 100. 

Note: Your solution will need to reference doc("courses.xml") to access the data. 

**Answer**

```
doc("courses.xml")//Course[@Enrollment>100 and contains(Description,"system")]/Instructors//Last_Name
```

## Q9

Return the title of the course with the largest enrollment. 

Note: Your solution will need to reference doc("courses.xml") to access the data. 
(This problem is quite challenging; congratulations if you get it right.) 

**Answer**

```
doc("courses.xml")//Course[@Enrollment = max(doc("courses.xml")//Course/@Enrollment)]/Title
```