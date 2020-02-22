# Select, Project, Join In-Video Quiz

## Q1 

Statement A: It can be useful to compose two selection operators.

For example: \sigma_{state=`CA'}(\sigma_{enr>8000} \mathrm{College})

Statement B: It can be useful to compose two projection operators.

For example: \pi_{GPA} (\pi_{sID,GPA,HS} \mathrm{Student})

- Both statements are true.
- Statement A is true but Statement B is false.
- Statement B is true but Statement A is false.
- **Both statements are false.**

## Q2

Which of the following expressons does NOT return the names and GPAs of students with HS>1000 who applied to CS and were rejected?

- \pi_{sName, GPA}(\sigma_{Student.sID=Apply.sID}(\sigma_{HS\gt1000}(Student) \times \sigma_{major=`CS` \wedge dec=`R`}(Apply)))
- \pi_{sName, GPA}(\sigma_{Student.sID=Apply.sID \wedge HS \gt 1000 \wedge major=`CS` \wedge dec=`R`}(Student \times \pi_{sID, major, dec}Apply))
- \sigma_{Student.sID=Apply.sID}(\pi_{sName, GPA}(\sigma_{HS \gt 1000}Student \times \sigma_{major=`CS` \wedge dec=`R`}Apply)) [X]

## Q3

Which of the following English sentences describes the result of this expression:

- All student-college name pairs, where the student is applying to major in CS at the college, the college is in California, and the - college is smaller than some high school
- Students paired with all California colleges to which the student applied to major in CS, where at least one of those colleges is smaller than the student's high school
- Students paired with all colleges smaller than the student's high school to which the student applied to major in CS, where at least one of those colleges is in California
- **Students paired with all California colleges smaller than the student's high school to which the student applied to major in CS**

## Q4 

Which of the following expressions finds the IDs of all students such that some college bears the student's name?

- \pi_{sID}(College \Join Student)
- \pi_{sID}(\sigma_{cName=sName}(College \times Student))
- \pi_{sID}(\pi_{cName}College \Join \pi_{cName}(\sigma_{sName=cName}Student)) [X]
- \pi_{sID}(\sigma_{cName=sName}(\pi_{sID}Student \times College \times Student)